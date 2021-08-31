
## Overview
This document describes how to create a TCR Enterprise Edition instance in Tencent Container Registry (TCR).

## Prerequisites

Before creating a TCR Enterprise Edition instance, complete the following tasks:
- [Sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).
- Activate the TCR-dependent Tencent Cloud service, [Cloud Object Storage (COS)](https://console.cloud.tencent.com/cos5).
- To access the instance through a Virtual Private Network (VPC), activate the [VPC](https://console.cloud.tencent.com/vpc) service.
- Activate the TCR service in the console and grant required permissions to your COS and VPC resources.

## Directions
1. Log in to the [Tencent Cloud console] (https://console.cloud.tencent.com/) and choose **Tencent Cloud Services** > **TKE** > **TCR** to go to the TCR console.
2. Click **Instance List** in the left sidebar to go to the "Instance List" page. Then, click **Create**.
3. In the "Create Instance" window, configure the following information to create an instance, as shown in the figure below.
![](https://main.qcloudimg.com/raw/d3b838aea1b189b51e533e95ee4bf087.png)
 - **Instance Name**: enter a custom instance name. The name must be globally unique and cannot be identical with an existing instance name of your own or other users. This name is used to access the domain name of this TCR instance. **The name cannot be changed once the instance is created.** We recommend that you use an abbreviation that combines the company name and instance region or project as the instance name.
 - **Instance Region**: select a region where you want to deploy the instance. **The region cannot be changed once the instance is created.** Select a region based on the location of the container cluster resources.
 - **Instance Specification**: select the instance specifications that you want to purchase. Different instance specifications have different instance performance and quotas. For more information, see [Purchase Guide](https://intl.cloud.tencent.com/document/product/1051/35483).
 - **Instance Domain Name**: indicates the instance domain name that is automatically generated. Its prefix is the same as that of the instance name. **The instance domain name cannot be changed once the instance is created.** This domain name is used when you run the `docker login` command to log in to the instance.
 - **Backend Storage**: when an instance is created, a Tencent Cloud COS bucket will be automatically created and associated under the current account. Images and other data in the instance will be stored in the bucket, and storage and traffic costs will be incurred. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/436/16871). After instance creation, you can go to the COS console to view the bucket. Avoid mistakenly deleting the bucket. Otherwise, data such as images hosted in the instance can be lost.
 - **Instance Tag**: bind the newly created instance with a Tencent Cloud tag. You can also bind and edit it on the instance details page after instance creation.
4. Click **OK** to create an instance. This process takes about 1 minute to complete.
You can check the instance creation progress on the "Instance List" page. If the instance state becomes "Running" shown in the figure below, the instance was successfully created and is running properly.
![](https://main.qcloudimg.com/raw/44107d5f8be85e6069d3ad526d23c8c9.png)
>? If the creation duration exceeds the expectation or the instance state is abnormal, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact us.
