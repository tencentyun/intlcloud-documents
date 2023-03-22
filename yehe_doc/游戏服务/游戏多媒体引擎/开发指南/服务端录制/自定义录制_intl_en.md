This document describes how to integrate the **GME server-side recording** feature through custom recording.



## Use Cases

GME provides **server-side recording** capabilities for voice chat audio streams to help you implement various scenarios, including content retention, management, and reproduction. In full recording mode, you can record all voice chat rooms in the application. In custom recording mode, you can record the specified room. In both recording modes, you can record the mixed stream by room or single stream by user. Recording files will be stored in **COS** under your account.

This document describes how to develop and integrate **custom recording**. To enable full recording for your application, see [Full Recording](https://www.tencentcloud.com/document/product/607/53747).

>! 
>- Using GME's server-side recording feature will incur recording service fees. Billing for this feature at Tencent Cloud International will officially start on April 1, 2023. For billing details, see [Purchase Guide](https://www.tencentcloud.com/document/product/607/50009).
>- Recording files will be stored in **COS** under your account, and **COS bills** will be generated based on your specific usage information such as storage volume, duration, and access frequency. For billing details, see [Billing Overview](https://www.tencentcloud.com/zh/document/product/436/16871).

## Prerequisites

- **You have activated the voice chat service** as instructed in [Activating Services](https://www.tencentcloud.com/document/product/607/10782).
- **You have activated the server-side recording service.** Currently, this feature is only available to allowed users. To try it out, contact us to add you to the allowlist.
- **You have integrated the GME SDK**, including core APIs and voice chat APIs. For more information, see [Quick Integration of Native SDK](https://www.tencentcloud.com/document/product/607/40858), [Quick Integration of SDK for Unity](https://www.tencentcloud.com/document/product/607/44544), and [Quick Integration of SDK for Unreal Engine](https://www.tencentcloud.com/document/product/607/44545).


## Service Architecture

![](https://staticintl.cloudcachetci.com/yehe/backend-news/zUFy538_PRELIM__%E6%B8%B8%E6%88%8F%E5%A4%9A%E5%AA%92%E4%BD%93%E5%BC%95%E6%93%8E_%E4%BA%A7%E5%93%81%E7%9B%AE%E5%BD%95_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US-2.png)

## Feature Overview

### 1. Recording scope
You can specify the ID of a room to record the mixed stream or a user in a room to record a single stream in the server API.
For the ID of the room to be recorded, you can specify players to be recorded in a allowlist and players not to be recorded in a blocklist through server API parameters.

### 2. Relevant APIs

- [ ***StartRecord()*** ](https://www.tencentcloud.com/document/product/607/53736)  **Starts recording**
This API is used to specify single-stream recording or mixed-stream recording, `RoomID` of the room to be recorded, and the subscribed allowlist/blocklist of user IDs.

- [ ***StopRecord()***](https://www.tencentcloud.com/document/product/607/53735)  **Ends recording**
This API is used to end recording for a `taskid`. If you don't record the `taskid`, you can use `DescribeTaskInfo()` to get the `taskid` of the ongoing recording task in the specified room.

- [***ModifyRecordInfo()***](https://www.tencentcloud.com/document/product/607/53737)  **Updates the recording information**
This API is used to update the recording information of a `taskid` such as recording type and subscribed allowlist/blocklist of user IDs. If you don't record the `taskid`, you can use `DescribeTaskInfo()` to get the `taskid` of the ongoing recording task in the specified room.

- [***DescribeTaskInfo()***](https://www.tencentcloud.com/document/product/607/53738) **Queries the room recording information**
This API is used to query the recording information of the specified room such as `taskid` of the ongoing recording task and subscribed allowlist/blocklist of user IDs.

- [***DescribeRecordInfo()***](https://www.tencentcloud.com/document/product/607/53739) **Queries the recording task information**
This API is used to query the task information of a `taskid` such as recording type, recorded room ID, recorded user ID, and recording file information.


### 3. Recording mechanism

#### Recording task start
- After the [***StartRecord()***](https://www.tencentcloud.com/document/product/607/53736)*** API is called, the specified room recording task will start.

#### Recording task ending
- After the [***StopRecord()***](https://www.tencentcloud.com/document/product/607/53735)***  API is called, the specified room recording task will stop.


#### Recording file generation time
- Room mixed-stream recording file: After a room recording task starts, if a user is in the room, the mixed-stream audio file will start to be generated immediately; otherwise, file generation will start immediately after the first user enters the room.
- User single-stream recording files: After a room recording task starts, if a user within the recording scope enters the room, the single-stream audio file of the user will start to be generated immediately.


#### Recording task segmentation

- If a single audio file lasts two hours or longer, it will be segmented automatically.
- If a user turns off the mic, the user's single-stream recording will be segmented automatically. After a user turns on the mic, a new segment will be generated.
- If an ongoing recording task is interrupted due to an exception, a new segment will be generated after the task restarts automatically.


#### Recording task event notification

- A recording task event will be notified to the configured callback URL through the callback mechanism. If such an event occurs, you will receive a callback notification such as **Recording started**, **Recording stopped**, or **The recording file has been uploaded**.
- For the specific callback information, see [Recording Callback Description](https://www.tencentcloud.com/document/product/607/53749).


### 4. Storage location

With GME's server-side recording, recording files will be stored in the specified bucket in **COS** under your account. You need to specify the bucket region. For the specific available regions, see [Regions and Access Endpoints](https://www.tencentcloud.com/document/product/436/6224).


### 5. Recording file format

- .mp3


### 6. Recording file naming convention

- User single-stream recording files: bizid_roomid_userid/${task start time}_${id}_audio.mp3
- Room mixed-stream recording file: bizid_roomid/${taskid}_${task start time}_${id}_audio.mp3

 ***bizid***: GME application ID, which can be obtained in the [GME console](https://console.tencentcloud.com/gamegme).
 ***roomid***: Voice chat room ID, which is defined and passed in to the GME SDK when you use the voice chat service.
 ***userid***: Player ID, which is defined and passed in to the GME SDK when you use the voice chat service.
 ***taskid***: Recording task ID, which is generated by the GME recording service. Each recording task has a unique task ID.
 ***id***: Serial number of a recording task segment, which starts from `0`.



## Integration directions

<dx-steps>
-<dx-tag-link link="#StartRealTimeASR" tag="business side">Configure the recording service in the console</dx-tag-link>
-<dx-tag-link link="#StartRealTimeASR" tag="business side">Call the server API to define the recording scope</dx-tag-link>
-<dx-tag-link link="#callback" tag="business side">Receive the recording task callback (optional)</dx-tag-link> 
-<dx-tag-link link="#result" tag="business side">View/Manage recording files</dx-tag-link>
</dx-steps>


### Step 1. Configure the recording service in the console

Log in to the [GME console](https://console.tencentcloud.com/gamegme), click **Service Management** on the left sidebar, locate the target application, and click **Set** to enter the **Details** page.
- #### Activating/Deactivating the recording service

![](https://qcloudimg.tencent-cloud.cn/raw/4d72f57ae8f4463bc009d8ef8048232e.png)


In the **Voice Recording Service** section, click **Modify** and select **Enable**.

When you activate the recording service for the first time, GME will request access to your **COS service**. You need to grant the access in the pop-up window to activate the server-side recording service.


![](https://qcloudimg.tencent-cloud.cn/raw/5e38302c5e3b0013ba53bd29af14fab2.png)

- #### Configuring the recording file storage location

Click **Bind** next to **Recording File Bucket**.
In the **Bind Bucket** pop-up window, you can bind an existing COS bucket (created in the [COS console](https://console.tencentcloud.com/cos/bucket) in advance) or create a bucket.

![](https://qcloudimg.tencent-cloud.cn/raw/30faa09353cdd31c537803f72bca25b2.png)

- #### Configuring the recording event callback (optional)
If you want to receive the event callbacks of the recording service, you can configure the callback URL. On the **Details** page, click **Modify** in the **Voice Recording Service** section and click **Modify** next to **Callback URL**. In the pop-up window, enter the URL for receiving callbacks. Currently, event callback messages are pushed only for the recording task completion status.

![](https://qcloudimg.tencent-cloud.cn/raw/cbc0275b887b6bd402f41f9f5c325a5b.png)

- #### Configuring the recording scope
You can select **Custom recording** or **Full recording** for **Recording Scope**. Here, you need to select **Custom recording**; otherwise, the server APIs will fail to be called.


After setting the above configuration items, click **Save**, and the recording service will be activated. If you no longer need the service, select **Disable** for the recording service in the console to avoid incurring additional fees.



### Step 2. Receive the recording task callback (optional)

If a callback URL is configured in **step 1**, you can receive recording task event callbacks.


### Step 3. Call the server API to define the recording scope
You need to call relevant APIs based on your actual business needs. When designing the call time sequence and process, note that:
- (1) You can initiate a request to start recording for an existing `RoomId` only. If the specified `RoomId` doesn't exist, the recording task will fail to be created.
- (2) If you don't actively call the API for stopping recording, the recording process will continue as long as there is a user in the room. If all users in the room have left, the original recording task process will continue for 12 hours, during which recording will start automatically when a user enters the room. After 12 hours, recording won't start automatically when a user enters the room.



### Step 4. View/Manage recording files

An audio file can be generated in several minutes after a recording task stops. You need to log in to the [COS console](https://console.tencentcloud.com/cos/bucket) to view and manage recording files.







