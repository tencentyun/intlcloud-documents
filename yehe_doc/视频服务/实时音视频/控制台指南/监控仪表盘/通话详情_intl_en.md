This document describes the information you can view on the details page of a particular call room in the monitoring dashboard.



## Directions

1. Log in to the TRTC console, click **[Monitoring Dashboard](https://console.cloud.tencent.com/trtc/monitor)**, and find the room whose call details you want to view.
2. Click the room ID or **View Call Details** on the right to go to the details page.
   ![](https://main.qcloudimg.com/raw/fb52699e808f400969a6816d5457cc4d.png)

## Information Displayed

### Basic information

- **Call room information:** the basic information of the call room, including **SDKAppID**, **Application Name**, **Room ID**, **User Count**, **Start Time - End Time**, and **Room Duration**.
  ![](https://main.qcloudimg.com/raw/417aecad2089acc5ac1f38480dba5d66.png)
- **Current time range:** the time range queried. The calls of up to 5 hours can be displayed per query.
  ![](https://main.qcloudimg.com/raw/9d8e9db11232fd9f4c19d60676551373.png)

### User list

This section shows the user information of the call, including user ID, role, type, region, stay in the selected time range, time of room entry and exit, length of stay, SDK version, SDK type, as well as device and network information.
![](https://main.qcloudimg.com/raw/d69b22d292699374390ca3909bd4669a.png)

| Item                       | Description                                                         |
| ---------------------------- | ------------------------------------------------------------ |
| User ID                      | By default, the recently joined 6 users are displayed. To display more than 6 users, click **Add user** or **View All Users**. Up to 20 users can be displayed.|
| User Role                     | Anchor or audience. Anchors can send and receive data, but audience can only receive data. |
| User Type                     | Upstream or downstream. A green up arrow means the user has sent data, and a yellow down arrow means the user has received data. |
| Region                         | The geographic location of the user                                         |
| User’s Stay in This Period | A blue segment represents the period when the user is in the room, and the gray segment represents the period when the user is not in the room. |
| Room In/Out Time               | The time of the user’s first entry and last exit                 |
| Duration                     | The length of the user’s stay in the room                                 |
| SDK Version                     | The version number of the user’s SDK                                |
| SDK Type                     | The platform or OS used by the user                               |
| Device                     | The model or number of the device used by the user                                   |
| Network                     | The network type used by the user (empty if the user uses WeChat Mini Program)                 |



### Data received and sent

A user in a call receives the data of other users while sending local data. It is therefore necessary to display the information of data going both ways. By default, the call details page of the monitoring dashboard displays statistics from the perspective of the **[receiver](#receive)**. You can also switch to the perspective of the **[sender](#send)**.

#### Receiver<span id="receive"></span>

![](https://main.qcloudimg.com/raw/36f243b1f17e2c5d2ef393530f2c714b.png)

- You can switch between four tabs: **All**, **Video**, **Audio**, and **Screen Sharing**. A tab is displayed only if the corresponding data is received.
- By default, the graph shows the data received from all remote users, which is marked by different colors. You can select a specific remote user to view the data received from that user.
- Red lines in the graph indicate network jitter. You can click **Select sender to view details** in the top right and select the corresponding user ID to check the details in [End-to-End Details](https://intl.cloud.tencent.com/zh/document/product/647/39071).
- If a long time span is displayed, you can use the mouse wheel to zoom in part of the graph to view the details of a specific point.



#### Sender<span id="send"></span>
![](https://main.qcloudimg.com/raw/67419d268bea1b7d8e0ba0b7c4a67164.png)
- You can switch between four tabs: **All**, **Video**, **Audio**, and **Screen Sharing**. A tab is displayed only if the corresponding data is sent.
- Red lines in the graph indicate network jitter. You can click **View details** in the top right to check the details in [End-to-End Details](https://intl.cloud.tencent.com/zh/document/product/647/39071).
- If a long time span is displayed, you can use the mouse wheel to zoom in part of the graph to view the details of a specific point.

