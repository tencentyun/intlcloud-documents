容器服务-最佳实践-网络-在 TKE 中实现自定义域名解析
## Overview

When using TKE or EKS, you may need to resolve the custom internal domain names in the following scenarios:

- You build an external centralized storage service, and need to send the monitoring or log collection data in the cluster to the external storage service through a fixed internal domain name.
- During the containerization of traditional services, the code of some services is configured to call other internal services with a fixed domain name, and the configuration cannot be modified, that is, the Service name of Kubernetes cannot be used for calling.



## Solutions
This document describes the following three solutions for using custom domain name resolution in a cluster:

| Solutions | Advantages |
|---------|---------|
| [Using CoreDNS Hosts plugin to configure arbitrary domain name resolution](#scheme1) | This solution is simple and intuitive. You can add arbitrary resolution records. |
| [Using CoreDNS Rewrite plugin to map a domain name to the service in the cluster](#scheme2) | There is no need to know the IP address of the resolution record in advance, but the IP address mapped by the resolution record must be deployed in the cluster. |
| [Using CoreDNS Forward plugin to set the external DNS as the upstream DNS](#scheme3) | You can manage a large number of resolution records. As all records are managed in the external DNS, you do not need to modify the CoreDNS configuration when adding or deleting records. |

>? In the first two solutions, you need to modify CoreDNS configuration file each time you add a resolution record (no need to restart). Please select the solution based on your actual needs.


## Examples



### Using CoreDNS Hosts plugin to configure arbitrary domain name resolution

1. Run the following command to modify the `configmap` of `CoreDNS`, as shown below:
``` bash
kubectl edit configmap coredns -n kube-system
```
2. Modify the `hosts` configuration to add the domain name to the `hosts`, as shown below:
```
hosts {
        192.168.1.6     harbor.oa.com
        192.168.1.8     es.oa.com
        fallthrough
}
```
 >?Map `harbor.oa.com` to 192.168.1.6 and map `es.oa.com` to 192.168.1.8.

 **The complete configurations are as follows**:
```yaml
apiVersion: v1
data:
      Corefile: |2-
        .:53 {
            errors
            health
            kubernetes cluster.local. in-addr.arpa ip6.arpa {
                pods insecure
                upstream
                fallthrough in-addr.arpa ip6.arpa
            }
            hosts {
                192.168.1.6     harbor.oa.com
                192.168.1.8     es.oa.com
                fallthrough
            }
            prometheus :9153
            forward . /etc/resolv.conf
            cache 30
            reload
            loadbalance
        }
kind: ConfigMap
metadata:
      labels:
        addonmanager.kubernetes.io/mode: EnsureExists
      name: coredns
      namespace: kube-system
```



### Using CoreDNS Rewrite plugin to map a domain name to the service in the cluster



If you need to deploy a service with a custom domain name in a cluster, you can use the Rewrite plugin of CoreDNS to resolve the specified domain name to the ClusterIP of a Service.

1. Run the following command to modify the `configmap` of `CoreDNS`, as shown below:
```bash
kubectl edit configmap coredns -n kube-system
```
2. Run the following command to add the Rewrite configuration, as shown below:
```bash
rewrite name es.oa.com es.logging.svc.cluster.local
```
	>?Map the `es.oa.com` to the `es` service deployed under the `logging` namespace. Separate multiple domain names with carriage returns.

 **The complete configurations are as follows**:
```yaml
apiVersion: v1
data:
      Corefile: |2-
        .:53 {
            errors
            health
            kubernetes cluster.local. in-addr.arpa ip6.arpa {
                pods insecure
                upstream
                fallthrough in-addr.arpa ip6.arpa
            }
            rewrite name es.oa.com es.logging.svc.cluster.local
            prometheus :9153
            forward . /etc/resolv.conf
            cache 30
            reload
            loadbalance
        }
kind: ConfigMap
metadata:
      labels:
        addonmanager.kubernetes.io/mode: EnsureExists
      name: coredns
      namespace: kube-system
```



### Using CoreDNS Forward plugin to set the external DNS as the upstream DNS

1. Check the `forward` configuration. The default configuration of `forward` is as follows, which means that the domain name that is not in the cluster is resolved by the `nameserver` configured in the `/etc/resolv.conf` file of the node where CoreDNS is located.
```yaml
forward . /etc/resolv.conf
```
2. Configure `forward` and replace `/etc/resolv.conf` explicitly with the external DNS server address, as shown below:
```yaml
forward . 10.10.10.10
```
 **The complete configurations are as follows**:
```yaml
apiVersion: v1
data:
      Corefile: |2-
        .:53 {
            errors
            health
            kubernetes cluster.local. in-addr.arpa ip6.arpa {
                pods insecure
                upstream
                fallthrough in-addr.arpa ip6.arpa
            }
            prometheus :9153
            forward . 10.10.10.10
            cache 30
            reload
            loadbalance
        }
kind: ConfigMap
metadata:
      labels:
        addonmanager.kubernetes.io/mode: EnsureExists
      name: coredns
      namespace: kube-system
```
3. Configure the resolution record of the custom domain name to the external DNS. It is recommended to add the nameserver in `/etc/resolv.conf` on the node to the upstream of external DNS. Because some services rely on Tencent Cloud internal DNS resolution, if it is not set as the upstream of self-built DNS, some services may not work properly. This document takes [BIND 9](https://www.isc.org/bind/) as an example to modify the configuration file and write the upstream DNS address into forwarders, as shown below:


>! If the external DNS Server and the request source are not in the same Region, some Tencent domain names that do not support cross-region access may become invalid.

```yaml
options {
        forwarders {
                183.60.83.19;
                183.60.82.98;
        };
        ...
```



## References

- [CoreDNS Hosts](https://coredns.io/plugins/hosts/)
- [CoreDNS Rewrite](https://coredns.io/plugins/rewrite/)
- [CoreDNS Forward](https://coredns.io/plugins/forward/)
