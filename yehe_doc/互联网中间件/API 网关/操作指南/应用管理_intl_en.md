## Overview

An application is an identity that calls an API. It needs to be authorized by the API before it can call the API. Each application has a key pair of `ApiAppKey` and `ApiAppSecret`. `ApiAppKey` needs to be passed in as a parameter in the header of a request, and `ApiAppSecret` needs to be used to calculate the request signature. For more information on the signature calculation method, please see [Application Authentication Method](https://intl.cloud.tencent.com/document/product/628/40304).

## Prerequisites

The API authentication method is "application authentication".

## Directions
### Application creation

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway) and click **Application** on the left sidebar to enter the application management page.
2. On the application management page, click **Create Application** in the top-left corner, fill in the form, and submit it to create an application.

### API authorization

Authorization refers to granting an application the permission to call an API. The application needs to be authorized by the API first before it can call the API. There are two ways of authorization:

| Authorization Method | Applicable Scenario | Description |
|---------|---------|---------|
| Direct authorization | Application created by yourself | - |
| <nobr>Partner authorization</nobr> | Use the APIs provided by partners (other accounts) | Create your own application and provide its ID to the API provider. The API provider can search for the application ID to perform authorization |


You can click the following tabs to view the directions of the corresponding authorization method.
<dx-tabs>
::: Direct authorization
1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway) and click **Service** on the left sidebar.
2. In the service list, click the name of the target service to view it.
3. In the service information, click the **Manage API** tab and click **Authorization** behind the API list to start authorization.
4. Select the environment and application to be authorized. On the left are your applications. Click **Search** directly, and the applications under the current account will be automatically loaded.
:::
::: Partner authorization
1. Log in to the API Gateway console and click **Service** on the left sidebar.
2. In the service list, click the name of the target service to view it.
3. In the service information, click the **Manage API** tab and click **Authorization** behind the API list to start authorization.
4. If you want to authorize applications under other accounts, you need to select the application ID, enter it in the text box, and then click **Search** to query.
:::
</dx-tabs>




## Notes

- The key pair of `AppKey` and `AppSecret` has all the permissions of the application and should be kept private. If it is leaked, you can reset it in the API Gateway console.
- You can create multiple applications and authorize them to different APIs according to your business needs.
- You can create, modify, and delete applications, view application details, manage keys, and view authorized APIs in the API Gateway console.
