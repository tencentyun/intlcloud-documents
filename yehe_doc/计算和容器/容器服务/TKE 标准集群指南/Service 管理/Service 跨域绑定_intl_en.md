## Overview

When you use the Service of public network CLB type, the CLB is generated for random availability zone in the VPC where the cluster resides by default. Currently, TKE Service of public network CLB allows you to specify availability zones, including availability zones in other regions. This document describes how to bind and specify availability zones for CLB Service across regions via the console and YAML.


## Use Cases

- The cross-region access or cross-VPC access of CLB must be supported. That is, the VPC where the CLB resides and the VPC where the cluster resides are not in the same VPC.
- The availability zone of CLB must be specified to realize unified management of resources.

>?
> 1. Cross-region binding is only available to bill-by-IP accounts.
> 2. If you need to use the CLB that is not in the same VPC as this cluster, you need to connect the VPCs of the current cluster and the CLB via [CCN](https://intl.cloud.tencent.com/document/product/1003/30062).
> 2. After the VPCs are connected, please [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) to apply for this feature.
> 3. You should enter the region ID in the following YAML. You can check the region ID in [Regions and Availability Zones](https://intl.cloud.tencent.com/document/product/457/36736).


## Directions

You can bind and specify availability zones for CLB Service across regions via the console and YAML.


<dx-tabs>
:::Console
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. In the **Cluster** page, click the ID of the cluster for which you need to create a Service to go to the cluster management page.
3. Select **Services and Routes** > **Service** to go to the **Service** management page, as shown below:
   ![](https://main.qcloudimg.com/raw/7b2a359695867defbbf8f9d12da1cd64.png)
4. Click **Create** to go to the **Create Service** page.
5. Configure the availability zone rules in the “Create Service” page. The configuration rules are as follows:
 - **Service Access**: select **LoadBalancer (public network)**.
 - **Current VPC**: use the CLB in the VPC where the cluster resides. **Random AZ** is recommended to avoid the instance creation failure due to the resource shortage in the specified availability zone.
 - **Other VPC**: it only supports the VPC that has connected to the VPC of the current cluster via [CCN](https://console.cloud.tencent.com/vpc/ccn). **Random AZ** is recommended to avoid the instance creation failure due to the resource shortage in the specified availability zone.
     ![](https://main.qcloudimg.com/raw/897bf7ca89f2b22377c273915def1683.png)
     :::
     ::: YAML
     <dx-alert infotype="explain" title="">
1. If you need to use the CLB that is not in the same VPC as this cluster, you need to connect the VPCs of the current cluster and the CLB via [CCN](https://intl.cloud.tencent.com/document/product/1003/30062).
2. After the VPCs are connected, please [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) to apply for this feature.
</dx-alert>
#### Sample 1
If you only need to specify the availability zone of the VPC where the cluster resides, for example, if the VPC of the cluster is located in Guangzhou, and you need to specify the CLB of Guangzhou Zone 1 for CLB Service, you can add the following annotations to the YAML of the Service:
```sh
service.kubernetes.io/service.extensiveParameters: '{"ZoneId":"ap-guangzhou-1"}'
```
#### Sample 2
If you need to use a CLB that is not in the VPC of the cluster, you can add the following annotations to the YAML of the Service:
<dx-codeblock>
:::  sh
service.cloud.tencent.com/cross-region-id: "ap-guangzhou" 
service.cloud.tencent.com/cross-vpc-id: "vpc-646vhcjj"
:::
</dx-codeblock><dx-alert infotype="notice" title="">
If you need to specify the availability zone, you also need to add the annotations of sample 1.
</dx-alert>
#### Sample 3
Select an existing load balancer for remote access, as shown below:
<dx-codeblock>
:::  yaml
service.cloud.tencent.com/cross-region-id: "ap-guangzhou" 
service.kubernetes.io/tke-existed-lbid: "lb-342wppll"
:::
</dx-codeblock>
#### Sample 4 
The annotation in the service YAML is as follows:
<dx-codeblock>
:::  yaml
# Create a CLB for remote access
apiVersion: v1
kind: Service
metadata: 
  annotations: 
    service.cloud.tencent.com/cross-region-id: "ap-chongqing"
    service.cloud.tencent.com/cross-vpc-id: "vpc-mjekzyps"
  name: echo-server-service
  namespace: default
spec: 
  ...... 
--- 
# Use the existing CLB of other region
apiVersion: v1
kind: Service
metadata: 
  annotations: 
    service.cloud.tencent.com/cross-region-id: "ap-chongqing"
    service.kubernetes.io/tke-existed-lbid: "lb-o8ugf2wb"
  name: echo-server-service
  namespace: default
spec: 
  ...... 
:::
</dx-codeblock>For detailed Service annotations, please see [Service Annotation](https://intl.cloud.tencent.com/document/product/457/39142).
:::
</dx-tabs>
