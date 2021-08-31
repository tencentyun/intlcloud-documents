## Overview

This document describes how to create an API connecting to Mock in the backend through the API Gateway console.

>!If the API connects to Mock in the backend, only fixed data can be returned. Therefore, you are advised to use Mock for testings but not in actual business scenarios.


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
![](https://main.qcloudimg.com/raw/ff19cf6d5e757d455a92e1ee0ab9ea43.png)

> ?
> - If the request protocol is HTTPS, a request must carry SNI. To ensure request security, API Gateway will deny requests without SNI.
> - SNI (Server Name Indication) is an extension to TLS. It is used to address situations where a server has multiple domain names and is supported by the protocol since TLSv1.2. Previous SSL handshake messages didn't carry the destination address to be accessed by the client. If a server has multiple virtual hosts, each of which has a unique domain name and uses a unique certificate, then it will not be able to determine which certificate to return to the client. SNI addresses this issue by providing the host information in `Client Hello`.

### Step 3. Configure Mock in the backend

Mock returns a response that has a fixed configuration to an API request. It is typically used for development testing. API configuration and response can be completed in advance before the backend service is completed. To connect with Mock, you only need to configure your returned data and click **Complete**.
![](https://main.qcloudimg.com/raw/c4aedc20312dbf18ca939559ff03b4f0.png)
