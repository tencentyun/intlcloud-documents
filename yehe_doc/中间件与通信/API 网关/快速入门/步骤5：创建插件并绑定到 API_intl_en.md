## Overview

This document describes how to create a plugin and bind it to a created API in the API Gateway console.

## Prerequisites

You have [created an API](https://intl.cloud.tencent.com/document/product/628/44318).

## Directions

1. In the [API Gateway console](https://console.cloud.tencent.com/apigateway), select **Plugin** > **System Plugin** on the left sidebar.
2. Click **Create** and enter the plugin information.
   ![](https://qcloudimg.tencent-cloud.cn/raw/6c92c031f1a203e3349f194851261413.png)
   - Plugin Name: it can contain up to 50 letters, digits, and underscores. **exampleplugin** is entered here as an example.
   - Type: select **IP access control**.
   - Plugin Description: description of the plugin. **Test** is entered here as an example.
   - Attribute: blocklist or allowlist. **Allowlist** is selected here as an example.
   - IP: enter the IP address or CIDR block that can access the API.
   - Tag: it is optional and makes it easier to categorize and manage resources.
3. Click **Save**.
4. On the plugin list page, click **Bind API** in the **Operation** column of the just created plugin.
	 ![](https://qcloudimg.tencent-cloud.cn/raw/47e97a4e1c6e4ede0739a3140733f508.png)
   - Service: select the just created **exampleservice** service.
   - Select Environment: select **Release**.
   - Select APIs to bind: select the just created **exampleapi** API.
5. Click **OK**.

