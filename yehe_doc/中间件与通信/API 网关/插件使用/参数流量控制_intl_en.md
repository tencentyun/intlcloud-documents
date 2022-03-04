
## Overview

The parameter traffic throttling plugin can control the traffic according to the configured request parameters and conditions. It can be configured as follows:

- You can set traffic throttling by second, minute, hour, and day.
- You can set conditions for client request parameters and built-in system parameters of API Gateway to use different traffic throttling dimensions.
- You can use a single parameter or combine multiple parameters to configure traffic throttling.

>!As the parameter traffic throttling plugin and [basic traffic throttling plugin](https://intl.cloud.tencent.com/document/product/628/40307) are for the same purpose, an API can be bound to only one of them.

## Directions

### Step 1. Create a plugin

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway)
2. On the left sidebar, click **Plugin** to enter the plugin list page.
3. Click **Create** in the top-left corner of the page and select **Parameter Traffic Throttling** as the plugin type to create a parameter traffic throttling plugin.

| Parameter | Required | Description |
| ------------ | ------------------ | ------------------------------------------------------------ |
| Enable default policy | Yes               | Whether to enable the default policy. The default policy implements traffic throttling at the API level and is independent from all other traffic throttling policies. For each request, the default policy will be checked first before other policies. |
| Default threshold   | Yes if the default policy is enabled | Upper limit of the number of times an API can be accessed within a certain period of time, which must be a positive integer. |
| Default traffic throttling duration | Yes if the default policy is enabled | It supports four units: second, minute, hour, and day, and is used together with the default threshold.       |
| Traffic throttling policy     | Yes               | Parameter traffic throttling policy. You can create up to 10 policies in the same parameter traffic throttling plugin. The configuration items in a policy are as detailed below. |

You can create up to 10 traffic throttling policies in the same parameter traffic throttling plugin. Each policy has the following configuration items:

| Parameter | Required | Description |
| ------------ | -------- | ------------------------------------------------------------ |
| Policy name     | Yes     | Current policy name, which can contain up to 50 characters and must be unique in the same plugin. |
| Weight         | Yes     | You can enter a positive integer between 0 and 100, which must be unique in the same plugin. The greater the weight, the higher the priority. |
| Trigger condition     | No     | If you set a condition, only when it is met can this traffic throttling policy be executed.<br>Enter a conditional expression. For more information on the rules of writing conditional expressions, see **[Notes](#notice)**. |
| Traffic throttling parameter location | Yes     | You can enter only one traffic throttling parameter and need to select the location and set the parameter name. For example, `Header.ClientIP` indicates to perform traffic throttling for each value of the `ClientIP` parameter in `Header`.<br>The following locations are supported: Header, Query, and Path. The `Path` parameter represents a complete API path, for which you don't need to enter the parameter name. |
| Traffic throttling parameter name | Yes     | You can enter only one traffic throttling parameter and need to select the location and set the parameter name. For example, `Header.ClientIP` indicates to perform traffic throttling for each value of the `ClientIP` parameter in `Header`.<br>The traffic throttling parameter name needs to be used together with the parameter location. The `Path` parameter represents a complete API path, for which you don't need to enter the parameter name. |
| Threshold       | Yes     | Traffic throttling threshold for the traffic throttling parameter in this policy, which must be a positive integer and used together with the traffic throttling duration. |
| Traffic throttling duration     | Yes     |   It supports four units: second, minute, hour, and day, and is used together with the threshold.           |

### Step 2. Bind an API and make the plugin effective

1. Select the just created plugin in the plugin list and click **Bind API** in the **Operation** column.
2. In the **Bind API** pop-up window, select the service, environment, and the API to which the plugin needs to be bound.
   ![](https://qcloudimg.tencent-cloud.cn/raw/e9e674392e0070e320d38c1c00fc1ba2.png)
3. Click **OK** to bind the plugin to the API. At this time, the configuration of the plugin has taken effect for the API.

## How It Works

![](https://qcloudimg.tencent-cloud.cn/raw/75df4215d303d402915d6ad9abfc7946.png)

- The default policy implements traffic throttling at the API level and is independent from all other traffic throttling policies. For each request, the default policy will be checked first before other policies.
- If you configure multiple traffic throttling policies in a plugin, API Gateway will sort them in a descending order by the policy weight and check whether the request meets the condition of each policy one by one. If any policy is not met, traffic throttling will be triggered, and the request will be rejected.
- When a traffic throttling policy is being checked, if a conditional expression is configured, the condition will be checked first before the parameter; otherwise, the parameter will be checked directly.
- If you set the threshold to 10 per minute for the `header.userid` parameter in a traffic throttling policy, the threshold will take effect for each different value of this parameter in the request.

## PluginData

```json
{
    "default_window":60, // Traffic throttling time window in seconds. If the value is 0, traffic throttling will be disabled by default
    "default_rate_limit":5, // Traffic throttling threshold, which must be a positive integer
    "strategies":[ // List of parameter traffic throttling policies. You can add 1–10 policies
        {
            "name":"a", // Policy name.
            "strategy_weight":0, // Policy execution priority, which must be unique. The higher the value, the higher the execution priority
            "parameters":[ // List of traffic throttling parameters. Currently, you can add only one parameter
                {
                    "type":"query", // Type of traffic throttling parameter. Valid values: [query,header,path]
                    "name":"a" // Name of traffic throttling parameter. If the parameter type is `path`, the parameter will be the complete request path, and you don't need to pass in `name`
                }
            ],
            "rate_limit":1, // Traffic throttling threshold, which must be a positive integer
            "window":1, // Traffic throttling time window in seconds
            "condition":"" // Policy trigger condition. If the value is an empty string, the policy will be executed unconditionally
        }
    ]
}
```

## Notes[](id:notice)

Conditional expressions of the parameter traffic throttling plugin are the same as those of the conditional routing plugin. For more information on how to write expressions, see [Conditional Expression Writing Guide](https://intl.cloud.tencent.com/document/product/628/44308).
