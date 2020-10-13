LVB supports screencapture and porn detection. After you configure a screencapture and porn detection template in the console and associate it with a push domain name, LVB takes screenshots of the live stream and stores them or porn detection data into Cloud Object Storage (COS). If the push domain name has been associated with a callback template, Tencent Cloud will send a request to customers’ servers when a callback event is triggered during live streaming, and the customers’ servers are responsible for answering the request. After verification, a JSON package containing porn detection callbacks can be obtained.
This document describes how to create, modify and delete a screencapture and porn detection template in the console.

You can create a screencapture and porn detection template in the following ways:

- Create a template in the LVB Console. For more information, please see [Creating a Screencapture and Porn Detection Template](#Screenshot).
- Create a template through APIs.



## Notes

- The screencapture feature can be enabled alone, but the porn detection feature can be enabled only when the screencapture feature is enabled.
- Fees will be charged for screencapture and porn detection features. The former charges 0.0176 USD per thousand screenshots; the latter charges 0.2294 USD per thousand screenshots.
- The generated screenshots are stored in your COS bucket and will incur COS storage fee. For more information, please see [COS Pricing](https://intl.cloud.tencent.com/document/product/436/6239).
- To enable the screencapture feature, you must first grant LVB the permission to write to your COS bucket. For more information, please see [How to Authorize LVB to Store Screenshots in a COS Bucket](https://intl.cloud.tencent.com/document/product/267/33384).
- After a template has been created, you can associate it with a push domain name. For more information, please see [Screencapture and Porn Detection Configuration](https://intl.cloud.tencent.com/document/product/267/31063). The association will take effect in about 5–10 minutes. 
- The screencapturing and porn detection templates are managed at the domain name level in the console, and rules created by APIs cannot be canceled for the time being. If you associated a template with a specified stream through the screencapturing and porn detection APIs and want to unassociate it, you need to call the [DeleteLiveSnapshotRule](https://intl.cloud.tencent.com/document/product/267/30833) API.



## Prerequisites

- You have activated LVB and added a [push domain name](https://intl.cloud.tencent.com/document/product/267/35970).
- You have created a COS bucket and authorized LVB to store screenshots in the COS bucket. For more information, please see [How to Authorize LVB to Store Screenshots in a COS Bucket](https://intl.cloud.tencent.com/document/product/267/33384).



<span id="Screenshot"></span>
## Creating a Screencapture and Porn Detection Template

1. Log in to the LVB Console, and select **Feature Configuration** > **[LVB Screencapturing & Porn Detection](https://console.cloud.tencent.com/live/config/jtjh)**.
2. Click **+**, enter configuration information, and click **Save**.
![](https://main.qcloudimg.com/raw/722ecf606d4a24f9cc7eed879faf5200.jpg)
<table>
<thead><tr><th width="15%">Configuration Item</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Template Name</td>
<td>The name of the screencapture and porn detection template. It contains only letters, digits, underscores, and dashes, with a length of up to 30 characters.</td>
</tr><tr>
<td>Template Description</td>
<td>The description of the screencapture and porn detection template. It contains only letters, digits, underscores, and dashes, with a length of up to 100 characters.</td>
</tr><tr>
<td>Screencapture Interval</td>
<td>Screencapture interval during push. The value ranges from 5 to 300 seconds, and is 10 seconds by default.<br>Note: the value must be a multiple of 5.</li></td>
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
		<li>{AppName}: push AppName</li>
		<li>{PushDomain}: push domain name</li>
		<li>{StreamID}: stream ID</li>
		<li>{Year}: screenshot time (year)</li>
		<li>{Month}: screenshot time (month)</li>
		<li>{Day}: screenshot time (day)</li>
		<li>{Hour}: screenshot time (hour)</li>
		<li>{Minute}: screenshot time (minute)</li>
		<li>{Second}: screenshot time (second)</li>
		<li>{Width}: width of the screenshot</li>
		<li>{Height}: height of the screenshot</li><li>{Ext}: extension (.jpg)</li>
	</ul>Note: it contains only letters, digits, placeholders, and symbols (-, !, _, ., *).
	<br>Example: if the file name format is <code> {Year}-{Month}-{Day}- {Hour}-{Ext}</code>, the screenshot automatically captured during live streaming at 14:00:00, January 1, 2020 will be stored and named "2020010114.jpg" in COS.</td>
</tr>
</tbody></table>


## Modifying a Template

1. Select **Feature Configuration** > **[LVB Screencapturing & Porn Detection](https://console.cloud.tencent.com/live/config/jtjh)**.
2. Find the desired screencapture and porn detection template that you have created, and click **Edit** on the right to modify template information.
3. Click **Save**.

![](https://main.qcloudimg.com/raw/92b5d256a3c042de01e159da98ed7070.jpg)

## Deleting a Template

If the template is associated, you need to unassociate it before you can delete it. For more information, please see [Disassociating a Screencapture and Porn Detection Template](https://intl.cloud.tencent.com/document/product/267/31063#.E8.A7.A3.E7.BB.91.E6.88.AA.E5.9B.BE.E9.89.B4.E9.BB.84.E6.A8.A1.E6.9D.BF).

1. Select **Feature Configuration** > **[LVB Screencapturing & Porn Detection](https://console.cloud.tencent.com/live/config/jtjh)**.
2. Find the desired screencapture and porn detection template that you have created, and click the deletion icon at the top.
3. In the pop-up dialog box, click **OK** to confirm the deletion.

![](https://main.qcloudimg.com/raw/9762959b185290f8c4562c32c801de16.jpg)




## Associating the Template with a Domain Name

 For more information, see [Screencapture and Porn Detection Configuration](https://intl.cloud.tencent.com/document/product/267/31063). 
