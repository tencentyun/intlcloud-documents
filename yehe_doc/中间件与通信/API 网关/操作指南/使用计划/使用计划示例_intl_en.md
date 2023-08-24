## Scenarios
To call a service after it is published, you need to create a key-value pair secret and a usage plan and bind them to the service environment.
This document describes how to configure a user-specific usage plan and make it available to the users.

## Prerequisite
1. [Create a service](https://intl.cloud.tencent.com/document/product/628/11787)‍ and [create and debug an API](https://intl.cloud.tencent.com/document/product/628/11795).
2. [Publish the service](https://intl.cloud.tencent.com/document/product/628/11809) to an environment, such as the release environment.

## Directions
### Creating a key-value pair secret
1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway/index), and click **Application** on the left sidebar to enter the application management page.
2. On the application management page, click **Secret** on the top to open the secret management page.
3. Click **Create**, select the secret type and complete the following information.
<dx-tabs>
::: Auto-generated
Enter the secret name.
Secret name: Up to 50 characters ([a-z], [A-Z], [0-9] and [_])
:::
::: Custom secret
Enter the secret name, SecretId and SecretKey.
- Secret name: Up to 50 characters ([a-z], [A-Z], [0-9] and [_-])
- ‍SecretId: 5-50 characters ([a-z], [A-Z], [0-9] and [_-])
- ‍SecretKey: 10-50 characters ([a-z], [A-Z], [0-9] and [_-])
:::
</dx-tabs>
4. Click **Submit** to generate a secret or save the custom key-value pair secret (SecretId and SecretKey).
![](https://main.qcloudimg.com/raw/774299c4fa7afdc0db1247a7d26f02f4.png)

### Creating a usage plan
1. On the left sidebar, click [Usage Plan](https://console.cloud.tencent.com/apigateway/plan) to enter the usage plan list page.
2. Click **Create** in the top-left corner and enter the configuration information as prompted.
3. Click **Submit** to complete the creation.

### Binding usage plan to secret
1. On the [Usage Plan](https://console.cloud.tencent.com/apigateway/plan) page, click the ID of the target usage plan to enter the usage plan details page.
2. On the usage plan details page, click **Bind Key**.
3. Check the `SecretId` to be bound and click **Submit** to complete the binding.
![](https://main.qcloudimg.com/raw/774299c4fa7afdc0db1247a7d26f02f4.png)

### Binding a usage plan with a service environment
1. Select a created service on the [Service](https://console.cloud.tencent.com/apigateway/service) list page, switch to the **Usage Plan** tab, and click **Bind**.
![](https://main.qcloudimg.com/raw/a2c9314e9fb5fa9d72d8a5a7a8f2bebe.png)
2. In the usage plan binding window, select an effective environment and usage plan to be bound.
Effective environments: publish, pre-publish, and testing
3. Click **Submit** to complete the binding.
![](https://main.qcloudimg.com/raw/b831f08fab2563c4d07d175ffcb093c5.png)
>!Usage plans bound with the same key-value pair cannot be bound to the same environment.

Now you can share the SecretId and SecretKey to the end user. The end user can use the provided `SecretId` and `SecretKey` through the second-level domain name of the service (or a bound private domain name) to access the APIs published in the service.
