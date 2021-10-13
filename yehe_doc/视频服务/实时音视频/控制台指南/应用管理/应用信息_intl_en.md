After creating an application, you can click **Application Info** to view its detailed information, including the basic information, relayed live streaming information, TRTC service status, and tags.

## Application Info
### Description
1. Log in to the TRTC console and click **[Application Management](https://console.cloud.tencent.com/trtc/app)** to view the application list.
2. Find the application whose information you want to view, and click **Application Info** on the right.
![](https://main.qcloudimg.com/raw/495a71aedd1f8ab6296be0d9e3c31406.png)
3. View the basic information of the application in the **Application Info** section on the **Application Info** tab page.
![](https://main.qcloudimg.com/raw/0fc9aeb7b75617c9b702a8f2c5e4a8ba.png)
<table>
<tr><th width="18%">Item</th><th>Description</th></tr><tr>
<td>Application name</td>
<td>The name specified during application creation, can be modified</td>
</tr><tr>
<td>SDKAppID</td>
<td>The SDKAppID generated automatically upon application creation. It uniquely identifies an application and is a required parameter for calling audio APIs.</td>
</tr><tr>
<td>Creation time</td>
<td>Time when the application is created</td>
</tr><tr>
<td>Description</td>
<td>Description of the application, can be modified</td>
</tr><tr>
<td>Application source</td>
<td>Source of the application<ul style="margin:0"><li/>This item is displayed if <a href="https://intl.cloud.tencent.com/document/product/1047/34540">the application is created automatically after TRTC is activated in the IM console</a>.<li/>It is not displayed if the application is manually created in the TRTC console.</ul></td>
</tr></table>



### Modifying application info
1. In **[Application Management](https://console.cloud.tencent.com/trtc/app)**, click **Application Info** for the application whose information you want to modify.
2. In the **Application Info** section on the **Application Info** tab page, click **Edit**.
![](https://main.qcloudimg.com/raw/818c5c71aa54d05b6bed152121d43e6e.png)
3. In the dialog box that pops up, modify the **Application Name** or **Description**, and click **Modify** to save the information.
![](https://main.qcloudimg.com/raw/019312c2244ee5e311619dc64436b960.png)
> ? 
> - **Application Name** can contain up to 15 characters. Only numbers, letters, Chinese characters, and underscores (_) are allowed.
> - **Description** can contain up to 300 characters. Only numbers, letters, Chinese characters, and underscores (_) are allowed.



## Relayed Live Streaming Info
In relayed live streaming, TRTC uses a relaying and transcoding cluster to convert its UDP audio/video streams into RTMP streams in the cloud, which are then pushed to the standard live streaming system and distributed through CDNs. You will need the information here to implement [CDN Relayed Live Streaming](https://intl.cloud.tencent.com/document/product/647/35242).
![](https://main.qcloudimg.com/raw/d16f88ce8704ee236866bc9947df2f17.png)

## TRTC Service Status
This section shows the status of TRTC basic and value-added services, which may be **Normal** or **Disabled**.
- **Normal:**
If the status is normal, you have access to both the basic and value-added services. To avoid service suspension, please purchase [new packages](https://buy.cloud.tencent.com/trtc) in a timely manner or, if you have [enabled pay-as-you-go](https://intl.cloud.tencent.com/document/product/647/41979), make sure that your [account](https://console.cloud.tencent.com/expense) has sufficient balance.
![](https://main.qcloudimg.com/raw/0e2b88e7a8fc1ac1186bcbcd703a9fe4.png)
- **Disabled:**
If the status is disabled, you have access to neither the basic nor value-added services. This may involve one of three circumstances.
	1. If you haven’t enabled pay-as-you-go, the services may have been suspended automatically for your account after your trial package is used up or expires. You can [purchase a package](https://buy.cloud.tencent.com/trtc) or [enable pay-as-you-go](https://intl.cloud.tencent.com/document/product/647/41979) to resume the services.
	2. If you have enabled pay-as-you-go, the service suspension may be a result of overdue payments in your account. The services will be resumed once you [make the payment](https://console.cloud.tencent.com/expense/overview).
	3. You may have manually disabled an application, in which case you can click **Enable Application** to resume the services.
![](https://main.qcloudimg.com/raw/faa1e34ad79109a665af1393b0cfeb5f.png)

[](id:deactivate)
### Manually disabling application
1. Mouse over **More** and click **Disable Application**.
2. Read the notes and click **Disable**.
3. To prevent losses caused by unintentional operations, you need to verify your identity again.
4. An application disabling operation takes effect 3-5 minutes after initiation. Please wait.

[](id:enable)
### Manually enabling application
1. Click **Enable Application**.
2. Read the notes and click **Enable**.
3. To prevent losses caused by unintentional operations, you need to verify your identity again.
4. An application enabling operation takes effect 3-5 minutes after initiation. Wait and refresh the page.

[](id:delete)
### Manually deleting application
1. Mouse over **More** and click **Delete Application**.
2. Read the notes and click **Delete**.
3. To prevent losses caused by unintentional operations, you need to verify your identity again.
4. An application deleting operation takes effect 3-5 minutes after initiation. Please wait.

>?
>- The console will not require verification within 30 minutes after you verify your identity again.
>- After an application is disabled/deleted, new users will be unable to enter the [rooms](https://intl.cloud.tencent.com/document/product/647/37714#room) under the application, but costs will still be incurred for existing users. You can force close the rooms using the [room closing](https://intl.cloud.tencent.com/document/product/647/34269) API.
>- After an application is disabled/deleted, its basic services (audio/video call, interactive live streaming) and value-added services (mixtranscoding, on-cloud recording, etc.) will become unavailable.
>- An application disabling/enabling/deleting operation takes effect 3-5 minutes after initiation.


## Tag
[Tags](https://intl.cloud.tencent.com/document/product/651/13334) are used to mark and sort your Tencent Cloud resources. For example, your company may have multiple business units, each using one or more TRTC applications. You can tag the applications with the information of the corresponding business units.

### Adding tags
1. In **[Application Management](https://console.cloud.tencent.com/trtc/app)**, click **Application Info** for the application whose tag information you want to modify.
2. In the **Tag** section on the **Application Info** tab page, click **Edit**.
![](https://main.qcloudimg.com/raw/faa1e34ad79109a665af1393b0cfeb5f.png)
3. In the dialog box that pops up, select a **tag key** and **tag value** created in **[Tag List](https://console.cloud.tencent.com/tag/taglist)**.
![](https://main.qcloudimg.com/raw/7189bab1421cb112881d20dfce1d31a8.png)
>? 
>- If existing tags do not meet your needs, you can create new tags in [Tag List](https://console.cloud.tencent.com/tag/taglist).
>- You can add multiple tags for an application by clicking **+Add**.
4. Click **OK** to save the information. A dialog box pops up telling you whether the operation is successful.

### Deleting tags
1. In **[Application Management](https://console.cloud.tencent.com/trtc/app)**, click **Application Info** for the application whose tag information you want to modify.
2. In the **Tag** section on the **Application Info** tab page, click **Edit**.
	![](https://main.qcloudimg.com/raw/a1af1f92b7c266cf9b3648dc149aa68e.png)
3. In the dialog box that pops up, find the tag you want to delete, and click the delete button on its right.
![](https://main.qcloudimg.com/raw/85ecd7649149a03d4b44faba367718e2.png)
4. Click **OK** to save the information. A dialog box pops up telling you whether the operation is successful.



## Documentation
- To create an application, see [Creating Application](https://intl.cloud.tencent.com/document/product/647/39077).
- To search for an application in the application list, see [Searching Application](https://intl.cloud.tencent.com/document/product/647/39078).
- To configure the functions of an application or view configuration information, see [Function Configuration](https://intl.cloud.tencent.com/document/product/647/39080).
- If you want to set an image as the background displayed during on-cloud stream mixing, you can add the image in **Material Management**. For detailed instructions, see [Material Management](https://intl.cloud.tencent.com/document/product/647/39081).
- To get the demo source code for a quick start, see [Quick Start](https://intl.cloud.tencent.com/document/product/647/39082).







