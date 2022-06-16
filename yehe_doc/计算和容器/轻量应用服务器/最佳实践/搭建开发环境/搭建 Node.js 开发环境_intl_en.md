## Overview
Node.js is an event-driven I/O server-side JavaScript environment based on the Chrome V8 engine. Fast and powerful, it can be used to build all kinds of web applications and work as the backend service environment for mini programs.


<dx-alert infotype="explain" title="">
In the following example, we use the Node.js application image, which is based on CentOS 8.2 64-bit. Note that application images are subject to updates from time to time, and the actual image information on the purchase page shall prevail.
</dx-alert>



## Directions
1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse) and configure the following parameters:
 - **Region** and **Availability zone**: Select the region and AZ near your target users to reduce the network latency and improve their access speed.
 - **Image**: Select the **Node.js** application image.
 - **Instance bundle**: Select an instance bundle according to the required instance configuration (including CPU, memory, system disk, bandwidth, and monthly traffic).
 - **Instance name**: Enter a custom instance name. If it is left empty, the selected image name will be used as the name by default. When multiple instances are created in a batch, their names will be consecutive with auto-incrementing suffixes. For example, if you enter "LH" as the name and select 3 as the quantity, 3 instances "LH1", "LH2", and "LH3" will be created.
 - **Purchase period**: One month by default.
 - **Quantity**: One instance by default.
2. Click **Buy now** to submit your order and make the payment as prompted.

## Relevant Operations

### Viewing application information
1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse).
2. In the instance list, select the target instance created with the Node.js application image to enter its details page.
3. Select the **Pre-installed application** tab to enter the application details page.
![](https://qcloudimg.tencent-cloud.cn/raw/ab8001d0ccbf664d802f19a35122b5f2.png)
You can view the configuration items of pre-installed applications.
 - Node.js and NGINX software installation paths.
 - The npm and npx paths of Node.js, and the primary configuration file path of NGINX.

### Using FTP tool to upload code and debug
1. Log in to the instance created with the Node.js application image. Set up the FTP service as instructed in [Building FTP Service using Linux Instance](https://intl.cloud.tencent.com/document/product/1103/47402).
2. Use an FTP tool (such as WinSCP) on your local computer to upload your website code to the instance and test and debug the service.


### Enabling HTTPS access
You can install an SSL certificate and enable HTTPS access for your website. See [Installing Certificate on NGINX Server](https://intl.cloud.tencent.com/document/product/1103/47406).

