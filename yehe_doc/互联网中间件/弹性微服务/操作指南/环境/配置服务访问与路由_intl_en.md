## Overview

This document describes how to configure service access and routing in the TEM console. You can configure forwarding rules, so that different URLs can access different services in the cluster. The use cases of this feature include:

- Scenarios with services that require public network access entries, such as microservice gateway services.
- Scenarios where domain name association is needed.
- Scenarios where the same domain name has different routing/forwarding paths.
- Scenarios where different domain names need to point to the same service.

>?Currently, only the HTTP protocol is supported, and HTTPS will be supported on future versions.

## Directions

1. Log in to the [TEM console](https://console.cloud.tencent.com/tem).
2. On the **Environment** page, select a deployment region and click **Edit** under the target environment block.
3. In the **Access and Routing** module, enter the forwarding configuration information.
	 ![](https://main.qcloudimg.com/raw/669fbae90edc6cc1873f89bc535011cb.png)
   - Listening Port: HTTP:80.
   - Domain Name: existing domain names can be bound. If there are no domain names, you will be assigned an IPv4 IP by default.
   - Path: the default value is "/". You can configure according to the actual situation.
   - Backend Service: select according to the actual situation.
   - Service Port: select according to the actual situation.
4. Click **OK** to complete the service access and routing configuration.
