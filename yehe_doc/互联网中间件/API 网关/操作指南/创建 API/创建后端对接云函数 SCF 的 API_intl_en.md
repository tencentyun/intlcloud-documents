## Overview

This document describes how to create an API connecting to SCF in the backend through the API Gateway console.

## Prerequisites
You have [created a service](https://intl.cloud.tencent.com/document/product/628/11787).

## Directions
### Step 1. Create a general API

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway/index?rid=1) and click **Service** in the left sidebar.
2. In the service list, click the name of the target service to view it.
3. In the service details, click the **Manage API** tab and choose to create a **General API** based on the backend business type.
4. Click **Create** for subsequent configuration.

### Step 2. Perform frontend configuration

The frontend configuration of an API refers to the relevant configurations provided for external access, including the API name, frontend type, request protocol, HTTP method, URL path, and input parameter definition.

#### Configuring basic frontend information

- **API Name**: name of the API you create, which must be unique within the current service and can contain up to 60 characters.
- **Frontend Type**: supports HTTP&HTTPS and WS&WSS.
- **Path**: You can write a valid URL path as needed. If you need to configure dynamic parameters in the path, please use `{}` to enclose the parameter names. For example, the `/user/{userid}` path declares the `userid` parameter in the path, which must be defined as a path-type input parameter. Query parameters do not need to be defined in the URL path.
  **Regular expression match is supported**. Taking `/user` as an example of the path:
	- `=/user`: indicates exact match. When there are multiple APIs with `/user`, APIs configured with `=/user` have the highest matching priority.
	- `/user/{id}`: indicates that there is a dynamic parameter in the path. When there are multiple APIs with `/user`, APIs configured with a dynamic parameter have the third-highest matching priority.
	- `/user`: indicates access by exact match or prefix match. `/user`, `/usertest`, and `/user/test/a` all can access APIs with the path of `/user`.
- **Request Method**: supports GET, POST, PUT, DELETE, and HEAD.
- **Authentication Type**: supports [No authentication](https://intl.cloud.tencent.com/document/product/628/11820), [Key pari](https://intl.cloud.tencent.com/document/product/628/11819), and [OAuth 2.0](https://intl.cloud.tencent.com/document/product/628/34065).
- **CORS is supported**: configures cross-origin resource sharing (CORS). If enabled, `Access-Control-Allow-Origin : *` will be added to the response header by default.

#### Configuring frontend parameters

**Input parameters**: the input parameters include parameters from the header, query, and path, where a path parameter corresponds to a dynamic parameter defined in the URL path. For any parameter, the parameter name, parameter type, and parameter data type must be specified, and whether it is required, its default value, sample data, and description can be specified optionally. With these configuration items, API Gateway helps you with documentation and preliminary verification of input parameters.
![](https://main.qcloudimg.com/raw/9788b49935d2bba47a72e491af1a2a5b.png)

> ?
> - If the request protocol is HTTPS, a request must carry SNI. To ensure request security, API Gateway will deny requests without SNI.
> - SNI (Server Name Indication) is an extension to TLS. It is used to address situations where a server has multiple domain names and is supported by the protocol since TLSv1.2. Previous SSL handshake messages didn't carry the destination address to be accessed by the client. If a server has multiple virtual hosts, each of which has a unique domain name and uses a unique certificate, then it will not be able to determine which certificate to return to the client. SNI addresses this issue by providing the host information in `Client Hello`.

### Step 3: Configure SCF in the backend

The backend configuration of an API refers to the configuration that actually provides the service. API Gateway converts a frontend request based on the backend configuration and forwards the call to the actual service.
If your business is implemented in SCF and you want to open up your service capabilities through API Gateway, you can select SCF as the backend connection type.

![](https://main.qcloudimg.com/raw/347da1dcf7fc39be1c56e4a56c65f45c.png)

When connecting to SCF in the backend, you need to enter the following parameters:

| No. | Parameter | Description |
| ---- | -------- | -------------------------------------- |
| 1 | Namespace | Namespace of the connected function, which is `default` by default |
| 2 | Name | Name of the connected function |
| 3 | Version | Version of the connected function. Default value: `$LATEST` |
| 4 | Backend timeout | The default value is `15` (seconds). |
| 5 | Response integration | See [Response integration](#1) for more information. |

Response integration: [](id:1)

Request method is the method to process requests sent from API Gateway to SCF, and response method is the method to process the returned values sent from SCF to API Gateway. Request method and response method can be implemented using pass-through or integration.

- If response integration is not enabled, the pass-through mode will be used. That is, when API Gateway sends a request to SCF, the request information will be combined into a fixed structure, which will be received by SCF. The response will be passed through without being processed and can only be in JSON format.
- If response integration is enabled, the integration mode will be used. That is, when API Gateway sends a request to SCF, the request information will be combined into a fixed structure, and SCF also returns a fixed structure. API Gateway will map the structure returned by SCF to `statusCode`, `header`, `body` as well as other fields, and then return it to the client.

If response integration is enabled, you must configure the SCF to return data in the following format to API Gateway for parsing:

```
{ 
        "isBase64Encoded": false, // Whether Base64 encoding is used. Valid values: `true`, `false` 
        "statusCode": 200, // HTTP request status code 
        "headers": {"Content-Type":"text/html"}, // `Content-Type` can contain only strings but not arrays.
        "body": "<html><body><h1>Heading</h1><p>Paragraph.</p></body></html>" 
}
```

The structure format of requests sent from API Gateway to SCF is as follows:

```
{
  "requestContext": {
    "serviceId": "service-f94sy04v",
    "path": "/test/{path}",
    "httpMethod": "POST",
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
    "User-Agent": "User Agent String",
    "x-api-requestid": "c6af9ac6-7b61-11e6-9a41-93e8deadbeef"
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
  "httpMethod": "POST",
  "isBase64Encoded": "true"
}
```

> ? You can implement backend web services by writing SCF functions and providing services through API Gateway which will pass the request content as parameters to the function and return the result from the function back to the requester as the response. For more information, please see [API Gateway Trigger Overview](https://intl.cloud.tencent.com/document/product/583/12513).

### Step 4. Configure the response

API response configuration: includes the configuration of API response data and API error codes.
API response data configuration: indicates the type of returned data, including the data samples of successful and failed calls.
API error code definition: indicates the additional error code, error message, and description.

> ?Currently, API Gateway directly passes through the response result to the requester without processing it. When SDK documentation is generated, the entered sample responses will also be displayed in the documentation, which will help users better understand the meanings of APIs.
