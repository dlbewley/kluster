# Proof of Concept 

This is a proof of concept demonstrating the use of Kustomize to build a cluster using Hive API and RH ACM followed by day 2 configurations such as oauth, RBAC, and console tweaks.

The idea is you would add directories under [clusters/](clusters/) and do this:

```bash
cd clusters/sno1

# authenticate to hub cluster
kustomize build kustomize/clusterdeploy > example-output-1.yaml
# apply cluster deployment
oc apply -f example-output-1.yaml

# wait for ACM to build sno1 cluster

# authenticate to managed (sno1) cluster
kustomize build kustomize > example-output-2.yaml
# apply day 2 cutomizations
oc apply -f example-output2.yaml
```

What say you?
