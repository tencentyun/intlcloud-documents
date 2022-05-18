This document describes how [audio call](https://intl.cloud.tencent.com/document/product/647/36066), [video call](https://intl.cloud.tencent.com/document/product/647/36066), and [interactive live audio/video streaming](https://intl.cloud.tencent.com/document/product/647/37286) are billed on a monthly basis.

You can use the [TRTC price calculator](https://intl.cloud.tencent.com/pricing/trtc/calculator) to estimate your cost.

If you have a contract with TRTC, the billing details in the contract will apply.

>? Cumulative video resolution applies to accounts whose first TRTC [application](https://intl.cloud.tencent.com/document/product/647/37714) is created on or after October 27, 2021.



## Billing Details

TRTC adds up the audio and video durations of all projects under your [account](https://console.intl.cloud.tencent.com/trtc) at the end of each month. Note that video durations are classified into four categories based on "cumulative video resolution" and are priced differently. TRTC offers each account a [10,000-minute free package per month](https://intl.cloud.tencent.com/document/product/647/42735), which can offset your monthly durations. The remaining durations multiplied by their unit prices are your total monthly cost.

### Formula

**Monthly cost** = **Audio duration** x **Unit price of audio duration** + **Video durations of different categories** x **Unit price of the corresponding category**

### Audio and video durations

The audio/video duration of a call is **the sum of the durations of all users**.

-   **Video duration**: If a user subscribes to video streams, video duration will be billed. Note that if a user subscribes to both audio and video streams, only video duration will be counted.
-   **Audio duration**: If a user does not subscribe to video streams, their duration will be counted as audio duration, regardless of whether they subscribe to audio streams. In other words, if a user subscribes to video streams, their duration will be billed as video duration; if they do not subscribe to video or audio streams, the duration of their stay in the room will still be billed as audio duration.

### Pricing

| Category          | Price (USD/1,000 Min) | Cumulative Video Resolution                                       |
| :---------------- | :------------------ | ------------------------------------------------------------ |
| Audio              | 0.99                | -                                                            |
| HD        | 3.99                | Resolution ≤ 921,600 (1280 x 720)                                 |
| Full HD | 8.99                | 921,600 (1280 x 720)＜ Resolution ≤ 2,073,600 (1920 x 1080)    |
| 2K            | 15.99               | 2,073,600 (1920 x 1080) ＜ Resolution ≤ 3,686,400 (2560 x 1440) |
| 4K            | 35.99               | 3,686,400 (2560 x 1440) ＜ Resolution ≤ 8,847,360 (4096 x 2160) |

For example, if a user subscribes to two 960 x 720 video streams, the user’s cumulative video resolution is 960 x 720 + 960 x 720 = 1,382,400, which falls in the category of FHD.



## Billing Example 1

This section uses an example to show you how TRTC calculates fees.

Assume that six users entered a room at the same time and communicated over video for 60 minutes.

There were three anchors (A, B, and C) in the room. The video resolution of A was 960 x 720, and that of B and C were both 640 x 480. Two of the audience members subscribed to the video streams of all anchors, while the other subscribed to audio only. A also shared the screen at a resolution of 1920 x 1080.

### Cumulative video resolution and duration of each user

The table below shows the cumulative resolution of videos received by each user, the categories the resolutions fall in, and their prices.

|User   | Streams Received                                  | Resolution  | Cumulative Resolution | Category | Duration (Min) |
| :---------------- | :-------------------------------------- | :-------------------------------------------- | :-------- | :----------- | ------------ |
| A (shared the screen) | B’s and C’s video streams                     | 640 x 480 x 2                                 | 614,400   | HD    | 60           |
| B            | A’s video and screen sharing streams + C’s video stream | (960 x 720) + (640 x 480) + (1920 x 1080)     | 3,072,000 | 2K       | 60           |
| C            | A’s video and screen sharing streams + B’s video stream | (960 x 720) + (640 x 480) + (1920 x 1080)     | 3,072,000 | 2K       | 60           |
| Audience 1            | A’s video and screen sharing streams + B’s and C’s video streams | (960 x 720) + (640 x 480 x 2) + (1920 x 1080) | 3,379,200 | 2K       | 60           |
| Audience 2            | A’s video and screen sharing streams + B’s and C’s video streams | (960 x 720) + (640 x 480 x 2) + (1920 x 1080) | 3,379,200 | 2K       | 60           |
| Audience 3            | Audio streams only              | -                                             | -         | Audio         | 60           |

The figure below shows the billing details:

![Billing example -2@2x](https://qcloudimg.tencent-cloud.cn/raw/b9284fc7114058229815f4ce13168aa3.png)

### Cost calculation

Formula: **Monthly cost** = **Audio duration** x **Unit price of audio duration** + **Video durations of different categories** x **Unit price of the corresponding category**

<table>
     <tr>
         <th style="text-align:center">Billable Item</th>
         <th style="text-align:center">Total Duration (Min) = Sum of User Durations</th>
         <th style="text-align:center">Unit Price (USD/1,000 Min)</th>
         <th style="text-align:center">Cost by Category (USD)</th>
         <th style="text-align:center">Total Cost (USD, rounded to 2 decimals) </th>
     </tr>
     <tr>
         <td style="text-align:center">HD</td>
         <td style="text-align:center">60 x 1 = 60</td>
         <td style="text-align:center">3.99</td>
         <td style="text-align:center">(60/1000) × 3.99 = 0.2394</td>
         <td style="text-align:center" rowspan="3">4.14</td>
     </tr>
     <tr>
         <td style="text-align:center">2K</td>
         <td style="text-align:center">60 x 4 = 240</td>
         <td style="text-align:center">15.99</td>
         <td style="text-align:center">(240/1000) x 15.99 = 3.8376</td>
     </tr>
 		 <tr>
         <td style="text-align:center">Audio</td>
         <td style="text-align:center">60 x 1 = 60</td>
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">(60/1000) x 0.99 = 0.0594</td>
     </tr>
</table>


## Billing Example 2

This section uses an example to show you how TRTC calculates fees.
Assume that six users entered a room at the same time and communicated over video for 60 minutes.
There were four anchors (A, B, C, and D) in the room. The video resolution of A, B, and C was 480 x 480, while D published only audio. One of the audience members subscribed to the video streams of all anchors, and the other subscribed to audio only.

### Cumulative video resolution and duration of each user

The table below shows the cumulative resolution of videos received by each user, the categories the resolutions fall in, and their prices.

| User   | Streams Received                                  | Resolution  | Cumulative Resolution | Category | Duration (Min) |
| ------ | --------------------------------------------- | ------------- | ---------- | ---------------- | ------------ |
| A | B’s and C’s video streams + D’s audio stream         | 480 x 480 x 2  | 460,800    | HD        | 60           |
| B | A’s and C’s video streams + D’s audio stream         | 480 x 480 x 2  | 460,800    | HD        | 60           |
| C | A’s and B’s video streams + D’s audio stream         | 480 x 480 x 2  | 460,800    | HD        | 60           |
| C | A’s, B’s, and C’s video streams         | 480 x 480 x 3  | 691,200    | HD        | 60           |
| Audience 1 | A’s, B’s and C’s video streams + D’s audio stream         | 480 x 480 x 3  | 691,200    | HD        | 60           |
| Audience 2 | Audio streams only                    | -             | -          | Audio             | 60           |

### Cost calculation

Formula: **Monthly cost** = **Audio duration** x **Unit price of audio duration** + **Video durations of different categories** x **Unit price of the corresponding category**

<table>
     <tr>
         <th style="text-align:center">Billable Item</th>
         <th style="text-align:center">Total Duration (Min) = Sum of User Durations</th>
         <th style="text-align:center">Unit Price (USD/1,000 Min)</th>
         <th style="text-align:center">Cost by Category (USD)</th>
         <th style="text-align:center">Total Cost (USD, rounded to 2 decimals) </th>
     </tr>
     <tr>
         <td style="text-align:center">HD</td>
         <td style="text-align:center">60 x 5 = 300</td>
         <td style="text-align:center">3.99</td>
         <td style="text-align:center">(300/1000) x 3.99 = 1.197</td>
         <td style="text-align:center" rowspan="3">1.26</td>
     </tr>
 		 <tr>
         <td style="text-align:center">Audio</td>
         <td style="text-align:center">60 x 1 = 60</td>
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">(60/1000) x 0.99 = 0.0594</td>
     </tr>
</table>


## Note

There are some other matters that merit your attention.

### Price calculator

You can use the [TRTC Price Calculator](https://intl.cloud.tencent.com/pricing/trtc/calculator) to estimate your cost.

### Accuracy of durations

TRTC calculates durations in seconds and converts monthly cumulative seconds to minutes for billing. Specifically, it adds up the audio and video durations (in seconds) for a month and divides them by 60. The results are **rounded up** to the nearest whole number. For example, if your account consumed 59 seconds of audio duration and 61 seconds of video duration in a month, you would be billed for 1 minute of audio duration and 2 minutes of video duration. The margin of error for monthly durations is smaller than 1 minute.

### Dual-stream resolution

In the dual-stream mode, a user’s resolution is calculated as follows:

- If the user subscribes to the high-quality stream, the resolution of the high-quality stream set by the sender will be used for the calculation of the cumulative resolution.
- If the user subscribes to the low-quality stream, the actual resolution of the video received will be used for the calculation of the cumulative resolution.

### Resolution of screen sharing

The resolution set in `TRTCVideoEncParam` is used for the billing of screen sharing duration. For how to set the resolution, see the documents below:

-   All platforms (C++): [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ab1fc5a303726a666d30051c836e33fdd)
-   iOS: [startScreenCaptureInApp](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#abf51acf26b2212192f7145468886b791), [startScreenCaptureByReplaykit](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#abebcd402e310d5d7dcbef9f6b601cfc4)
-   macOS: [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a59b16baa51d86cc0465dc6edd3cbfc97)
-   Android: [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aacbe76e164030701d261a2edbc43668f)

On web, a target resolution may be unattainable due to device and browser restrictions, in which case the browser will adjust the resolution automatically to make it as close as possible to the target, and the actual resolution will be used for billing. For details, see [setScreenProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#setScreenProfile).

### Cost of using other products/services

If you use other Tencent Cloud products or TRTC services that are not video call or interactive live streaming, for example, [on-cloud recording](https://intl.cloud.tencent.com/document/product/647/45176), you will be charged additional fees. For details, see the billing documents of the corresponding products or TRTC services.
