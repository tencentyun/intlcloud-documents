## Installing NginxIngress Component[](id:Nginx-ingress)

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the **Cluster management** page, click the ID of the target cluster to go to the cluster details page.
3. In the left sidebar, click **Add-on management** to go to the **Add-on list** page.
4. On the **Add-On List** page, select **Create**. On the **Create Add-on** page, select NginxIngress.
5. Click **Done**. You can view the **Addon Details** in **Services and Routes** > **NginxIngress**.


## Installation Methods
You can use the following installation methods to install Nginx-ingress in TKE based on the requirements of your business scenarios:
- [Use DaemonSet to deploy Nginx-ingress in the specified node pool](#DaemonSet)
- [Use Deployment + HPA mode and specify the scheduling rule for deployment](#Deployment+HPA)
- [Connect the Nginx frontend to a load balancer for deployment](#LB)


### Using DaemonSet to deploy Nginx-ingress in specified node pool (recommended)[](id:DaemonSet)

As Nginx is a key traffic ingress gateway, we recommend you deploy Nginx-ingress in the specified node pool rather than on the same node with other businesses. The deployment architecture is as shown below:
![](https://main.qcloudimg.com/raw/70b726a482703a3c1b959844da65ff89.png)

#### Installation procedure
>? If you use this installation method, you can enjoy the complete scaling capabilities of the node pool and can remove and add Nginx replicas simply by adjusting the number of nodes in the node pool subsequently.
>
1. Prepare a node pool for Nginx-ingress deployment and set a taint to prevent other Pods from being scheduled to the node pool. For more information on the deployment node pool, see [Node Pool Overview](https://intl.cloud.tencent.com/document/product/457/35900).
2. [Install the Nginx-ingress component](#Nginx-ingress) in the cluster.
3. On the cluster information page, select **Services and Routes** > **NginxIngress** and click **Add Nginx Ingress Instance** (a cluster can have multiple Nginx instances).
![](https://qcloudimg.tencent-cloud.cn/raw/315acb32b566355751c3797e698fd081.png)
4. In the **Create NginxIngress** pop-up window, select **Specify a node pool as DaemonSet to deploy** for **Deploy modes** and set other parameters as needed.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/sIDx070_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221223182211.png)
 - **Node pool**: configure the node pool.
 - **Nginx configuration**: you need to set **Request** to a value lower than the model configuration of the node pool (as the nodes have reserved resources). **Limit** is optional.
 - **Image tag**:
     - For Kubernetes clusters on v1.20 or earlier, the Nginx Ingress add-on is on v1.0.0, and the Nginx instance image can only be on v41.0.
     - For Kubernetes clusters on v1.20 or earlier, the Nginx Ingress add-on is on v1.1.0, and the Nginx instance image can only be on v41.0 or v49.3.
     - For Kubernetes clusters on v1.22 or later, the Nginx Ingress add-on can only be on v1.1.0, and the Nginx instance image can only be on v1.1.3.
>? For more information on Nginx instance versions, visit [GitHub](https://github.com/kubernetes/ingress-nginx). For detailed directions on how to upgrade a cluster, see [Upgrading a Cluster](https://intl.cloud.tencent.com/document/product/457/30640). For detailed directions on how to upgrade the Nginx Ingress add-on, see [Add-On Lifecycle Management](https://intl.cloud.tencent.com/document/product/457/38705).
>
4. Click **OK**.



### Using Deployment + HPA mode and specifying scheduling rule for deployment[](id:Deployment+HPA)
If you use the Deployment + HPA mode to deploy Nginx-ingress, you can configure a taint and tolerance to deploy Nginx instances and business Pods in a distributed manner based on your business needs. With HPA, you can configure auto scaling for Nginx instances based on metrics such as CPU and memory utilization. The deployment architecture is as shown below:
![](https://main.qcloudimg.com/raw/ab2743999ad2c8fbc8806673c77e0ef4.png)


#### Installation procedure
1. Prepare a node pool for Nginx-ingress deployment and set a taint to prevent other Pods from being scheduled to the node pool. For more information on the deployment node pool, see [Node Pool Overview](https://intl.cloud.tencent.com/document/product/457/35900).
2. [Install the Nginx-ingress component](#Nginx-ingress) in the cluster.
3. On the cluster information page, select **Services and Routes** > **NginxIngress** and click **Add Nginx Ingress Instance** (a cluster can have multiple Nginx instances).
4. In the **Create NginxIngress** pop-up window, select **Custom Deployment + HPA** for **Deploy modes** and set other parameters as needed.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/dkFS318_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221223182221.png)
 - **Nginx configuration**: you need to set **Request** to a value lower than the model configuration of the node pool (as the nodes have reserved resources). **Limit** is optional.
 - **Node Scheduling Policy**: specify a policy as needed.
 - **Image tag**:
     - For Kubernetes clusters on v1.20 or earlier, the Nginx Ingress add-on is on v1.0.0, and the Nginx instance image can only be on v41.0.
     - For Kubernetes clusters on v1.20 or earlier, the Nginx Ingress add-on is on v1.1.0, and the Nginx instance image can only be on v41.0 or v49.3.
     - For Kubernetes clusters on v1.22 or later, the Nginx Ingress add-on can only be on v1.1.0, and the Nginx instance image can only be on v1.1.3.
>? For more information on Nginx instance versions, visit [GitHub](https://github.com/kubernetes/ingress-nginx). For detailed directions on how to upgrade a cluster, see [Upgrading a Cluster](https://intl.cloud.tencent.com/document/product/457/30640). For detailed directions on how to upgrade the Nginx Ingress add-on, see [Add-On Lifecycle Management](https://intl.cloud.tencent.com/document/product/457/38705).
>
5. Click **OK**.




### Connecting Nginx frontend to load balancer for deployment[](id:LB)

If only Nginx is deployed in the cluster, external traffic cannot be received, so you also need to configure the Nginx frontend load balancer. TKE currently provides a product-like installation capability, and you can also select different deployment modes based on your business needs.

#### Directly connecting cluster in VPC-CNI mode to Nginx Service (recommended)

If your cluster is in VPC-CNI mode, we recommend you directly connect to the Nginx Service through CLB. The load of node pool deployment is used as an example in the following figure:
![](https://main.qcloudimg.com/raw/c77cf9503a0b98886c402647dd7ec558.png)
This solution, with high performance and without manual maintenance of CLB, is the optimal solution. It requires the cluster to enable VPC-CNI. This solution is recommended for the cluster that has configured the VPC-CNI network plug-in, or the Global Router network plug-in with VPC-CNI enabled (both modes are enabled).

#### Using common Service in LoadBalancer mode in cluster in Global Router mode

If your cluster does not support the VPC-CNI mode network, you can also use a common Service in LoadBalancer mode for traffic access.  
Currently, Services in LoadBalancer mode in TKE are implemented based on NodePort by default. CLB is bound to the NodePort of each node to use it as a real server and forwards the traffic to the NodePort, and then the request is routed to the backend Pod of the Service through iptables or IPVS on the node. This scheme is simplest, but the traffic passes through NodePort, which means that there is one more layer for forwarding, and the following problems may exist:
- The forwarding path is relatively long: after reaching NodePort, traffic goes through the CLB within K8s and is then forwarded through iptables or ipvs to Nginx. This increases network time consumption.
- Passing through NodePort will necessarily cause SNAT. If traffic is too concentrated, port exhaustion or conntrack insertion conflicts can easily occur, leading to packet loss and causing some traffic exceptions.
- The NodePort of each node also serves as a CLB. If the CLB is bound with the NodePorts of large numbers of nodes, the CLB status is distributed among each node, which can easily cause global load imbalance.
- The CLB carries out health probes on NodePort, and probe packets are ultimately forwarded to the Pods of Nginx-ingress. If the CLB is bound with too many nodes, and the number of Pods of Nginx-ingress is small, the probe packets will cause immense pressure on Nginx-ingress.



#### Using HostNetwork + load balancer mode

The console does not support setting this mode currently. You can manually modify the YAML file of the Nginx workload to set the network mode to HostNetwork and manually create a CLB instance to bind the node port exposed by Nginx.
Note that when you use HostNetwork, to avoid port listening conflicts, Nginx-ingress Pods cannot be scheduled to the same node.



## Default Parameters for Nginx-ingress Installation in TKE



### Setting Nginx-ingress parameters

In the details page of Nginx-ingress addon, you can select an Nginx-ingress instance to edit YAML in **Nginx Configuration** tab.
>! By default, Nginx won't restart after parameter configuration, and it will take a short while for the parameters to take effect.

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the **Cluster management** page, click the ID of the target cluster to go to the cluster details page.
3. In the left sidebar, click **Add-on management** to go to the **Add-on list** page.
4. Click **Update Nginx Configuration** on the right of the target component to enter the **Nginx Configuration** page.
5. Select the target Nginx-ingress instance and click **Edit YAML**.
6. On the **Update ConfigMap** page, edit the YAML file and click **Done**.

### Parameter configuration sample code


```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: alpha-ingress-nginx-controller
  namespace: kube-system
data:
  access-log-path: /var/log/nginx/nginx_access.log
  error-log-path: /var/log/nginx/nginx_error.log
  log-format-upstream: $remote_addr - $remote_user [$time_iso8601] $msec "$request" $status $body_bytes_sent "$http_referer" "$http_user_agent" $request_length $request_time [$proxy_upstream_name] [$proxy_alternative_upstream_name] [$upstream_addr] [$upstream_response_length] [$upstream_response_time] [$upstream_status] $req_id
  keep-alive-requests: "10000"
  max-worker-connections: "65536"
  upstream-keepalive-connections: "200"
```

>!
- Do not modify `access-log-path `, `error-log-path`, and `log-format-upstream`; otherwise, CLS log collection will be affected.
- If you need to configure different parameters for your business, see [Official Document](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/configmap/).
