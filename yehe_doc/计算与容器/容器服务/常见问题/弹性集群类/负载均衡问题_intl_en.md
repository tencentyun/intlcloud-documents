

This document describes the FAQs of CLB, and introduces the causes and solutions of various FAQs of Service/Ingress CLB.

Prerequisites:
- You are familiar with K8s [Concepts](https://kubernetes.io/zh/docs/concepts/), such as Pod, workload, Service, Ingress, etc.
- You are familiar with the general operations of Elastic Cluster in [TKE console](https://console.cloud.tencent.com/tke2/ecluster?rid=1).
- You can use kubectl command line tool to manage the K8s cluster resources.



>! There are many methods to manage the K8s cluster resources. This document describes how to manage K8s cluster resources through the Tencent Cloud console and kubectl command line tool.


[](id:Ingress)
### Which Ingress can EKS create CLB instance for?
EKS will create CLB instances for Ingress that meets the following conditions:

<table>
<thead>
<tr>
<th>Requirements for Ingress resources</th>
<th>Notes</th>
</tr>
</thead>
<tbody><tr>
<td>annotations contains the following key-value pairs: kubernetes.io/ingress.class: qcloud</td>
<td>If you don’t want EKS to create a CLB instance for Ingress, for example, you want to use nginx-Ingress, you only need to make sure the key-value pairs are not contained in the annotations.</td>
</tr>
</tbody></table>





### How do I view the CLB instance created by EKS for Ingress?





If EKS has successfully created CLB instance for Ingress, it will write the VIP of the CLB instance into the `status.loadBalancer.ingress` of the Ingress resource, and write the following key-value pairs into annotations.
```plaintext
kubernetes.io/ingress.qcloud-loadbalance-id: CLB instance ID
```

To view the CLB instance created by EKS for Ingress:
1. Log in to the TKE console and click **[Elastic Cluster](https://console.cloud.tencent.com/tke2/ecluster?rid=1)** in the left sidebar.
2. On the "Elastic Cluster" page, click the ID of the target cluster to go to the cluster management page.
3. In the cluster management page, select **Services and Routes** > **Ingress** in the left sidebar.
4. You can find the CLB instance ID and its VIP in the **Ingress** page, as shown in the figure below:
![](https://main.qcloudimg.com/raw/df7c11ad5612690543b6b54a151a3c68.png)

[](id:Service)
### Which Service can EKS create CLB instance for?
EKS will create CLB instances for Service that meets the following conditions:


<table>
<thead>
<tr>
<th>K8s Version</th>
<th>Requirements for Service resources</th>
</tr>
</thead>
<tbody><tr>
<td>All K8s versions supported by EKS</td>
<td>spec.type is LoadBalancer.</td>
</tr>
<tr>
<td>The modified version of K8s (Server GitVersion returned by kubectl version has "eks.*" or "tke.*" suffix).</td>
<td>spec.type is ClusterIP, and the value of spec.clusterIP is <strong>not</strong> None (that is, a non-Headless ClusterIP Service).</td>
</tr>
<tr>
<td>The non-modified version of K8s (Server GitVersion returned by kubectl version does not have "eks.*" or "tke.*" suffix).</td>
<td>spec.type is ClusterIP, and spec.clusterIP is specified as an empty string ("").</td>
</tr>
</tbody></table>



>! If the CLB instance is successfully created, EKS will write the following key-value pairs into Service annotations:
>```plaintext
>service.kubernetes.io/loadbalance-id: CLB instance ID
>```




### How do I view the CLB instance created by EKS for the Service?
If EKS has successfully created CLB instance for Service, it will write the VIP of the CLB instance into the `status.loadBalancer.ingress` of the Service resource, and write the following key-value pairs into annotations.
```plaintext
kubernetes.io/ingress.qcloud-loadbalance-id: CLB instance ID
```
To view the CLB instance created by EKS for Service:
1. Log in to the TKE console and click **[Elastic Cluster](https://console.cloud.tencent.com/tke2/ecluster?rid=1)** in the left sidebar.
2. On the "Elastic Cluster" page, click the ID of the target cluster to go to the cluster management page.
3. In the cluster management page, select **Services and Routes** > **Service** in the left sidebar.
4. You can find the CLB instance ID and its VIP in the **Service** page, as shown in the figure below:
![](https://main.qcloudimg.com/raw/d7f3465e7e11921768390504661b9c74.png)

### Why is the ClusterIP of Service invalid (cannot be accessed normally) or there is no ClusterIP?
For the Service whose spec.type is LoadBalancer, currently EKS does not allocate ClusterIP by default, or the allocated ClusterIP is invalid (cannot be accessed normally). If users need to use ClusterIP to access the Service, they can add the following key-value pairs in annotations to indicate that EKS implements ClusterIP based on the private network CLB.
```plaintext
service.kubernetes.io/qcloud-clusterip-loadbalancer-subnetid: Service CIDR subnet ID
```
The Service CIDR subnet ID is specified when you create the cluster, and is a string in `subnet-********` format. You can view the subnet ID on the CLB basic information page.


>!Only EKS clusters that use the modified version of K8s (Server GitVersion returned by kubectl version has "eks.*" or "tke.*" suffix) supports this feature. For the EKS clusters created earlier that use the non-modified version of K8s (the Server GitVersion returned by kubectl version does not have the "eks.*" or "tke.*" suffix), you need to upgrade the K8s version to use this feature.



### How do I specify the CLB instance type (public or private network)?
You can specify the CLB instance type via TKE console or Kubectl command line tool.
#### Specifying via TKE console
- For Ingress, select **Public Network** or **Private Network** for **Network Type** to specify the CLB instance type.
![](https://main.qcloudimg.com/raw/70c560014a3c6219d57f2f4d8681263d.png)

- For Service, set the **Service Access** to specify the CLB instance type. **Via VPC** means the private network CLB instance.
![](https://main.qcloudimg.com/raw/cdd3ff57d349ed587a86c645233e807f.png)

#### Specifying via kubectl command line tool
- The created CLB instance is of the “public network” type by default.
- If you need to create a CLB instance of the "private network" type, you need to add the corresponding annotation for the Service or Ingress.

| Resource Type | Add the following key-value pairs in the annotation |
|----------------------------------------------------|------------------------------------------|
| Service | service.kubernetes.io/qcloud-loadbalancer-internal-subnetid: subnet ID |
| Ingress | kubernetes.io/ingress.subnetId: subnet ID |


>! The subnet ID is a string in the form of subnet-********, and the subnet must be in the VPC specified for the **Cluster Network** when creating the cluster. The VPC information can be found in the **Basic Information** of the cluster in TKE console.




### How do I specify the existing CLB instance?
You can specify the existing CLB instance via TKE console or Kubectl command line tool.
####  Specifying via TKE console
When creating a Service or Ingress, you can select **Use Existing** to use the existing CLB instance. For Service, you can switch to “Use Existing” to use the existing CLB instance through “Update Access Method” after Service is created.

#### Specifying via kubectl command line tool
When creating a Service/Ingress or modifying a Service, you need to add the corresponding annotation for the Service or Ingress.

| Resource Type | Add the following key-value pairs in the annotation |
|----------------------------------------------------|------------------------------------------|
| Service | service.kubernetes.io/tke-existed-lbid:  CLB instance ID |
| Ingress | kubernetes.io/ingress.existLbId: CLB instance ID |



>!The existing CLB instance cannot be the CLB instance created by EKS for Service or Ingress, and EKS does not support multiple Service/Ingress to share the same existing CLB instance.







### How do I view the access log of a CLB instance?
Only the layer-7 CLB instance supports configuring access logs, but the access logs of layer-7 CLB instance created by EKS for Ingress is not enabled by default. You can enable the access log of the CLB instance in the details page of the CLB instance, as shown below:
1. Log in to the TKE console and click **[Elastic Cluster](https://console.cloud.tencent.com/tke2/ecluster?rid=1)** in the left sidebar.
2. On the "Elastic Cluster" page, click the ID of the target cluster to go to the cluster management page.
3. In the cluster management page, select **Services and Routes** > **Ingress** in the left sidebar.
4. In **Ingress** page, click the CLB instance ID to go to the CLB basic information page.
![](https://main.qcloudimg.com/raw/32a6e8e6eb32fb57ef30397cc538b779.png)
5. In **Access Log (Layer-7)** section of CLB basic information page, click <img src="https://main.qcloudimg.com/raw/e941fb45439168529b4dad02337b4823.png" style="margin:-3px 0px"/> to enable CLB access log, as shown below:
![](https://main.qcloudimg.com/raw/e7e0ec9032c12e9b094ea3f10d80dff1.png)


### Why didn't EKS create a CLB instance for Ingress or Service?
Please refer to [Which Ingress can EKS create CLB instance for?](#Ingress) and [Which Service can EKS create CLB instance for?](#Service) to confirm whether the corresponding resources have the conditions to create CLB instance. If the conditions are met but the CLB instance is not successfully created, you can use the `kubectl describe` command to view the related events of the resource.
Generally, EKS will output the related “Warning” events. In the following example, the output event indicates that there are no available IP resources in the subnet, so the CLB instance cannot be successfully created.
![](https://main.qcloudimg.com/raw/1b8a8815c0478a3acf6735f991bf7f8f.png)


### Why do I fail to access CLB VIP?
Please follow the steps below to analyze:

#### Viewing the CLB instance type
 1. On the **Service** or **Ingress** page, click the CLB instance ID to go to the CLB basic information page.
![](https://main.qcloudimg.com/raw/8d8d309a9906d6685cf292899d5501b1.png)   
 2. You can view the **Instance Type** of the above CLB instance in the CLB basic information page.      

#### Confirming whether the environment for accessing CLB VIP is normal
 - If the **Instance Type** of the CLB instance is the private network, its VIP can only be accessed in the VPC to which it belongs.
 Since the IP of the Pods in the EKS cluster is the ENI IP in the VPC, you can access the VIP of the CLB instance of any Service or Ingress in the cluster in the Pods.
>!LoadBalancer system always has loopback problems (for example, [**Troubleshoot Azure Load Balancer**](https://docs.microsoft.com/en-us/azure/load-balancer/load-balancer-troubleshoot#cause-3- accessing-the-load-balancer-from-the-same-vm-and-network-interface )). Please do not access the services provided by the workload through the VIP opened by itself (via Service or Ingress) in the Pods to which this workload belongs. That is, Pods should not access the services provided by themselves through VIP (including "private network" and "public network"). Otherwise, the access delay may increase, or the access will be blocked when there is only one RS/Pod under the rules corresponding to the VIP.
 - If the **Instance Type** of the CLB instance is the public network, its VIP can be accessed in an environment with public network access enabled.
If you want to access the public network VIP in the cluster, please ensure that the public network access has been enabled for the cluster by configuring a NAT gateway or other methods.

#### Viewing the RS in CLB including (and only including) the IP and port of the expected Pods
In CLB management page, select the **Listener Management** tab to view the forwarding rules (layer-7 protocol) and the bound backend services (layer-4 protocol). The IP address is expected to be the IP of each Pod. The example is as follows:
![](https://main.qcloudimg.com/raw/ca445b6b0705aecf48c247d5136c67b1.png)
        

#### Confirming whether the corresponding Endpoints are normal
If you have correctly set the labels for the workload and the Selectors for the Service resource, after the Pods of the workload run successfully, you can find that Pods are added by K8S to the ready IP list of the Endpoints corresponding to the Service by running the `kubectl get endpoints` command. The example is as follows:
![](https://main.qcloudimg.com/raw/a9c2f30d7fe877a86c2c4c4698149719.png)
Pods that are created but in an abnormal state are added by K8S to the unready IP list of the Endpoints corresponding to the Service. The example is as follows:
![](https://main.qcloudimg.com/raw/e05d38fb229a83add115abfcb2a9529f.png)

>!You can run the `kubectl describe` command to view the cause of the abnormal Pods. >The command is as follows:
>```plaintext
>kubectl describe pod nginx-7c7c647ff7-4b8n5 -n demo
>```


#### Confirming whether Pods can provide services normally
Even Pods in the Running state may not be able to provide services normally due to some exceptions. For example, the specified protocol + port are not listened to, the internal logic of Pods is incorrect, the process is blocked, etc. You can run the `kubectl exec` command to log in to the Pod, and run the `telnet/wget/curl` command or use a custom client tool to directly access the Pod IP+ port. If the direct access fails in the Pod, you need to further analyze the reasons why the Pod cannot provide services normally.

#### Confirm whether the security group bound to the Pod allows the protocol and port of the service provided by the Pod
The security group controls the network access policy of Pods, just like the IPTables rules in the Linux server. Please check based on the actual situation:


#### Creating a workload via TKE console
The interactive process requires to specify a security group, and EKS will use this security group to control the Pods' network access policy. The specified security group will be stored in the `spec.template.metadata.annotations` of the workload, and finally added to the annotations of the Pods. Examples are as follows:
![](https://main.qcloudimg.com/raw/6cda3f21be34e514927c10b840b0acaa.png)

#### Running kubectl command to create a workload
If you create a workload through the kubectl command and do not specify a security group for Pods (by adding annotations), EKS will use the default security group of the default project in the same region under the account. The directions are as follows:
 1. Log in to the VPC console, and click **[Security Group](https://console.cloud.tencent.com/vpc/securitygroup?rid=5&rid=5)** in the left sidebar.
 2. Select the **Default Project** of the same region at the top of the **Security Group** page.
 3. You can view the default security group in the list, and click **Modify Rule** to view the details.
![](https://main.qcloudimg.com/raw/a443c60e8dba406138ac2acacf7b6bf9.png)





#### Contact us
If the problem persists, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact us.

