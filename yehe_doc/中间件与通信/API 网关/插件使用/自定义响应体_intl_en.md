## Overview

The response body sent to the Client by API Gateway contains many fields. If you want to modify the content of the response body, you can do so via custom response body plugin.

## How It Works

The custom response body plugin is implemented based on SCF and applies during the response process as follows:
The service backend will send the response body to the API Gateway after processing the request packet. The API Gateway will forward the response content to the specified SCF instead of sending it to the Client after receiving it. SCF will send the modified content of response body to the API Gateway after modifying it. Then, the API Gateway will forward the modified response body to service backend.

## Prerequisites

- You have activated [SCF](https://console.cloud.tencent.com/scf/list).

## Directions

### Step 1: creating an SCF to modify the response body

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/list).
2. Click **Function Service** on the left sidebar to open the function list page.
3. Click **Create** at the upper-left corner of the page to create an SCF that is used to modify the response body.

> ?You need to write the SCF that is used to modify the response body. For more information, see [Template of Custom Response Body SCF](https://github.com/tencentyun/serverless-demo/blob/master/Python3.6-APIGWCustomRequest/src/index.py).

### Step 2: creating a custom response body plugin[](id:step2)

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway)
2. On the left sidebar, click **Plugin - Custom Plugin** to open the custom plugin list page.
3. Create **Create** at the upper-left corner of the page to create a custom response body plugin. You need to enter the following parameters:

| Parameter | Type | Description |
| ----------- | -------- | ------------------------------------------------------------ |
| Select an SCF | Required | You need to select the namespace, name and version of the SCF that is used to modify the response body. |
| Backend timeout    | Required | This sets the backend timeout that the API Gateway forwards the response to the SCF that is used to modify the response body. The maximum time limit is 30 minutes. When no response is returned before the timeout after the API Gateway calls the SCF, the API Gateway will end the call and return an error message. |
| Custom content | Required | It sets the response content sent to the SCF by the API Gateway. You can select Header, Body and response status code. The response content not selected will not be modified and will be returned to the Client as is. |
| Base64 encoding | Required | It specifies whether to Base64-encode the response content to be forwarded by the service backend to the SCF. Generally, it is applicable to binary content. |

![](https://qcloudimg.tencent-cloud.cn/raw/f77fdd378bb923aa4be290bacc02e204.png)

4. Click **Save** to complete the process.

### Step 3: binding the API

1. Select the plugin created in [step 2](#step2) from the plugin list. Click **Bind API** in the **Operation** column.
2. In the **Bind API** pop-up window, select the service, environment, and the API to which the plugin needs to be bound.
   ![](https://main.qcloudimg.com/raw/d7fd3c3539d6f623f45ebfdf0674d97e.png)
3. Click **OK** to bind the plugin to the API. At this time, the configuration of the plugin has taken effect for the API.

## pluginData

```json
{
    "endpoint_timeout":15, // Backend timeout period in seconds. Value range: 0–60
    "func_name":"test_name", // Custom SCF name
    "func_namespace":"test_namespace", // Custom SCF namespace
    "func_qualifier":"$LATEST", // Custom SCF version
    "is_base64_encoded":true, // Whether to Base64-encode the response content to be forwarded by the service backend to the SCF
    "is_custom_status":true, // Whether to send the response status code content to the SCF
    "is_custom_headers":true, // Whether to send the response Header content to the SCF
    "is_custom_body":true, // Whether to send the response Body content to the SCF
    "user_id":1253970226 // appid
}
```

## Notes

- Binding a custom plugin to the API means creating a trigger for the SCF to trigger the API. Deleting the trigger on the SCF side means unbinding the plugin from the API.
- For now, the custom response body plugin only supports event-triggered function and does not support HTTP-triggered function.
- The priority of the custom response body plugin is lower than that of all plugins applied during the request process.
- If the custom response body plugin is bound to an API with a Mock or TSF backend, it will not take effect.
- The custom response body plugin does not support the HTTP2 protocol.
- The custom response body plugin does not support the response body compressed in the gzip format returned by the backend.


