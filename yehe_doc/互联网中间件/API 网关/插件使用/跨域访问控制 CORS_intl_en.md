## Overview

Cross-Origin Resource Sharing (CORS) is a W3C standard. It allows web application servers to perform cross-origin access control, so that cross-origin data transfer can be conducted securely. Currently, API Gateway supports configuring CORS rules to allow or deny corresponding cross-origin requests as needed.

If the default CORS configuration of API Gateway cannot meet your needs, you can configure custom complex CORS rules through the CORS plugin and bind them to APIs for taking effect.

## Directions

### Step 1. Create a plugin

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway).
2. On the left sidebar, click **Plugin** to enter the plugin list page.
3. Click **Create** in the top-left corner of the page and select **Cross-Origin Resource Sharing (CORS)** as the plugin type to create a CORS plugin.

| Parameter | Required | Description |
| -------------- | -------- | ------------------------------------------------------------ |
| Origin | Yes | Specify the origins of allowed cross-origin requests; <br>You can specify multiple origins and separate them by commas; <br>You can configure `*`, which means that all domain names are allowed; <br>Be careful not to omit the protocol name `http` or `https`. If the port is not the default port 80, you also need to include the port. |
| Method | Yes | GET, PUT, POST, DELETE, and HEAD methods are supported. You can enumerate one or more allowed CORS request methods. |
| Allow-Headers | No | Specify the custom HTTP request headers that can be used for subsequent `OPTIONS` requests; <br>You can specify multiple headers and separate them by commas; <br>You can configure `*`, which means that all header are allowed; <br>If you leave this parameter empty, all headers will be denied. |
| Expose-Headers | No | Specify the headers that can be exposed to the `XMLHttpRequest` object; <br>You can specify multiple headers and separate them by commas; <br>You can configure `*`, which means that all header are allowed; <br>If you leave this parameter empty, all headers will be denied. |
| Allow Cookies | No | Specify whether to allow cookies. |
| Max-Age | Yes | Set the validity period of the result obtained by `OPTIONS`. The value must be a positive integer, such as 600. |

![](https://main.qcloudimg.com/raw/b541e49d5a73e73109ff511869c44d48.png)

### Step 2. Bind an API and make the plugin effective

1. Select the just created plugin in the list and click **Bind API** in the **Operation** column.
2. In the **Bind API** pop-up window, select the service, environment, and the API that needs to be bound to the plugin.
   ![](https://main.qcloudimg.com/raw/5ecc46c0cacb83b911097f4903701d89.png)
3. Click **OK** to bind the plugin to the API. At this time, the configuration of the plugin has taken effect for the API.

## Notes

Currently, there are two places in API Gateway where you can set CORS rules:

- Create API > frontend configuration > CORS is supported: enable the **CORS is supported** configuration item when creating an API, and API Gateway will add `Access-Control-Allow-Origin : *` in the response header by default.
- The CORS plugin as described in this document.

The CORS plugin has a higher priority than the **CORS is supported** configuration item. When the former is bound to an API, the latter of the API will not take effect.
