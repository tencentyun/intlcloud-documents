## Operation Scenarios
This document describes how to create a general API in the API Gateway Console and configure the frontend, backend, and response result in detail.


## Step 1. Create a general API
1. Log in to the [API Gateway Console](https://console.cloud.tencent.com/apigateway/index?rid=1).
2. In the service list, click the name of the target service to view it.
3. In the service details, click the **Manage API** tab and choose to create a **General API** based on the backend business type.
4. Click **Create** for subsequent configuration.

## Step 2. Configure the frontend
The frontend configuration of an API refers to the configuration provided for external access, including the API name, frontend type, request protocol, HTTP method, URL path, and definitions of input parameters.

### Configuring basic frontend information
- **API name**: name of the API you create, which must be unique within the current service and can contain up to 60 characters.
- **Frontend type**: API Gateway supports two frontend types: HTTP and WebSocket.
 - HTTP: suitable for situations where the backend is integrated with HTTP, Mock, or a cloud function.
 - WebSocket: suitable for situations where WebSocket is used for the business and the backend is integrated with WebSocket or a cloud function.
- **Request protocol**: API Gateway supports HTTP/HTTPS protocols in three modes: HTTP only, HTTPS only, and HTTP/HTTPS.
-  **HTTP method**: you can select GET, POST, PUT, DELETE, or HEAD.
- **URL path**: you can write a valid URL path as needed. If you need to configure a dynamic parameter in the path, please use `{}` to enclose the parameter name. For example, the `/user/{userid}` path declares the `userid` parameter in the path, which must be defined as a path-type input parameter. A query parameter does not need to be defined in the URL path.
**Regular expression match is supported**. Taking `/user` as an example of the path:
 - `=/user`: indicates exact match. When there are multiple APIs with `/user`, APIs configured with `=/user` have the highest matching priority.
 - `^~/user`: indicates matching the `user` prefix. When there are multiple APIs with `/user`, APIs configured with `^~/user` have the second highest matching priority.
 - `/user/{id}`: indicates that there is a dynamic parameter in the path. When there are multiple APIs with `/user`, APIs configured with a dynamic parameter have the third highest matching priority.
 - `/user`: indicates access by exact match or prefix match. `/user`, `/usertest`, and `/user/test/a` all can access APIs with the path of `/user`.
 - Standard regular expressions are supported; for example, the asterisk (*) matches the preceding subexpression zero or more times, while the question mark (?) matches the preceding subexpression zero or one time.

### Configuring frontend parameters
**Input parameters**: the input parameters include parameters from the header, query, and path, where a path parameter corresponds to a dynamic parameter defined in the URL path. For any parameter, the parameter name, parameter type, and parameter data type must be specified, and whether it is required, its default value, sample data, and description can be specified optionally. With these configuration items, API Gateway helps you with documentation and preliminary verification of input parameters.
![](https://main.qcloudimg.com/raw/5c5350abfae7dcbcf1903d8d25a9b59d.png)
>
>- If the request protocol is HTTPS, a request must carry SNI. In order to ensure request security, API Gateway will reject requests without SNI.
>- SNI (Server Name Indication) is an extension to TLS used to address situations where a server has multiple domain names, which is supported by the protocol since TLSv1.2. Previous SSL handshake messages didn't carry the destination address to be accessed by the client. If a server has multiple virtual hosts, each of which has a unique domain name and uses a unique certificate, then it will not be able to determine which certificate to return to the client. SNI addresses this issue by providing the host information in `Client Hello`.

## Step 3. Configure the backend

The backend configuration of an API refers to the configuration that actually provides the service. API Gateway converts a frontend request based on the backend configuration and forwards the call to the actual service.
The backend configuration provided by API Gateway varies slightly by frontend type as described below:
- If the frontend type is HTTP, the backend configuration includes [integrating with HTTP](#http), [integrating with SCF](#scf), and [integrating with Mock](#mock).
- If the frontend type is WebSocket, the backend configuration includes [integrating with WebSocket](#websocket) and [integrating with SCF](#scf).

<span id="http"></span>
### Integrating with HTTP 
If your business is deployed in another cloud or on your local server and is opened with HTTP, select the HTTP integration for the backend.

Configuration instructions:
1. To integrate with HTTP, you must select HTTP as the backend type.
2. Choose whether to enable VPC. To enable VPC, select VPC resources as prompted in the console.
3. Enter the backend domain name which begins with `http://` or `https://` excluding the path, such as `http://api.myservice.com` or `http://108.160.162.30`.
4. Enter the backend path starting with `/`, such as `/path` or `/path/{petid}`.
5. Select the request method. The request methods for the frontend and the backend can be different.
6. Set the backend timeout period (up to 30 minutes). During a call, if there is no response after the timeout period elapses, API Gateway will terminate the call and return the corresponding error message.
7. Set the backend parameters that map the frontend.
8. Click **Next** and configure the response result.
![](https://main.qcloudimg.com/raw/259092151bb811311c3d05bfd16ace65.png)


#### API Gateway backend integration with CLB resources in VPC
If you want to integrate the backend with CLB in VPC, the frontend can be configured in the same way as other APIs, and the backend should be configured in the following way:
1. In the backend configuration, select the VPC to be integrated with.
![](https://main.qcloudimg.com/raw/15e6d1daba72708d28747fa38ad1dcfd.png)
2. After selecting the VPC where your resource resides, select CLB as the resource type in VPC. Currently, API Gateway only allows you to integrate with CLB in VPC, and integration with other Tencent Cloud resources in VPC will be supported in the future.
![](https://main.qcloudimg.com/raw/0be3289e9aa42e8cef8bf0062a1a00bf.png)
3. Enter `http://vip+port` or `https://vip+port` at the backend address. The requests sent to CLB will be HTTP requests or HTTPS requests depending on the content you enter. The VIP here is the VIP of the private network CLB instance, which can be viewed in its basic information.
![](https://main.qcloudimg.com/raw/dda0cba1faf5a0276c9dab5dff1e75f5.png)
4. Select a listener type.
 - If you select the CLB listener type of HTTP/HTTPS, you should configure the backend path as the path configured in the CLB listener.
Domain name and path configured in the CLB listener:
![](https://main.qcloudimg.com/raw/0343ecb570624f0c71f11e3ca0805a63.png)
 The backend path in API Gateway must be the same as that in CLB.
![](https://main.qcloudimg.com/raw/4637b8ae237e84dc3632ee1a5abf36f4.png)
 You also need to configure a parameter named `host` as a constant parameter and place it in the header, whose value should be the domain name configured in the CLB listener.
![](https://main.qcloudimg.com/raw/d1d6bb3a99344099385dc8b19ee23386.png)
 - If you select the CLB listener type of TCP/UDP, you should configure the backend path as the path required by the business in the real CVM instance of the CLB instance.
If you have configured host verification in CVM, you need to configure a parameter named `host` as a constant parameter and select the address to place it based on your actual business needs, just like with a layer-7 listener. Subsequent configuration is the same as that of other APIs.
> When the backend is integrated with CLB, security groups on the real CVM instance should open the IP ranges of `100.64.0.0/10` and `9.0.0.0/8`.

<span id="scf"></span>
### Integrating with SCF
If you choose not to enable response integration (existing mode) for API Gateway integration with SCF, the request information will be combined in a fixed structure when API Gateway sends a request to SCF, and the fixed structure will be received by SCF. The return will be passed through without being processed.

Configuration instructions:
1. When you integrate the backend with SCF, you should configure the functions you created on SCF.
2. Configure the timeout period and click **Complete**.
![](https://main.qcloudimg.com/raw/8d970528f85847bdf02aab4cfb5b4d9d.png)
If you choose to enable response for API Gateway integration with SCF, the request information will be combined in a fixed structure when API Gateway sends a request to SCF, and the content returned by SCF should also be in a fixed structure. API Gateway will then map the content returned by SCF to `statusCode`, `header`, and `body` and return it to the client.

In this case, you need to return data in the following format to API Gateway for parsing:
```
{ 
        "isBase64Encoded": false, // Whether Base64 encoding is used. The value is `true` or `false` 
        "statusCode": 200, // HTTP request status code 
        "headers": {"Content-Type":"text/html"}, 
        "body": "<html><body><h1>Heading</h1><p>Paragraph.</p></body></html>" 
}
```

The structure sent by API Gateway to SCF is in the following format:
```
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
    "Accept-Language": "en-US,en,cn",
    "Accept": "text/html,application/xml,application/json",
    "Host": "service-3ei3tii4-251000691.ap-guangzhou.apigateway.myqloud.com",
    "User-Agent": "User Agent String"
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
> You can implement backend web services by writing SCF functions and providing services through API Gateway which will pass the request content as parameters to the function and return the result from the function back to the requester as the response. For more information, please see [API Gateway Trigger Overview](https://intl.cloud.tencent.com/document/product/583/12513).

<span id="mock"></span>
### Integrating with Mock 
Mock returns a response that has a fixed configuration to an API request. It is typically used for development testing. API configuration and response can be completed in advance before the backend service is completed. To integrate with Mock, you only need to configure your returned data and click **Complete**.
![](https://main.qcloudimg.com/raw/40ce80c320c12721efabae202e296b30.png)

<span id="websocket"></span>
### Integrating with WebSocket
If WebSocket is used for your business, you can integrate WebSocket with your backend service in generally the same way as [integrating with HTTP](#http), except that the backend domain name should begin with `ws://` or `wss://` excluding the path.
![](https://main.qcloudimg.com/raw/7426c3ce1db7a9a8fa9366cb63c1f04d.png)

## Step 4. Configure the response
API response configuration includes the configuration of API response data and API error codes.
API response data configuration: indicates the type of returned data, including data samples of successful and failed calls.
API error code definition: indicates additional error code, error message, and description.

> Currently, API Gateway directly passes through the response result to the requester without processing it. When SDK documentation is generated, the entered sample responses will also be displayed in the documentation, which will help users better understand the meanings of APIs.
