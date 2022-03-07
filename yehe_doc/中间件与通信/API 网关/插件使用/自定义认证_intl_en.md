## Overview

If the verification and authentication method provided by the API Gateway cannot meet your requirements, you can use custom verification plugin to verify and authenticate a request.

Custom verification plugin applies during the request process. The API Gateway will forward the request to the verification SCF after receiving it from the Client. Then, the request will be forwarded to the service backend only if it passes the verification by the SCF, otherwise the request will be denied.
<img  src="https://qcloudimg.tencent-cloud.cn/raw/eaad1bafed794ebf70d0fbbd3d0e01bf.png" width="600px">


## Prerequisites

- You have activated [SCF](https://console.cloud.tencent.com/scf/list).

## Directions

### Step 1: creating a verification SCF

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/list).
2. Click **Function Service** on the left sidebar to open the function list page.
3. Click **Create** at the upper-left corner of the page to create a verification SCF.

> ?
> - You need to write the verification SCF. For more information, see [Template of Custom Verification SCF](https://github.com/tencentyun/serverless-demo/blob/master/Python3.6-APIGWCustomAuth/src/index.py).
> - Custom verification plugin requires to return the value of api-auth in the Body of the response body that is returned to the gateway. When the value is `true`, it means the verification is passed; when the value is `false` or `null`, it means the verification is failed.


### Step 2: creating a custom verification plugin

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway)
2. On the left sidebar, click **Plugin - Custom Plugin** to open the custom plugin list page.
3. Create **Create** at the upper-left corner of the page to create a custom verification plugin. You need to enter the following parameters:

| Parameter | Required | Description |
| ------------ | -------- | ------------------------------------------------------------ |
| Select an SCF | Required | You need to select the namespace, name and version of the verification SCF. |
| Backend timeout    | Required | This sets the backend timeout that the API Gateway forwards the request to the verification SCF. The maximum time limit is 30 minutes. When no response is returned before the timeout after the API Gateway calls the SCF, the API Gateway will end the call and returns an error message. |
| Whether to send Body | Required | When the value is "Yes", the Header, Body and Query requested by the Client will be sent to the SCF; when the value is "No", the Body requested will not be sent. |
| Verification parameter | Optional | It sets the request parameters for verification. When caching time is not `0`, this parameter must be set. When caching is enabled, the verification result will be queried with this parameter as the search condition. |
| Caching time | Required | It sets the caching time for the verification result. `0` indicates that caching is not enabled. Caching time can be up to 3,600 seconds. |

![](https://qcloudimg.tencent-cloud.cn/raw/1bdab422c46bae1be216a2dca590a75d.png)

> ? After caching is enabled, the API Gateway will record the relationship between the value of authentication parameter and the value of api-auth. If there is subsequent request during caching time, and the value of authentication parameter is the same as the value of the first request, the request will not be forwarded to the SCF and will be processed according to the value of api-auth for the first request.

4. Click **Save** to complete the process.


### Step 3: binding the API

1. Select the just created plugin in the list and click **Bind API** in the **Operation** column.
2. In the **Bind API** pop-up window, select the service, environment, and the API to which the plugin needs to be bound.
   ![](https://qcloudimg.tencent-cloud.cn/raw/e9e674392e0070e320d38c1c00fc1ba2.png)
3. Click **OK** to bind the plugin to the API. At this time, the configuration of the plugin has taken effect for the API.


## pluginData

```json
{
    "cache_time":10,   // Verification result caching duration in seconds. Value range: 0–3600
    "endpoint_timeout":15, // Backend timeout period in seconds. Value range: 0–60
    "func_name":"test_name", // Custom SCF name
    "func_namespace":"test_namespace", // Custom SCF namespace
    "func_qualifier":"$LATEST", // Custom SCF version
    "is_send_body":true, // Whether to send the request Body to the SCF
    "header_auth_parameters":[ // Verification parameter in Header location. The plugin caches the verification result based on the parameter value
        "Header1"
    ],
    "query_auth_parameters":[ // Verification parameter in Query location. The plugin caches the verification result based on the parameter value
        "Query1"
    ],
    "user_id":1253970226, // appid
    "version":"2021-12-26 17:17:49" // Plugin version in the format of `yyyy-MM-dd HH:mm:ss`. When you edit the plugin, the new value passed in will invalidate the result cached in the plugin
}
```

## Notes

- When you enable caching and configure the verification parameter, the API Gateway will conduct parameter verification. If the request does not transfer the verification parameter, the API Gateway will report an error message "xxx parameter is missing". The values are case insensitive for parameter verification and cache hitting conducted by the API Gateway.
- Binding a custom plugin to the API means creating a trigger for the SCF to trigger the API. Deleting the trigger on the SCF side means unbinding the plugin from the API.
- For now, the custom verification plugin only supports event-triggered function and does not support HTTP-triggered function.
- The custom verification plugin can coexist with the verification method provided by the API Gateway. The latter takes priority. We recommend that you set the API where the custom verification plugin bound to "free from verification".
