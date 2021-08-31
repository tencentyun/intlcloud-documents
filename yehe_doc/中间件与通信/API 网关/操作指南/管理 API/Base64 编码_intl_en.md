## Overview

If Tencent Cloud API Gateway is connected with the SCF backend, binary data cannot be directly uploaded due to the trigger limits. Therefore, binary data must be Base64-encoded before the upload. API Gateway allows you to Base64-encode the client’s request body before it is passed to SCF. Once the Base64 encoding feature is enabled, you can upload binary data to SCF without modifying the client code.

The Base64 encoding feature provides the following two trigger modes to facilitate the needs of different scenarios:
- **Trigger All**: Base64-encodes all requested content for all requests before passing the content to SCF.
- **Trigger by Header**: Base64-encodes the requested content based on the trigger rules (required) configured. API Gateway will verify the request headers according to the trigger rules. Only requests with the specific `Content-Type` or `Accept` header will be Base64-encoded before being passed to SCF. Requests that do not meet the rules will be passed to SCF without being Base64-encoded.

## Interaction Process

![](https://main.qcloudimg.com/raw/74fc6a41ec95b542d095c6f43cd8c2f3.svg)

## Directions

### Configuring trigger all

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway/index?rid=1) and click **Service** in the left sidebar.
2. On the service list page, click the desired service name to view the API list.
3. Click **Create**, configure the API frontend, and click **Next**.
4. In the **Backend Configuration** step, choose **Serverless Cloud Function (SCF)** in the **Backend Type** filed, enable **Base64 Encoding**, and configure other fields as needed. In this way, Base64 encoding will be enabled for the created API with the default trigger mode **Trigger All**.
![](https://main.qcloudimg.com/raw/ac1d3b4252952f3d92b3c028fb88d138.png)

### Configuring trigger by header

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway/index?rid=1) and click **Service** in the left sidebar.
2. On the service list page, click the desired service name to view the API list.
3. Click the desired API (backend of the desired API must be SCF) to go to the API detail page. Then, choose the **Basic Configurations** tab and find the **Base64 Encoding** area.
4. Click **Edit** on the right of **Base Encoding** and click **Trigger by Header** > **Add Trigger Rule**. Then, select a header in **Parameter** and set the value as needed.
5. Click **Save**.
![](https://main.qcloudimg.com/raw/2aeabc7d61bc069d1fdf5128815f77d6.png)

## Notes
- For requests that have successfully triggered Base64 encoding, API Gateway will Base64-encode the request body and set the value of the `isBase64Encoded` field to `True` before passing the requests to SCF. You can determine whether the requests are Base64-encoded according to the value of this field. (For more information, please see [Structures Passed by API Gateway to Backend](https://intl.cloud.tencent.com/document/product/628/38896)).
- Due to the trigger limits, the requested content that API Gateway can pass to SCF at a time cannot be larger than 6 MB. In other words, the Base64 encoding feature only supports passing files that are smaller than 6 MB after being Base64-encoded. To pass files larger than 6 MB, please upload with COS by referring to [Uploading Files](https://intl.cloud.tencent.com/document/product/628/38852).
- The **Trigger by Header** mode adopts fuzzy match for the trigger rules. Only the `Content-Type` and `Accept` request headers are supported. API Gateway applies a logical OR across multiple trigger rules. That is, Base64 encoding will be triggered as long as one of the trigger rules is met.
