## Overview

TKE supports the installation of Nginx-ingress addon and uses it to access Ingress traffic. For more information about Nginx-ingress, see [Nginx-ingress Instructions](https://intl.cloud.tencent.com/document/product/457/39143). This document describes the best practices of Nginx-ingress addon.


## Prerequisites

- You have installed [Nginx-ingress](https://intl.cloud.tencent.com/document/product/457/38981) addon.


## Operation Directions

### Opening multiple Nginx Ingress traffic entries for the cluster

After the Nginx-ingress addon is installed, there will be a Nginx-ingress operator addon under `kube-system`. You can use this addon to create multiple Nginx Ingress instances. Each Nginx Ingress instance uses a different IngressClass and uses a different CLB as a traffic entry, so that different ingresses can be bound to different traffic entries. You can create multiple Nginx Ingress instances for the cluster based on your actual needs.


1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the **Cluster Management** page, click the ID of the target cluster to go to the cluster details page.
3. In the left sidebar, click **Add-on Management** to go to the **Add-on List** page.
4. Click the installed Nginx-ingress addon to go to the details page.
5. Click **Add Nginx Ingress Instance** to configure the Nginx Ingress instances as needed, and specify a different IngressClass name for each instance.
>?For the details of installing Nginx Ingress instance, see [Installing Nginx-ingress Instance](https://intl.cloud.tencent.com/document/product/457/38981).
6. When creating an Ingress, you can specify a specific IngressClass to bind the Ingress to a specific Nginx Ingress instance. You can create Ingress via console or YAML.
<dx-tabs>
::: Create\san\sIngress\svia\sconsole
See [Creating an Ingress](https://intl.cloud.tencent.com/document/product/457/30673) for more information on how to create an Ingress in the console.
- **Ingress Type**: select **Nginx Load Balancer**.
- **Class**: select the Nginx Ingress instance created in the previous steps.
:::
::: Creating\san\sIngress\svia\sYAML 
See [Creating Ingress](https://intl.cloud.tencent.com/document/product/457/30673) for more information about how to create an Ingress via YAML and specify the annotation (`kubernetes.io/ingress.class`) of ingressClass.
![](https://main.qcloudimg.com/raw/e4ee61dd452ccc512ba8fc5b85ab5714.png)
:::
</dx-tabs>





### Performance optimization

#### CLB-to-Pod direct access mode

When the cluster network mode is Global Router, CLB-to-Pod direct access mode is not enabled by default. It is recommended to enable CLB-to-Pod direct access mode based on the following directions:

1. Enable the [VPC-CNI](https://intl.cloud.tencent.com/document/product/457/38970) mode for the cluster.
2. When creating a Nginx Ingress instance, you can check **Select CLB-to-Pod direct access mode** to enable traffic to bypass the NodePort and reach the Pod directly to improve performance
>? For the details of installing Nginx Ingress instance, see [Installing Nginx-ingress Instance](https://intl.cloud.tencent.com/document/product/457/38981).





#### Adjusting the LB bandwidth limit

As the traffic entry, if LB needs a higher concurrency or throughput, you can set the bandwidth limit based on the actual needs when creating a Nginx Ingress instance and allocate a higher bandwidth for Nginx Ingress.

If you have a bill-by-CVM account ([Checking Account Type](https://intl.cloud.tencent.com/document/product/684/15246)), the bandwidth limit is determined by the node bandwidth. You can adjust the node bandwidth limit based on the following conditions:

- If the CLB-to-Pod direct access mode is enabled, the total LB bandwidth is the sum of the bandwidths of the nodes where the Nginx Ingress instance Pods locate. It is recommended to plan some nodes with high public network bandwidth to deploy Nginx Ingress instances (Specify a node pool as DaemonSet to deploy).
- If the CLB-to-Pod direct access mode is not enabled, the total bandwidth of LB is the sum of the public network bandwidths of all nodes.



#### Nginx Ingress parameter optimization

The Nginx Ingress instance can optimize the kernel parameters and the configuration of Nginx Ingress by default. For details, see [Nginx Ingress High-Concurrency Practices](https://intl.cloud.tencent.com/document/product/457/38300). You can refer to the following directions to customize.

<dx-tabs>
::: Modifying\sthe\skernel\sparameters
Edit the deployed Daemonset or Deployment of nginx-ingress-conntroller (depending on the instance deployment options), and modify initContainers (You cannot modify the resources under kube-system in the console. Please use Kubectl to modify.), as shown below:
![](https://main.qcloudimg.com/raw/821faeb4970ddebe190577d1ca213b84.png)
:::
::: Modifying\sNginx\sIngress\sconfiguration
In **Nginx Configuration** tab, select the instance to modify, click **Edit YAML**, and modify the ConfigMap configuration of the Ingress instance, as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/0dff8e74bbf2ca816ace212556ee7e55.png)

>? For details of ConfigMap configuration, see [Official Document](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/configmap/).
:::
</dx-tabs>






### Improving the observability of Nginx Ingress

#### Enabling monitoring and log

After creating a Nginx Ingress instance, you can enable the log and monitoring configuration of the instance in **Log/Monitoring**, which is convenient for troubleshooting and viewing the status metrics of the instance, as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/61f5e9cf53e1eb8e603317e4ef442375.png)

- The log configuration relies on [Cloud Log Service](https://intl.cloud.tencent.com/document/product/614). For how to enable, see [Nginx-ingress Log Configuration](https://intl.cloud.tencent.com/document/product/457/38983).

>?It is strongly recommend to enable monitoring and log configurations for all Nginx Ingress instances.

#### Viewing monitoring dashboard

1. After enabling the monitoring configuration, you can click **View Monitoring** to go to the cloud native monitoring, as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/4c37a0df6d9bb32f0926e37dfac9cca8.png)
2. Enter the Grafana dashboard and switch to the **NGINX Ingress controller** dashboard to check the monitoring views, as shown below:
![](https://main.qcloudimg.com/raw/82ae23289f21bdd5d0bc9cdf3a8b8ed7.png)

#### Log search and log dashboard

After enabling the log configuration, you can click **More** under **Operation** on the right side of an instance in the Nginx Ingress list page, and select **Check access logs in CLS** or **View Access Log Dashboard**. as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/43b136031103365a24c7380ecdc121f7.png)
- Click **Check access logs in CLS** to go to the CLS and select the logset and topic corresponding to the instance in **Search and Analyze** to view the access and error logs of Nginx Ingress.
- Click **View Access Log Dashboard** to go to the dashboard that displays statistics based on the Nginx Ingress log data.

