
## Scenario
This document describes how to create a TCR Enterprise Edition instance in Tencent Container Registry (TCR).

## Prerequisites

Before creating a TCR Enterprise Edition instance, complete the following tasks:
- [Sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985), and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).
- Submit an application, and obtain the qualification for the TCR beta test.
- Activate the TCR-dependent cloud product, [Cloud Object Storage (COS)](https://console.cloud.tencent.com/cos5).
- If you need to access the instance through a Virtual Private Network (VPC), activate the [VPC](https://console.cloud.tencent.com/vpc) service.
- Activate the TCR service on the console and grant certain operation permissions to your COS and VPC resources.

## Procedure
1. Log in to the Tencent Cloud console and choose **Products** -> **Compute** -> **Tencent Container Registry** to go to the TCR console.
2. Select **Instance List** in the left sidebar to go to the "Instance List" page, and click **Create**.
3. In the "Create Instance" window, configure the following information to create an instance. See the figure below.

 - **Instance Name**: enter a custom instance name. This document uses `demo-tcr` as an example. The name is globally unique and cannot be identical with an existing instance name of your own or other users. This name is used to access the domain name of this TCR instance. **The name cannot be modified after creation.** We recommend that you use an abbreviation that combines the company name and instance region or project as the instance name.
  - **Instance Region**: select a region where you want to deploy the instance. **The region cannot be changed after the instance is created.**. If possible, select a region where your main business is located. More regions to choose from will be gradually be made available. If you have special requirements, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
 - **Instance Specification**: select the instance specifications you wish to purchase. Different instance specifications have different instance performance and quotas and apply to different application scenarios and business scales. You can purchase only a **Standard** edition instance in the beta phase.
 - **Instance Domain Name**: the instance domain name that is automatically generated. Its prefix is the same as that of the instance name. **The instance domain name cannot be modified after the instance is created.** This domain name is used when you run the `docker login` command to log in to the instance.
4. Click **OK** to create an instance. This process takes about 1 minute.
You can check the instance creation progress on the "Instance List" page. If the instance status changes to "Running" as shown in the figure below, the instance was successfully created and is running properly.

> If it takes too long to create an instance or the displayed status is abnormal, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>
