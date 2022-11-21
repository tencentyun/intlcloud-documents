This document describes how to enable on-cloud recording of `TUICallKit` to help you archive and review important calls. Here, two schemes are provided: [automatic recording](#Option1) and [RESTful API-based recording](#Option2).

>? `TUICallKit` integrates multiple basic Tencent Cloud PaaS services, and its audio/video capabilities rely on [TRTC](https://www.tencentcloud.com/document/product/647/35078). To use the on-cloud recording feature of `TUICallKit`, you need to configure it in the [TRTC console ](https://console.tencentcloud.com/trtc/app).

[](id:Option1)
## Scheme 1. Automatic Recording (Recommended)

We recommend you use the automatic recording scheme. In this scheme, recording is not manually started or stopped by you. Instead, recording tasks are managed on the TRTC backend, and a call will be recorded automatically when there is an audio/video stream being upstreamed. You can integrate it quickly and easily as follows: 

1. Find the application of the target `SDKAppId` in [**Application Management**](https://console.tencentcloud.com/trtc/app) in the TRTC console and enter the **Function Configuration** page.

2. In the **On-Cloud Recording Configuration** card on the **Function Configuration** page, **enable the on-cloud recording** feature. In the **Global Auto-Recording Template** card, click **Create Template**. ![img](https://qcloudimg.tencent-cloud.cn/raw/8ea4cb2a816edfdc7e26816505a75eca.png)

3. We recommend the following configuration parameter settings for audio/video call business scenarios such as one-to-one and group calls. You can also customize the recording template as needed. ![img](https://qcloudimg.tencent-cloud.cn/raw/8f8a9d9d029d63fa2d70c1105630aa20.png)

>! Global recording can mix the streams of up to eight users. If a call involves more than eight users (including the local user), the stream of the last user cannot be recorded.

After the global automatic recording feature is enabled, when a call is answered and there is audio/video being upstreamed, a recording task will be triggered automatically, and recording will stop automatically when the call ends. If a user leaves the room due to poor network conditions or other exceptions, the recording backend will automatically stop the recording task based on the configured `MaxIdleTime` value (maximum idle time, which is five seconds by default) to avoid incurring unnecessary fees.

4. After the template is created, select **Global Auto-Recording**. 

[](id:Option2)
## Scheme 2. RESTful API-Based Recording

If the automatic recording scheme doesn't meet your needs, you can also use the more flexible RESTful API-based recording scheme. In this scheme, you can record and subscribe to a specified anchor in the room, customize the layout of mixed streams, and update the layout and subscription during recording. However, **using its features requires using it together with the business backend service and performing complex integration operations**:

1. Find the application of the target `SDKAppId` in [**Application Management**](https://console.tencentcloud.com/trtc/app) in the TRTC console and enter the **Function Configuration** page.

2. In the **On-Cloud Recording Configuration** card on the **Function Configuration** page, **enable the on-cloud recording** feature. **Manual custom recording**, i.e., the RESTful API-based recording mode, is selected by default. ![img](https://qcloudimg.tencent-cloud.cn/raw/8ea4cb2a816edfdc7e26816505a75eca.png)

3. Then, you can call the RESTful API [CreateCloudRecording](https://www.tencentcloud.com/document/product/647/46960) to start on-cloud recording. Here, we recommend you listen on the notification event of [TUICallObserver](https://www.tencentcloud.com/document/product/647/51007) to start recording when an audio/video call starts. Below is the Java code sample:

```java
TUICallEngine.createInstance(context).addObserver(new TUICallObserver() {
    @Override
    public void onCallBegin(TUICommonDefine.RoomId roomId, TUICallDefine.MediaType callMediaType, TUICallDefine.Role callRole) {
        // Tell your business backend to start a recording task by using the relevant RESTful API.
    }
});
```

4. Because a call may be hung up on the client due to an exception such as poor network conditions or process termination, to stop recording, we recommend you subscribe to the callback for the TRTC room status (for more information, see [Event Callbacks](https://www.tencentcloud.com/document/product/647/39558)) and call the RESTful API [DeleteCloudRecording](https://www.tencentcloud.com/document/product/647/46959) to stop the on-cloud recording task when receiving the callback for TRTC room dismissal. 

## FAQs

### 1. How do I view the detailed recording durations?

You can view the detailed recording durations on the [On-Cloud Recording](https://console.tencentcloud.com/trtc/statistics/cloud-record) page in the TRTC console.

### 2. How do I view recorded files?

Log in to the [VOD console](https://console.tencentcloud.com/vod), select **Video/Audio Management** on the left sidebar, click **Search by prefix** above the list, select **Search by prefix**, and enter the keyword in the search box. The recording filenames are in the following formats:

- The filename format of an MP4 single-stream recording file: `<SdkAppId>_<RoomId>_UserId_s_<UserId>_UserId_e_<MediaId>_<Index>.mp4`
- The filename format of an MP4 mixed-stream recording file: `<SdkAppId>_<RoomId>_<Index>.mp4`