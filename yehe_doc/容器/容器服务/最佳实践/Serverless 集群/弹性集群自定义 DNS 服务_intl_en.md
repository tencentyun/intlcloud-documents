


>? The entry for DNS Forward configuration is no longer available. The parameters of DNS Forward configured previously will be synced and updated in the Corefile of CoreDNS. If you want to modify the DNS service of the cluster, please refer to the following instructions or the directions of native Kubernetes CoreDNS.

## Overview
This document describes how to modify the DNS service of a cluster through modifying the CoreDNS configuration file.

## Prerequisites
You have [created an serverless cluster](https://intl.cloud.tencent.com/document/product/457/34048). You need to select **Deploy CoreDNS to allow the service discovery in the cluster** in the advanced configuration at the time of creation.

## Directions

### Default Corefile configuration

When a CoreDNS is deployed in an serverless cluster, a Configmap is mounted by default to act as the CoreDNS configuration file (i.e. Corefile).
The default configuration of Corefile is as follows:

```
apiVersion: v1
kind: ConfigMap
metadata:
  name: coredns
  namespace: kube-system
data:
  Corefile: |
    .:53 {
        errors
        health :8081
        kubernetes cluster.local in-addr.arpa ip6.arpa {
           pods insecure
           fallthrough in-addr.arpa ip6.arpa
           ttl 30
        }
        prometheus :9153
        forward . 183.60.83.19 183.60.82.98
        cache 30
        loop
        reload
        loadbalance
    }    
```

Each configuration item adopts the configuration of native Kubernetes. For details, see [CoreDNS](https://kubernetes.io/zh/docs/tasks/administer-cluster/dns-custom-nameservers/#coredns). Please note:

- `forward`：183.60.83.19, 183.60.82.98 is the default DNS address of Tencent Cloud.


### Customize configuration of Corefile
You can modify ConfigMap of CoreDNS (i.e. Corefile) to modify relevant configuration of service discovery. The use method is consistent with that of the native kubernetes. For details, see [Customizing DNS Service](https://kubernetes.io/docs/tasks/administer-cluster/dns-custom-nameservers/).
