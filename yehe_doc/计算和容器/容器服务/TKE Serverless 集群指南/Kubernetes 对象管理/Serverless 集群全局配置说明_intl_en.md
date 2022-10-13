
## Overview
TKE Serverless cluster supports global configuration through ConfigMaps. In scenarios of automatic TKE super node scaling and a pure TKE Serverless cluster, if you need to batch set annotations for each super node or Pod, configuration at the super node or Pod level will be complicated and is highly intrusive to the business YAML file. Therefore, TKE Serverless cluster offers global configuration capabilities to allow you to perform global configuration through ConfigMaps, so as to add Annotations to each Pod in the cluster.

## Directions
1. Create the `eks-config` ConfigMap under `kube-system`.
2. Set the parameters to make it take effect for all TKE Serverless cluster Pods.
Below is the global configuration:
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: eks-config
  namespace: kube-system
data:
  pod.annotations: |
    eks.tke.cloud.tencent.com/resolv-conf: |
      nameserver 183.60.83.19 
    eks.tke.cloud.tencent.com/host-sysctls: "[{"name": "net.core.rmem_max","value": "26214400"}]"
```

## Configuration Priority Description

The global configuration has the lowest priority, next is the configuration at the super node level, and the Pod configuration has the highest priority. If configurations conflict, the one with the higher priority will take effect.
