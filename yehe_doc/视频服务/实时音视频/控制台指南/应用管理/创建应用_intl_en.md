TRTC manages different businesses or projects by application. You can create different applications for your business or projects in the TRTC console to achieve data separation.

## Note
Each Tencent Cloud account can create up to 100 TRTC applications.

## Creating Application
1. Log in to the [TRTC console](https://console.cloud.tencent.com/trtc) and click **Application Management** on the left sidebar.
![](https://main.qcloudimg.com/raw/ee125318641e0016ea0bae0d6951a2e3.png)
2. Click **Create Application** and enter an application name.
![](https://main.qcloudimg.com/raw/4b65679f0b045b660f11d18b799f5de8.png)
> ? An application name can contain up to 15 characters. Only digits, letters, Chinese characters, and underscores are allowed.
3. Click **Confirm**.


## Viewing Application List
After an application is created, its information, including SDKAppID, application name, tag, service status, and creation time, is displayed in the application list.
![](https://main.qcloudimg.com/raw/617da5aea2eaa92a75c043f8d1e3b1d3.png)

| Item  | Description  |
| ---------------------- | ---------------------- |
| SDKAppID | SDKAppID is the unique identifier of an application and is generated automatically upon application creation. It is a required parameter for calling audio APIs. |
| Application name | The name specified during application creation |
| Tag | Tags added in [Application Info](https://intl.cloud.tencent.com/zh/document/product/647/39079), <br/>used to mark and sort your Tencent Cloud resources. For example, your company may have multiple business units, each using one or more TRTC applications. You can tag the applications with the information of the corresponding business units. |
| Service status | The service status of the application, which may be **Normal** or **Disabled**.<br/>If it is **Disabled**, please check whether your [package](https://console.cloud.tencent.com/trtc/package) has remaining minutes, and whether your account has overdue payment. |
| Creation time | Time when the application is created                                         |
| Operation | **Usage Statistics**, **Function Configuration**, **Application Info**    |



## References
- To search for an application in the application list, see [Searching for Application](https://intl.cloud.tencent.com/zh/document/product/647/39078).
- To view the basic information of an application, see [Application Info](https://intl.cloud.tencent.com/zh/document/product/647/39079).
- To configure the functions of an application or view configuration information, see [Function Configuration](https://intl.cloud.tencent.com/zh/document/product/647/39080).
- To set an image as the background displayed during on-cloud stream mixing, add the image in **Material Management**. For details, see [Material Management](https://intl.cloud.tencent.com/zh/document/product/647/39081).
- To get the demo source code for a quick start, see [Quick Start](https://intl.cloud.tencent.com/zh/document/product/647/39082).
