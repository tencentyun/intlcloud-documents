## Overview

This document describes how to configure application access and routing in the TEM console. You can configure forwarding rules to implement HTTP/HTTPS forwarding rules over the public network. The use cases of this feature include:

- Scenarios with applications that require public network access entries, such as microservice gateway applications.
- Scenarios where domain name association is needed.
- Scenarios where the same domain name has different routing/forwarding paths.
- Scenarios where different domain names need to point to the same application.

## Directions

1. Log in to the [TEM console](https://console.cloud.tencent.com/tem).
2. On the **Environment** page, select a deployment region and click the target environment to enter the environment details page.
3. Select the **Access Configuration** tab on the top, click **Create**, and enter the forwarding rule name.
   ![](https://main.qcloudimg.com/raw/d123003055bc8ed29d40afb9dd020194.png)
   - Network Type: public network. For more information on intra-environment access, please see [Creating and Deploying Application](https://intl.cloud.tencent.com/document/product/1094/40362).
   - Load Balancer: it will be automatically created.
   - Protocol and Port: HTTP:80 and HTTPS:443 are supported, and HTTPS domain names can be bound to certificates.
   - Forwarding Configuration:
     - Domain Name: existing domain names can be bound. If there are no domain names, you will be assigned an IPv4 IP by default.
     - Path: the default value is "/". You can configure according to the actual situation.
     - Backend Service: select according to the actual situation.
     - Service Port: select according to the actual situation.
   - Server Certificate: if the HTTP protocol is selected, you need to select a server certificate. If the existing certificates are not suitable, you can [create one](https://console.cloud.tencent.com/clb/cert).
4. Click **OK** to complete the application access and routing configuration.

## Relevant Operations
- If you want to modify an access configuration rule, click **Edit** in the **Operation** column of the target rule and modify the access configuration in the pop-up window.
- If you want to delete an access configuration rule, click **Delete** in the **Operation** column of the target rule and delete the access configuration in the pop-up window.
- If you want to view the details of a forwarding rule, click **View Forwarding Rule** in the **Operation** column of the target rule and view the details in the pop-up window.
