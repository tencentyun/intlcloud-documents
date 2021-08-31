## Overview

[Enterprise Identity and Access Management (EIAM)](https://console.cloud.tencent.com/eiam) is Tencent Cloud's centralized digital identity control service. It allows you to centrally manage user accounts, assign access permissions, and configure identity verification rules to avoid security accidents caused by improper assignment of employee accounts and authorization.
EIAM and Tencent Cloud API Gateway are deeply integrated through the OAuth2.0 protocol. You can easily combine them to implement RESTful web API identity verification: use EIAM to maintain a user pool and authorize users in the pool to access the APIs managed by the API Gateway.

This document describes how to create a user pool in EIAM, integrate the API Gateway and the user pool, and call the APIs integrated with the user pool.

## Prerequisites

You have activated the [EIAM service](https://console.cloud.tencent.com/eiam).

## Solution Strengths

Compared with the traditional OAuth2.0 mode, API Gateway EIAM verification has the following advantages:

- Standard OAuth2.0 protocol
- EIAM for user pool maintenance, eliminating the need to build a verification server
- Authentication based on verification capabilities for API security protection
- Various RBAC models built in EIAM, eliminating the need to build an authentication server and authorization models
- Quick and easy creation of authorization and service APIs
- Built-in cache mechanism for faster access

<img src="https://main.qcloudimg.com/raw/a7c9c61a515f0159e992564486ca0f4e.png" width="450px">

## Directions

### Step 1: create an API whose authentication mode is EIAM verification

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway/service) and click **Service** in the left sidebar.
2. In the service list, click the name of the target service.
3. On the service information page, click the **Manage API** tab and click **Create** at the top of the service list to start API creation.
4. On the API creation page, select **EIAM Verification** as the authentication type. API Gateway provides two access modes:
   - Create an EIAM application: create an EIAM application and bind it with the current API Gateway API.
   - Select an existing EIAM application: select an existing EIAM application and bind it with the current API Gateway API.

>?You can click the following tabs to view the configuration items of the two access modes.
<dx-tabs>
::: Creating an EIAM Application
| Parameter | Required | Description |
| -------------- | -------- | ------------------------------------------------------------ |
| Verification and Authentication    | Yes       | Two options are available: **Only verify identity** and **Verify identity and authenticate**.<li>Verification: verify user identities based on usernames and passwords</li><li>Authentication: determine whether users have the permission to access gateway resources based on usernames</li> |
| EIAM Application Type  | Yes       | Two options are available: **Non-Web client** and **Web client**.<li>Non-Web client: suitable for API calling initiated by non-web clients, such as servers, C/S architecture system clients, app clients, and mini program clients. This application type supports POST requests. Users need to request a token from the authorization API and use the token to request the service API. </li><li>Web client: suitable for API calling initiated by web clients, such as browsers and client application web viewers. These clients can receive return information in web redirection mode.</li> |
| Token Validity | Yes       | Validity period of a single issued token. When the validity period of the current token expires, you need to get a new token.  |
:::
::: Selecting an Existing EIAM Application
| Parameter | Required | Description |
| -------------- | -------- | ------------------------------------------------------------ |
| Select EIAM Application | Yes       | Select an existing EIAM application from the list to create a binding relationship.         |
| Verification and Authentication    | Yes       | Two options are available: **Only verify identity** and **Verify identity and authenticate**.<li>Verification: verify user identities based on usernames and passwords</li><li>Authentication: determine whether users have the permission to access gateway resources based on usernames</li> |
| EIAM Application Type  | Yes       | Two options are available: **Non-Web client** and **Web client**.<li>Non-Web client: suitable for API calling initiated by non-web clients, such as servers, C/S architecture system clients, app clients, and mini program clients. These clients allow users to initiate requests via POST, and the users need to request a token from the authorization API and then use the token to request the service API. </li><li>Web client: suitable for API calling initiated by web clients, such as browsers and client application web viewers. These clients can receive return information in web redirection mode.</li> |
| Token Validity | Yes       | Validity period of a single issued token. When the validity period of the current token expires, you need to get a new token. If the access mode is **selecting an existing EIAM application**, this configuration item automatically inherits the configuration of the selected EIAM application and does not support manual configuration. |
:::
</dx-tabs>

**Non-web client architecture**
![](https://main.qcloudimg.com/raw/adce9c932cadfb70af7ea3ffdd7dc141.png)

**Web client architecture**
![](https://main.qcloudimg.com/raw/51d0a6ae8f2f00eeae87a9e8d65a733d.png)

5. Complete the subsequent creation process in turn and click **Complete**. The API whose authentication mode is EIAM verification is created.
   ![](https://main.qcloudimg.com/raw/aba88527aa46af44f4202ef75ec06966.png)

### Step 2: create a user pool and a user in EIAM[](id:step2)

1. Log in to the [EIAM console](https://console.cloud.tencent.com/eiam). In the left sidebar, choose **User Management** -> **Organizations**.
2. Select an appropriate organization and click **Create User**.
3. Set parameters as required.
	 ![](https://main.qcloudimg.com/raw/2ad13ffffeacc1aa8b18ffce01fbdd82.png)

### Step 3: authorize the user in EIAM

1. Log in to the [EIAM console](https://console.cloud.tencent.com/eiam). In the left sidebar, choose **Authorization Management** -> **Application Authorization**.
2. Select the **User Authorization** tab and click **Create Authorization Role**.
3. Select the EIAM application created or bound in step 1, select the user created in step 2, and authorize the user.
	 ![](https://main.qcloudimg.com/raw/a8ef4a3a2f57299a7f40631b76ea89bc.png)

### Step 4: use the created user to call the API Gateway API

Use the account and password of the user created in [step 2](#step2) to call the API Gateway API.
>?You can click the following tabs to view the API calling methods for non-web and web clients.

<dx-tabs>
::: Non-Web Client
1. Request the authorization API to get the token.
   The query request parameter **username** is the username of the user created in [step 2](#step2).
   The query request parameter **password** is the password of the user created in [step 2](#step2).
![](https://main.qcloudimg.com/raw/aa53522a3084a8e7eb8a5db434cb00bc.png)

2. Use the token obtained to request the service API.
   The header parameter **Authorization** must be in the `Bear id_token="<Content of the token obtained>"` format.
	```
	curl http://service-xxxxxxxx-1234567890.gz.apigw.tencentcs.com/work -H'Authorization:Bearer id_token="eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE1OTIyNzk3MTAsImZvbyI6ImJhciIsImlhdCI6MTU5MjI3OTQxMCwianRpIjoiZlBGYlFZRkR4REx3d0lXTFl0aHBBQSIsIm5iZiI6MTU5MjI3OTQxMCwid3VwIjo5MH0.0JQquNRVCQ8n9hPV-mJi6Mku_7G3T1jFp68Sk2AYBijpzzBMQ1KOcREyo9G6QOpvdctynGOAPkL3cwqeTzkFhWgGj633pu_MdLjlectEBMGyVQIv6pL8OBMCHMQzTUTpHWJ_NoUkLpRLKGqZFFcXW8q7v4KeCbf8xHUa9OCH5VF2JxYOnFWDVgucSqao06r0Jaq64LDwKIhLw77ujheKpcBjRrf1kqoIpqk2qhb8CzxM36g_DawMadzKmX49dT-k7auNnI2xUtu5CZdXZ3lSmLeicXfGjc66rrH_acqUqipZRKeeQ5F3Ma467jPQaTeOKiCMHwS2_yp-sXNU2GzxOA"'
	```
	- For unauthorized users:
	If the status code 403 "Access not authorized" is returned during authentication verification, the user is not authenticated.
	![](https://main.qcloudimg.com/raw/dbf69b0bbc346900c299bbf506abe4fc.png)

	- For authorized users:
	If the API backend calling result is returned during authentication verification, the user can call the API.
	![](https://main.qcloudimg.com/raw/f7df9b839b44744af1909c120b435337.png)
:::
::: Web Client
1. Enter the API access address in the browser. The login page is displayed.
	<img src="https://main.qcloudimg.com/raw/eef8349bdc4aa266c59545be7bc0f95f.png" width="450px">
2. On the login page, enter the username and password of the user created in step 2 to call the API.
:::
</dx-tabs>



## Notes

- EIAM verification applies only to the API Gateway service for which public network access is enabled. If the access mode of your API Gateway service is **Private VPC**, EIAM verification cannot be used.
- If the authorization relationship changes in EIAM, you need to request the authorization API to get the token again.
