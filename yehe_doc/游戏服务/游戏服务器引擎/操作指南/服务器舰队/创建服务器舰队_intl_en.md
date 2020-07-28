## Overview

This document describes how to create a server fleet, which is a group of managed resources in the form of CVM instances, to deploy game servers. The fleet size is subject to the number of instances you assign, and can be manually or automatically scaled to meet players' needs.

## Prerequisites

You have completed the [GSE Application Form](https://intl.cloud.tencent.com/apply/p/k0b6pvbhs6) and your application has been approved.

## Directions

1. Log in to the [GSE Console](https://console.cloud.tencent.com/gse/asset) and click **Fleet** on the left sidebar to enter the server fleet page.
2. click **Create** in the top-left corner.
3. In the fleet creation page, enter information such as [Basic Info](#.E5.9F.BA.E6.9C.AC.E4.BF.A1.E6.81.AF), [Process Management](#.E8.BF.9B.E7.A8.8B.E7.AE.A1.E7.90.86), [Deployment Configuration](#.E9.83.A8.E7.BD.B2.E9.85.8D.E7.BD.AE), and [Network](#.E7.BD.91.E7.BB.9C).

#### Basic information
  - Name: enter the server fleet name. We recommend you use a meaningful fleet name, so that it can be easily identified in the list.
  - Asset Package Name: select a created valid asset package in the drop-down list. If there are no packages, please [create one](https://intl.cloud.tencent.com/document/product/1055/36674) first.
  - Description: enter the server fleet description, which is optional and used to help identify the fleet.
  - "Asset Package ID", "Asset Package Size", and "OS" will be automatically entered based on the selected asset package name.
      ![](https://main.qcloudimg.com/raw/c47bfd7a581fa7152edfaec6c4ebd3c7.png)

#### Process management
  Configure how server processes run on each CVM instance.
  - Launch Path: enter the path of a server executable in the asset package. Currently, a launch path starts with the game server location `/local/game/`.
  - Launch Parameter: enter the information to be delivered to the server executable during launch. It is in the format of a set of command line parameters and is optional.
  - Concurrent processes allowed: enter the number of allowed concurrent server processes using this configuration on each CVM instance in the server fleet.
  - Max Concurrent Game Server Sessions Activation: set the number of game server sessions that can be activated at the same time on a CVM instance. You can select "Unlimited" or "Limited" (the maximum value is 20,000). When multiple new game server sessions are launched on one CVM instance, this limit helps reduce their performance impact on each other.
  - Game Server Session Activation Timeout: enter the maximum time period for a new game server session to be activated. You can set timeout period to be less than or equal to 600s.
    ![](https://main.qcloudimg.com/raw/c3bd554f125f7a73d5dea4ebb54d589a.jpg)


#### Deployment configuration
  - Server Instance Type: server model of the server fleet to be created.
  - Enable VPC: after enabling access to Tencent Cloud VPC network, you can access the server and other resources under your VPC.
    ![](https://main.qcloudimg.com/raw/ab0e82ae9cea60618ef634ed58c5230f.jpg)


 <span id="test12"></span>
#### Network
  - Network Security Group: you can define the access permission to your server processes for inbound traffic. Before allowing access, you must set at least one port for the fleet.
    - Port range: specify the range of numbers of the ports that can be opened for inbound connections to the game servers. The range must be within 1025 to 60000.
    - Protocol: select the communication protocol to be used by the fleet; TCP or UDP.
    - IP range: specify the valid IP range for CVM instances in the fleet. You can use a CIDR block to represent a range (such as `0.0.0.0/0`, which indicates that access requests from any user can be allowed).
  - Instance Count: enter the number of CVM instances. After the server fleet is created successfully, you can modify the count on the scaling policy page in server fleet details.
  - Protection Policy: protection policies include time-period protection, full protection, and no protection.
    When you call the process termination API, the process will be actively terminated. If you do not call this API, one of the following protection policies will be executed accordingly:
    - Time-period protection: in case of trigging reduction or an unhealthy process, the system will terminate the process after a period of time, which ranges from 5 to 1,440 minutes and is 60 minutes by default.
    - Full protection: the process can be terminated only when there are no processes running on the CVM instance.
    - No protection: in case of trigging reduction or an unhealthy process, the system will terminate the process after up to 5 minutes.
      ![](https://main.qcloudimg.com/raw/3478d408969d34e9daf49d199004c8df.png)

4. After configuring the information above, click **Create** to create a server fleet.
5. After the server fleet is successfully created, you can view, delete, or perform other operations on it on the server fleet page. In addition, you can click the server fleet ID to view information such as the basic information, event, instance list, scaling, game session, process management, ports and protocol, asset package, and VPC.



