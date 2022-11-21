## Overview

If the verification and authentication method provided by API Gateway cannot meet your requirements, you can use the custom authentication plugin with custom code.

The custom verification plugin applies during the request process. API Gateway will forward the request to the verification function after receiving it from the client. You can deploy the verification function in SCF, on the public network, or in a VPC. Then, the request will be forwarded to the service backend only if it passes the verification; otherwise, the request will be denied.

![](https://qcloudimg.tencent-cloud.cn/raw/14de216be4c6fd3341bd1d260779f3d4.png)

## Prerequisites

For verification services deployed in SCF, you need to enable the [SCF](https://console.cloud.tencent.com/scf/list) service.

## Directions

### Step 1. Create a verification function
For verification functions deployed on the public network or in a VPC, you can skip this step.

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/list).
2. Click **Functions** on the left sidebar to enter the function list page.
3. Click **Create** at the upper-left corner of the page to create a verification SCF.


### Step 2. Create a custom verification plugin

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway).
2. On the left sidebar, click **Plugin** > **Custom Plugin** to enter the custom plugin list page.
3. Click **Create** in the top-left corner of the page to create a custom verification plugin.
	- For verification services deployed in SCF, you need to enter the following data when creating the custom verification plugin:
<table>
<tr>
<th style="width:12%">Parameter</th>
<th style="width:10%">Required</th>
<th>Description</th>
</tr>
<tr>
<td>Function</td>
<td>Yes</td>
<td>Select the namespace, name, and version of the verification function.</td>
</tr>
<tr>
<td>Backend timeout</td>
<td>Yes</td>
<td>Set the backend timeout that API Gateway forwards the request to the verification function. The maximum time limit is 30 minutes. When no response is returned before the timeout after API Gateway calls the function, API Gateway will end the call and return an error message.</td>
</tr>
<tr>
<td>Whether to send the Body</td>
<td>Yes</td>
<td><ul><li>When the value is `Yes`, the Header, Body, and Query requested by the client will be sent to the function.</li>
<li>When the value is `No`, the requested Body will not be sent.</li></ul>
</td>
</tr>
<tr>
<td>Verification Parameters</td>
<td>No</td>
<td>Set the request parameters for verification. When **Cache Period** is not `0`, this parameter must be set. When caching is enabled, the verification result will be queried with this parameter as the search criterion.</td>
</tr>
<tr>
<td>Cache Period</td>
<td>Yes</td>
<td>Set the cache validity period for the verification result. `0` indicates that caching is not enabled. The cache validity period can be up to 3,600 seconds.</td>
</tr>
</table>
	- For verification services deployed on the public network, you need to enter the following data when creating the custom verification plugin:
<table>
<tr>
<th style="width:12%">Parameter</th>
<th style="width:10%">Required</th>
<th>Description</th>
</tr>
<tr>
<td>Request method</td>
<td>Yes</td>
<td>Request method of the custom verification function, which can be GET, POST, PUT, DELETE, HEAD, and ANY.</td>
</tr>
<tr>
<td>Public network service</td>
<td>Yes</td>
<td>Access address of the custom verification service, which can be an HTTP or HTTPS address.</td>
</tr>
<tr>
<td>Path match mode</td>
<td>Yes</td>
<td>It can be backend path or full path match.
<ul><li>Backend path match: The configured path is used to request the service.</li>
<li>Full path match: The overlapping part is used to request the service. For example, if the configured API path is `/a/` and the request path is `/a/b`, then the path transferred to the service will be `/b` after full path match is enabled.</li></ul>
</td>
</tr>
</table>
<img src = "https://qcloudimg.tencent-cloud.cn/raw/ed0d1da4947eec16a8c49b6990bf29b6.png"> 
	- For verification services deployed in a VPC, you need to enter the following data when creating the custom verification plugin:
<table>
<tr>
<th style="width:12%">Parameter</th>
<th style="width:10%">Required</th>
<th>Description</th>
</tr>
<tr>
<td>VPC</td>
<td>Yes</td>
<td>Select the VPC of the verification service.</td>
</tr>
<tr>
<td>Request method</td>
<td>Yes</td>
<td>Request method of the custom verification function, which can be GET, POST, PUT, DELETE, HEAD, and ANY.</td>
</tr>
<tr>
<td>Backend address</td>
<td>Yes</td>
<td>Access address of the custom verification service, which can be an HTTP or HTTPS address.</td>
</tr>
</table>
<img src = "https://qcloudimg.tencent-cloud.cn/raw/ad1af755730f533eddc3b870f9399166.png"> 



### Step 3. Bind the API

1. Select the just created plugin in the list and click **Bind API** in the **Operation** column.
2. In the **Bind API** pop-up window, select the service, environment, and the target API.
   ![](https://main.qcloudimg.com/raw/d7fd3c3539d6f623f45ebfdf0674d97e.png)
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
