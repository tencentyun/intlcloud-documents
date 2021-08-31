After creating an application, you can click **Application Info** to view its detailed information, including the basic information, relayed live streaming information, TRTC service status, and tags.

## Application Info
### Description
1. Log in to the TRTC console and click **[Application Management](https://console.cloud.tencent.com/trtc/app)** to view the application list.
2. Select the application whose information you want to view, and click **Application Info** on the right.
![](https://main.qcloudimg.com/raw/140eeec2a024881d78415a370b4a8f72.png)
3. View the basic information of the application in the **Application Info** section on the **Application Info** tab page.
![](https://main.qcloudimg.com/raw/a46256ac10d3cc75cb16f729b43db7ac.png)
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
1. In **[Application Management](https://console.cloud.tencent.com/trtc/app), click **Application Info** for the application whose information you want to modify.
2. In the **Application Info** section on the **Application Info** tab page, click **Edit**.
![](https://main.qcloudimg.com/raw/6e4bde40b65e7d8404252f325821e248.png)
3. In the dialog box that pops up, modify the **Application Name** or **Description**, and click **Modify** to save the information.
![](https://main.qcloudimg.com/raw/53835eaaf18af6eef5f967262438e987.png)
   > ? 
   > - **Application Name** can contain up to 15 characters. Only numbers, letters, Chinese characters, and underscores (_) are allowed.
   > - **Description** can contain up to 300 characters. Only numbers, letters, Chinese characters, and underscores (_) are allowed.



## Relayed Live Streaming Info
In relayed live streaming, TRTC uses relayed transcoding clusters to convert its UDP audio/video streams into RTMP streams in the cloud, which are then pushed to the standard CSS system and distributed through CDN. You will need the information here to implement [CDN Relayed Live Streaming](https://intl.cloud.tencent.com/document/product/647/35242).
![](https://main.qcloudimg.com/raw/9606f50bb11f2755b1746ad4c57d27b9.png)

## TRTC Service Status
This section shows the TRTC service status of the current application, which may be **Available** or **Unavailable**.
- **Available**: you can use TRTC services after purchasing a package.
![](https://main.qcloudimg.com/raw/ff72db0b4a215748f41367e37045c9ee.png)
- **Unavailable**: you cannot use TRTC services if you haven’t purchased a package.
![](https://main.qcloudimg.com/raw/a4c933c1ef07b1beba0609b166dfa187.png)

## Tag
[Tags](https://intl.cloud.tencent.com/document/product/651/13334) are used to mark and sort your Tencent Cloud resources. For example, your company may have multiple business units, each using one or more TRTC applications. You can tag the applications with the information of the corresponding business units.

### Adding tags
1. In **[Application Management](https://console.cloud.tencent.com/trtc/app)**, click **Application Info** for the application whose tag information you want to modify.
2. In the **Tag** section on the **Application Info** tab page, click **Edit**.
![](https://main.qcloudimg.com/raw/1997cdcbccb2cf93b8e445840663716e.png)
3. In the dialog box that pops up, select a **tag key** and **tag value** created in **[Manage Tags](https://console.cloud.tencent.com/tag/taglist)**.
![](https://main.qcloudimg.com/raw/e33e23ecf9ea2d488507744943db1313.png)
>? 
>- If existing tags do not meet your needs, click [Manage Tags](https://console.cloud.tencent.com/tag/taglist) to create new tags.
>- You can add multiple tags for an application by clicking **+Add**.
4. Click **OK** to save the information. A dialog box pops up telling you whether the operation is successful.

### Deleting tags
1. In **[Application Management](https://console.cloud.tencent.com/trtc/app)**, click **Application Info** for the application whose tag information you want to modify.
2. In the **Tag** section on the **Application Info** tab page, click **Edit**.
	![](https://main.qcloudimg.com/raw/6940f4a0f0a08634321fdd2453e1fb6d.png)
3. In the dialog box that pops up, find the tag you want to delete, and click the delete button on its right.
![](https://main.qcloudimg.com/raw/f2b1c6b4aab719038025acbfb4b48e24.png)
4. Click **OK** to save the information. A dialog box pops up telling you whether the operation is successful.



## References
- To create an application, see [Creating Application](https://intl.cloud.tencent.com/zh/document/product/647/39077).
- To search for an application in the application list, see [Searching for Application](https://intl.cloud.tencent.com/zh/document/product/647/39078).
- To configure the functions of an application or view configuration information, see [Function Configuration](https://intl.cloud.tencent.com/zh/document/product/647/39080).
- If you want to set an image as the background displayed during on-cloud stream mixing, you can add the image in **Material Management**. For details, see [Material Management](https://intl.cloud.tencent.com/zh/document/product/647/39081).
- To get the demo source code for a quick start, see [Quick Start](https://intl.cloud.tencent.com/zh/document/product/647/39082).









