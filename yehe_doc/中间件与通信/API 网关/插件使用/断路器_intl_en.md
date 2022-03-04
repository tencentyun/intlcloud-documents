## Overview

You can use the circuit breaker plugin for circuit breaking and downgrade when the backend is exceptional in order to protect the backend and recover the requests after it returns to normal.

>! The circuit breaker supports only APIs in [dedicated instances](https://intl.cloud.tencent.com/document/product/628/40305) but not shared instances.

## How It Works

![](https://qcloudimg.tencent-cloud.cn/raw/8bc578e1686993758428bcbc691847b7.png)
You can set configuration items such as **judgment time window**, **error condition**, **number of errors**, **circuit breaking duration**, and **downgraded backend configuration** in the circuit breaker plugin.
A circuit breaker cycle can be divided into three phases:

- If the number of times the backend of an API bound to the circuit breaker plugin triggers the **error condition** within the **judgment time window** exceeds the **number of errors**, the system will trigger and enable the circuit breaker.
- After the circuit breaker is enabled, it will work for the time specified by the **circuit breaking duration** in seconds, during which all requests will be forwarded to the backend specified by the **downgraded backend configuration**.
- After the **circuit breaking duration** ends, the circuit breaker will be disabled, and requests will return to normal.

## Directions

### Step 1. Create a plugin

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway)
2. On the left sidebar, click **Plugin** > **System Plugin** to enter the system plugin list page.
3. Click **Create** in the top-left corner of the page and select **Circuit Breaker** as the plugin type to create a circuit breaker plugin. The plugin configuration items are as detailed below:
<table>
<tr>
<th>Parameter</th>
<th>Required	</th>
<th>Description</th>
</tr>
<tr>
<td>Error condition	</td>
<td>Yes	</td>
<td>It is the condition for judging whether a request is considered an error. For more information, see the <a href = "#table">table below</a>.</td>
</tr>
<tr>
<td>Number of errors</td>
<td>Yes	</td>
<td>It is the threshold of number of errors. If it is exceeded within the time window, the circuit breaker will be enabled.</td>
</tr>
<tr>
<td>Judgment time window</td>
<td>Yes	</td>
<td>It is the judgment time window ranging from 10 to 90 seconds.</td>
</tr>
<tr>
<td>Circuit breaking duration</td>
<td>Yes	</td>
<td>It is the circuit breaking duration ranging from 15 to 300 seconds.</td>
</tr>
<tr>
<td>Downgraded backend type</td>
<td>Yes	</td>
<td>Valid values: Disable, Public network URL/IP, VPC resources, SCF, Mock, and TSF.</br> If you select **Disable**, after the circuit breaker is enabled, the backend will not be downgraded, and the error will be reported to the client; if you select another option, the selected backend will be downgraded to after the circuit breaker is enabled.</td>
</tr>
<tr>
<td>Downgraded backend configuration</td>
<td>Yes if the downgraded backend type is not `Disable`</td>
<td>Enter an API backend configuration YAML file. For more information, see <a href = "#YAML">How to Write YAML for Downgraded Backend Configuration</a>.</td>
</tr>
</table>
The circuit breaker plugin supports the following conditions:<span id = "table"></span>
<table>
<tr>
<th>Error Condition Type</th>
<th>Description</th>
</tr>
<tr>
<td>Backend response time</td>
<td>If the backend response time exceeds the configured threshold, the request will be considered an error.</td>
</tr>
<tr>
<td>Backend error code</td>
<td>If the backend error codes include or do not include certain error codes, the request will be considered an error. Multiple error codes should be separated with commas.</td>
</tr>
<tr>
<td>Backend timeout</td>
<td>	If the backend timeout period set in the API backend configuration is exceeded, the request will be considered an error.</td>
</tr>
</table>


### Step 2. Bind an API and make the plugin effective

1. Select the just created plugin in the list and click **Bind API** in the **Operation** column.
2. In the **Bind API** pop-up window, select the service, environment, and the API to which the plugin needs to be bound.
   ![](https://qcloudimg.tencent-cloud.cn/raw/e9e674392e0070e320d38c1c00fc1ba2.png)
3. Click **OK** to bind the plugin to the API. At this time, the configuration of the plugin has taken effect for the API.

## PluginData

```json
{
    "failure_condition":"latency_seconds>1 or func_not_in(status_code,{200,201,202})",  // Error condition
    "failure_threshold":20,   // Maximum number of errors for circuit breaker triggering, which must be a positive integer
    "time_window":50,    // Error count judgment time window in seconds. Value range: 10–90 seconds
    "open_state_duration":69,    // Circuit breaking duration in seconds. Value range: 15–300 seconds
    "backend_type":"MOCK",    // Downgraded backend type. Valid values: MOCK, HTTP, SCF, VPC, UPSTREAM, TSF
    "backend_config":{    // Downgraded backend configuration
        "ServiceType":"MOCK",
        "ServiceMockReturnMessage":"hello mock from strategy"
    }
```

## How to Write YAML for Downgraded Backend Configuration[](id:YAML)

Write the YAML file by referring to the YAML template on the plugin creation page. The fields are in one to one correspondence to the backend configuration fields in the `CreateApi` API.
