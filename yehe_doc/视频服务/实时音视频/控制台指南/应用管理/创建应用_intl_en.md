TRTC manages different businesses or projects by application. You can create different applications for your business or projects in the TRTC console to achieve data separation.

## Note
Each Tencent Cloud account can create up to 100 TRTC applications. 

## Creating Application
1. Log in to the [TRTC console](https://console.cloud.tencent.com/trtc) and click **Application Management** on the left sidebar.
![](https://main.qcloudimg.com/raw/a88a4f5fbb885b419edbcc98fbfbe029.png)
2. Click **Create Application**, enter an application name, and tag your application.
![](https://main.qcloudimg.com/raw/b5b2b29fe4117bd0c02808f3a9ca4f67.png)
> ? An application name can contain up to 15 characters. Only digits, letters, Chinese characters, and underscores are allowed.
3. Click **Confirm**.


## Viewing Application List
After an application is created, its information, including `SDKAppID`, application name, tag, service status, and creation time, is displayed in the application list.
![](https://main.qcloudimg.com/raw/0432fbcb57941feb8797c70dfd017ea4.png)

| Item  | Description  |
| ---------------------- | ---------------------- |
| SDKAppID | `SDKAppID` is the unique identifier of an application and is generated automatically upon application creation. It is a required parameter for calling audio APIs. |
| Application name | The name specified during application creation |
| Tag | Tags added in [Application Info](https://intl.cloud.tencent.com/document/product/647/39079). <br/>You can use tags to mark and sort your Tencent Cloud resources. For example, your company may have multiple business units, each using one or more TRTC applications. You can tag the applications with the information of the corresponding business units. |
| Service status | The service status of the application, which may be **Normal** or **Disabled**.<br/>If it is **Disabled**, please check whether your [package](https://console.cloud.tencent.com/trtc/package) has remaining minutes, and whether your [account](https://console.cloud.tencent.com/expense/overview) has overdue payment. |
| Creation time | Time when the application is created                                         |
| Operation | **Usage Statistics**, **Function Configuration**, **Application Info**    |



## Documentation
- To search for an application in the application list, see [Searching Application](https://intl.cloud.tencent.com/document/product/647/39078).
- To view the basic information of an application, see [Application Info](https://intl.cloud.tencent.com/document/product/647/39079).
- To configure the functions of an application or view configuration information, see [Function Configuration](https://intl.cloud.tencent.com/document/product/647/39080).
- If you want to set an image as the background displayed during on-cloud stream mixing, you can add the image in **Material Management**. For detailed instructions, see [Material Management](https://intl.cloud.tencent.com/document/product/647/39081).
- To get the demo source code for a quick start, see [Quick Start](https://intl.cloud.tencent.com/document/product/647/39082).
