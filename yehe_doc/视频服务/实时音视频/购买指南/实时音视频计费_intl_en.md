# Billing of TRTC Basic Services

This document describes how [audio call](https://intl.cloud.tencent.com/document/product/647/36064), [video call](https://intl.cloud.tencent.com/document/product/647/36063), and [interactive live audio/video streaming](https://intl.cloud.tencent.com/document/product/647/36059) are billed on a monthly basis.

If you have a contract with TRTC, the billing details in the contract will apply.

## Billable Items

TRTC adds up the audio and video durations of all projects under your [account](https://console.intl.cloud.tencent.com/trtc) at the end of each month. Note that video durations are classified into three categories based on resolution and priced differently. TRTC offers each account a [10,000-minute free package per month](), which will be deducted from your total monthly durations. The remaining durations multiplied by their unit prices are your total monthly cost.

Cost formula:

**Monthly cost** = **Audio duration** × **Unit price of audio duration** + **Video durations of different categories** × **Unit price of the corresponding category**

### Duration

The audio/video duration of a call is **the sum of the durations of all users in the call**.

-   **Video duration**: If a user subscribes to video streams, video duration will be billed. Note that if a user subscribes to both audio and video streams, only video duration will be counted.
-   **Audio duration**: If a user does not subscribe to video streams, audio duration will be billed regardless of whether he or she subscribes to audio streams.

### Unit price

The table below lists the unit prices of audio and video durations:

| Duration          | Unit Price (USD/1,000 Min) |
| :---------------- | :------------------ |
| Audio              | 0.99                |
| SD        | 1.99                |
| HD        | 3.99                |
| FHD | 14.99               |

TRTC classifies video durations into three categories based on the aggregate resolution of all videos a user receives and prices them individually, as shown below:

| Category      | Resolution Range                                  |
| :---------------- | :-------------------------------------------------------- |
| SD        | Aggregate resolution ≤ 307,200 (640 × 480)                         |
| HD        | 307,200 (640 × 480) < Aggregate resolution ≤ 921,600 (1280 × 720) |
| FHD | Aggregate resolution > 921,600 (1280 × 720)                        |

For example, if a user subscribes to two 960 × 720 video streams, the aggregate resolution would be 960 × 720 + 960 × 720 = 1,382,400, which falls in the category of FHD.

## Prepaid Package

TRTC offers [general packages](), from which audio, SD video, HD video, and FHD video durations are deducted in the proportion of **1:1, 2:1, 4:1, and 15:1** respectively. For example, for 1 minute of HD video duration used, 4 minutes will be deducted from a general package.

Below are the prices of general packages:

<table>
     <tr>
         <th style="text-align:center">Package Type</th>  
         <th style="text-align:center">Package Duration (1,000 Min)</th> 
         <th style="text-align:center">List Unit Price (USD/1,000 Min)</th> 
         <th style="text-align:center">Package Unit Price (USD/1,000 Min)</th> 
         <th style="text-align:center">Package Price (USD)</th> 
          <th style="text-align:center">Discount</th> 
     </tr>
     <tr>
         <td style="text-align:center" rowspan="4">Fixed-time package</td>   
         <td style="text-align:center">25</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.960</td>
         <td style="text-align:center">24</td>   
         <td style="text-align:center">3% off</td>     
     </tr> 
     <tr>
         <td style="text-align:center">250 </td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.908</td>
         <td style="text-align:center">227</td>   
         <td style="text-align:center">8% off</td>   
     </tr> 
     <tr>
         <td style="text-align:center">1000 </td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.856</td>
         <td style="text-align:center">856</td>   
         <td style="text-align:center">13.5% off</td>   
     </tr> 
     <tr>
         <td style="text-align:center">3000</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.805</td>
         <td style="text-align:center">2416</td>   
         <td style="text-align:center">18.7% off</td>   
     </tr> 
     <tr>
         <td style="text-align:center" rowspan="5">Custom package</td>   
         <td style="text-align:center">0 < T < 25</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.99</td>
         <td style="text-align:center" rowspan="5">Package unit price × Package duration (T)</td>   
         <td style="text-align:center"> - </td>    
     </tr> 
     <tr>
         <td style="text-align:center">25 ≤ T < 250</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.960</td>
         <td style="text-align:center">3% off</td>    
     </tr> 
     <tr>
         <td style="text-align:center">250 ≤ T < 1000</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.908</td>
         <td style="text-align:center">8% off</td>   
     </tr> 
     <tr>
         <td style="text-align:center">1000 ≤ T < 3000</td>
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.856</td>
         <td style="text-align:center">13.5% off</td>   
     </tr> 
     <tr> 
         <td style="text-align:center">T ≥ 3000</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.805</td>
         <td style="text-align:center">18.7% off</td>   
     </tr> 
</table>

> ?
>- The package unit prices in the table are rounded up to 3 decimal places. However, in actual billing, unit prices are rounded to 8 decimal places.
>- Currently, you need to be on our allowlist to use TRTC prepaid packages. You can [contact us]() to add your account to the list.
>- If your monthly usage exceeds 3 million minutes on average, you can [contact us]() for deeper discounts.

## Billing Examples

This section describes how TRTC calculates aggregate resolution, durations, and costs.

Assume that 5 users entered the same room and interacted for 60 minutes. Users A, B, and C are in the role of “anchor”. User A sent video at a resolution of 960 × 720, while B and C both sent video at a resolution of 640 × 480. The other two users subscribed to all three anchors’ video streams. User A’s screen was shared with other users in the room. Both the send and receive resolution for screen sharing were 1920 × 1080.

### Aggregate resolution

The table below shows how to calculate each user’s aggregate resolution, which determines the category a user’s video duration falls in.

| User              | Streams Subscribed                 |  Resolution Calculation                              | Aggregate Resolution  | Category |
| :---------------- | :--------------------------- | :-------------------------------------------- | :-------- | :----------- |
| Anchor A (shared screen) | 2 anchors                     | 640 × 480 × 2                                 | 614,400   | HD    |
| Anchor B            | 2 anchors + Anchor A’s screen  | (960 × 720) + (640 × 480) + (1920 × 1080)     | 3,072,000 | FHD |
| Anchor C            | 2 anchors + Anchor A’s screen | (960 × 720) + (640 × 480) + (1920 × 1080)     | 3,072,000 | FHD |
| Audience 1            | 3 anchors + Anchor A’s screen | (960 × 720) + (640 × 480 × 2) + (1920 × 1080) | 3,379,200 | FHD |
| Audience 2            | 3 anchors + Anchor A’s screen | (960 × 720) + (640 × 480 × 2) + (1920 × 1080) | 3,379,200 | FHD |

### Cost

The table below shows how to calculate the total cost of the streaming session:

<table>
     <tr>
         <th style="text-align:center">Billable Item (Video Duration Category)</th>
         <th style="text-align:center">Total Duration (Min) = Sum of Users’ Durations</th>
         <th style="text-align:center">Unit Price (USD/1,000 Min)</th>
         <th style="text-align:center">Cost by Category (USD)</th>
         <th style="text-align:center">Total Cost (USD, rounded to 2 decimals) </th>
     </tr>
     <tr>
         <td style="text-align:center">HD</td>
         <td style="text-align:center">60</td>
         <td style="text-align:center">3.99</td>
         <td style="text-align:center">(60/1000) × 3.99 = 0.2394</td>
         <td style="text-align:center" rowspan="2">13.68</td>
     </tr>
     <tr>
         <td style="text-align:center">FHD</td>
         <td style="text-align:center">60 × 4 = 240</td>
         <td style="text-align:center">14.99</td>
         <td style="text-align:center">(240/1000) × 14.99 = 13.44</td>
     </tr>
</table>

## Notes

This section provides extra information on billing.

### Accuracy of durations

TRTC calculates durations in seconds and converts monthly cumulative seconds to minutes for billing. Specifically, it adds up the audio and video durations (in seconds) for a month and divides them by 60. The results are **rounded up** to the nearest whole number. For example, if your account generated 59 seconds of audio duration and 61 seconds of video duration a month, you would be billed for 1 minute of audio duration and 2 minutes of video duration. The margin of error for monthly durations is smaller than 1 minute.

### Dual-stream resolution

In the dual-stream mode, a user’s resolution is calculated as follows:

- If the user subscribes to the big-image stream, the resolution of the big-image stream set by the sender will be used for calculating aggregate resolution.
- If the user subscribes to the small-image stream, the actual resolution of video received will be used for calculating aggregate resolution.

### Resolution of screen sharing

The unit price of a screen sharing duration depends on the resolution set in `TRTCVideoEncParam`. For how to set the resolution, please see the documents below:

-   All platforms (C++): [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#ab1fc5a303726a666d30051c836e33fdd)
-   iOS: [startScreenCaptureInApp](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#abf51acf26b2212192f7145468886b791), [startScreenCaptureByReplaykit](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#abebcd402e310d5d7dcbef9f6b601cfc4)
-   macOS: [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a59b16baa51d86cc0465dc6edd3cbfc97)
-   Android: [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#aacbe76e164030701d261a2edbc43668f)

On web, a target resolution may be unattainable due to device and browser restrictions, in which case the browser will adjust the resolution automatically to make it as close as possible to the target, and the actual resolution will be used for billing. For details, please see [setScreenProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#setScreenProfile).

### Cost of using other products/services

If your application scenario involves TRTC products or services other than video call and interactive live streaming, for example, On-Cloud MixTranscoding, you will be charged additional fees. You can refer to the billing document of the corresponding product or service for details.
