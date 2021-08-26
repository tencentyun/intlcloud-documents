
## Overview

This document describes how to use CLB as the access entry of a serverless service and work with SCF to quickly deploy a web service. In this way, you can enjoy the strengths of Serverless services, such as low cost and OPS-free usage, and smoothly migrate your application to the cloud.

## Directions

### Creating VPC[](id:createVPC) 
Log in to the [VPC console](https://console.cloud.tencent.com/vpc) to create a VPC and subnet as instructed in [Building Up an IPv4 VPC](https://intl.cloud.tencent.com/document/product/215/31891).

<dx-alert infotype="notice" title="">
The VPC should be deployed in the same region as the CLB instance and SCF webpage. This document uses **Shanghai** as an example.
</dx-alert>




### Creating CLB instance[](id:createCLB)

1. Log in to the [CLB console](https://console.cloud.tencent.com/clb/instance?rid=4&pid=0&type=OPEN) to create a CLB instance as instructed in [Getting Started with CLB](https://intl.cloud.tencent.com/document/product/214/8975).
This document uses **Shanghai** as an example. Select the VPC created in the [previous step](#createVPC).
2. After successful creation, find the target CLB instance on the **Instance Management** page and configure a listener for it as instructed in [Configuring an HTTP Listener](https://intl.cloud.tencent.com/document/product/214/32515).
This document uses the listener `clb-scf-web` and listening protocol port number `81` as an example. 



### Creating SCF function
1. Log in to the SCF console and select **[Function Service](https://console.cloud.tencent.com/scf/list)** on the left sidebar.
2. At the top of the **Function Service** page, select the **Shanghai** region and click **Create** to enter the function creating page.
    Set the following parameter information and click **Next** as shown below:
 - **Creation Method**: select **Template**.
 - **Fuzzy Search**: enter "Web static page hosting" and "Python3.6" and search.
 Click **Learn More** in the template to view relevant information in the **Template Details** pop-up window, which can be downloaded.
3. In **Basic Configuration**, enter the **function name** and select the **function region**.
   - Function Name: enter `clb-scf-web` for example.
   - Region: select the region of the CLB instance, such as **Shanghai**.
4. In **Trigger Configuration**, select **Custom Creation** and use the trigger to bind CLB to SCF.
   - Triggered Version: select **Default Traffic**.
   - Trigger Method: select **CLB Trigger**.
   - Instance ID: select the CLB instance created in the [previous step](#createCLB), such as `clb_serverless_web`.
   - Listener: select the configured listener. In this example, the listener listens on port `81`.
   - Domain Name/Host: select **Create Rule**.
   - Add Domain Name: enter the VIP of the CLB instance in the added domain name.
   <dx-alert infotype="explain" title="">
The VIP is the IP address through which CLB provides service to clients.
   </dx-alert>
   - URL Path: enter the URL path of the website starting with `/`, such as `/demo`.
5. Click **Complete** to redirect to the **Deployment Log** page and view the function and trigger creation progress.

### Testing CLB entry
1. Log in to the SCF console and select **[Function Service](https://console.cloud.tencent.com/scf/list)** on the left sidebar.
2. At the top of the **Function Service** page, click the created function `clb-scf-web`.
3. On the function details page, select **Trigger Management**.
4. On the **Trigger Management** page, get the trigger access path and view the webpage.



