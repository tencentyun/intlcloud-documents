## Overview

This document describes how to create a server fleet, which is a group of managed resources in the form of CVM instances, to deploy game servers. The fleet size is subject to the number of instances you assign, and can be manually or automatically scaled to meet players' needs.



## Directions

1. Log in to the [GSE console](https://console.cloud.tencent.com/gse/asset) and click **Fleet** on the left sidebar to enter the server fleet page.
2. Select the service region in the top-left corner and click **Create**.
3. On the **Create Fleet** page, enter information such as [basic info](#.E5.9F.BA.E6.9C.AC.E4.BF.A1.E6.81.AF), [process management](#.E8.BF.9B.E7.A8.8B.E7.AE.A1.E7.90.86), [deployment configuration](#.E9.83.A8.E7.BD.B2.E9.85.8D.E7.BD.AE), and [internet](#.E7.BD.91.E7.BB.9C).

### Basic info
To create a server fleet, you can use **asset package** or **image** according to the resource type:

- **Asset package**
![](https://main.qcloudimg.com/raw/c47bfd7a581fa7152edfaec6c4ebd3c7.png)
  - Name: enter the server fleet name. We recommend you use a meaningful fleet name, so that it can be easily identified in the list.
  - Resource Type: select asset package or image from the drop-down list.
  - Asset Package Name: select a valid asset package from the drop-down list or [create one](https://intl.cloud.tencent.com/document/product/1055/36674) first.
  - Description: enter the server fleet description, which is optional and used to help identify the fleet.
  - **Asset Package ID**, **Asset Package Size**, and **OS** will be automatically entered based on the selected asset package name.

- **Image**
![](https://main.qcloudimg.com/raw/8158e3185b3b42bbd01487d1926adf6b.png)
  - Name: enter the server fleet name. We recommend you use a meaningful fleet name, so that it can be easily identified in the list.
  - Resource Type: select asset package or image from the drop-down list.
  - Image Name: select a valid image from the drop-down list or [create one](https://intl.cloud.tencent.com/document/product/1055/39061) first.
  - Description: enter the server fleet description, which is optional and used to help identify the fleet.
  - **Image ID**, **Image Size** and **Image OS** will be automatically entered based on the selected image name.
 >!Using **Image** to create a server fleet requires authorization, which means you need to authorize the image resources to GSE. To do so, click **Share** > **Go to CAM** > **Authorize**.
>

### Process management
  Configure how server processes run on each CVM instance.
  - Launch Path: enter the path of a server executable file in the asset package. Download the asset package to the `/local/game/` path on the Linux platform and to the `C:\game\` path on the Windows platform. The decompressed full path of the server process is as follows
   - Liunx: `/local/game/YourGameServerBuild`
   - Windows: `C:\game\YourGameServerBuild.exe`
  - Launch Parameter: enter the information to be delivered to the server executable file during launch. It is in the format of a set of command line parameters and is optional.
  - Concurrent processes allowed: specify this configuration allows how many processes concurrently run on each CVM instance in the server fleet.
  - Max Concurrent Game Server Session Activation: set the number of game server sessions that can be concurrently activated on a CVM instance. You can select **Unlimited** or **Limited** (the maximum value is 20,000). When multiple new game server sessions are launched on one CVM instance, this limit can reduce their performance impact on each other.
  - Game Server Session Activation Timeout: enter the maximum time period for a new game server session to be activated. You can set the timeout period to be no more than 600s.

![](https://main.qcloudimg.com/raw/c3bd554f125f7a73d5dea4ebb54d589a.jpg)

>?
>- Concurrent processes allowed: the total number of game processes that need to be launched for a launch path binary
>- Max Concurrent Game Server Session Activation: the number of instantaneous concurrencies of the game server sessions in “activating” state.

 

### Deployment configuration
  - Server Instance Type: server model of the server fleet to be created.
  - Enable VPC: after enabling access to Tencent Cloud VPC, you can access the servers and other resources in your VPC.
      
  ![](https://main.qcloudimg.com/raw/5284d28b11f74f42a3a3c39e2fc2f45a.png)


 <span id="test12"></span>
### Internet
  - Network Security Group: you can define the access permission to inbound traffic of your server processes. Before allowing access, you must set at least one port for the fleet.
    - Port range: specify the range of numbers of the ports that can be opened for inbound connections to the game servers. The range must be 1025–60000.
    - Protocol: select TCP or UDP as the communication protocol of the fleet.
    - IP range: specify the valid IP range for CVM instances in the fleet. You can use a CIDR block to represent a range (such as `0.0.0.0/0`, which indicates that access requests from any user can be allowed).
  - Number of instances: refers to the number of CVM instances. After the server fleet is created successfully, this number can be modified on the scaling policy page in the server fleet details.
  - Protection Policy: includes time-period protection, full protection, and no protection.
    When you call the process termination API, the process will be actively terminated. If you do not call this API, one of the following protection policies will be executed accordingly:
    - Time-period protection: in case of a scaling-in or an unhealthy process, the system will terminate the process after a period of time between 5 to 1,440 minutes (60 minutes by default).
    - Full protection: the process can be terminated only when there are no processes running on the CVM instance.
    - No protection: in case of a scaling-in or an unhealthy process, the system will terminate the process after up to 5 minutes.
         
   ![](https://main.qcloudimg.com/raw/3478d408969d34e9daf49d199004c8df.png)

4. After configuring the information above, click **Create** to create a server fleet.
5. After the server fleet is successfully created, you can view, delete, or perform other operations on the server fleet page. You can also click the server fleet ID to view information such as basic information, events, instance list, scaling, game sessions, process management, ports and protocols, asset packages, and VPC.



