## Overview

You can configure the cache plugin to enable API Gateway to store backend responses. When receiving requests with the same parameters, API Gateway can directly return the cached responses with no need to forward the requests to the backend service. This reduces the load on the backend, shortens the latency, and makes your business smoother.

## Directions

### Step 1. Create a plugin

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway)
2. On the left sidebar, click **Plugin** > **System Plugin** to enter the system plugin list page.
3. Click **Create** in the top-left corner of the page and select **Cache** as the plugin type to create a cache plugin. The plugin configuration items are as detailed below:
<table>
<tr>
<th>Parameter</th>
<th>Required	</th>
<th>Description</th>
</tr>
<tr>
<td>Cache parameter</td>
<td>Yes	</td>
<td>The cached content can be distinguished by the parameter or the combination of multiple parameters. Supported parameter locations include Header, Path, and Query.</td>
</tr>
<tr>
<td>Request method</td>
<td>Yes	</td>
<td>You can select multiple methods. Valid values: GET, POST, PUT, DELETE, HEAD.</td>
</tr> 
<tr>
<td>Cache status code</td>
<td>Yes	</td>
<td>Only responses with a status code set in the cache plugin will be cached. You can separate multiple status codes with commas.</td>
</tr>
<tr>
<td>Cache-Control</td>
<td>Yes	</td>
<td>It specifies whether to use the `Cache-Control` request header to affect the cache policy. It is disabled by default.</td>
</tr>
<tr>
<td>Cache duration</td>
<td>Yes	</td>
<td>It is the cache validity period, which is a positive integer between 0 and 3600.</td>
</tr>
</table>


### Step 2. Bind an API and make the plugin effective

1. Select the just created plugin in the list and click **Bind API** in the **Operation** column.
2. In the **Bind API** pop-up window, select the service, environment, and the API to which the plugin needs to be bound.
   ![](https://qcloudimg.tencent-cloud.cn/raw/a91c4bdedc7bef63610b0124747fda8e.png)
3. Click **OK** to bind the plugin to the API. At this time, the configuration of the plugin has taken effect for the API.

## PluginData

```json
{
	"cache_key_params": [{ // Parameter for distinguishing between cached responses. The source of `parameter` is the parameter defined in the API, and the valid values of `position` are `header`, `query`, and `path`
		"parameter": "param1",
		"position": "header"
	}, {
		"parameter": "param2",
		"position": "query"
	}, {
		"parameter": "param3",
		"position": "path"
	}],
	"cacheable_methods": ["GET", "POST"], // HTTP methods of requests whose responses can be cached. Valid values: GET, POST, PUT, DELETE, HEAD
	"cacheable_response_codes": [200, 301, 404], // HTTP return codes of responses that can be cached
	"cache_control": false, // Whether to enable the `Cache-Control` syntax in the HTTP standard. After it is enabled, `Cache-Control` of requests and responses will take effect, and the custom TTL will be ignored
	"ttl": 300 // Custom cache validity period, which will take effect if `cache_control` is `false`. Value range: [1,3600]
}
```


## Notes

- The values are case-insensitive for parameter verification and cache hitting conducted by API Gateway.
- For a shared instance, the maximum cache capacity in each region for each user is 5 MB. The maximum of total cache capacity of each shared instance is 1 GB.
- After `Cache-Control` is enabled, the gateway will process the cache according to the convention in the `Cache-Control` request/response header. In this case, if the gateway cannot get the `Cache-Control` header, the response will be cached by default, and the `cache duration` field configured in the plugin will be used as the cache validity period.
