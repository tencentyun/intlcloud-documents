## Overview
The API debugging page allows you to verify the correctness of an API immediately after completing its configuration by initiating a simulated API call and viewing the specific request response. If the API fails to work as expected, you can modify the configuration according to the response to make it meet your design expectations.

## Prerequisites
You have [created a general API](https://intl.cloud.tencent.com/document/product/628/11795).

## Directions
1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway/index?rid=1) and click **Service** in the left sidebar to enter the service list page.
2. Click a service name to enter the service details page, and click **Manage API** at the top to manage the API.
3. Select the API to be debugged in the general API list. Click **Debug** in the operation column to go to the debugging page.
	On this page, you can see the frontend configuration information of the API to be debugged, including the path, request method and Content-Type. For the request parameters (not displayed if you do not configure them):
	- If you configure a parameter to have a default value, the default value will be populated in the input box by default;
	- If you configure a parameter to be required, a check will be performed to verify whether any value has been entered for it before testing;
	- If your request method is POST, PUT, or DELETE, you will be required to enter a value for the `Body` parameter.
>? If a parameter is optional and the user does not enter any value for the parameter, API Gateway will send a `null` to the backend by default.
4. Click **Send request**, you will see the response body and response headers.
Response: the response code and data actually returned to the frontend after the API call.
![](https://main.qcloudimg.com/raw/3b9c79de835f326ddb90064b8361d42e.png)

