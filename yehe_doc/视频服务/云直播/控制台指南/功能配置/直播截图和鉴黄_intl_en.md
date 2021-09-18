CSS provides screencapture and porn detection. After you configure a screencapture and porn detection template in the console and bind it with a push domain name, CSS takes screenshots of the live stream and stores them or porn detection data into Cloud Object Storage (COS). After the push domain name has been bound with a callback template, if a callback event is triggered during live streaming, Tencent Cloud will send a request to the client server which is responsible for the response. After passing the verification, the server will obtain a JSON packet containing the porn detection callback.
This document describes how to create, bind, unbind, modify, and delete a screencapture and porn detection template in the console.

You can create a screencapture and porn detection template in the following ways:

- Create a template in the CSS console. For details, see [Creating a Screencapture and Porn Detection Template](#Screenshot).
- Create a template with APIs. For specific parameters and samples, see [CreateLiveSnapshotTemplate](https://intl.cloud.tencent.com/document/product/267/30834).



## Notes

- You can enable screencapture directly. To enable porn detection, you must enable screencapture first.
- Using screencapture and porn detection will incur fees. The unit prices for screencapture and porn detection are 0.0176 USD per thousand screenshots and 0.2294 USD per thousand screenshots respectively. For details, see [Intelligent Porn Detection](https://intl.cloud.tencent.com/document/product/267/39607).  
- The generated screenshots will be stored in your COS bucket and will incur COS storage fees. For more information, see [COS Pricing](https://intl.cloud.tencent.com/pricing/cos).
- To enable the screencapture feature, you must first grant CSS the permission to write to your COS bucket. For more information, see [Authorizing CSS to Store Screenshots in a COS Bucket](https://intl.cloud.tencent.com/document/product/267/33384).
- After creating a template, you can bind it with a push domain name. For more information, see [Screencapture and Porn Detection Configuration](https://intl.cloud.tencent.com/document/product/267/31063). The binding takes effect in about 5-10 minutes. 
- In the console, you can manage screencapture and porn detection templates by domain name, but cannot cancel rules created by APIs. If you have bound a template with a specified stream through screencapture and porn detection APIs and want to unbind them, you need to call the [DeleteLiveSnapshotRule](https://intl.cloud.tencent.com/document/product/267/30833) API.
- Binding, unbinding, or modifying a template affects only new live streams after the update but not ongoing ones. To make the new rule take effect for ongoing live streams, you need to interrupt them and push them again.



## Prerequisites

- You have activated CSS and added a [push domain name](https://intl.cloud.tencent.com/document/product/267/35970).
- You have created a COS bucket and authorized CSS to store screenshots in the COS bucket. For more information, see [How to Authorize CSS to Store Screenshots in a COS Bucket](https://intl.cloud.tencent.com/document/product/267/33384).



<span id="Screenshot"></span>
## Creating a Screencapture and Porn Detection Template

1. Log in to the CSS console, and select **Feature Configuration** > **[Live Screencapture & Porn Detection](https://console.cloud.tencent.com/live/config/jtjh).
2. Click **Create Screencapture and Porn Detection Template**, configure settings, and then click **Save**.
![](https://main.qcloudimg.com/raw/544c2127f7870add334eaf760f1da089.png)
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
<td>Auto screencapture interval during the push, in seconds. Value range: 2 (default)-300
<td>Intelligent Porn Detection</td>
<td>Whether to enable intelligent porn detection. If it is enabled, you need to configure a callback template before you can receive porn detection results.</td>
</tr><tr>
<td>Storage Account</td>
<td>You can select **Current Account** or **Other Account**.</td>
</tr><tr>
<td>CosAppId</td>
<td>Required only when the storage account (the account where the COS service is under) is set to **Other Account**. You can get the value of the `AppId` in <a href="https://console.cloud.tencent.com/developer">**Account Information**</a> of the storage account.</td>
</tr><tr>
<td>Bucket</td>
<td>Select a **COS** bucket that you have created and authorized.</td>
</tr><tr>
<td>Region</td>
<td>The region where the bucket resides in. It cannot be modified.</td>
</tr><tr>
<td>Folder</td>
<td>Click the box to select a COS folder. The folder name is in the format of <code>{Year}-{Month}-{Day}/</code> by default.<br>Note: the name of a COS folder can contain only letters, digits, placeholders, and symbols <code>-, !, _, ., *</code>.</td>
</tr><tr>
<td>File Name</td>
<td>The format of the screenshot file name. Default format: <code>{StreamID}-screenshot-{Hour}-{Minute}-{Second}-{Width}x{Height}{Ext}</code>. It can be customized by splicing the following parameters:
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
        <li>{Width}: width of the screenshot</li>
        <li>{Height}: height of the screenshot</li><li>{Ext}: extension (.jpg)</li>
    </ul>Note: it can contain only letters, digits, placeholders, and symbols (-, !, _, ., *).
    <br>Example: if the file name format is <code> {Year}-{Month}-{Day}- {Hour}-{Ext}</code>, the screenshot automatically captured during live streaming at 14:00:00, January 1, 2020 will be stored and named "2020010114.jpg" in COS.</td>
</tr>
</tbody></table>


<span id="conect"></span>
## Binding a Template with Domain Names

1. Log in to the CSS console and select **Feature Configuration** > **[Live Screencapture & Porn Detection](https://console.cloud.tencent.com/live/config/jtjh).
2. Enter the domain name binding page in either of the following ways:
    - **Directly bind a domain name**: click **Bind Domain Name** in the upper left.
    ![](https://main.qcloudimg.com/raw/20490c4aa318f5b5253d0b82c1672087.png)
    - **Bind a domain name after creating a screencapture and porn detection template:** after successfully [creating a screencapture and porn detection template](#Screenshot), click **Bind Domain Name** in the pop-up.
    ![](https://main.qcloudimg.com/raw/727b1d25f256a655478312ee45814a32.png)
1. Select a **screencapture and porn detection template** and a **push domain name** in the domain name binding window and then click **Confirm**.
![](https://main.qcloudimg.com/raw/5612913bcbb6ac1cb5207dcc03e997c4.png)
>? You can click **Add** to bind multiple push domain names with this template.


<span id="unite"></span>
## Unbinding a Template from Domain Names

1. Log in to the CSS console and select **Feature Configuration** > **[Live Screencapture & Porn Detection](https://console.cloud.tencent.com/live/config/jtjh).
2. Select a screencapture and porn detection template with bound domain names, find the target domain name, and click **Unbind**.
   ![](https://main.qcloudimg.com/raw/fd20557cc393cc483d9a36dd0ddb6652.png)
3. In the pop-up, click **Confirm**.
   ![](https://main.qcloudimg.com/raw/9182f6589885ecba5fafcea075c9184e.png)


<span id="change"></span>
## Modifying a Template

1. Log in to the CSS console and select **Feature Configuration** > **[Live Screencapture & Porn Detection](https://console.cloud.tencent.com/live/config/jtjh).
2. Find the desired screencapture and porn detection template that you created, and click **Edit** on the right to modify template information.
3. Click **Save**.

![](https://main.qcloudimg.com/raw/0ec0dcb3dc35571e1aab74b20d533c35.png)


<span id="delete"></span>
## Deleting a Template

>! If the template has been bound with domain names, you need to [unbind](#unite) them before deleting the template.

1. Log in to the CSS console and select **Feature Configuration** > **[Live Screencapture & Porn Detection](https://console.cloud.tencent.com/live/config/jtjh).
2. Find the desired screencapture and porn detection template that you have created, and click **Delete** at the top.
3. In the pop-up, click **Confirm**.

![](https://main.qcloudimg.com/raw/6ae7a299517803a92776d8077ccda1d3.png)



## Operations
For more information about **binding** and **unbinding a domain name** with or from a screencapture and porn detection template, see [Screencapture and Porn Detection Configuration](https://intl.cloud.tencent.com/document/product/267/31063).
