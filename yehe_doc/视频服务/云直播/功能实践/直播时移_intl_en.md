Based on the live recording capability, the time shifting feature stores the TS (Transport Stream) segment addresses and TS files separately into the VOD system. A client can replay video content before the current time point by passing in a time parameter in the URL with the time-shift playback domain name.

## How It Works

In a common live broadcast in HLS format, the pushed video content is sliced into multiple TS segments. When a viewer watches it, the TS segment addresses are accessed by requesting the .m3u8 files to get the TS files. In this case, because the TS files are not persisted, the viewer cannot replay the live video content before the current time point.

## Notes

Fees for VOD traffic and storage will be incurred when you enable the time shifting feature.
## Usage of Time Shifting

### Prerequisites

-  You have [signed up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and verified your identity. 
-  You have activated the CSS service and added a [push domain name](https://intl.cloud.tencent.com/document/product/267/35970). 

<span id="step1"></span>

### Step 1. Activate VOD service

1. Log in to the [VOD console](https://console.cloud.tencent.com/vod/overview) and click **Activate Now**.
2. Select the checkbox to agree to the service agreement, and click **OK** to activate VOD service. Log in to the VOD console.
<span id="step2"></span>
### Step 2. Add a domain name of the time-shift playback

To add the Tencent Cloud VOD domain name for time-shift playback, perform the following:

1. Enter **VOD console** > **Distribution and Playback** > **Domain Name**.
2. Click **Add Domain** and enter the VOD domain name. For more information, please see [Distribution and Playback Settings](https://intl.cloud.tencent.com/document/product/266/35572).
3. Configure the new domain CNAME.
<span id="step3"></span>
### Step 3. Associate a recording template

1. Log in to the CSS console and go to **Feature Configuration** > **[Live Recording](https://console.cloud.tencent.com/live/config/record)**.
2. Click **Create Recording Template** to create a recording template. For more information, please see [Recording Configuration](https://intl.cloud.tencent.com/document/product/267/34223).
   > ! 
   >- Choose **HLS** for the file type.
   >- Define the file storage duration, which should be no less than the [time-shift duration](#step4).
3. Associate the recording template with the push domain name to be configured. For more information, please see [Recording Configuration](https://intl.cloud.tencent.com/document/product/267/31064).

<span id="step4"></span>
### Step 4. Activate the time shifting feature

Go to the [ticket system](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=39&source=0&data_title=%E4%BA%91%E7%9B%B4%E6%92%AD%20%20CSS&step=1) to submit a ticket. Select “CSS” and request to activate time shift feature and provide the following parameters:

- **VOD domain name for time-shift playback** added in [Step 2](#step2).
- Recording template ID added in [Step 3](#step3). 
- Define time-shift duration `timeshift_dur` in seconds
  > ? 
  >- Time-shift duration, which refers to the maximum time-shift duration (up to 7 days currently).
  >- The defined duration may not take accurately. We recommend that you adding a little buffer.
  >- Suppose the duration is configured as 7200 (2 hours), you will be able to request time-shifted contents generated less than 2 hours ago (`delay`, or the time-shift duration will range from 90 seconds to 2 hours). When any content generated more than 2 hours ago is requested, `HTTP 404` will be returned even if there is live streaming content. 



## Playback Request

**Request URL format**

```
http://[Domain]/timeshift/[AppName]/[StreamName]/timeshift.m3u8?delay=xxx
```

### Parameters

| Parameter           | Description                                                         |
| -------------- | ------------------------------------------------------------ |
| [Domain]       | The registered domain name of the time shifting feature, namely, the [time-shift playback domain name](#step2) you added to the VOD console.     |
| timeshift      | Fixed field which needs no modification                                           |
| [AppName]      | Application name. Suppose your application name is `live`, then enter `live`           |
| [StreamName]   | Stream name. You need fill in the stream name of your request                                 |
| timeshift.m3u8 | Fixed field which needs no modification                                           |
| delay           | The time-shift duration in seconds. This value is larger than or equals to 90. It will default back to 90 if the configured value is less than 90.

## Sample

Suppose current time-shift domain name is `testtimeshift.com`, time-shift application name is `live` and the stream name is `SLPUrIFzGPE`. If you need to play back live content generated five minutes ago, the request URL should be: 

```
http://testtimeshift.com/timeshift/live/SLPUrIFzGPE/timeshift.m3u8?delay=300
```
