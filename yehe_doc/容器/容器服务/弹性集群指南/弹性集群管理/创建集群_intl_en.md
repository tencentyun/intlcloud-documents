## Introduction
This document describes how to create an elastic cluster in the TKE console to help you get started with Elastic Kubernetes Service (EKS).



## Prerequisites
You have activated required permissions for EKS in the [CAM console](https://console.cloud.tencent.com/cam/overview).

## Directions
1. Log in to the TKE console and click **[Elastic Cluster](https://console.cloud.tencent.com/tke2/ecluster)** in the left sidebar.
2. On the page that appears, select the region where you want to create the elastic cluster and then click **Create**.
3. On the **Create Elastic Cluster** page that appears, specify the cluster information as instructed below.
 - **Cluster Name**: the name of the cluster to be created. Up to 60 characters allowed.
 - **Kubernetes Version**: the Kubernetes version of the cluster to be created. It supports V1.12 and later. For a comparison of the features of different versions, see [Supported Versions of the Kubernetes Documentation](https://kubernetes.io/docs/home/supported-doc-versions/).
 - **Region**: the region where the cluster to be created is located. We recommend that you select the region closest to you to help minimize access latency and improve the download speed.
 - **Cluster Network**: an existing VPC for elastic clusters. You can select a subnet of the VPC to serve as a container network for the elastic cluster. For more information, see [VPC Documentation](https://intl.cloud.tencent.com/document/product/215/535).
 - **Container Network**: assigns an IP address for containers in the cluster. The IP should be in the range the of container network. Pods in an elastic cluster directly use the IP addresses of a VPC subnet. We recommend that you select a subnet with sufficient available IP addresses and is not shared with other products. For more information, see [Container Network Description](#ContainerNetwork).
 - **Cluster Description**: specifies the information about the cluster to be created. This description will be displayed on the **Cluster Information** page.
4. Click **Complete** to start creating the cluster. You can view the creation progress on the **Elastic Cluster** page.

<span id="ContainerNetwork"></span>

## Container Network Description

In EKS, pods directly run on the specified VPC. Each pod is bound to an ENI in the specified VPC throughout its lifecycle. You can view the ENIs bound to the pods in the [ENI List](https://console.cloud.tencent.com/vpc/eni).

>
>- We recommend that you configure multiple availability zones for the container network so that your workloads can be automatically distributed to multiple availability zones, which improves usability.
>- Ensure that the subnet assigned to the container network has sufficient available IP addresses, so as to prevents pod creation failure caused by insufficient IPs when creating a large-scale workload.
