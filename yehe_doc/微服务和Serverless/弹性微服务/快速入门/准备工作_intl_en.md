## Overview

Following the getting started tutorial, you can quickly start your TEM experience and try deploying a demo application provided by us or an application developed by yourself.

This document describes the preparations you need to complete before using TEM to host your application, including registering an account, applying for the beta test eligibility, and creating an environment and VPC.


## Directions

### Step 1. Register an account

Before starting using Tencent Cloud services, you need to [register a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) first.



### Step 2. Create an environment and VPC

1. Log in to the [TEM console](https://console.cloud.tencent.com/tem) and enter the **Environment** page.
2. At the top of the **Environment** page, select a **deployment region** and click **Create**.
3. In the pop-up window, configure the environment information.
![](https://main.qcloudimg.com/raw/bb401e16c8e7069e8a4f085afe38a6ee.png)
	- Name: enter up to 40 characters.
	- VPC: select an existing VPC. If your existing VPCs are not suitable or you haven't created a VPC yet, you can click [Create VPC](https://console.cloud.tencent.com/vpc/vpc?rid=4) to create one (the selected region must be the same as that of the environment), return to and refresh this page, and select it.
	- Subnet: select an existing subnet. We recommend you choose multi-AZ deployment to improve the disaster recovery capabilities. If your existing subnets are not suitable or you haven't created a subnet yet, you can click [Create Subnet](https://console.cloud.tencent.com/vpc/subnet?rid=4&unVpcId=) to create one, return to and refresh this page, and select it.                 
4. Click **OK** and the environment will enter the **Initializing** status. Wait 4–5 minutes, and the environment will be created.



### Step 3. Deploy an application

For the specific process of deploying an application, please see the corresponding document based on your application type:

- [General application](https://intl.cloud.tencent.com/document/product/1094/41384)
- [Microservice application](https://intl.cloud.tencent.com/document/product/1094/41385)
