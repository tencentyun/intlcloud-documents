## Plugin Overview

Plugins are advanced feature configurations provided by API Gateway. You can create configuration items such as IP access control through plugins and then bind the plugins to APIs for them to take effect.

Plugins have the following advantages over traditional configuration items:
- Feature configuration is decoupled from API configuration. One plugin can be bound to multiple APIs under different services.
- Hot update is supported for configurations. After a plugin is bound to an API, it can take effect without releasing the service.

## Directions

### Step 1. Create a plugin

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway).
2. Click **Plugin** in the left sidebar to open the plugin list page.
3. Click **Create** in the upper-left corner of the page to create a plugin.
	 ![](https://qcloudimg.tencent-cloud.cn/raw/a064331f17a771fe762e0d129371da25.png)

### Step 2. Bind an API and make the plugin effective

1. Select the just created plugin in the list and click **Bind API** in the **Operation** column.
2. In the **Bind API** pop-up window, select the service, environment, and the API to which the plugin needs to be bound.
	 ![](https://qcloudimg.tencent-cloud.cn/raw/2e08aca19af7543fb10971219aa43665.png)
3. Click **OK** to bind the plugin to the API. At this time, the configuration of the plugin has taken effect for the API.

### Step 3. View the plugins bound to an API

1. Click **Service** in the left sidebar.
2. In the service list, click the name of the target service.
3. In the API list, click the name of the target API to enter the API details page.
4. On the API details page, select the tab of **Plugin management** to view the information of the plugins bound to the target API.
	 ![](https://qcloudimg.tencent-cloud.cn/raw/4d5737db571db217dda896ad82a4d7f6.png)

## Supported Plugin Type

- IP access control

>? API Gateway currently only supports the IP access control plugin and will offer more plugins such as traffic throttling, circuit breaker, and parameter conversion in the future.

## Plugin Rules

- An API only allows one plugin of the same type to be bound to it.
- Plugins are region-specific and can be bound to APIs only in the same region. Cross-region binding is not supported.
- APIs can be bound to plugins only after they are released in the corresponding environment. Unreleased APIs cannot be bound.
- The deactivation of APIs does not affect their binding relationships with plugins, and the plugins will still take effect after the APIs are re-released in the environment.
- Plugins support hot updates, and all binding and unbinding operations can take effect without re-releasing the service.
- After APIs are deleted, their binding relationships with plugins will also be deleted.
