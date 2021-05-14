## Plugin Overview

Plugins are advanced feature configurations provided by API Gateway. You can create configuration items such as IP access control through plugins and then bind the plugins to APIs for them to take effect.

Plugins have the following advantages over traditional configuration items:
- Feature configuration is decoupled from API configuration. One plugin can be bound to multiple APIs under different services.
- Hot update is supported for configurations. After a plugin is bound to an API, it can take effect without publishing the service.

## Directions

### Step 1. Create a plugin

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway).
2. On the left sidebar, click **Plugin** to enter the plugin list page.
3. Click **Create** in the top-left corner to create a plugin.


### Step 2. Bind an API and make the plugin effective

1. Select the just created plugin in the list and click **Bind API** in the **Operation** column.
2. In the **Bind API** pop-up window, select the service, environment, and the API that needs to be bound to the plugin.

3. Click **OK** to bind the plugin to the API. At this time, the configuration of the plugin has taken effect for the API.

### Step 3. View the plugins bound to an API

1. On the left sidebar, click **Service** to enter the service list page.
2. In the service list, click the name of the target service to view it.
3. In the API list, click the name of the target API to enter the API details page.
4. On the API details page, click the **Bound Plugin** tab to view the information of plugins bound to the target API.


## Supported Plugin Type

- IP access control

>? API Gateway currently only supports the IP access control plugin and will offer more plugins such as traffic throttling, circuit breaker, and parameter conversion in the future.

## Plugin Rules

- An API can be bound to only one plugin of the same type.
- Plugins are region-specific and can be bound to APIs only in the same region. Cross-region binding is not supported.
- APIs can be bound to plugins only after they are published in the corresponding environment. Unpublished APIs cannot be bound.
- The deactivation of APIs does not affect their binding relationships with plugins, and the plugins will still take effect after the APIs are republished in the environment.
- Plugins support hot updates, and all binding and unbinding operations can take effect without republishing the service.
- After APIs are deleted, their binding relationships with plugins will also be deleted.
