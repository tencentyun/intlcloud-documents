## Scenarios

The response body sent to the Client by API Gateway contains many fields. If you want to modify the content of the response body, you can do so via custom response body plugin.

The custom response body plugin applies during the response process, and the response content rewriting service can be deployed in SCF, on the public network, or in a VPC. The service backend will send the response body to API Gateway after processing the request message. API Gateway will forward the response content to the response body modification service after receiving it. The modification service will send the modified content of the response body to API Gateway after modifying it. Then, API Gateway will forward the modified response body to the service backend.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/Rn6Y872_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_168188624396.png)

## Prerequisites

Any one of the following: 

1. Activate [SCF](https://console.cloud.tencent.com/scf/list).
2. Connect your service to the public network.
3. Activate [VPC](https://console.cloud.tencent.com/vpc/vpc?rid=1).

## Directions
We take SCF as an example in this document.

### Step 1. Create a function to modify the response body

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/list).
2. Click **Function Service** in the left sidebar to open the function list page.
3. Click **Create** in the top-left corner of the page to create a function that is used to modify the response body.

### Step 2. Create a custom response body plugin[](id:step2)

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway).
2. On the left sidebar, click **Plugin** > **Custom Plugin** to enter the custom plugin list page.
3. Click **Create** in the top-left corner of the page to create a custom response body plugin.
	- For verification services deployed in SCF, you need to enter the following data when creating the custom response plugin:
<table>
<tr>
<th style="width:12%">Parameter</th>
<th style="width:10%">Required</th>
<th>Description</th>
</tr>
<tr>
<td>Function</td>
<td>Yes</td>
<td>Select the namespace, name, and version of the response body modification function.</td>
</tr>
<tr>
<td>Backend timeout</td>
<td>Yes</td>
<td>Set the backend timeout that API Gateway forwards the request to the function that is used to modify the response body. The maximum time limit is 30 minutes. When no response is returned before the timeout after API Gateway calls the function, API Gateway will end the call and return an error message.</td>
</tr>
<tr>
<td>Custom content</td>
<td>Yes</td>
<td>Set the response content sent by API Gateway to the function used to modify the response body. You can select Header, Body, and Query. The response content not selected will not be modified and will be forwarded to the client as is.</td>
</tr>
<tr>
<td>Base64 Encoding</td>
<td>Yes</td>
<td>Specify whether to Base64-encode the response content to be forwarded by the service backend to the function. Generally, it is applicable to binary content.</td>
</tr>
</table>
	- For verification services deployed on the public network, you need to enter the following data when creating the custom response plugin:
<table>
<tr>
<th style="width:12%">Parameter</th>
<th style="width:10%">Required</th>
<th>Description</th>
</tr>
<tr>
<td>Request method</td>
<td>Yes</td>
<td>Request method of the custom response body function, which can be GET, POST, PUT, DELETE, HEAD, and ANY.</td>
</tr>
<tr>
<td>Public network service</td>
<td>Yes</td>
<td>Access address of the custom response body rewriting service, which can be an HTTP or HTTPS address.</td>
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
<img src = "https://staticintl.cloudcachetci.com/yehe/backend-news/VaTk806_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_1cd7dbeb-5440-4c25-8720-11bcee29302e.png"> 
	- For verification services deployed in a VPC, you need to enter the following data when creating the custom response plugin:
<table>
<tr>
<th style="width:12%">Parameter</th>
<th style="width:10%">Required</th>
<th>Description</th>
</tr>
<tr>
<td>VPC</td>
<td>Yes</td>
<td>Select the VPC of the response body rewriting service.</td>
</tr>
<tr>
<td>Request method</td>
<td>Yes</td>
<td>Request method of the response body rewriting function, which can be GET, POST, PUT, DELETE, HEAD, and ANY.</td>
</tr>
<tr>
<td>Backend address</td>
<td>Yes</td>
<td>Access address of the response body rewriting service, which can be an HTTP or HTTPS address.</td>
</tr>
</table>
<img src = "https://staticintl.cloudcachetci.com/yehe/backend-news/cruV961_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_92662b80-36b9-4ccf-990f-7c8aafa4dd1b.png"> 


### Step 3: binding the API

1. Select the plugin created in [step 2](#step2) from the plugin list. Click **Bind API** in the **Operation** column.
2. In the **Bind API** pop-up window, select the service, environment, and the API that needs to be bound to the plugin.
   ![](https://staticintl.cloudcachetci.com/yehe/backend-news/h49G353_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_f4777ebb-a6ba-45ce-a946-4712123b309c.png)
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

- Binding a custom plugin to the API means creating a trigger for the function to trigger the API. Deleting the trigger on the SCF side means unbinding the plugin from the API.
- Currently, the custom response body plugin supports only event-triggered functions but not HTTP-triggered functions.
- The priority of the custom response body plugin is lower than that of all plugins applied during the request process.
- If the custom response body plugin is bound to an API with a Mock or TSF backend, it will not take effect.
- The custom response body plugin does not support the HTTP2 protocol.
- The custom response body plugin does not support the response body compressed in the gzip format returned by the backend.

