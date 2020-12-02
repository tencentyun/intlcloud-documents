LVB supports the live streaming callback feature. You can create and configure a callback template in the console, set an address to receive the callback of a triggering event, and associate the template with a push domain name. After the successful association, if an event configured in the template triggers the callback during a live streaming, Tencent Cloud will actively send a request to the customer server which is responsible for the response. After verification, a JSON packet of the callback can be obtained through the path corresponding to the event.
This document describes how to create, modify and delete a callback template in the console. 

**You can create a callback template in the following ways:**
- Create a template in the LVB Console. For more information, please see [Creating a Callback Template](#Callback).
- Create a template through APIs.


## Notes

- After a template has been created, you can [associate it with a push domain name](https://intl.cloud.tencent.com/document/product/267/31065). The association will take effect in about 5-10 minutes.
- The `HTTP` or `HTTPS` server, whose address is configured as the callback address in the template to receive the callback, must be able to receive the request and respond normally.
- The callback templates are managed at the domain name level in the console, and rules created by APIs cannot be canceled for the time being. If you associated a template with a specified stream through the callback APIs and want to unassociate it, you need to call the [DeleteLiveCallbackRule](https://intl.cloud.tencent.com/document/product/267/30814) API.
- For more information on LVB callback protocols, please see [Event Message Notification Protocol](https://intl.cloud.tencent.com/document/product/267/31566).
- For more information on LVB callback parameters and examples, please see [Event Message Notification Parameter Descriptions](https://intl.cloud.tencent.com/document/product/267/31566).
- For more information on LVB callback notification parameters, please see the following:
	- [**LVB push** event](https://intl.cloud.tencent.com/document/product/267/31566)
	- [**LVB stream interruption** event](https://intl.cloud.tencent.com/document/product/267/31566)
	- [**LVB recording** file generation event](https://intl.cloud.tencent.com/document/product/267/31566)
	- [**LVB screenshot** file generation event](https://intl.cloud.tencent.com/document/product/267/31566)
	- [**Screencapture and porn detection result** file generation event](https://intl.cloud.tencent.com/document/product/267/31564)




<span id="Callback"></span>
## Creating a Callback Template

1. Log in to the [LVB Console](https://console.cloud.tencent.com/live).
2. Select **Feature Configuration** > **[LVB Callback](https://console.cloud.tencent.com/live/config/callback)** on the left sidebar.
3. Click **+** to create a callback template, enter configuration information in the pop-up window, and click **Save**.
![](https://main.qcloudimg.com/raw/e79b06c3fecbfaa34d124f820e10ff2c.png)
<table>
<thead><tr><th width="17%">Configuration Item</th><th>Description</th></tr></thead><tbody><tr>
<td>Template Name</td>
<td>Name of the callback template. It contains only letters, digits, underscores, and dashes, with a length of up to 30 characters.</td>
</tr><tr>
<td>Template Description</td>
<td>Description of the callback template. It contains only letters, digits, underscores, and dashes, with a length of up to 100 characters.</td>
</tr><tr>
<td>Callback Key</td>
<td>Custom callback key.<br>It contains only letters and digits with a length of up to 32 characters. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/267/31566">Event Message Notification</a>.</td>
</tr><tr>
<td>Push Callback</td>
<td>Enter an address starting with `http`, `https`, etc. to receive the push callback.</td>
</tr><tr>
<td>Interruption Callback</td>
<td>Enter an address starting with `http`, `https`, etc. to receive the interruption callback.</td>
</tr><tr>
<td>Recording Callback</td>
<td>Enter an address starting with `http`, `https`, etc. to receive the recording callback.</td>
</tr><tr>
<td>Screencapture Callback</td>
<td>Enter an address starting with `http`, `https`, etc. to receive the screencapture callback.</td>
</tr><tr>
<td>Porn Detection Callback</td>
<td>Enter an address starting with `http`, `https`, etc. to receive the porn detection callback.</td>
</tr>
</tbody></table>


<span id="change"></span>
## Modifying a Template

1. Select **Feature Configuration** > **[LVB Callback](https://console.cloud.tencent.com/live/config/callback)** .
2. Find the desired callback template that you have created, and click **Edit** on the right to modify template information.
3. Click **Save**.

![](https://main.qcloudimg.com/raw/885d9f6ec5ee5b921865cba965068de0.jpg)

<span id="delete"></span>
## Deleting a Template

If the template is associated, you need to unassociate it before you can delete it. For more information, please see [Unassociating a Callback Template](https://intl.cloud.tencent.com/document/product/267/31065#untie).

1. Select **Feature Configuration** > **[LVB Callback](https://console.cloud.tencent.com/live/config/callback)** .
2. Find the desired callback template that you have created, and click the deletion icon at the top.
3. In the pop-up window, click **OK** to confirm the deletion.

![](https://main.qcloudimg.com/raw/1bf90e6b3197dd2e18aff8c52cbe331c.jpg)

