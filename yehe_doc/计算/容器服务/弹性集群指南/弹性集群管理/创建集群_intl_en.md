## Operation Scenarios
This document describes how to create an elastic cluster in the TKE console to help you get started with Elastic Kubernetes Service (EKS).



## Prerequisites
You have activated required permissions for EKS in the [CAM console](https://console.cloud.tencent.com/cam/overview).

## Procedure
1. Log in to the TKE console and click **[Elastic Cluster](https://console.cloud.tencent.com/tke2/ecluster)** in the left sidebar.
2. On the page that appears, select the region where you want to create the elastic cluster and then click **Create**, as shown in the following figure.
![](https://main.qcloudimg.com/raw/b87df2b1d8b2ba95de0b91d859d17f41.png)
3. On the **Create Elastic Cluster** page that appears, specify the cluster information as prompted.
![](https://main.qcloudimg.com/raw/aecfb417ed5aa0b84bd17bf8d10e3410.png)
 - **Cluster Name**: indicates the name of the cluster to be created. The value is up to 60 characters in length.
 - **Kubernetes Version**: indicates the version of the cluster to be created. Version 1.12 and later can be selected. For a comparison of the features of different versions, see [Supported Versions of the Kubernetes Documentation](https://kubernetes.io/docs/home/supported-doc-versions/).
 - **Region**: indicates the region where the cluster to be created is located. We recommend that you select the region closest to you to help minimize access latency and improve the download speed.
 - **Cluster Network**: indicates an existing VPC for elastic clusters. You can select a subnet of the VPC to serve as a container network for the elastic cluster. For more information, see [VPC](https://intl.cloud.tencent.com/document/product/215/535).
 - **Container Network**: assigns an IP address within the container IP range for containers in the cluster. Pods in an elastic cluster directly use the IP addresses of a VPC subnet. We recommend that you select a subnet with sufficient available IP addresses that do not conflict with those of other products. For more information, see [Container Network Description](#ContainerNetwork).
 - **Cluster Description**: indicates the information about the cluster to be created. This description will be displayed on the **Cluster Information** page.
4. Click **Complete** to start creating the cluster. You can view the creation progress on the **Elastic Cluster** page.


## Container Network Description<span id="ContainerNetwork"></span>
In EKS, pods directly run in the VPC instance specified by users. Each pod is bound to an ENI in the specified VPC throughout its lifecycle. You can view the ENIs bound to the pods in the [ENI List](https://console.cloud.tencent.com/vpc/eni).

>
>- We recommend that you configure multiple availability zones for the container network so that your workloads can be automatically distributed to multiple availability zones, which improves usability.
>- Ensure that a subnet with sufficient available IP addresses is assigned to the container network. This prevents the lack of IP addresses from causing pod creation failure when the creation workload is high.
