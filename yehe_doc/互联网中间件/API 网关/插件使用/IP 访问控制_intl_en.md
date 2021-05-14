## Overview

IP access control is a security protection capability provided by API Gateway. It is mainly used to restrict the source IPs of API callers. You can allow/reject API requests from a certain source by configuring the IP allowlist/blocklist of an API.

>?The original IP access control policy data has been migrated to the IP access control plugin, which can be managed on the [Plugin](https://console.cloud.tencent.com/apigateway/plugin) page.

## Directions

### Step 1. Create a plugin

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway).
2. On the left sidebar, click **Plugin** to enter the plugin list page.
3. Click **Create** in the top-left corner to create an IP access control plugin.


### Step 2. Bind an API and make the plugin effective

1. Select the just created plugin in the list and click **Bind API** in the **Operation** column.
2. In the **Bind API** pop-up window, select the service, environment, and the API that needs to be bound to the plugin.

3. Click **OK** to bind the plugin to the API. At this time, the configuration of the plugin has taken effect for the API.

## Notes

- The IP access control plugin supports blocklist and allowlist modes. When the allowlist is used, requests from IPs not in the allowlist will be rejected by API Gateway; when the blocklist is used, requests from IPs in the blocklist will be rejected by API Gateway.
- Multiple IPs or CIDR blocks can be entered in the IP access control plugin, which should be separated with semicolons.
