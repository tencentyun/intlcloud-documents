
## Overview

The backend gRPC plugin is used in the scenarios where the HTTP/HTTPS protocol is used for communication from the client to the API Gateway, and the gRPC/gRPCS protocol is used for communication from the API Gateway to the backend.
Though the backend gRPC plugin, the API Gateway can obtain the `.proto` file (it is used to convert the HTTP/HTTPS protocol to the gRPC/gRPCS protocol), convert the request content according to the rule defined in the `.proto` file, and send the converted content to the backend.

## Request Process

![](https://qcloudimg.tencent-cloud.cn/raw/bd46af6b1986b5ce1b06be2dd904e494.png)

## Directions

### Step 1. Create the plugin

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway).
2. Click **Plugin** > **System Plugin** in the left sidebar.
3. On the page that appears, click **Create** in the upper-left corner. Select **Backend gRPC** for the plugin type, and create a backend gRPC plugin. The configuration item for this plugin is as follows:

<table>
<tr>
<th>Parameter</th>
<th>Required</th>
<th>Description</th>
</tr>
<tr>
<td>.proto description file</td>
<td>Yes</td>
<td>A <code>.proto</code> file that is used to convert the HTTP/HTTPS protocol to the gRPC/gRPCS protocol.</br>The code in the file follows the ProtoBuf syntax and supports both proto2 and proto3 versions.</td>
</tr>
</table>


### Step 2. Bind an API and make the plugin effective

1. Select the just created plugin in the list and click **Bind API** in the **Operation** column.
2. In the **Bind API** pop-up window, select the service, environment, and the API to which the plugin needs to be bound.
3. Click **OK** to bind the plugin to the API. At this time, the configuration of the plugin has taken effect for the API.

## Notes

- the size of `.proto` description file cannot exceed 1MB.
- the description file must strictly follow the ProtoBuf syntax.
- when the HTTP/HTTPS protocol is configured for the API frontend and the gRPC/gRPCS protocol is configured for the backend, an error will occur for the request if the backend gRPC plugin is not bound to the API.
- only when the client request method is POST, GET, PUT, PATCH or DELETE, "the API with the HTTP/HTTPS protocol configured for the frontend and the gRPC/gRPCS protocol configured for the backend" can be requested properly, otherwise an error will occur.
