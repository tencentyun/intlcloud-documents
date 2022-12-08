
## Overview
As DNS is the first step in service access in a Kubernetes cluster, its stability and performance are of great importance. How to configure and use DNS in a better way involves many aspects. This document describes the best practices of DNS.

## Selecting the Most Appropriate CoreDNS Version

The following table lists the default CoreDNS versions deployed in TKE clusters on different versions.

| TKE Version | CoreDNS Version |
| :------------------: | :------------------: |
| v1.22 | [v1.8.4](https://github.com/coredns/coredns/releases/tag/v1.8.4) |
| v1.20 | [v1.8.4](https://github.com/coredns/coredns/releases/tag/v1.8.4) |
| v1.18 |  [v1.7.0](https://github.com/coredns/coredns/releases/tag/v1.7.0) |
| v1.16 |  [v1.6.2](https://github.com/coredns/coredns/releases/tag/v1.6.2) |
| v1.14 |  [v1.6.2](https://github.com/coredns/coredns/releases/tag/v1.6.2) |

Due to historical reasons, CoreDNS 1.6.2 may still be deployed in clusters on v1.18 or later. If the current CoreDNS version doesn't meet your requirements, you can manually upgrade it as follows:
- [Upgrading to v1.7.0](#1.7.0)
- [Upgrading to v1.8.4](#1.8.4)

## Configuring an Appropriate Number of CoreDNS Replicas
1. The default number of CoreDNS replicas in TKE is `2`, and `podAntiAffinity` is configured to deploy the two replicas on different nodes.
2. If your cluster has more than 80 nodes, we recommend you install NodeLocal DNSCache as instructed in [Using NodeLocal DNS Cache in a TKE Cluster](https://intl.cloud.tencent.com/document/product/457/34061).
3. Generally, you can determine the number of CoreDNS replicas based on the QPS of business access to DNS, number of nodes, or total number of CPU cores. After you install NodeLocal DNSCache, we recommend you use up to 10 CoreDNS replicas. You can configure the number of replicas as follows:
   Number of replicas = min ( max ( ceil (QPS/10000), ceil (number of cluster nodes/8) ), 10 )
	 Sample:
	- If the cluster has ten nodes and the QPS of DNS service requests is 22,000, configure the number of replicas to 3.
	- If the cluster has 30 nodes and the QPS of DNS service requests is 15,000, configure the number of replicas to 4.
	- If the cluster has 100 nodes and the QPS of DNS service requests is 50,000, configure the number of replicas to 10 (NodeLocal DNSCache has been deployed).
4. You can [install the DNSAutoScaler add-on](https://intl.cloud.tencent.com/document/product/457/39122) in the console to automatically adjust the number of CoreDNS replicas (smooth upgrade should be configured in advance). Below is its default configuration:
```
data:
  ladder: |-
    {
      "coresToReplicas":
      [
        [ 1, 1 ],
        [ 128, 3 ],
        [ 512,4 ],
      ],
      "nodesToReplicas":
      [
        [ 1, 1 ],
        [ 2, 2 ]
      ]
    }
```


## Using NodeLocal DNSCache
NodeLocal DNSCache can be deployed in a TKE cluster to improve the service discovery stability and performance. It improves cluster DNS performance by running a DNS caching agent on cluster nodes as a DaemonSet.
For more information on NodeLocal DNSCache and how to deploy NodeLocal DNSCache in a TKE cluster, see [Using NodeLocal DNS Cache in a TKE Cluster](https://intl.cloud.tencent.com/document/product/457/34061).

## Configuring Smooth Upgrade
During node restart or CoreDNS upgrade, some CoreDNS replicas may be unavailable for a period of time. You can configure the following items to maximize the DNS service availability and implement smooth upgrade.

### Configuring the session persistence timeout period of the IPVS UDP protocol
If the cluster uses the IPVS mode of kube-proxy and the business itself doesn't provide the UDP service, you can reduce the session persistence timeout period of the IPVS UDP protocol to minimize the service unavailability.
1. If the cluster is on v1.18 or later, kube-proxy provides the `--ipvs-udp-timeout` parameter with the default value of `0s`, or the system default value `300s` can be used. We recommend you configure `--ipvs-udp-timeout=10s`. Configure the kube-proxy DaemonSet as follows:
```
    spec:
      containers:
      - args:
        - --kubeconfig=/var/lib/kube-proxy/config
        - --hostname-override=$(NODE_NAME)
        - --v=2
        - --proxy-mode=ipvs
        - --ipvs-scheduler=rr
        - --nodeport-addresses=$(HOST_IP)/32
        - --ipvs-udp-timeout=10s
        command:
        - kube-proxy
        name: kube-proxy
```
2. If the cluster is on v1.16 or earlier, kube-proxy doesn't support this parameter, and you can use the `ipvsadm` tool to batch modify the information on nodes as follows:
```
yum install -y ipvsadm
ipvsadm --set 900 120 10
```
3. After completing the configuration, verify the result as follows:
```
ipvsadm -L --timeout
Timeout (tcp tcpfin udp): 900 120 10
```

>! After completing the configuration, you need to wait for five minutes before proceeding to the subsequent steps. If your business uses the UDP service, [submit a ticket](https://console.tencentcloud.com/workorder/category) for assistance.


### Configuring graceful shutdown for CoreDNS
You can configure `lameduck` to make replicas that have already received a shutdown signal continue providing the service for a certain period of time. Configure the CoreDNS ConfigMap as follows (below is only part of the configuration of CoreDNS 1.6.2; for the configuration of other versions, see [Manual Upgrade](#1.7.0)):
```
          .:53 {
              health {
                  lameduck 30s
              }
              kubernetes cluster.local. in-addr.arpa ip6.arpa {
                  pods insecure
                  upstream
                  fallthrough in-addr.arpa ip6.arpa
              }
          }
```

### Configuring CoreDNS service readiness confirmation
After a new replica starts, you need to check its service readiness and add it to the backend list of the DNS service.
1. Open the `ready` plugin and configure the CoreDNS ConfigMap as follows (below is only part of the configuration of CoreDNS 1.6.2; for the configuration of other versions, see [Manual Upgrade](#1.7.0)):
```
           .:53 {
               ready
               kubernetes cluster.local. in-addr.arpa ip6.arpa {
                   pods insecure
                   upstream
                   fallthrough in-addr.arpa ip6.arpa
               }
           }
```
2. Add the `ReadinessProbe` configuration for CoreDNS:
```yaml
    readinessProbe:
      failureThreshold: 5
      httpGet:
        path: /ready
        port: 8181
        scheme: HTTP
      initialDelaySeconds: 30
      periodSeconds: 10
      successThreshold: 1
      timeoutSeconds: 5
```

## Configuring CoreDNS to Access Upstream DNS over UDP
If CoreDNS needs to communicate with the DNS server, it will use the client request protocol (UDP or TCP) by default. However, in TKE, the upstream service of CoreDNS is the DNS service in the VPC by default, which offers limited support for TCP. Therefore, we recommend you configure using UDP as follows (especially when NodeLocal DNSCache is installed):
```
          .:53 {
              forward . /etc/resolv.conf {
                  prefer_udp
              }
          }
```

## Configuring CoreDNS to Filter HINFO Requests

As the DNS service in the VPC doesn't support DNS requests of the HINFO type, we recommend you configure as follows to filter such requests on the CoreDNS side (especially when NodeLocal DNSCache is installed): 
```
          .:53 {
              template ANY HINFO . {
                  rcode NXDOMAIN
              }
          }
```

## Configuring CoreDNS to Return "The domain name doesn't exist" for IPv6 AAAA Record Queries
If the business doesn't need to resolve IPv6 domain names, you can configure as follows to reduce the communication costs:
```
		.:53 {
			template ANY AAAA {
				rcode NXDOMAIN
			}
		}
```

>! Do not use this configuration in IPv4/IPv6 dual-stack clusters.




## Configuring Custom Domain Name Resolution
For more information, see [Implementing Custom Domain Name Resolution in TKE](https://intl.cloud.tencent.com/document/product/457/39125).


## Manual Upgrade

<span id="1.7.0"></span>
### Upgrading to v1.7.0

1. Edit the `coredns` ConfigMap.
```shell
kubectl edit cm coredns -n kube-system
```
Modify the content as follows:
```
        .:53 {
            template ANY HINFO . {
                rcode NXDOMAIN
            }
            errors
            health {
                lameduck 30s
            }
            ready
            kubernetes cluster.local. in-addr.arpa ip6.arpa {
                pods insecure
                fallthrough in-addr.arpa ip6.arpa
            }
            prometheus :9153
            forward . /etc/resolv.conf {
                prefer_udp
            }
            cache 30
            reload
            loadbalance
        }
```

2. Edit the `coredns` Deployment.
```shell
kubectl edit deployment coredns -n kube-system
```
Replace the image as follows:
```yaml
image: ccr.ccs.tencentyun.com/tkeimages/coredns:1.7.0
```


<span id="1.8.4"></span>
### Upgrading to v1.8.4

1. Edit the `coredns` ClusterRole.
```
kubectl edit clusterrole system:coredns
```
Modify the content as follows:
```
rules:
- apiGroups:
  - '*'
  resources:
  - endpoints
  - services
  - pods
  - namespaces
  verbs:
  - list
  - watch
- apiGroups:
  - discovery.k8s.io
  resources:
  - endpointslices
  verbs:
  - list
  - watch
```

2. Edit the `coredns` ConfigMap.
```shell
kubectl edit cm coredns -n kube-system
```
Modify the content as follows:
```
        .:53 {
            template ANY HINFO . {
                rcode NXDOMAIN
            }
            errors
            health {
                lameduck 30s
            }
            ready
            kubernetes cluster.local. in-addr.arpa ip6.arpa {
                pods insecure
                fallthrough in-addr.arpa ip6.arpa
            }
            prometheus :9153
            forward . /etc/resolv.conf {
                prefer_udp
            }
            cache 30
            reload
            loadbalance
        }
```

3. Edit the `coredns` Deployment.
```shell
kubectl edit deployment coredns -n kube-system
```
Replace the image as follows:
```yaml
image: ccr.ccs.tencentyun.com/tkeimages/coredns:1.8.4
```



## Suggestions on Business Configuration
In addition to the best practices of the DNS service, you can also perform appropriate optimization configuration on the business side to improve the DNS user experience.

1. By default, a domain name in a Kubernetes cluster generally can be resolved after multiple resolution requests. By viewing `/etc/resolv.conf` in a Pod, you will see that the default value of `ndots` is `5`. For example, when the `kubernetes.default.svc.cluster.local` Service in the `debug` namespace is queried:
	- The domain name has four dots (`.`), so the system tries adding the first `search` to use `kubernetes.default.svc.cluster.local.debug.svc.cluster.local` for query, but cannot find the domain name.
	- The system continues to use `kubernetes.default.svc.cluster.local.svc.cluster.local` for query, but still cannot find the domain name.
	- The system continues to use `kubernetes.default.svc.cluster.local.cluster.local` for query, but still cannot find the domain name.
	- The system tries using `kubernetes.default.svc.cluster.local` without adding the extension. The query succeeds, and the responding `ClusterIP` is returned.

2. The above simple Service domain name can be resolved successfully after four resolutions, and there are a large number of useless DNS requests in the cluster. Therefore, you need to set an appropriate `ndots` value based on the access type configured for the business to reduce the number of queries:
```yaml
spec:
  dnsConfig:
    options:
    - name: ndots
      value: "2"
  containers:
  - image: nginx
    imagePullPolicy: IfNotPresent
    name: diagnosis
```
3. In addition, you can optimize the domain name configuration for your business to access Services:
	- The Pod should access a Service in the current namespace through `<service-name>`.
	- The Pod should access a Service in another namespace through `<service-name>.<namespace-name>`.
	- The Pod should access an external domain name through a fully qualified domain name (FQDN) with a dot (`.`) added at the end to reduce useless searches.


## Related Content
### Configuration description
- **errors**
It outputs an error message.

- **health**
It reports the health status and is used for health check configuration such as `livenessProbe`. It listens on port 8080 by default and uses the path `http://localhost:8080/health`.
>! If there are multiple server blocks, `health` can be configured only once or configured for different ports.
>
```
com {
    whoami
    health :8080
}

net {
    erratic
    health :8081
}
```

- **lameduck**
It is used to configure the graceful shutdown duration. It is implemented as follows: the hook executes `sleep` when CoreDNS receives a shutdown signal to ensure that the service can continue to run for a certain period of time.

- **ready** 
It reports the plugin status and is used for service readiness check configuration such as `readinessProbe`. It listens on port 8181 by default and uses the path `http://localhost:8181/ready`.

- **kubernetes** 
It is a Kubernetes plugin that can resolve Services in the cluster.

- **prometheus** 
It is a `metrics` data API used to get the monitoring data. Its path is `http://localhost:9153/metrics`. 

- **forward (proxy)**
It forwards requests failed to be processed to an upstream DNS server and uses the `/etc/resolv.conf` configuration of the host by default.
	- According to the configuration of `forward aaa bbb`, the upstream DNS server list `[aaa,bbb]` is maintained internally.
	- When a request arrives, an upstream DNS server will be selected from the `[aaa,bbb]` list to forward the request according to the preset policy (`random|round_robin|sequential`, where `random` is the default policy). If forwarding fails, another server will be selected for forwarding, and regular health check will be performed on the failed server until it becomes healthy.
	- If a server fails the health check multiple times (twice by default) in a row, its status will be set to `down`, and it will be skipped in subsequent server selection.
	- If all servers are down, the system randomly selects a server for forwarding.
Therefore, CoreDNS can intelligently switch between multiple upstream servers. As long as there is an available server in the forwarding list, the request can succeed.

- **cache**
It is the DNS cache.

- **reload**
It hotloads the Corefile. It will reload the new configuration in two minutes after the ConfigMap is modified.

- **loadbalance** 
It provides the DNS-based load balancing feature by randomizing the order of records in the answer.


### Resource usage of CoreDNS

<dx-tabs>
::: Memory
- It is subject to the number of Pods and Services in the cluster.
- It is affected by the size of enabled cache.
- It is affected by the QPS.

Below is the official data of CoreDNS:
**MB required (default settings) = (Pods + Services) / 1000 + 54**

![CoreDNS in Kubernetes Memory Use](https://docs.google.com/spreadsheets/d/e/2PACX-1vS7d2MlgN1gMrrOHXa7Zn6S3VqujST5L-4PHX7jr4IUhVcTi0guXVRCgtIYrtLm3qxZWFlMHT-Xt9n3/pubchart?oid=191775389&format=image)
:::
::: CPU
It is subject to the QPS.

Below is the official data of CoreDNS:
Single-replica CoreDNS with a running node specification of two vCPUs and 7.5 GB MEM:

| Query Type | QPS              | Average Latency (ms)   | Memory Delta (MB)  |
|:-------------:|:--------------:|:----------------------:|:----------------------:|
| external    |  6733 | 12.02 |  +5                  |
| internal    | 33669            | 2.608              | +5                  |
:::
</dx-tabs>
