By default, sub-users have no permission to use database audit in TDSQL-C for MySQL. Therefore, you need to create policies if you want them to use it.

[Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583) is a web service provided by Tencent Cloud that helps you securely manage access to the resources under your Tencent Cloud account. CAM allows you to create, manage, or terminate users or user groups and control who is allowed to use your Tencent Cloud resources through identity and policy management.

When using CAM, you can associate a policy with a user or user group to allow or forbid them to use specified resources to complete specified tasks. For more information on CAM policies, see [Element Reference](https://intl.cloud.tencent.com/document/product/598/10603).

## Directions
1. Log in to the [CAM console](https://console.cloud.tencent.com/cam) with the root account, locate the target sub-user in the user list, and click **Authorize**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/ihnQ419_51.png)
2. In the pop-up window, select the **QcloudCynosDBFullAccess** or **QcloudCynosDBReadOnlyAccess** preset policy and click **OK** to complete the authorization.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/CZQx309_52.png)
