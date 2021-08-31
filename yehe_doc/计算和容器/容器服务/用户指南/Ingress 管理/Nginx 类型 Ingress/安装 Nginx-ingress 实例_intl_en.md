<span id="Nginx-ingress"></span>
## Installing NginxIngress Addon
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the “**Cluster Management** page, click the ID of the target cluster to go to the cluster details page.
3. In the left sidebar, click **Add-on Management** to go to the **Add-on List** page.
![](https://main.qcloudimg.com/raw/04312e2e5736ed4be538911502c63a3b.png)
4. On the "Add-on List" page, click **Create**. On the displayed "Create Add-on" page, select **NginxIngress**.
![](https://main.qcloudimg.com/raw/ececc5fbac93e9b7073ca01a5b20171f.png)
5. Click **Done** to install the add-on.


## Installation Method
You can choose one of the following installation methods to install Nginx-ingress in TKE based on your business needs.
- [Deploying via specifying a node pool as DaemonSet](#DaementSet)
- [Deploying via Deployment + HPA and specifying scheduling policy](#Deployment+HPA)
- [Deploying via Nginx accessing a frontend LB](#LB)



<span id="DaementSet"></span>
### Deploying via specifying a node pool as DaemonSet (recommended)

Nginx is a key traffic access gateway. It is recommended that you use the specified node pool to deploy Nginx-Ingress rather than deploy Nginx and other services in the same node. The deployment architecture is shown in the figure below:
![](https://main.qcloudimg.com/raw/70b726a482703a3c1b959844da65ff89.png)
The installation directions are as follows:
>? The capability of node pool scaling is supported by using this installation method. You can implement the scaling of Nginx replicas through adjusting the number of node pools.

1. Prepare the node pool for deploying Nginx-Ingress, and set the taint (to prevent other Pods from scheduling this node pool). For how to deploy node pool, see [Node Pool Overview](https://intl.cloud.tencent.com/document/product/457/35900).
2. [Install NginxIngress Addon](#Nginx-ingress) in the cluster.
3. In the details page of the created Nginx Ingress addon, click **Add Nginx Ingress Instance** (a cluster can have multiple Nginx instances at the same time).

4. In the pop-up window, select **Specify a Node Pool as DaemonSet to Deploy** for **Deploy Modes** and set other parameters as needed.
![](https://main.qcloudimg.com/raw/fa11343e51e9643bc1fe90d4e2fbb100.png)
 - **Node Pool**: select a node pool.
 - **Nginx Configuration**: the configuration of **Request** must be less than the model configuration of the node pool (the node itself has resource reservation). **Limit** can be left empty.
5. Click **OK**.


<span id="Deployment+HPA"></span>
### Deploying via Deployment + HPA and specifying scheduling policy
If you use Deployment + HPA to deploy Nginx-Ingress, you can configure the taint and toleration to implement the decentralized deployment of Nginx and service Pod based on your business needs. Meanwhile, with HPA, Nginx can realize auto-scaling according to metrics such as CPU and memory. The deployment architecture is shown in the figure below:
![](https://main.qcloudimg.com/raw/ab2743999ad2c8fbc8806673c77e0ef4.png)


#### Installation
1. Set the node label of the Nginx to deploy in the cluster. For details, see [Setting a Node Label](https://intl.cloud.tencent.com/document/product/457/30657).
2. [Install NginxIngress Addon](#Nginx-ingress) in the cluster.
3. In the details page of the created Nginx Ingress addon, click **Add Nginx Ingress Instance** (a cluster can have multiple Nginx instances at the same time).
4. In the pop-up window, select **Custom Deployment + HPA** for **Deploy Modes** and set other parameters as needed.
 - **Node Scheduling Policy**: specify the scheduling policy as needed.
 - **Nginx Configuration**: the configuration of **Request** must be less than the model configuration of the node pool (the node itself has resource reservation). **Limit** can be left empty.
5. Click **OK**.



<span id="LB"></span>
### Deploying via Nginx accessing a frontend LB

If you only deploy Nginx in the cluster, you need to configure a frontend LB for the Nginx to receive the external traffic. TKE now provides productized installation capabilities and you can select different deployment mode based on your business needs.

#### Using Service with CLB-to-Nginx direct connection for cluster in VPC-CNI mode (recommended)

If the cluster is in VPC-CNI mode, it is recommended that you use Service with CLB-to-Nginx direct connection. The following figure shows an example of the load deployed by the node pool.
![](https://main.qcloudimg.com/raw/c77cf9503a0b98886c402647dd7ec558.png)
This solution, with high performance and without manual maintenance of CLB, is the optimal solution. It requires the cluster to enable VPC-CNI. This solution is recommended for the cluster that has configured the VPC-CNI network plug-in, or the Global Router network plug-in with VPC-CNI enabled (both modes are enabled).

#### Using Service of general Loadbalancer type for cluster in Globalrouter mode

If the cluster does not support VPC-CNI mode network, you can use Service of general Loadbalancer type to access traffic. 
Currently, by default, a Service of LoadBalancer type on TKE is implemented based on NodePort. The CLB binds the NodePort of each node as the RS (Real Server) and forwards traffic to the NodePort of each node, and then through Iptables or IPVS, nodes route requests to the corresponding backend Pod of the Service. This is the simplest solution, but traffic passes through a layer of NodePort, so there’s one more layer for forwarding, which leads to the following issues:
- The forwarding path is relatively long: after reaching NodePort, traffic goes through the CLB within K8s and is then forwarded through iptables or ipvs to Nginx. This increases network time consumption.
- Passing through NodePort will necessarily cause SNAT. If traffic is too concentrated, port exhaustion or conntrack insertion conflict can easily occur, leading to packet loss and causing some traffic to become exceptional.
- The NodePort of each node also serves as a CLB. If the CLB is bound with the NodePorts of large numbers of nodes, the CLB status is distributed among each node, which can easily cause global load imbalance.
- The CLB carries out health probes on NodePort, and probe packets are ultimately forwarded to the Pods of Nginx-ingress. If the CLB is bound with too many nodes, and the number of Pods of Nginx-ingress is small, the probe packets will cause immense pressure on Nginx-ingress.



#### Using HostNetwork + LB mode

This mode cannot be directly operated on console. You can manually modify the Yaml to configure the network mode of the Nginx workload to HostNetwork. In HostNetwork network mode, user can create load balancer to forward to the corresponding port of the node.
Note that when hostNetwork is used, to avoid port monitoring conflicts, Nginx-ingress Pods cannot be scheduled to the same node.



## Installing Nginx-ingress Default Parameters in TKE



### Nginx-ingress parameter settings

In the details page of Nginx-ingress addon, you can select a Nginx-ingress instance to edit YAML in **Nginx Configuration** tab.
>! By default, Nginx will not be restarted after the parameters are configured and there is a slight delay in the effect time.

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the “**Cluster Management** page, click the ID of the target cluster to go to the cluster details page.
3. In the left sidebar, click **Add-on Management** to go to the **Add-on List** page.
4. Click **Update Nginx Configuration** on the right side of the addon that needs to set parameters to go to the **Nginx Configuration** page.
5. Select an Nginx Ingress instance and click **Edit YAML**.
6. Configure the parameters in **Update ConfigMap** page, and then click **Complete**.

### Configuration parameter sample


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
>- Please do not modify 'access-log-path', 'error-log-path' and 'log-format-upstream', otherwise, the CLS log collection will be affected.
>- If you need to configure different parameters for your business, see [Official Document](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/configmap/).















