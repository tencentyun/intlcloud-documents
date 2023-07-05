## Overview 

All cloud users want their migrations to the cloud to be efficient, stable, and highly available, but this depends on system availability, data reliability, and OPS stability. This document describes the check items for deploying containerized applications to the cloud from three perspectives: evaluation item, impact, and reference. This will help ensure you experience a smooth and efficient migration to Tencent Kubernetes Engine (TKE).


## Check Items

### System availability
<table>
	<th style="width:10%">Category</th><th style="width:32%">Item</th><th style="5%">Type</th><th style="width:38%">Impact</th><th style="width:15%">Reference</th>
    <tr>
        <td rowspan="6">Cluster</td>
				<td>Before creating a cluster, plan the node network and container network to suit your application scenario to prevent restricted capacity scaling in the future.</td>
				<td>Network planning</td>
				<td>If you have small-scale subnets or container IP ranges, your cluster may support fewer nodes than your application actually needs.</td>
				<td><li><a href="https://intl.cloud.tencent.com/document/product/215/31795">Network Planning</a></li><li><a href="https://intl.cloud.tencent.com/document/product/457/38966">Network Settings for Containers and Nodes</a></li></td>
    </tr>
    <tr>
        <td>Before creating a cluster, review your planning of direct connect, peering connection, container IP ranges, and subnet IP ranges to prevent IP range conflicts and impacts on your applications.</td>
				<td>Network planning</td>
				<td>For simple networking scenarios, follow the instructions on the page to configure cluster-related IP ranges to avoid conflicts. For complex networking
scenarios, such as peering connection, direct connect, and VPN, improper network planning can affect the normal communication within your application.
</td><td>-</td>
    </tr>
    <tr>
        <td>When you create a cluster, a new security group is automatically bound to the cluster. You can also set custom security group rules to meet the needs of your application.</td>
				<td>Deployment</td>
				<td>Security groups provide an important means of security isolation. Improper security policy configuration may lead to security-related risks, service connectivity issues, and other problems.</td><td><a href="https://intl.cloud.tencent.com/document/product/457/9084">Configuring TKE Security Groups</a></td>
    </tr>
    <tr>
        <td>As the runtime components currently supported by TKE, Containerd and Docker suit different scenarios. When creating a cluster, select the appropriate container runtime component according to your application scenarios.</td><td>Deployment</td><td>Once the cluster is created, modifications to the runtime component and version only take effect to new nodes that are not assigned to any node pool. Existing nodes are not affected.</td><td><a href="https://intl.cloud.tencent.com/document/product/457/31088">How to Choose Between Containerd and Docker</a></td>
    </tr>
	<tr>
        <td>By default, Kube-proxy uses iptables to balance the load between Service and Pod. When creating a cluster, you can quickly enable IPVS for traffic distribution and load balancing.</td>
				<td>Deployment</td>
				<td>You can enable IPVS when creating a cluster. It will take effect for the entire cluster and cannot be disabled.</td>
				<td><a href="https://intl.cloud.tencent.com/document/product/457/30641">Enabling IPVS for a Cluster</a></td>
    </tr>
	<tr>
        <td>When creating a cluster, choose the independent cluster mode or managed cluster mode as needed.</td><td>Deployment</td><td>The Master and Etcd of the managed cluster are not user resources and are managed and maintained by Tencent Cloud's technical team. You cannot modify the deployment scale and service parameters of Master and Etcd. If you do need to modify them, choose the independent deployment mode.</td>
				<td><li><a href="https://intl.cloud.tencent.com/document/product/457/30635">Cluster Overview</a></li><li><a href="https://intl.cloud.tencent.com/document/product/457/31417">Introduction to Cluster Hosting Modes</a></li></td>
    </tr>
    <tr>
        <td rowspan="4">Workload<br></td>
				<td>When creating a workload, set the CPU and memory limits to improve the robustness of your application.</td>
				<td>Deployment</td>
				<td>When multiple applications are deployed on one node, if an application without resource upper and lower limits encounters a resource leak, exceptions will occur in other applications on the same node due to the lack of resources, and they will report monitoring information errors.</td><td><a href="https://intl.cloud.tencent.com/document/product/457/30667">Setting Resource Limits for Workloads</a></td>    </tr>
    <tr>
        <td>When creating a workload, you can configure container health checks, which are "liveness check" and "readiness check".</td><td>Reliability</td><td>If container health checks are not configured, when application exceptions occur, the pod will not be able to detect them to automatically restart the application for recovery. In this case, while the pod seems normal, the application in the pod will behave abnormally.</td><td><a href="https://intl.cloud.tencent.com/document/product/457/30669">Configuring Health Checks for Workloads</a></td>
    </tr>
    <tr>
        <td>When creating a service, choose the appropriate service access method as needed. Four access methods are currently supported: Via Internet, Intra-cluster, Via VPC, and Node Port Access.</td>
				<td>Deployment</td>
				<td>An improper access method may cause access logic confusion and waste resources inside and outside the service.</td><td><a href="https://intl.cloud.tencent.com/document/product/457/36832">Service Management</a></td>
    </tr>
    <tr>
        <td>When creating a workload, do not set the number of pod replicas to 1. Set a node scheduling policy based on the needs of your application.</td>
				<td>Reliability</td>
				<td>Setting the number of pod replicas to 1 incurs service exceptions when node exceptions or pod exceptions occur. To ensure that your pod can be scheduled successfully, ensure that the node has resources available for container scheduling after setting the scheduling rules.</td><td><li><a href="https://intl.cloud.tencent.com/document/product/457/30662">Adjusting the Pod Quantity</a></li><li><a href="https://intl.cloud.tencent.com/document/product/457/30668">Setting Scheduling Rules for Workloads</a></li></td>
    </tr>
</table>


### Data reliability
<table>
	<th style="width:10%">Category</th><th style="width:32%">Item</th><th style="5%">Type</th><th style="width:38%">Impact</th><th style="width:15%">Reference</th>
    <tr>
        <td>Container data persistence</td><td>Apply pod data storage and choose an appropriate volume type as needed.</td><td>Reliability</td><td>When a node fails to be restored following an exception, the data in the local disk cannot be restored. However, cloud storage can provide extremely high data reliability in this situation.</td><td><a href="https://intl.cloud.tencent.com/document/product/457/30678">Volume Management</a></td>
    </tr>
</table>

### Ops stability
<table>
   	<th style="width:10%">Category</th><th style="width:32%">Item</th><th style="5%">Type</th><th style="width:38%">Impact</th><th style="width:15%">Reference</th>
    <tr>
        <td rowspan="2">Engineering</td><td>Check whether the quotas of resources such as CVMs, VPCs, subnets, and CBS disks can meet customer needs.</td><td>Deployment</td><td>Insufficient quotas will cause resource creation to fail. If you have enabled auto scaling, ensure that you have sufficient quotas for your Tencent Cloud services</td><td><li><a href="https://intl.cloud.tencent.com/document/product/457/9087">Quota Limits for Cluster Purchase</a></li><li><a href="https://intl.cloud.tencent.com/document/product/215/38959">Quota Limits</a></li></td>
    </tr>
    <tr>
        <td>We recommend that you do not modify the kernel parameters, system configurations, versions of cluster core components, security groups, and LB parameters on the nodes in your cluster.</td><td>Deployment</td><td>This may cause TKE cluster features or Kubernetes components installed on the node to fail, making the node unavailable for application deployment.</td><td><a href="https://intl.cloud.tencent.com/document/product/457/34022">High-risk Operations in TKE</a></td>
    </tr>
	<tr>
        <td>Proactive<br>OPS</td><td>TKE provides multidimensional monitoring and alarm features, along with basic resource monitoring provided by Cloud Monitor, to provide more refined metrics. Configuring monitoring and alarm helps you receive prompt alarms and locate faults in case of exceptions.</td><td>Monitoring</td><td>If the monitoring and alarm features are not configured, no normal standard can be established for container cluster performance, and alarms will not be promptly received when an exception occurs. In this case, you will have to manually inspect your environment.</td><td><li><a href="https://intl.cloud.tencent.com/document/product/457/30688">Setting Alarms</a></li><li><a href="https://intl.cloud.tencent.com/document/product/457/30689">Viewing Monitoring Data</a></li><li><a href="https://intl.cloud.tencent.com/document/product/457/30691">List of Monitoring and Alarm Metrics</a></li></td>
    </tr>
</table>
