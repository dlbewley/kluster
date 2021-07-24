# Proof of Concept 

This is a proof of concept demonstrating the use of Kustomize to build a cluster using Hive API and RH ACM followed by day 2 configurations such as oauth, RBAC, and console tweaks.

The idea is you would add directory per cluster under [clusters/](clusters/) which will act as overlay for bases under [kustomize/](kustomize/).

Goal is that the would-be overlays in [clusters/*/kustomize/](clusters/sno1/kustomize/) may have minimal YAML duplication from bases in [kustomize/](kustomize/) resources which are defined with `name: tbd`.

This leads to some sed-like behavior that is probably frowned upon by the [Kustomize](https://kustomize.io) intelligencia. 

_Eg._
```yaml
patches:
  - target:
      kind: ManagedCluster
      name: tbd
    patch: |-
      - op: replace
        path: /metadata/name
        value: sno1
```

Tell me if I'm totally bonkers.
## Howto

* Deploy _sno1_ single node cluster

```bash
cd clusters/sno1

# authenticate to hub cluster
kustomize build kustomize/clusterdeploy > example-output-1.yaml
# apply cluster deployment
oc apply -f example-output-1.yaml

# wait for ACM to build sno1 cluster
```

* Apply some day 2 customizations

```bash
# authenticate to managed (sno1) cluster
kustomize build kustomize > example-output-2.yaml
# apply day 2 cutomizations
oc apply -f example-output2.yaml
```