## Feature Overview

In device use cases, if system parameters need to be updated for devices, such as device IP, port number, and serial port parameter, the remote configuration feature can be used to this end.

## Feature Details

Remote device configuration supports two configuration update methods: active distribution by IoT Hub and active request by device. For scenarios where all devices under the same product need to update their configurations, the former can be used to distribute the configuration information to all devices through the remote configuration topic. For scenarios where certain devices need to update their configurations, the latter can be used.

- Remote configuration request topic: `$config/operation/${productid}/${devicename}`
- Remote configuration subscription topic: `$config/operation/result/${productid}/${devicename}`

>?   
>- `${productID}`: product ID
>- `${deviceName}`: device name

### Active distribution by IoT Hub

1. The device subscribes to the remote configuration topic.
2. On the configuration page in the [IoT Hub console](https://console.cloud.tencent.com/iothub), enable remote configuration and enter the configuration information in JSON format.

3. Click **Batch Distribute** to distribute the configuration information to all devices under the product in batches through the remote configuration subscription topic.
The format of the message distributed by the cloud through the remote configuration subscription topic is as follows:
```json
{"type":"push",
    "result":0,
	"payload":{yourConfigurationMessage}
}
​```Parameter description:
<table>
	<thead>
	<tr>
	<th align="center">Parameter</th>
	<th align="center">Type</th>
	<th align="left">Description</th>
	</tr>
	</thead>
	<tbody><tr>
	<td align="center">type</td>
	<td align="center">string</td>
	<td align="left">The value is `push` for active distribution by IoT Hub.<ul><li>push: active distribution by IoT Hub</li><li>reply: active request by device</li></ul></td>
	</tr>
	<tr>
	<td align="center">result</td>
	<td align="center">int</td>
	<td align="left">Error code.<ul><li>0: success</li><li>1001: the configuration is disabled</li></ul></td>
	</tr>
	<tr>
	<td align="center">payload</td>
	<td align="center">string</td>
	<td align="left">Configuration information details</td>
	</tr>
	</tbody></table>

After the device successfully receives the configuration information distributed by IoT Hub, it will get the configuration information by calling the callback function provided in the SDK and update the information into its system parameters. The logic of updating configuration parameters in this part should be customized by yourself.

### Active request by device

1. On the configuration page in the console, enable remote configuration and enter the configuration information in JSON format.
2. The device subscribes to the remote configuration topic and sends a remote configuration request through the topic.
3. After the cloud successfully receives the device's request for remote configuration information, it will send the device configuration information on the configuration page to the device through the remote configuration subscription topic.
 - The content of the configuration request message sent by the device is fixed as follows:
```
{"type":"get"}
```
Parameter description:
<table>
<thead>
<tr>
<th align="center">Parameter</th>
<th align="center">Type</th>
<th align="center">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="center">type</td>
<td align="center">string</td>
<td align="center">The value is `get` for active request by device</td>
</tr>
</tbody></table>
   - The format of the message distributed by the cloud through the remote configuration subscription topic is as follows:
​```json
{"type":"reply",
	  "result":0,
	  "payload":{yourConfigurationMessage}
}
```
Parameter description:
<table>
<thead>
<tr>
<th align="center">Parameter</th>
<th align="center">Type</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="center">type</td>
<td align="center">string</td>
<td align="left">The value is `reply` for active request by device.<ul><li>push: active distribution by IoT Hub</li><li>reply: active request by device</li></ul></td>
</tr>
<tr>
<td align="center">result</td>
<td align="center">int</td>
<td align="left">Error code.<ul><li>0: success</li><li>1001: the configuration is disabled</li></ul></td>
</tr>
<tr>
<td align="center">payload</td>
<td align="center">string</td>
<td align="left">Configuration information details</td>
</tr>
</tbody></table>
4. The steps after the device receives the data are the same as those of active distribution by the cloud.

### Configuration information management

IoT Hub provides the configuration information management feature, and you can query the last five configuration information records in the console. After you edit and save the configuration information again, the last configuration information will be displayed in the configuration information record. You can view the number, update time, and configuration content for easy management.
![](https://main.qcloudimg.com/raw/6bcd507b059e99a667b27f40d3d2036b.png)
