## Overview

The request body sent to service backend by the Client contains many fields. If you want to modify the content of the request body, you can do so via custom request body plugin.

The custom request body plugin applies during the request process. The request body rewriting service can be deployed in SCF, on the public network, or in a VPC. API Gateway will forward the request content to the request body rewriting service after receiving it from the client. The rewriting service will send the content of the request body to API Gateway after modifying it. Then, API Gateway will forward the modified request body to the service backend.

![](https://qcloudimg.tencent-cloud.cn/raw/8aedabdaec35a1c52df74f4f0f1925c7.png)

## Prerequisites

For verification services deployed in SCF, you need to enable the [SCF](https://console.cloud.tencent.com/scf/list) service.

## Directions

### Step 1. Create a function to modify the request body
For verification functions deployed on the public network or in a VPC, you can skip this step.

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/list).
2. Click **Functions** on the left sidebar to enter the function list page.
3. Click **Create** at the upper-left corner of the page to create a SCF that is used to modify the request body.


### Step 2. Create a custom request body plugin[](id:step2)

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway).
2. On the left sidebar, click **Plugin** > **Custom Plugin** to enter the custom plugin list page.
3. Click **Create** in the top-left corner of the page to create a custom request body plugin.
	- For verification services deployed in SCF, you need to enter the following data when creating the custom request body plugin:
<table>
<tr>
<th style="width:12%">Parameter</th>
<th style="width:10%">Required</th>
<th>Description</th>
</tr>
<tr>
<td>Function</td>
<td>Yes</td>
<td>Select the namespace, name, and version of the function that is used to modify the request body.</td>
</tr>
<tr>
<td>Backend timeout</td>
<td>Yes</td>
<td>Set the backend timeout that API Gateway forwards the request to the function that is used to modify the request body. The maximum time limit is 30 minutes. When no response is returned before the timeout after API Gateway calls the function, API Gateway will end the call and return an error message.</td>
</tr>
<tr>
<td>Custom content</td>
<td>Yes</td>
<td>Set the request content sent by API Gateway to the function used to modify the request body. You can select Header, Body, and Query. The request content not selected will not be modified and will be forwarded to the service backend as is.</td>
</tr>
<tr>
<td>Base64 Encoding</td>
<td>Yes</td>
<td>Specify whether to forward the request content to the function after applying Base64 encoding. Generally, it is applicable to binary content.</td>
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
<td>Request method of the custom request body function, which can be GET, POST, PUT, DELETE, HEAD, and ANY.</td>
</tr>
<tr>
<td>Public network service</td>
<td>Yes</td>
<td>Access address of the request body service, which can be an HTTP or HTTPS address.</td>
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
<img src = "https://qcloudimg.tencent-cloud.cn/raw/d9949dc29680fa9f537591c31f25ce79.png"> 
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
<td>Select the VPC of the custom request rewriting service.</td>
</tr>
<tr>
<td>Request method</td>
<td>Yes</td>
<td>Request method of the custom request rewriting service, which can be GET, POST, PUT, DELETE, HEAD, and ANY.</td>
</tr>
<tr>
<td>Backend address</td>
<td>Yes</td>
<td>Access address of the custom request body service, which can be an HTTP or HTTPS address.</td>
</tr>
</table>
<img src = "https://qcloudimg.tencent-cloud.cn/raw/778a19c16faf213034ec34ca27b3f155.png"> 


### Step 3. Bind the API

1. Select the plugin created in [step 2](#step2) from the list. Click **Bind API** in the **Operation** column.
2. In the **Bind API** pop-up window, select the service, environment, and the target API.
   ![](https://main.qcloudimg.com/raw/d7fd3c3539d6f623f45ebfdf0674d97e.png)
3. Click **OK** to bind the plugin to the API. At this time, the configuration of the plugin has taken effect for the API.

## How to Write Custom Request Body Function[](id:scfdemo)
### Returned value definition
The custom request body plugin of API Gateway needs to receive the response in a certain format returned by the custom request body SCF. The specific format is as follows:
```
{
  "replace_headers":{
    "header1":"header1-value",
    "header2":"header2-value"
  },
  "remove_headers":[
    "header3",
    "header4"
  ],
  "replace_body":"hello",
  "replace_querys":{
    "query1":"query1-value",
    "query2":"query2-value"
  },
  "remove_querys":[
    "query3",
    "query4"
  ]
}
```

### Demo for Python
For more information on how to write the function that is used to modify the request body in Python, see [Custom Request Body Demo for Python](https://github.com/tencentyun/serverless-demo/blob/master/Python3.6-APIGWCustomRequest/src/index.py).

### Demo for Java
```
package com.example.demo;

import com.google.gson.JsonArray;
import com.google.gson.JsonObject;
import com.qcloud.services.scf.runtime.events.APIGatewayProxyRequestEvent;

public class Demo {

	public String mainHandler(APIGatewayProxyRequestEvent request) {
		System.out.println("helloworld");
		System.out.println(request.getHttpMethod());
		JsonObject resp = new JsonObject();
		headerHandler(request, resp);
		headerQuery(request, resp);
		headerBody(request, resp);
		return resp.toString();
	}

	private void headerHandler(APIGatewayProxyRequestEvent request, JsonObject resp) {
		JsonObject replace_headers = new JsonObject();
		JsonArray remove_headers = new JsonArray();
		// Sample: Replace or add `header1` and `header2`
		replace_headers.addProperty("header1", "header1-value");
		replace_headers.addProperty("header2", "header2-value");

		// Sample: Delete `query3`
		remove_headers.add("header3");
		resp.add("replace_headers", replace_headers);
		resp.add("remove_headers", remove_headers);
	}

	private void headerQuery(APIGatewayProxyRequestEvent request, JsonObject resp) {
		JsonObject replace_querys = new JsonObject();
		JsonArray remove_querys = new JsonArray();

		// Sample: Replace or add `query1` and `query2`
		replace_querys.addProperty("query1", "query1-value");
		replace_querys.addProperty("query2", "query2-value");

		// Sample: Delete `query3`
		remove_querys.add("query3");
		resp.add("replace_querys", replace_querys);
		resp.add("remove_querys", remove_querys);
	}

	private void headerBody(APIGatewayProxyRequestEvent request, JsonObject resp) {
		resp.addProperty("replace_body", "{'name':'Yagr'}");
	}
}
```

## PluginData

```json
{
    "endpoint_timeout":15, // Backend timeout period in seconds. Value range: 0–60
    "func_name":"test_name", // Custom SCF name
    "func_namespace":"test_namespace", // Custom SCF namespace
    "func_qualifier":"$LATEST", // Custom SCF version
    "is_base64_encoded":true, // Whether to forward the request content to the SCF after applying Base64 encoding
    "is_send_req_body":true, // Whether to send the request Body content to the SCF
    "is_send_req_headers":true, // Whether to send the request Header content to the SCF
    "is_send_req_querys":true, // Whether to send the request Query content to the SCF
    "user_id":1253970226 // appid
}
```

## Notes

- Binding a custom plugin to the API means creating a trigger for the SCF to trigger the API. Deleting the trigger on the SCF side means unbinding the plugin from the API.
- For now, the custom request body plugin only supports event-triggered function and does not support HTTP-triggered function.
