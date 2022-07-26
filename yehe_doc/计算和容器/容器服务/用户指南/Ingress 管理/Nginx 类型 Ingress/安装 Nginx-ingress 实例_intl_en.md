





## Installing NginxIngress Component[](id:Nginx-ingress)
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the **Cluster Management** page, click the ID of the target cluster to go to the cluster details page.
3. In the left sidebar, click **Add-on Management** to go to the **Add-on List** page.
4. On the **Add-On List** page, select **Create**. On the **Create Add-on** page, select NginxIngress.
5. Click **Done** to complete the process.


## Installation
You can use the following installation methods to install Nginx-ingress in TKE based on the requirements of your business scenarios:
- [Use DaemonSet to deploy Nginx-ingress in the specified node pool](#DaemonSet)
- [Use Deployment + HPA mode and specify the scheduling rule for deployment](#Deployment+HPA)
- [Connect the Nginx frontend to a load balancer for deployment](#LB)




### Using DaemonSet to deploy Nginx-ingress in specified node pool (recommended)[](id:DaemonSet)

As Nginx is a key traffic ingress gateway, we recommend you deploy Nginx-ingress in the specified node pool rather than on the same node with other businesses. The deployment architecture is as shown below:
![](https://main.qcloudimg.com/raw/70b726a482703a3c1b959844da65ff89.png)
Install Nginx-ingress in the following steps:

>? If you use this installation method, you can enjoy the complete scaling capabilities of the node pool and can remove and add Nginx replicas simply by adjusting the number of nodes in the node pool subsequently.
>
1. Prepare a node pool for Nginx-ingress deployment and set a taint to prevent other Pods from being scheduled to the node pool. For more information on the deployment node pool, see [Node Pool Overview](https://intl.cloud.tencent.com/document/product/457/35900).
2. [Install the Nginx-ingress component](#Nginx-ingress) in the cluster.
3. On the details page of the newly created Nginx-ingress component, click **Add Nginx Ingress Instance** (a cluster can have multiple Nginx instances).
4. In the pop-up window, select **Specify DaemonSet node pool for deployment** from the deployment options and set other parameters as needed as shown below:
![](https://main.qcloudimg.com/raw/fa11343e51e9643bc1fe90d4e2fbb100.png)
 - Node Pool: configure a node pool.
 - Nginx Configuration: you need to set **Request** to a value lower than the model configuration of the node pool (as the nodes have reserved resources). **Limit** is optional.
4. Click **OK**.



### Using Deployment + HPA mode and specifying scheduling rule for deployment[](id:Deployment+HPA)
If you use the Deployment + HPA mode to deploy Nginx-ingress, you can configure a taint and tolerance to deploy Nginx instances and business Pods in a distributed manner based on your business needs. With HPA, you can configure auto scaling for Nginx instances based on metrics such as CPU and memory utilization. The deployment architecture is as shown below:
![](https://main.qcloudimg.com/raw/ab2743999ad2c8fbc8806673c77e0ef4.png)


#### Installation steps
1. Set labels for the nodes where Nginx is to be deployed in the cluster. For detailed directions, see [Setting a Node Label](https://intl.cloud.tencent.com/document/product/457/30657).
2. [Install the Nginx-ingress component](#Nginx-ingress) in the cluster.
3. On the details page of the newly created Nginx-ingress component, click **Add Nginx Ingress Instance** (a cluster can have multiple Nginx instances).
4. In the pop-up window, select **Custom Deployment + HPA** from the deployment options and set other parameters as needed.
 - Node Scheduling Policy: specify a policy as needed.
 - Nginx Configuration: you need to set **Request** to a value lower than the model configuration of the node pool (as the nodes have reserved resources). **Limit** is optional.
5. Click **OK**.




### Connecting Nginx frontend to load balancer for deployment[](id:LB)

If only Nginx is deployed in the cluster, external traffic cannot be received, so you also need to configure the Nginx frontend load balancer. TKE currently provides a product-like installation capability, and you can also select different deployment modes based on your business needs.

#### Directly connecting cluster in VPC-CNI mode to Nginx Service (recommended)

If your cluster is in VPC-CNI mode, we recommend you directly connect to the Nginx Service through CLB. The load of node pool deployment is used as an example in the following figure:
![](https://main.qcloudimg.com/raw/c77cf9503a0b98886c402647dd7ec558.png)
The current scheme is most ideal as it has a high performance and does not require you to manually maintain CLB. However, the cluster needs to support VPC-CNI. If the VPC-CNI network plugin has been configured in your cluster, or the Global Router network plugin has been configured with the support for VPC-CNI enabled (mix of two modes), we recommend you use this scheme.

#### Using common Service in LoadBalancer mode in cluster in Global Router mode

If your cluster does not support the VPC-CNI mode network, you can also use a common Service in LoadBalancer mode for traffic access. 
Currently, Services in LoadBalancer mode in TKE are implemented based on NodePort by default. CLB is bound to the NodePort of each node to use it as a real server and forwards the traffic to the NodePort, and then the request is routed to the backend Pod of the Service through iptables or IPVS on the node. This scheme is simplest, but the traffic passes through NodePort, which means that there is one more layer for forwarding, and the following problems may exist:
- The forwarding path is relatively long: after reaching NodePort, traffic goes through the load balancer within Kubernetes and is then forwarded through iptables or IPVS to Nginx. This increases the network time.
- Passing through NodePort will necessarily cause SNAT. If traffic is too concentrated, port exhaustion or conntrack insertion conflicts can easily occur, leading to packet loss and causing some traffic exceptions.
- The NodePort of each node also serves as a load balancer. If CLB is bound to the NodePorts of a large number of nodes, the load balancing status will be distributed among each node, which can easily cause a global load imbalance.
- CLB carries out health check on NodePort, and health check packets are ultimately forwarded to the Pods of Nginx-ingress. If the CLB is bound to too many nodes, and the Nginx-ingress instance has a small number of Pods, the health check packets will put immense pressure on Nginx-ingress.



#### Using HostNetwork + load balancer mode

The console does not support setting this mode currently. You can manually modify the YAML file of the Nginx workload to set the network mode to HostNetwork and manually create a CLB instance to bind the node port exposed by Nginx.
Note that when you use HostNetwork, to avoid port listening conflicts, Nginx-ingress Pods cannot be scheduled to the same node.



## Default Parameters for Nginx-ingress Installation in TKE



### Nginx-ingress parameter setting method

On the Nginx parameter tab on the Nginx Ingress component page, select an Nginx-ingress instance to edit its YAML file.
>! By default, Nginx won't restart after parameter configuration, and it will take a short while for the parameters to take effect.

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the **Cluster Management** page, click the ID of the target cluster to go to the cluster details page.
3. In the left sidebar, click **Add-on Management** to go to the **Add-on List** page.
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
- You can configure different parameters based on your business needs as instructed in [ConfigMaps](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/configmap/).















