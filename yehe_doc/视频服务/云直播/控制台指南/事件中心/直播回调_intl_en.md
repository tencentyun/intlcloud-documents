CSS supports callbacks. To use this feature, you need to create a callback template in the console, configure an address to receive callbacks for an event, and then bind the template with your push domain name. If the event configured in the template triggers a callback during live streaming, Tencent Cloud will send a request to your server, which is responsible for responding to the request. After successful verification, the server will obtain a JSON packet of the callback through the address configured for the event.
This document describes how to create, modify and delete a callback template in the console. 

**You can create a callback template in the following ways:**
- Create a template in the CSS console. For details, see [Creating a Callback Template](#Callback).
- Create a template with APIs. For specific parameters and samples, see [CreateLiveCallbackTemplate](https://intl.cloud.tencent.com/document/product/267/30815).


## Notes

- After creating a template, you need to [bind it with a push domain name](https://intl.cloud.tencent.com/document/product/267/31065). The binding takes effect in about 5-10 minutes.
- The HTTP or HTTPS server, whose address is configured as the callback address in the template to receive the callback, must be able to receive the request and respond normally.
- In the console, you can manage callback templates by domain name, but cannot cancel rules created by APIs. If you bound a template with a specified stream through callback APIs and want to unbind them, you need to call the [DeleteLiveCallbackRule](https://intl.cloud.tencent.com/document/product/267/30814) API.
- For more information on live stream callback protocols, see [Event Message Notification Protocol](https://intl.cloud.tencent.com/document/product/267/38080).
- For more information on live stream callback notification parameters, see the following:
 - [Push event notification](https://intl.cloud.tencent.com/document/product/267/38081)
 - [Stream interruption event notification](https://intl.cloud.tencent.com/document/product/267/38081)
 - [Recording event notification](https://intl.cloud.tencent.com/document/product/267/38082)
 - [Screencapture event notification](https://intl.cloud.tencent.com/document/product/267/38083)
 - [Porn detection event notification](https://intl.cloud.tencent.com/document/product/267/38084)




## Creating Callback Template[](id:Callback)
1. Log in to the [CSS console](https://console.cloud.tencent.com/live).
2. Select **Event Center** > **[Live Stream Callback](https://console.cloud.tencent.com/live/config/callback)** in the left sidebar.
3. Click **Create Callback Template**, fill in the information, select the types of callbacks you want to receive, enter the callback URLs, and click **Save**.
![](https://main.qcloudimg.com/raw/e79b06c3fecbfaa34d124f820e10ff2c.png)
<table>
<thead><tr><th width="17%">Configuration Item</th><th>Description</th></tr></thead><tbody><tr>
<td>Template Name</td>
<td>Name of the callback template, which can contain up to 30 letters, digits, underscores (_), and hyphens (-).</td>
</tr><tr>
<td>Template Description</td>
<td>Description of the callback template, which can contain up to 100 letters, digits, underscores (_), and hyphens (-).</td>
</tr><tr>
<td>Callback Key</td>
<td>Custom callback key. <br>It can contain up to 32 letters, digits, underscores (_), and hyphens (-). For details, see <a href="https://intl.cloud.tencent.com/document/product/267/38081#.E5.9B.9E.E8.B0.83.E5.85.AC.E5.85.B1.E5.8F.82.E6.95.B0">Event Message Notification Common Parameters</a>.</td>
</tr><tr>
<td>Push Callback</td>
<td>Enter an address starting with `http`, `https`, etc. to receive push callbacks.</td>
</tr><tr>
<td>Interruption Callback</td>
<td>Enter an address starting with `http`, `https`, etc. to receive stream interruption callbacks.</td>
</tr><tr>
<td>Recording Callback</td>
<td>Enter an address starting with `http`, `https`, etc. to receive recording callbacks.</td>
</tr><tr>
<td>Screencapture Callback</td>
<td>Enter an address starting with `http`, `https`, etc. to receive screencapture callbacks.</td>
</tr><tr>
<td>Porn Detection Callback</td>
<td>Enter an address starting with `http`, `https`, etc. to receive porn detection callbacks.</td>
</tr>
</tbody></table>



## Modifying Callback Template[](id:change)

1. Select **Event Center** > **[Live Stream Callback](https://console.cloud.tencent.com/live/config/callback)**.
2. Select the target callback template and click **Edit** to modify its information.
3. After modification, click **Save**.

![](https://main.qcloudimg.com/raw/885d9f6ec5ee5b921865cba965068de0.jpg)


## Deleting Callback Template[](id:delete)

If a template is bound to a domain name, you need to unbind it before you can delete it. For detailed directions, see [Unbinding Callback Template](https://intl.cloud.tencent.com/document/product/267/31065#untie).

1. Select **Event Center** > **[Live Stream Callback](https://console.cloud.tencent.com/live/config/callback)**.
2. Find the target callback template, and click **Delete**.
3. In the pop-up, click **Confirm**.

![](https://main.qcloudimg.com/raw/1bf90e6b3197dd2e18aff8c52cbe331c.jpg)

