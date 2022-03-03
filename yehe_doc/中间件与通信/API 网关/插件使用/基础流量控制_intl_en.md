## Overview

Basic traffic throttling plugin is a powerful traffic throttling component provided by API Gateway. It can throttle traffic in three dimensions of API, application, and client IP by second, minute, hour, or day. You can create a basic traffic throttling plugin and bind it to your API to take effect and protect your backend services.

## Directions

### Step 1. Create a plugin

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway)
2. On the left sidebar, click **Plugin** to enter the plugin list page.
3. Click **Create** in the top-left corner of the page and select **Basic Traffic Throttling** as the plugin type to create a basic traffic throttling plugin.

| Parameter | Required | Description |
|---------|---------|---------|
| Duration | Yes | The duration of traffic throttling, which supports four dimensions: second, minute, hour, and day. It is used in conjunction with "traffic throttling threshold" to indicate the upper limit of the number of requests per unit time. |
| API Threshold | Yes | The upper limit of the number of times an API can be accessed within a certain period of time. |
| Application Threshold | No | The upper limit of the number of times an application can be accessed within a certain period of time, which takes effect for all applications bound to this API. |
| Client IP Threshold | No | The upper limit of the number of times a client IP can be accessed within a certain period of time, which takes effect for all client IPs bound to this API. |
| Special Application | No | Up to 30 items can be entered. For such applications, the basic API traffic throttling of the traffic throttling policy still takes effect, but you need to set an additional traffic throttling threshold for them. Meanwhile, the basic application traffic throttling and user traffic throttling of the traffic throttling policy will stop working for such applications. |
| <nobr>Special Client IP</nobr> | No | Up to 30 items can be entered. For such IPs, the basic API traffic throttling of the traffic throttling policy still takes effect, but you need to set an additional traffic throttling threshold for them. Meanwhile, the basic application traffic throttling and client IP traffic throttling of the traffic throttling policy will stop working for such IPs. |

 ![](https://main.qcloudimg.com/raw/d244afb76f2a5bfc3bea4cb9acb31cc0.png)

### Step 2. Bind an API and make the plugin effective

1. Select the just created plugin in the list and click **Bind API** in the **Operation** column.
2. In the **Bind API** pop-up window, select the service, environment, and the API to which the plugin needs to be bound.
   ![](https://main.qcloudimg.com/raw/492616bda938ea67dc415e99e0dce50e.png)
3. Click **OK** to bind the plugin to the API. At this time, the configuration of the plugin has taken effect for the API.

## PluginData

```json
{
    "expire_type":"hour", // Traffic throttling time window unit. Valid values: day, hour, minute, second
    "expire":1, // Traffic throttling time window
    "api_rate_limit":500, // API traffic throttling threshold, which must be a positive integer
    "app_rate_limit":1, // Application traffic throttling threshold, which must be a positive integer
    "ip_rate_limit":2, // Client IP traffic throttling threshold, which must be a positive integer
    "spec_app_rate_limits":[ // List of special applications for traffic throttling
        {
            "app_id":"app-3q9l4909", // Application ID
            "rate_limit":10 // Traffic throttling threshold, which must be a positive integer
        }
    ],
    "spec_ip_rate_limits":[ // List of special client IPs for traffic throttling
        {
            "ip_key":"172.16.0.1", // Client IP
            "rate_limit":10 // Traffic throttling threshold, which must be a positive integer
        }
    ]
}
```


## Notes

The basic traffic throttling plugin will be affected by service traffic throttling and API traffic throttling. If multiple traffic throttling rules take effect at the same time, the lowest threshold will prevail.
For example, if the traffic throttling threshold of an API is set to 500 QPS in the basic traffic throttling plugin, the traffic throttling threshold of the service to which the API belongs is 100 QPS, and the traffic throttling threshold of the API itself is 50 QPS, then the actually effective threshold is 50 QPS.
