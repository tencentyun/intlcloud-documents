Powered by the recording capability of CSS, the time shifting feature allows viewers to rewind and play back a video stream from earlier time points. When time shifting is enabled for a VOD playback domain, TS segment URLs and TS files for the video are saved in VOD, and the user can play back earlier video content by passing a time parameter in the request URL under the playback domain.



## How It Works
In HLS streaming, a video stream is split into TS segments. Viewers use an M3U8 file to access a TS segment URL, get the TS file, and play the video content starting from that TS segment.
>! TS files are not saved permanently, so there is a limit to how far back in time playback can start from.


## Note
The time shifting feature has been in beta testing so far. However, we will start charging for use of the feature starting from **00:00 on June 1, 2022**. For details, see [Notice: Time Shifting to Become Paid Feature](https://intl.cloud.tencent.com/document/product/267/46847). Time shifting relies on recording, so you will also be charged [live recording fees](https://intl.cloud.tencent.com/document/product/267/39605) by CSS and [storage and playback fees](https://intl.cloud.tencent.com/document/product/266/2838) by VOD.

## How to Use Time Shifting

### Prerequisites

-  You have [signed up for a Tencent Cloud account(https://intl.cloud.tencent.com/document/product/378/17985). 
-  You have activated CSS and added a [push domain name](https://intl.cloud.tencent.com/document/product/267/35970). 

[](id:step1)
### Step 1. Activate VOD

1. Log in to the [VOD console](https://console.cloud.tencent.com/vod/overview) and click **Activate Now**.
2. Select the checkbox to agree to the service agreement, and click **OK** to activate VOD.

[](id:step2)
### Step 2. Add a domain name

Follow the steps below to add a VOD domain name for time shifting:

1. Go to the VOD console and select **Distribution and Playback > Domain Name** on the left sidebar.
2. Click **Add Domain** and enter a VOD domain name that has been registered with an ICP filing number. For more information, see [Distribution and Playback Settings](https://intl.cloud.tencent.com/document/product/266/35572).
3. Add a CNAME record for the domain.

[](id:step3)
### Step 3. Bind a recording template

1. Go to the CSS console and select **Feature Configuration** > **[Live Recording](https://console.cloud.tencent.com/live/config/record)**.
2. Click **Create Recording Template**. For detailed directions for creating a recording template, see [Live Recording](https://intl.cloud.tencent.com/document/product/267/34223).
> ! 
> - Choose **HLS** as the recording format.
> - Enter a custom storage period, which cannot be shorter than the [time-shift duration](#step4).
3. Bind the recording template with the push domain you want to use. For detailed directions, see [Recording Configuration](https://intl.cloud.tencent.com/document/product/267/34224).

[](id:step4)
### Step 4. Enable time shifting

[Submit a ticket](https://console.cloud.tencent.com/workorder/category?step=0&source=0) to enable the time shifting feature. You need to select **CSS** as the product and provide the following information:

- The **VOD domain name** added in [Step 2](#step2).
- The ID of the recording template added in [Step 3](#step3).
- A custom value (seconds) for `timeshift_dur` (time-shift duration).
> ? 
> - The time-shift duration indicates how far back from the current time you can play back the video stream. Currently, the longest time-shift duration allowed is 7 days.
>- Given that the time-shift duration you configure may not exactly match the actual time-shift duration, we recommend you set the duration a little longer than you actually need.
>- For example, if the parameter is set to `7200` (2 hours), you will be able to request content generated 2 hours ago or later, and the value range for the playback delay parameter `delay` is 90 seconds to 2 hours. If `delay` is set to a value larger than 2 hours, `HTTP 404` will be returned even if there is live streaming content at that time point. 



## Playback Request

### Request URL format

```
http://[Domain]/timeshift/[AppName]/[StreamName]/timeshift.m3u8?delay=xxx
```

### Parameter description

| Parameter           | Description                                                         |
| -------------- | ------------------------------------------------------------ |
| [Domain]       | The VOD domain name added in [Step 2](#step2) for time shifting.     |
| timeshift      | A non-customizable parameter.                                           |
| [AppName]      | The application name. For example, if your application name is `live`, set this parameter to `live`.           |
| [StreamName]   | The stream name. Set this parameter to the name of the stream for which you want to enable time shifting.                                 |
| timeshift.m3u8 | A non-customizable parameter.                                           |
| delay          | The playback delay time (seconds). If you pass in a value smaller than `90`, `90` will be used.|

### Example

Suppose the time-shift domain name is `testtimeshift.com`, application name is `live`, and stream name is `SLPUrIFzGPE`. To play back video content from 5 minutes ago, you should use the following request URL:

```
http://testtimeshift.com/timeshift/live/SLPUrIFzGPE/timeshift.m3u8?delay=300
```
