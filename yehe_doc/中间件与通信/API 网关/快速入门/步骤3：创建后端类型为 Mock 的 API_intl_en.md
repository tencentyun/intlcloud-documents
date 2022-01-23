## Overview

This document describes how to create an API connecting to Mock on the backend under a created service in the API Gateway console.

>!If the API connects to Mock in the backend, only fixed data can be returned. Therefore, we recommend you use Mock for testings but not in actual business scenarios.

## Prerequisites

You have [created a service](https://intl.cloud.tencent.com/document/product/628/44317).

## Directions

1. In the service list, click a service name to enter the API list page.
2. On the **General API** tab, select **Create** and enter the API's frontend configuration information.
   - API Name: name of an API. **exampleapi** is entered here as an example.
   - Frontend Type: HTTP and WebSocket are supported. **HTTP** is selected here as an example.
   - Path: access path of the API. **/** is entered here as an example.
   - Request Method: request method of the API. **GET** is selected here as an example.
   - Authentication Type: authentication type of the API. **No authentication** is selected here as an example.
   - CORS Support: whether the API supports cross-origin resource sharing. **Yes** is selected here as an example.
   - Remarks: remarks of the API. **Test** is entered here as an example.
   - Parameter Configuration: frontend parameters of the API. Nothing is entered here.
     ![](https://qcloudimg.tencent-cloud.cn/raw/3297493162b368eb3d63dff03ee73939.png)
3. Click **Next** and enter the backend configuration information of the API.
   - Backend Type: type of the backend service of the API. **Mock** is selected here as an example.
   - Returned Data: data to be returned by Mock. **hello world, hello apigateway** is entered here as an example.
     ![](https://qcloudimg.tencent-cloud.cn/raw/617dfb02327f80fa19eef749024910cc.png)
4. Click **Complete**.

