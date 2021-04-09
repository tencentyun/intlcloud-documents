CSS supports screencapture and porn detection. After you configure a screencapture and porn detection template in the console and bind it to a push domain name, CSS takes screenshots of the live stream and stores them or porn detection data into Cloud Object Storage (COS). If the push domain name has been bound to a callback template, Tencent Cloud will send a request to your server when a callback event is triggered during live streaming, and your server is responsible for the response. After authentication, a JSON packet containing the porn detection callback information can be obtained.
This document describes how to create, modify, bind, unbind, and delete a screencapture and porn detection template in the console.

You can create a screencapture and porn detection template in the following ways:

- Create a template in the CSS console. For more information, please see [Creating Screencapture and Porn Detection Template](#Screenshot).
- Create a template with APIs. For specific parameters and samples, please see [CreateLiveSnapshotTemplate](https://intl.cloud.tencent.com/document/product/267/30834).



## Notes

- The screencapture feature can be enabled alone, but the porn detection feature can be enabled only after the screencapture feature is enabled.
- Fees will be charged for screencapture and porn detection features. The former charges 0.0176 USD per thousand screenshots; the latter charges 0.2294 USD per thousand screenshots.
- The generated screenshots are stored in your COS bucket and will incur COS storage fee. For more information, please see [COS Pricing](https://intl.cloud.tencent.com/document/product/436/6239).
- To enable the screencapture feature, you must first grant CSS the permission to write to your COS bucket. For more information, please see [How to Authorize CSS to Store Screenshots in a COS Bucket](https://intl.cloud.tencent.com/document/product/267/33384).
- After a template is created, you can bind it to a push domain name. For more information, please see [Screencapture and Porn Detection Configuration](https://intl.cloud.tencent.com/document/product/267/31063). The binding will take effect in about 5–10 minutes. 
- The screencapture and porn detection templates are managed at the domain name level in the console, and rules created by APIs cannot be canceled for the time being. If you bound a template to a specified stream through the screencapture and porn detection APIs and want to unbind it, you need to call the [DeleteLiveSnapshotRule](https://intl.cloud.tencent.com/document/product/267/30833) API.
- Binding, unbinding, and modifying a template affect only new live streams after the update but not ongoing ones. To make the new rule take effect for ongoing live streams, you need to interrupt them and push them again.



## Prerequisites

- You have activated the CSS service and added a [push domain name](https://intl.cloud.tencent.com/document/product/267/35970).
- You have created a COS bucket and authorized CSS to store screenshots in the COS bucket. For more information, please see [How to Authorize CSS to Store Screenshots in a COS Bucket](https://intl.cloud.tencent.com/document/product/267/33384).



<span id="Screenshot"></span>
## Creating Screencapture and Porn Detection Template

1. Log in to the CSS console and select **Feature Configuration** > **[Live Screencapture & Porn Detection](https://console.cloud.tencent.com/live/config/jtjh)**.
2. Click **+**, enter the configuration information, and click **Save**.
![](https://main.qcloudimg.com/raw/e17b92da94af4b583dab0273adb89447.jpg)
<table>
<thead><tr><th width="15%">Configuration Item</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Template Name</td>
<td>The name of the screencapture and porn detection template, which can contain up to 30 letters, digits, underscores (_), and hyphens (-).</td>
</tr><tr>
<td>Template Description</td>
<td>The description of the screencapture and porn detection template, which can contain up to 100 letters, digits, underscores (_), and hyphens (-).</td>
</tr><tr>
<td>Screencapture Interval</td>
<td>Screencapture interval during push. The value ranges from 5 to 300 seconds and is 10 seconds by default.<br>Note: the value must be a multiple of 5.</li></td>
</tr><tr>
<td>Smart Porn Detection</td>
<td>Whether to enable smart porn detection. If it is enabled, you need to configure a callback template before you can receive porn detection results.</td>
</tr><tr>
<td>Storage Account</td>
<td>You can select "Current Account" or "Other Account".</td>
</tr><tr>
<td>AppId</td>
<td>Required only when the storage account is set to "Other Account". You can get the value of APPID in <a href="https://console.cloud.tencent.com/developer">**Account Information**</a> of the account.</td>
</tr><tr>
<td>Bucket</td>
<td>Select a **COS** bucket that you have created and authorized.</td>
</tr><tr>
<td>Region</td>
<td>The region where the bucket resides. It cannot be modified.</td>
</tr><tr>
<td>Folder</td>
<td>Click the box to select a COS folder. The folder name is in the format of <code>{Year}-{Month}-{Day}/</code> by default.<br>Note: the name of a COS folder can contain only letters, digits, placeholders, and symbols <code>-, !, _, ., *</code>.</td>
</tr><tr>
<td>File Name</td>
<td>The format of the screenshot file name. Default value: <code>{StreamID}-screenshot-{Hour}-{Minute}-{Second}-{Width}x{Height}{Ext}</code>. It can be customized by splicing the following parameters:
	<ul style="margin:0">
		<li>{AppName}: push `AppName`</li>
		<li>{PushDomain}: push domain name</li>
		<li>{StreamID}: stream ID</li>
		<li>{Year}: screenshot time (year)</li>
		<li>{Month}: screenshot time (month)</li>
		<li>{Day}: screenshot time (day)</li>
		<li>{Hour}: screenshot time (hour)</li>
		<li>{Minute}: screenshot time (minute)</li>
		<li>{Second}: screenshot time (second)</li>
		<li>{Width}: screenshot width</li>
		<li>{Height}: screenshot height</li><li>{Ext}: extension (.jpg)</li>
	</ul>Note: it can contain only letters, digits, placeholders, and symbols (-, !, _, ., *).
	<br>Example: if the file name format is <code> {Year}-{Month}-{Day}- {Hour}-{Ext}</code>, the screenshot automatically captured during live streaming at 14:00:00, January 1, 2020 will be stored and named "2020010114.jpg" in COS.</td>
</tr>
</tbody></table>


<span id="conect"></span>
## Binding Domain Name

1. Log in to the CSS console and select **Feature Configuration** > **[Live Screencapture & Porn Detection](https://console.cloud.tencent.com/live/config/jtjh).
2. Enter the domain name binding page in either of the following ways:
	- **Directly bind a domain name**: click **Bind Domain Name** in the top-left corner.
	- **Bind a domain name after creating a screencapture and porn detection template:** after successfully [creating a screencapture and porn detection template](#Screenshot), click **Bind Domain Name** in the pop-up.
1. Select a **screencapture and porn detection template** and a **push domain name** in the domain name binding window and then click **OK**.
> ? You can click **Add** to bind multiple push domain names to this template.


<span id="unite"></span>
## Unbinding

1. Log in to the CSS console and select **Feature Configuration** > **[Live Screencapture & Porn Detection](https://console.cloud.tencent.com/live/config/jtjh).
2. Select domain names bound to the screencapture and porn detection template and click **Unbind**.
3. Confirm whether to unbind the domain name and click **OK** to unbind it.


<span id="change"></span>
## Modifying Template

1. Go to **Feature Configuration** > **[Live Screencapture & Porn Detection](https://console.cloud.tencent.com/live/config/jtjh).
2. Select the target screencapture and porn detection template and click **Edit** on the right to modify the template information.
3. Click **Save**.

![](https://main.qcloudimg.com/raw/976ee78aedebea43c6b3fe2e4e0ef41c.jpg)


<span id="delete"></span>
## Deleting Template

If a template has been bound to a domain name, you need to unbind the template before deleting it. For detailed directions, please see [Unbinding Screencapture and Porn Detection Configuration](https://intl.cloud.tencent.com/document/product/267/31063#.E8.A7.A3.E7.BB.91.E6.88.AA.E5.9B.BE.E9.89.B4.E9.BB.84.E6.A8.A1.E6.9D.BF).

1. Go to **Feature Configuration** > **[Live Screencapture & Porn Detection](https://console.cloud.tencent.com/live/config/jtjh).
2. Find the target screencapture and porn detection template that you have created and click the deletion icon at the top.
3. In the pop-up dialog box, click **OK** to confirm the deletion.

![](https://main.qcloudimg.com/raw/d4b62f44f9ecafdee20be7758f2042e1.jpg)



## Relevant Operations
## Binding Domain Name
For more information on how to **bind/unbind** a **domain name** to/from a screencapture and porn detection template, please see [Screencapture and Porn Detection Configuration](https://intl.cloud.tencent.com/document/product/267/31063). 
