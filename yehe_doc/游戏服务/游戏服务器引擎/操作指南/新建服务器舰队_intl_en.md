## Overview
This document describes how to create a server fleet.


## Prerequisites
You have completed the [GSE Application Form](https://intl.cloud.tencent.com/apply/p/k0b6pvbhs6) and your application has been approved.


## Directions
1. Log in to the [GSE Console](https://console.cloud.tencent.com/gse/asset) and click **Server Fleet** on the left sidebar.
2. Select the service region in the top-left corner and click **Create**.
3. Access the server fleet creation page, enter information such as the basic information, process management, deployment configuration, and network, and click **Create**.
 - **Basic Info**
    - Name: server fleet name.
    - Package Name: server fleet package name.
    - Description: server fleet description.
    ![](https://main.qcloudimg.com/raw/f688eb76f1ebbe921334be33b4521b18.jpg)
 - **Process Management**
    - Startup Path: you can configure one or multiple startup paths and set the startup parameters and the maximum number of allowed concurrent processes.
    - Max Concurrent Game Start Server Sessions: you can select `Unlimited` or `Limited`.
    - Timeout Period for Activating Game Server Sessions: you can set the timeout period to be less than or equal to 600 seconds.
    ![](https://main.qcloudimg.com/raw/c3bd554f125f7a73d5dea4ebb54d589a.jpg)
 - **Deployment Configuration**
    - Server Type: server model of the server fleet to be created.
    - Enable VPC: after enabling access to Tencent Cloud VPC, you can access the servers and other resources in your VPC.
    ![](https://main.qcloudimg.com/raw/ab0e82ae9cea60618ef634ed58c5230f.jpg)
 - **Network**
    - Network Port Settings: the settings include IP protocol and IP range.
    - Instance Count: after the server fleet is created successfully, you can modify the count on the scaling policy page in the server fleet details.
    - Protection Policy: if `Full protection` is selected, CVM instances can be terminated only when there are no game or player sessions running on them.
    ![](https://main.qcloudimg.com/raw/3478d408969d34e9daf49d199004c8df.png)
4. After the server fleet is successfully created, you can view, delete, or perform other operations on it on the server fleet page. In addition, you can click the server fleet ID to view information such as the basic information, events, the instance list, scaling, game sessions, process management, ports and protocols, and asset packages.

