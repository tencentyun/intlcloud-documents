

This document describes the FAQs of CLB, as well as the causes and solutions of various FAQs of Service/Ingress CLB.

Prerequisites:
- You are familiar with K8s [Concepts](https://kubernetes.io/zh/docs/concepts/), such as Pod, workload, Service, Ingress, etc.
- You are familiar with the general operations of Serverless Cluster in the [TKE console](https://console.cloud.tencent.com/tke2/ecluster?rid=1).
- You can use kubectl command line tool to manage the resources in K8s clusters.


<dx-alert infotype="notice" title=" ">
You can manage the K8s cluster resources in various ways. This document describes how to manage K8s cluster resources in Tencent Cloud console and through the kubectl command line tool.
</dx-alert>


### Which Ingress can TKE Serverless create CLB instance for?[](id:Ingress)
TKE Serverless will create CLB instances for Ingress that meets the following conditions:

<table>
<thead>
<tr>
<th>Requirements for Ingress resources</th>
<th>Notes</th>
</tr>
</thead>
<tbody><tr>
<td>Annotations contain the following key-value pairs: kubernetes.io/ingress.class: qcloud</td>
<td>If you don’t want TKE Serverless to create a CLB instance for Ingress (if, for example, you want to use Nginx-Ingress), you only need to make sure the key-value pairs are not contained in the annotations.</td>
</tr>
</tbody></table>





### How do I view the CLB instance created by TKE Serverless for Ingress?





If TKE Serverless has successfully created a CLB instance for Ingress, it will write the VIP of the CLB instance to the `status.loadBalancer.ingress` of the Ingress resource, and write the following key-value pairs to annotations.
```plaintext
kubernetes.io/ingress.qcloud-loadbalance-id: CLB instance ID
```

To view the CLB instance created by TKE Serverless for Ingress:
1. Log in to the TKE console and select **[Serverless Cluster](https://console.cloud.tencent.com/tke2/ecluster?rid=1)** in the left sidebar.
2. On the "Serverless cluster" page, click the ID of the target cluster to go to the cluster management page.
3. On the cluster management page, select **Service and route** > **Ingress** in the left sidebar.
4. You can find the CLB instance ID and its VIP on the **Ingress** page.
![](https://main.qcloudimg.com/raw/df7c11ad5612690543b6b54a151a3c68.png)

### Which Service can TKE Serverless create CLB instance for?[](id:Service)
TKE Serverless will create CLB instances for Service that meets the following conditions:


<table>
<thead>
<tr>
<th>K8s Version</th>
<th>Requirements for Service Resources</th>
</tr>
</thead>
<tbody><tr>
<td>All K8s versions supported by TKE Serverless</td>
<td>spec.type is LoadBalancer.</td>
</tr>
<tr>
<td>The modified version of K8s (Server GitVersion returned by kubectl version has the "eks.*" or "tke.*" suffix)</td>
<td>spec.type is ClusterIP, and the value of `spec.clusterIP` is <strong>not</strong>None, indicating a non-Headless ClusterIP Service.</td>
</tr>
<tr>
<td>The non-modified version of K8s (Server GitVersion returned by kubectl version does not have the "eks.*" or "tke.*" suffix)</td>
<td>spec.type is ClusterIP, and spec.clusterIP is specified as an empty string ("").</td>
</tr>
</tbody></table>


<dx-alert infotype="notice" title=" ">
If the CLB instance is successfully created, TKE Serverless will write the following key-value pairs to Service annotations:
```plaintext
service.kubernetes.io/loadbalance-id: CLB instance ID
```
</dx-alert>



### How do I view the CLB instance created by TKE Serverless for the Service?
If TKE Serverless has successfully created a CLB instance for Service, it will write the VIP of the CLB instance to the `status.loadBalancer.ingress` of the Service resource, and write the following key-value pairs to annotations.
```plaintext
kubernetes.io/ingress.qcloud-loadbalance-id: CLB instance ID
```
To view the CLB instance created by TKE Serverless for Service:
1. Log in to the TKE console and select **[Serverless Cluster](https://console.cloud.tencent.com/tke2/ecluster?rid=1)** in the left sidebar.
2. On the "Serverless cluster" page, click the ID of the target cluster to go to the cluster management page.
3. On the cluster management page, select **Service and route** > **Service** in the left sidebar.
4. You can find the CLB instance ID and its VIP on the **Service** page.
![](https://main.qcloudimg.com/raw/d7f3465e7e11921768390504661b9c74.png)

### Why is the ClusterIP of Service invalid (cannot be accessed normally) or why is there no ClusterIP?
For the Service whose spec.type is LoadBalancer, currently TKE Serverless does not allocate ClusterIP by default, or the allocated ClusterIP is invalid (cannot be accessed normally). If users need to use ClusterIP to access the Service, they can add the following key-value pairs in annotations to indicate that TKE Serverless implements ClusterIP based on the private network CLB.
```plaintext
service.kubernetes.io/qcloud-clusterip-loadbalancer-subnetid: Service CIDR block subnet ID
```
The Service CIDR block subnet ID, which is specified when you create the cluster, is a string in `subnet-********` format. You can view the subnet ID on the CLB basic information page.

<dx-alert infotype="notice" title=" ">
Only TKE Serverless clusters that use the modified version of K8s (Server GitVersion returned by kubectl version has the "eks.*" or "tke.*" suffix) supports this feature. For the TKE Serverless clusters created earlier that use the non-modified version of K8s (the Server GitVersion returned by kubectl version does not have the "eks.*" or "tke.*" suffix), you need to upgrade the K8s version to use this feature.
</dx-alert>



### How do I specify the CLB instance type (public or private network)?
You can specify the CLB instance type via TKE console or Kubectl command line tool.
<dx-tabs>
::: Specifying via TKE console
- For Ingress, select **Public network** or **Private network** for **Network type** to specify the CLB instance type.
![](https://main.qcloudimg.com/raw/70c560014a3c6219d57f2f4d8681263d.png)

- For Service, set the **Service access** to specify the CLB instance type. **Via VPC** means the private network CLB instance.
![](https://main.qcloudimg.com/raw/cdd3ff57d349ed587a86c645233e807f.png)
:::
::: Specifying via kubectl command line tool
- The created CLB instance is of the “public network” type by default.
- If you need to create a CLB instance of the "private network" type, you need to add the corresponding annotation for the Service or Ingress.

| Resource Type | Key-value pairs to be added to annotations |
|----------------------------------------------------|------------------------------------------|
| Service | service.kubernetes.io/qcloud-loadbalancer-internal-subnetid: subnet ID |
| Ingress | kubernetes.io/ingress.subnetId: subnet ID |

<dx-alert infotype="notice" title=" ">
The subnet ID is a string in the form of `subnet-********`, and the subnet must be in the VPC specified for the **Cluster network** when creating the cluster. The VPC information can be found in the **Basic information** of the cluster in TKE console.
</dx-alert>

:::
</dx-tabs>



### How do I specify the existing CLB instance?
You can specify the existing CLB instance via TKE console or Kubectl command line tool.
<dx-tabs>
::: Specifying via TKE console
When creating a Service or Ingress, you can select **Use existing** to use the existing CLB instance. For Service, you can switch to “Use existing” to use the existing CLB instance through “Update access method” after Service is created.
:::
::: Specifying via kubectl command line tool
When creating a Service/Ingress or modifying a Service, you need to add the corresponding annotation for the Service or Ingress.

| Resource Type | Key-value pairs to be added to annotations |
|----------------------------------------------------|------------------------------------------|
| Service | service.kubernetes.io/tke-existed-lbid:  CLB instance ID |
| Ingress | kubernetes.io/ingress.existLbId: CLB instance ID |


<dx-alert infotype="notice" title=" ">
The existing CLB instance cannot be the CLB instance created by TKE Serverless for Service or Ingress, and TKE Serverless does not support multiple Service/Ingress to share the same existing CLB instance.
</dx-alert>

:::
</dx-tabs>



### How do I view the access log of a CLB instance?
Only the layer-7 CLB instance supports configuring access logs, but the access logs of layer-7 CLB instance created by TKE Serverless for Ingress is not enabled by default. You can enable the access log of the CLB instance in the details page of the CLB instance, as shown below:
1. Log in to the TKE console and select **[Serverless Cluster](https://console.cloud.tencent.com/tke2/ecluster?rid=1)** in the left sidebar.
2. On the "Serverless cluster" page, click the ID of the target cluster to go to the cluster management page.
3. On the cluster management page, select **Service and route** > **Ingress** in the left sidebar.
4. On the **Ingress** page, click the CLB instance ID to go to the CLB basic information page.
![](https://main.qcloudimg.com/raw/32a6e8e6eb32fb57ef30397cc538b779.png)
5. In the **Access log (layer-7)** section of CLB basic information page, click <img src="https://main.qcloudimg.com/raw/e941fb45439168529b4dad02337b4823.png" style="margin:-3px 0px"/> to enable CLB access log.
![](https://main.qcloudimg.com/raw/e7e0ec9032c12e9b094ea3f10d80dff1.png)


### Why didn't TKE Serverless create a CLB instance for Ingress or Service?
Please refer to [Which Ingress can TKE Serverless create CLB instance for?](#Ingress) and [Which Service can TKE Serverless create CLB instance for?](#Service) to confirm whether the corresponding resources have the conditions to create CLB instance. If the conditions are met but the CLB instance is not successfully created, you can use the `kubectl describe` command to view the related events of the resource.
Generally, TKE Serverless will output the related “Warning” events. In the following example, the output event indicates that there are no available IP resources in the subnet, so the CLB instance cannot be successfully created.
![](https://main.qcloudimg.com/raw/1b8a8815c0478a3acf6735f991bf7f8f.png)




### How do I use the same CLB in multiple Services?
For TKE Serverless clusters, multiple Services cannot share the same CLB instance by default. If you hope that a Service uses the CLB occupied by other Services, please add this annotation and specify the value as "true": `service.kubernetes.io/qcloud-share-existed-lb: true`. For more information on this annotation, see [Annotation](https://intl.cloud.tencent.com/document/product/457/36162).




### Why do I fail to access CLB VIP?
Please follow the steps below to analyze:

#### Viewing the CLB instance type
 1. On the **Ingress** page, click the CLB instance ID to go to the CLB basic information page.
![](https://main.qcloudimg.com/raw/8d8d309a9906d6685cf292899d5501b1.png)   
 2. You can view the **Instance type** of the above CLB instance on the CLB basic information page.       

#### Confirming whether the environment for accessing CLB VIP is normal
 - If the **Instance type** of the CLB instance is the private network, its VIP can only be accessed in the VPC to which it belongs.
 Since the IP of the Pods in the TKE Serverless cluster is the ENI IP in the VPC, you can access the VIP of the CLB instance of any Service or Ingress in the cluster in the Pods.

>!LoadBalancer system always has loopback problems （for example, [Troubleshoot **Azure** Load Balancer](https://docs.microsoft.com/en-us/azure/load-balancer/load-balancer-troubleshoot#cause-3-accessing-the-load-balancer-from-the-same-vm-and-network-interface )）. Please do not access the services provided by the workload through the VIP opened by itself (via Service or Ingress) in the Pods to which this workload belongs. That is, Pods should not access the services provided by themselves through VIP (including "private network" and "public network"). Otherwise, the access delay may increase, or the access will be blocked when there is only one RS/Pod under the rules corresponding to the VIP.
 - If the **Instance type** of the CLB instance is the public network, its VIP can be accessed in an environment with public network access enabled.
If you want to access the public network VIP in the cluster, please ensure that the public network access has been enabled for the cluster by configuring a NAT gateway or other methods.

#### Viewing the RS in CLB including (and only including) the IP and port of the expected Pods
On the CLB management page, select the **Listener management** tab to view the forwarding rules (layer-7 protocol) and the bound backend services (layer-4 protocol). The IP address is expected to be the IP of each Pod. The example is as follows:
![](https://main.qcloudimg.com/raw/ca445b6b0705aecf48c247d5136c67b1.png)
        

#### Confirming whether the corresponding Endpoints are normal
If you have correctly set the labels for the workload and the Selectors for the Service resource, after the Pods of the workload run successfully, you can find that Pods are added by K8s to the ready IP list of the Endpoints corresponding to the Service by running the `kubectl get endpoints` command. The example is as follows:
![](https://main.qcloudimg.com/raw/a9c2f30d7fe877a86c2c4c4698149719.png)
Pods that are created but in an abnormal state are added by K8s to the unready IP list of the Endpoints corresponding to the Service. The example is as follows:
![](https://main.qcloudimg.com/raw/e05d38fb229a83add115abfcb2a9529f.png)
<dx-alert infotype="notice" title=" ">
You can run the `kubectl describe` command to view the cause of the abnormal Pods. The command is as follows:
```plaintext
kubectl describe pod nginx-7c7c647ff7-4b8n5 -n demo
```
</dx-alert>

#### Confirming whether Pods can provide services normally
Even Pods in the Running state may not be able to provide services normally due to some exceptions. For example, the specified protocol + port are not listened to, the internal logic of Pods is incorrect, the process is blocked, etc. You can run the `kubectl exec` command to log in to the Pod, and run the `telnet/wget/curl` command or use a custom client tool to directly access the Pod IP+ port. If the direct access fails in the Pod, you need to further analyze the reasons why the Pod cannot provide services normally.

#### Confirming whether the security group bound to the Pod allows the protocol and port of the service provided by the Pod
The security group controls the network access policy of Pods, just like the IPTables rules in the Linux server. Please check based on the actual situation:


<dx-tabs>
::: Creating a workload via TKE console
The interactive process requires to specify a security group, and TKE Serverless will use this security group to control the Pods' network access policy. The specified security group will be stored in the `spec.template.metadata.annotations` of the workload, and finally added to the annotations of the Pods. Examples are as follows:
![](https://main.qcloudimg.com/raw/6cda3f21be34e514927c10b840b0acaa.png)
:::
::: Running kubectl command to create a workload
If you create a workload through the kubectl command and do not specify a security group for Pods (by adding annotations), TKE Serverless will use the default security group of the default project in the same region under the account. The directions are as follows:
 1. Log in to the VPC console, and click **[Security Group](https://console.cloud.tencent.com/vpc/securitygroup?rid=5&rid=5)** in the left sidebar.
 2. Select **Default project** of the same region at the top of the **Security group** page.
 3. You can view the default security group in the list, and click **Modify rule** to view the details.
![](https://main.qcloudimg.com/raw/a443c60e8dba406138ac2acacf7b6bf9.png)
:::
</dx-tabs>




#### Contact us
If the problem persists, please [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) to contact us.

