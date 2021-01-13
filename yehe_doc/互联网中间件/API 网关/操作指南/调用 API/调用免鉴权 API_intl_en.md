## Overview

This document describes how to call an API that requires no authentication.

## Prerequisites

### Creating a no-auth API

1. In the [API Gateway console](https://console.cloud.tencent.com/apigateway/index?rid=1), create an API with **Authentication Type** set to **No authentication** (see [API Creation Overview](https://intl.cloud.tencent.com/document/product/628/11795)).
2. Publish the service to which the API belongs to the release environment (see [Service Release and Deactivation](https://intl.cloud.tencent.com/document/product/628/11809)).

#### Confirming information

Before calling the API, you must obtain information including the API’s request path, request method, and request parameters, which can be found in the **Default Access Address** section of the API’s details page.
![](https://main.qcloudimg.com/raw/e13578452b2b016734691c1c66fd970e.png)

#### Preparing tools

You can initiate requests from sources including browsers, browser plugins, Postman, and clients. Postman is recommended for simple validation.

## Directions

1. Below is the basic information of an API.
   Public domain name: http://service-p52nqnd0-1253970226.gz.apigw.tencentcs.com
   Published environment: release
   Access path: /api
   Request method: GET
   The default access address of an API is in the format of “public domain name or VPC domain name/published environment/access path”, so the default access address of the above API is: http://service-p52nqnd0-1253970226.gz.apigw.tencentcs.com/release/api.
2. Enter the access address in Postman, select `GET` as the request method, set the request parameters, and click **Send** to call the API.
   ![](https://main.qcloudimg.com/raw/ff9f2537a989ebaa646945f074a69a95.png)
