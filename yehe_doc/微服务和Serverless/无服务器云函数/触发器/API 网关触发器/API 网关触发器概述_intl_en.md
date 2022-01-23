You can implement backend web services by writing SCF functions and providing services through API Gateway which will pass the request content as parameters to the function and return the result from the function back to the requester as the response.

>! API Gateway triggers can trigger both event-triggered functions and HTTP-triggered functions. This document only describes the request method of **event-triggered function** triggering. For more information on HTTP-triggered function triggering, see [Trigger Management](https://intl.cloud.tencent.com/document/product/583/40691).

Characteristics of API Gateway triggers:

- **Push model**
  After API Gateway receives an API request, if the API Gateway backend is connected with an SCF function, the function will be triggered. Meanwhile, API Gateway will send the relevant information of the API request to the triggered function as `event` input parameters, such as the specific service that receives the request, API rule, actual request path, method, and `path`, `header`, and `query` of the request.
- **Sync invocation**
  API Gateway invokes the function synchronously, and it will wait for the function to return before the timeout period configured in it elapses. For more information on invocation types, see [Invocation Types](https://intl.cloud.tencent.com/document/product/583/9694).

## API Gateway Trigger Configuration

API Gateway triggers can be configured in the **[SCF console](https://console.cloud.tencent.com/scf/index)** or the **[API Gateway console](https://console.cloud.tencent.com/apigateway/index)**.
<dx-tabs>
::: SCF console
In the **SCF console**, you can add API Gateway triggers, select existing or create API services, and define the request methods (currently, six methods are supported, namely, **ANY, GET, HEAD, POST, PUT, and DELETE**), environments (test, pre-release, and release environments), and authentication methods (API Gateway key pair).
:::
::: API\s Gateway console
When configuring API rules in the **API Gateway console**, you can select SCF as the backend and select functions in the same region as the API service. In the API Gateway console, you can configure and manage advanced API services such as traffic throttling plan, blocklist, and allowlist.

When you configure the connection with SCF in API Gateway, you also need to configure the timeout period. The request timeout period in API Gateway and the execution timeout period in SCF take effect respectively. The timeout rules are as follows:
- **API Gateway timeout period > SCF timeout period**
  The SCF timeout period takes effect first, the API request response is `200 HTTP code`, but the returned content is the error message of SCF timeout.
- **API Gateway timeout period < SCF timeout period**
  The API Gateway timeout period takes effect first, the API request response is `5xx HTTP code`, which indicates that the request timed out.
  :::
  </dx-tabs>




## Limitation on API Gateway Trigger Binding

In API Gateway, one API rule can be bound to only one function, but one function can be bound to multiple API rules as the backend. You can create an API with different paths in the [API Gateway console](https://console.cloud.tencent.com/apigateway/index) and point the backend to the same function. APIs with the same path, same request method, and different release environments are regarded as the same API and cannot be bound repeatedly.

API Gateway triggers currently can only be bound to functions in the same region; for example, a function created in the Guangzhou region can only be bound to and triggered by API rules created in the Guangzhou region. If you want to trigger a function through API Gateway configuration in a specific region, please create a function in that region.


## Request and Response

Request method is the method to process request sent from API Gateway to SCF, and response method is the method to process the returned value sent from SCF to API Gateway. Both request and response methods can be planned and implemented by means of passthrough and integration.

### Integration request and passthrough request

Integration request means that API Gateway converts the content of the HTTP request into request data structures which are passed to the function for handling as `event` input parameters of the function. The following details the request data structures.

For more information on passthrough requests, see [Trigger Management](https://intl.cloud.tencent.com/document/product/583/40691#.E8.AF.B7.E6.B1.82.E4.B8.8E.E5.93.8D.E5.BA.94).

>! When transferring images or files to SCF through API Gateway, you need to Base64-encode them. If the size of a Base64-encoded file is above 6 MB, we recommend you upload the file to [COS](https://intl.cloud.tencent.com/zh/product/cos) through the client and pass the object address to SCF first. Then, SCF will pull the file from COS to complete the upload.


<a id="datastructures"></a>

#### Event message structures of integration request for API Gateway trigger

When an API Gateway trigger receives a request, it sends the event data to the bound function in JSON format as shown below:

```json
{
  "requestContext": {
    "serviceId": "service-f94sy04v",
    "path": "/test/{path}",
    "httpMethod": "POST",
    "requestId": "c6af9ac6-7b61-11e6-9a41-93e8deadbeef",
    "identity": {
      "secretId": "abdcdxxxxxxxsdfs"
    },
    "sourceIp": "10.0.2.14",
    "stage": "release"
  },
  "headers": {
    "accept-Language": "en-US,en,cn",
    "accept": "text/html,application/xml,application/json",
    "host": "service-3ei3tii4-251000691.ap-guangzhou.apigateway.myqloud.com",
    "user-Agent": "User Agent String"
  },
  "body": "{\"test\":\"body\"}",
  "pathParameters": {
    "path": "value"
  },
  "queryStringParameters": {
    "foo": "bar"
  },
  "headerParameters":{
    "Refer": "10.0.2.14"
  },
  "stageVariables": {
    "stage": "release"
  },
  "path": "/test/value",
  "queryString": {
    "foo" : "bar",
    "bob" : "alice"
  },
  "httpMethod": "POST"
}
```

The data structures are as detailed below:

| Structure | Description |
| --------------------- | ------------------------------------------------------------ |
| requestContext | Configuration information, request ID, authentication information, and source information of the API gateway where the request comes from. <ul class="params"><li>`serviceId`, `path`, and `httpMethod` are service ID, API path, and method of API Gateway. <li>`stage` indicates the environment of the request source API. <li>`requestId` identifies the unique ID of the current request. <li>`identity` identifies the user's authentication method and information. <li>`sourceIp` identifies the request source IP. </ul> |
| path | Records the complete `Path` information of the actual request. |
| httpMethod | Records the `HTTP` method of the actual request. |
| queryString | Records the complete `Query` content of the actual request. |
| body | Records the content of the actual request after being converted into a `String`. |
| headers | Records the complete `Header` content of the actual request. |
| pathParameters | Records the `Path` parameters configured in API Gateway and their actual values. |
| queryStringParameters | Records the `Query` parameters configured in API Gateway and their actual values. |
| headerParameters | Records the `Header` parameters configured in API Gateway and their actual values. |

>! 
> - The content of `requestContext` may be increased during API Gateway iteration. At present, it is guaranteed that the content of the data structure will only be increased but not reduced, so that the existing structure will not be compromised.
> - Parameters in real requests may appear in multiple locations and can be selected based on your business needs.

### Integration response and passthrough response

Integration response means that API Gateway parses the returned content of the function and constructs an HTTP response based on the parsed content. With the aid of integration response, you can control the status code, headers, and body content of the response by using code, and implement the response in a custom format, such as XML, HTML, JSON, and even JS. When using integration response, data structures need to be returned based on the [rules of integration response for API Gateway trigger](#apiStructure) before they can be successfully parsed by API Gateway; otherwise, error message `{"errno":403,"error":"Invalid scf response format. please check your scf response format."}` will appear.

Passthrough response means that API Gateway directly passes the returned content of the function to the API requester. Generally, the data format of this type of responses is fixed at JSON format, the status code is defined according to the status of function execution, and status code 200 is returned if the function is successfully executed. With passthrough response, you can get the JSON format and parse the structures at the call location to get the content in the structures.

>! 
>
>- If the API Gateway trigger is configured in the API Gateway console, the way to handle the response is passthrough response by default. To enable integration response, select **Enable integration response** at the backend configuration location in the API configuration and return the content in the data structures detailed below in the code.
>- If the API Gateway trigger is configured in the SCF console, the integration response feature is enabled by default. Please pay attention to the format of the returned data.



[](id:apiStructure)

#### Returned data structures of integration response for API Gateway trigger

If integration response is set for API Gateway, the data structure in the following JSON format should be returned to API Gateway.

```json
{
    "isBase64Encoded": false,
    "statusCode": 200,
    "headers": {"Content-Type":"text/html"},
    "body": "<html><body><h1>Heading</h1><p>Paragraph.</p></body></html>"
}
```

The data structures are as detailed below:

| Structure | Description |
| --------------- | ------------------------------------------------------------ |
| isBase64Encoded | This indicates whether the content in the `body` is Base64-encoded binary. It should be `true` or `false` in JSON format. The specification of `true` and `false` varies by language, so you should adjust based on your actual language. |
| statusCode | HTTP return code, which should be an integer value. |
| headers | HTTP return header, which should contain multiple `key-value` or `key:[value,value]` objects. Both key and value should be strings. The `Location` key header is not supported currently. |
| body | HTTP return body. |



Taking Python 3.6 as an example, the sample code is as follows:

``` python
# -*- coding: utf8 -*-
import json
def main_handler(event, context):
    return {
        "isBase64Encoded": false,
        "statusCode": 200,
        "headers": {"Content-Type":"text/html"},
        "body": "<html><body><h1>Heading</h1><p>Paragraph.</p></body></html>"
    }
```

The returned result of a function triggered by API Gateway is as follows:

![](https://qcloudimg.tencent-cloud.cn/raw/b79ae25ee95d35988c2b2797b8972781.png)

If you need to return multiple headers with the same key, you can use a string array to describe different values; for example:

```
{
    "isBase64Encoded": false,
    "statusCode": 200,
    "headers": {"Content-Type":"text/html","Key":["value1","value2","value3"]},
    "body": "<html><body><h1>Heading</h1><p>Paragraph.</p></body></html>"
}
```
