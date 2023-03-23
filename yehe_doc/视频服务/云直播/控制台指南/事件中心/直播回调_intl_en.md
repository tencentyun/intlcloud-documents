CSS supports callbacks. To use this feature, you need to create a callback template in the console, configure an address to receive callbacks for an event, and then bind the template with your push domain name. If the event triggers a callback during live streaming, Tencent Cloud will send a request to your server, which is responsible for responding to the request. After successful verification, the server will obtain a JSON packet of the callback through the address configured.
This document describes how to create, modify and delete a callback template in the console. 

**You can create a callback template in the following ways:**
- Create a template in the CSS console. For details, see [Creating a Callback Template](#Callback).
- Create a template with APIs. For the parameters and request sample, see [CreateLiveCallbackTemplate](https://intl.cloud.tencent.com/document/product/267/30815).


## Must-knows

- After creating a template, you need to [bind it with a push domain name](https://intl.cloud.tencent.com/document/product/267/31065). The binding takes effect in about 5-10 minutes.
- Make sure the HTTP or HTTPS server you use to receive callbacks are able to receive requests and respond normally.
- In the console, you can only bind and unbind callback templates at the domain level. For callback rules bound to specific streams by APIs, you need to call [DeleteLiveCallbackRule](https://intl.cloud.tencent.com/document/product/267/30814) to unbind them.
- For information on callback protocols, see [How to Receive Event Notification](https://intl.cloud.tencent.com/document/product/267/38080).
- For information about the parameters in a callback, see the following documents:
 - [Stream pushing](https://intl.cloud.tencent.com/document/product/267/38081)
 - [Stream interruption](https://intl.cloud.tencent.com/document/product/267/38081)
 - [Recording](https://intl.cloud.tencent.com/document/product/267/38082)
 - [Screencapturing](https://intl.cloud.tencent.com/document/product/267/38083)
 - [Porn detection](https://intl.cloud.tencent.com/document/product/267/38084)
 - [Relay](https://intl.cloud.tencent.com/document/product/267/42525)
 - [Push errors](https://www.tencentcloud.com/document/product/267/53310)



## Creating a Callback Template[](id:Callback)
1. Log in to the [CSS console](https://console.cloud.tencent.com/live).
2. Select **Event Center** > [Live Stream Callback](https://console.cloud.tencent.com/live/config/callback) in the left sidebar.
3. Click **Create Template**, fill in the information, select the types of callbacks you want to receive, enter the callback URLs, and click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/f8418ac2c646c3461d95d7fab157f2f3.png)
<table>
<thead><tr><th width="17%">Item</th><th>Description</th></tr></thead><tbody><tr>
<td>Template Name</td>
<td>The callback template name, which can contain up to 30 Chinese characters, letters, numbers, underscores (_), and hyphens (-).</td>
</tr><tr>
<td>Template Description</td>
<td>The description of the callback template, which can contain up to 100 Chinese characters, letters, numbers, underscores (_), and hyphens (-).</td>
</tr><tr>
<td>Callback Key</td>
<td>A custom callback key. <br>It can contain up to 32 letters and numbers. For details, see <a href="https://intl.cloud.tencent.com/document/product/267/38081#.E5.9B.9E.E8.B0.83.E5.85.AC.E5.85.B1.E5.8F.82.E6.95.B0">Common callback parameters</a>.</td>
</tr><tr>
<td>Push Callback</td>
<td>Enter an HTTP or HTTPS address to receive push callbacks.</td>
</tr><tr>
<td>Interruption Callback</td>
<td>Enter an HTTP or HTTPS address to receive push interruption callbacks.</td>
</tr><tr>
<td>Recording Callback</td>
<td>Enter an HTTP or HTTPS address to receive recording callbacks.</td>
</tr><tr>
<td>Screencapture Callback</td>
<td>Enter an HTTP or HTTPS address to receive screencapture callbacks.</td>
</tr><tr>
<td>Porn Detection Callback</td>
<td>Enter an HTTP or HTTPS address to receive porn detection callbacks.</td>
</tr><tr>
<td>Error callbacks</td>
<td>Enter an HTTP or HTTPS address to receive push error callbacks.</td>
</tr>
</tbody></table>




## Modifying a Callback Template[](id:change)

1. Select **Event Center** > [Live Stream Callback](https://console.cloud.tencent.com/live/config/callback).
2. Select the target callback template and click **Edit** to modify its information.
3. After modification, click **Save**.

![](https://qcloudimg.tencent-cloud.cn/raw/6350e65d695ece9c075dd3e053c1aeca.png)


## Deleting a Callback Template[](id:delete)

If a template is bound to a domain name, you need to unbind it before you can delete it. For detailed directions, see [Unbinding Callback Template](https://intl.cloud.tencent.com/document/product/267/31065#untie).

1. Select **Event Center** > [Live Stream Callback](https://console.cloud.tencent.com/live/config/callback).
2. Find the target callback template, and click **Delete**.
3. In the pop-up window, click **Confirm**.

![](https://qcloudimg.tencent-cloud.cn/raw/9cc8d3a6c82a8b54ae904ddcc9ca01f6.png)
