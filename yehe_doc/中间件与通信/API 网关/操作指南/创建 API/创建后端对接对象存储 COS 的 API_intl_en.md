## Overview

This document describes how to create an API connecting to [COS](https://console.cloud.tencent.com/cos) on the backend in the API Gateway console.

## Solution Strengths
- API Gateway and COS are interconnected over the private network, which has an excellent performance and doesn't incur public network traffic fees.
- API Gateway can calculate the COS signature, so there is no need to transform the client.

## Prerequisites
- You have [created an API Gateway service](https://intl.cloud.tencent.com/document/product/628/11787).
- You have [created a COS bucket](https://intl.cloud.tencent.com/document/product/436/13309) and [uploaded an object](https://intl.cloud.tencent.com/document/product/436/13321).

## Directions
### Step 1. Create a general API

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway/index?rid=1) and click **Service** on the left sidebar.
2. In the service list, click the name of the target service.
3. In the service details, click the **Manage API** tab and choose to create a **general API** based on the backend business type.
4. Click **Create** for subsequent configuration.

### Step 2. Configure the frontend

The frontend configuration of an API refers to the configuration provided for external access, including the API name, frontend type, request protocol, HTTP method, URL path, and input parameter definition. You need to set the following fields:
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Required</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>API name</td>
<td>Yes</td>
<td>Name of the API you create, which must be unique within the current service and can contain up to 60 characters.</td>
</tr>
<tr>
<td>Frontend type</td>
<td>Yes</td>
<td>Protocol for the client to access API Gateway. API Gateway supports two frontend types: <strong>HTTP&amp;HTTPS</strong> and <strong>WS&amp;WSS</strong>.</td>
</tr>
<tr>
<td>URL path</td>
<td>Yes</td>
<td>You can write a valid URL path as needed. <br><strong>Configure a dynamic parameter in the path</strong>: Use <code>{}</code> to enclose the parameter name. For example, the <code>/user/{userid}</code> path declares the `userid` parameter in the path, which must be defined as a path-type input parameter. A query parameter does not need to be defined in the URL path.<br><strong>Regular expression match is supported for the path </strong>: Taking <code>/user</code> as an example of the path: <br><code>=/user</code>: Indicates exact match. When there are multiple APIs with <code>/user</code>, APIs configured with <code>=/user</code> will be matched first.<br> <code>/user/{id}</code>: Indicates that there is a dynamic parameter in the path. When there are multiple APIs with <code>/user</code>, APIs configured with a dynamic parameter will be matched first.<br><code>/user</code>: Indicates access by exact match or prefix match. <code>/user</code>, <code>/usertest</code>, and <code>/user/test/a</code> all can access APIs with the path of <code>/user</code>.</td>
</tr>
<tr>
<td>Request method</td>
<td>Yes</td>
<td>You can select GET, POST, PUT, DELETE, or HEAD.</td>
</tr>
<tr>
<td>Authentication type</td>
<td>Yes</td>
<td>API authentication type. Multiple types are supported.</td>
</tr>
<tr>
<td>CORS is supported</td>
<td>Yes</td>
<td>It is used to configure cross-origin resource sharing (CORS). After it is enabled, <code>Access-Control-Allow-Origin : *</code> will be added to the response header by default.</td>
</tr>
<tr>
<td>Input parameter</td>
<td>No</td>
<td>The input parameters include parameters from the header, query, and path, where a path parameter corresponds to a dynamic parameter defined in the URL path. For any parameter, the parameter name, parameter type, and parameter data type must be specified, and whether it is required, its default value, sample data, and description can be specified optionally. With these configuration items, API Gateway helps you with documentation and preliminary verification of input parameters.</td>
</tr>
</tbody></table>
Click <b>Next</b> for backend configuration.

### Step 3. Configure the backend to interconnect with COS

The backend configuration of an API refers to the configuration that actually provides the service. API Gateway converts a frontend request based on the backend configuration and forwards the call to the actual service. If your business is deployed in COS and the backend needs to be interconnected with COS, you need to select COS as the backend type.
Configuration instructions:

| Parameter | Required | Description |
|---------|---------|---------|
| Action | Yes | COS API to be interconnected with API Gateway, which is linked with the request method in the frontend configuration. For more information, see [**Notes**](#notice). |
| Bucket | Yes | Only a bucket in the same region as API Gateway can be interconnected with. |
| Calculate COS signature | Yes | After it is enabled, the COS signature will be calculated in API Gateway, so the system doesn't need to request the client to calculate the signature. |
| Backend Path | Yes | 	It must start with "/". API Gateway will match objects in the bucket based on the path. |
| Path Match Method | Yes | **Full path match:** Objects in the bucket are matched by the combination of the frontend path and backend path. This is suitable for scenarios where objects to be manipulated are at different paths passed in by the client. For the specific match rules, see [**Notes**](#notice).</br>**Backend path match:** An object in the bucket is matched by only the frontend path. This is suitable for scenarios where only a fixed object needs to be manipulated. No matter which path the client uses for access, the request will be always forwarded to the COS object at the backend path. |



[](id:notice)
## Notes
### Linkages between request method and Action
Linkages between the request method and `Action` are as detailed below:

| Request Method Selected in Frontend Configuration | Action in Backend Configuration |
|---------|---------|
| GET | GetObject |
| PUT | PutObject |
| POST | PostObject, AppendObject |
| HEAD | HeadObject |
| DELETE | DeleteObject |

### Full path match rules
Passthrough path = backend path + request path - frontend path. Below are sample paths in four cases:

| Path  | Case 1 | Case 2 | Case 3 | Case 4 |
|---------|---------|---------|---------|---------|
| Frontend path | / | /a | /a | /a |
| Backend path | / | /b | / | /b |
| Request path | /a/b | /a/b | /a/b | /a/c |
| Passthrough path | /a/b | /b/b | /b | /b/c |
