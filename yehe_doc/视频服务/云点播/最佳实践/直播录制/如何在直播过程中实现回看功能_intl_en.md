Time-shift playback in live streaming is based on live recording, live streaming time shifting, and VOD accelerated distribution. After a live streaming starts, a viewer can choose a previous time point other than the current time to start watching. This is commonly used to play back highlights in sport events. Users can change the progress bar to view contents generated earlier than the current time without waiting until the end of the live streaming. At the same time, the live streaming stays the same and users can switch back to the live streaming.

## Features
- Users can specify the delay for playing live content, i.e., the difference between the playback start time and current time.
- Users can specify the bitrate for time shifting if a live stream is recorded in multiple bitrates.

## Prerequisites
- You have [signed up](https://intl.cloud.tencent.com/register) and [logged in to](https://intl.cloud.tencent.com/login) a Tencent Cloud account, and completed the identity verification. Unverified users cannot purchase instances of live streaming time shifting for Chinese mainland.
- You have activated the CSS service and added a [push domain name](https://intl.cloud.tencent.com/document/product/267/35970).

## Notes:
- To use time-shift playback, you need first enable the [time shifting](#time) feature.
- The smallest time-shift duration is 90s, which means there is a latency of over 90s in the playback content compared with the live streaming content.
- The time shifting feature is being beta tested and is not charged currently. However, the feature relies on live recording, so you will be charged a [live recording fee](https://intl.cloud.tencent.com/document/product/267/39605) and [storage and playback fees](https://intl.cloud.tencent.com/document/product/266/2838) for using the feature.

## Directions
### Step 1. Activate TRTC[](id:step1)
1. Log in to the [VOD console](https://console.cloud.tencent.com/vod/overview) and click **Activate Now**.
2. Check the checkbox to agree to the service agreement, and click **OK** to activate VOD service. Log in to the VOD console.


### Step 2. Add a domain name for time shifting[](id:step2)
To add the Tencent Cloud VOD domain name for time-shift playback, perform the following:
1. Log in to the [VOD console](https://console.cloud.tencent.com/vod/overview) and click **Distribution and Playback** > **Domain Name** in the left sidebar.
![](https://qcloudimg.tencent-cloud.cn/raw/f3a42999b551357b871b8b3381953ba1.png)
2. Click **Add Domain Name** and enter the VOD domain name. For more information, please see [Distribution and Playback Settings](https://intl.cloud.tencent.com/document/product/266/35572)
![](https://qcloudimg.tencent-cloud.cn/raw/167658ece2ff8138b1e3efdc53c5ebbc.png)

3. Configure the new domain CNAME.

### Step 3. Bind a recording template[](id:step3)
1. Log in to the [CSS console](https://console.cloud.tencent.com/live/config/record) and click **Feature Configuration** > **[Live Recording](https://console.cloud.tencent.com/live/config/record)**.
![](https://qcloudimg.tencent-cloud.cn/raw/712036b264c79e34f02655fa83488e0a.png)

2. Click **Create Recording Template** to create a recording template. For more information, please see [Recording Template Configuration](https://intl.cloud.tencent.com/document/product/267/34223).
![](https://qcloudimg.tencent-cloud.cn/raw/f3a89ef4c5b4ffded769dfcca0bb654b.png)
>!
>- Select HLS as the file type.
>- Set the file storage duration, which cannot be shorter than the [time-shift period](https://intl.cloud.tencent.com/document/product/267/31565).
2. Bind the recording template with the push domain name to be configured. For more information, please see [Recording Configuration](https://intl.cloud.tencent.com/document/product/267/34224).

### Step 4. Enable time shifting[](id:time)
You can [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=39&source=0&data_title=%E4%BA%91%E7%9B%B4%E6%92%AD%20%20CSS&step=1), select “CSS” and request to activate time shifting feature and provide the following parameters:
- VOD domain name for time-shift playback added in [Step 2](#step2).
- Recording template ID added in [Step 3](#step3).
- Set the time-shift period parameter `timeshift_dur`, which is measured in seconds.

>?
>- Time-shift period indicates how further back you can go in terms of time shifting. The maximum time-shift period allowed currently is 7 days.
>- The feature may not work exactly according to the period configured. We recommend you set the period a little longer than you actually need.
>- If the parameter is set to `7200` (2 hours), you will be able to request content generated since 2 hours ago. (i.e., the value range for the playback delay parameter `delay` is 90 seconds to 2 hours). If content generated more than 2 hours ago is requested, `HTTP 404` will be returned even if there is live streaming content.

## Playback Request
### Request URL format
```
http://[Domain]/timeshift/[AppName]/[StreamName]/timeshift.m3u8?delay=xxx
```

### Parameter description
| Parameter | Description |
|---------|---------|
| [Domain]       | The registered domain name of the time shifting feature, namely, the time-shift playback domain name you added to the VOD console.     |
| timeshift      | Fixed field which needs no modification                                           |
| [AppName]      | Application name. If your application name is `live`, then enter `live`.           |
| [StreamName]   | Stream name. Enter the name of the stream you request.                                |
| timeshift.m3u8 | Fixed field which needs no modification                                           |
| delay           | Playback delay (s). This parameter must be `90` or larger. It will be defaulted to `90` if the value specified is less than `90`.|

### Example
Suppose the time-shift domain name is `testtimeshift.com`, application name `live`, and stream name `SLPUrIFzGPE`. If you need to play back live content generated 5 minutes ago, the request URL should be:

`http://testtimeshift.com/timeshift/live/SLPUrIFzGPE/timeshift.m3u8?delay=300`
