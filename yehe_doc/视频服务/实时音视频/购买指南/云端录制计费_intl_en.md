This documents describes the billing mode of TRTC's [on-cloud recording feature](https://intl.cloud.tencent.com/document/product/647/45169).

If you have a contract with TRTC, the billing details in the contract will apply.



## Billable Items

TRTC calculates the total audio and video recording durations of all projects under your [account](https://console.intl.cloud.tencent.com/trtc) at the end of each month. Note that video recording durations are classified into four categories based on resolution and are priced differently. TRTC offers each account a [10,000-minute free package per month](https://intl.cloud.tencent.com/document/product/647/42735), which will be deducted from your total monthly duration. The remaining recording durations multiplied by their unit prices are your total monthly cost.

Cost formula:

**Monthly cost** = **Audio duration** × **Unit price of audio duration** + **Video durations of different categories** × **Unit price of the corresponding category**


### Duration

The duration usage of the TRTC on-cloud recording service is calculated from the start of recording to the end of recording. If both audio and video streams are recorded simultaneously, only video fees will be charged.

Video duration usage = amount of time the recording service records video in the TRTC room.

Audio duration usage = total amount of time recorded by the recording service in the TRTC room - video duration. Regardless of whether audio is recorded, it will be counted into audio duration usage.

The duration calculation is not related to the number of audio/video streams that are recorded. For example, if a recording task is started to simultaneously record the video streams of anchors A and B for 5 minutes, then the duration of the recording service will be 5 minutes, and fees will be charged based on the aggregate resolution in the task.

The duration calculation is related to the number of recording processes. If multiple recording tasks are started in the room concurrently, the duration of each task is calculated and included in the total usage of the month.


### Unit price

The unit prices of TRTC on-cloud recording are as follows:

<table>
     <tr>
         <th style="text-align:center">Type</th>
         <th style="text-align:center">Video Duration Type</th>
         <th style="text-align:center">Unit Price (USD/1,000 Min)</th>
 </tr>
     <tr>
         <td style="text-align:center">Audio recording</td>
         <td style="text-align:center">None</td>
         <td style="text-align:center">1.49</td>
 </tr>
  <tr>
         <td style="text-align:center" rowspan="4">Video recording</td>
         <td style="text-align:center">HD</td>
         <td style="text-align:center">5.99</td>
 </tr>
     <tr>
         <td style="text-align:center">FHD</td>
         <td style="text-align:center">13.49</td>
 </tr>
     <tr>
         <td style="text-align:center">2K</td>
         <td style="text-align:center">23.99</td>
 </tr>
     <tr>
         <td style="text-align:center">2K+</td>
         <td style="text-align:center">53.99</td>
 </tr> 
</table>

Video usage in TRTC is categorized into the following four types according to the aggregate resolution of all videos recorded and subscribed in the recording task. The fees for each type are calculated separately:

| Video Usage Type | Aggregate Resolution of Recorded Video |
| :---------------- | :----------------------------------------------------------- |
| HD        | Aggregate resolution ≤ 921,600 (1280 × 720)                           |
| FHD | 921,600 (1280 × 720) < Aggregate resolution ≤ 2,073,600 (1920 × 1080) |
| 2K                | 2,073,600 (1920 × 1080) < Aggregate resolution ≤ 3,686,400 (2560 × 1440) |
| 2K+               | 3,686,400 (2560 × 1440) < Aggregate resolution ≤ 8,847,360 (4096 × 2160) |

For example, if the recording service simultaneously records 2 video streams with a resolution of 960 × 720 each, then the aggregate resolution in the recording task will be 960 × 720 + 960 × 720 = 1,382,400, and the recording fees will be charged according to the FHD unit price.



## Billing Examples

This section describes how TRTC calculates aggregate resolution, durations, and fees.



Suppose you have a project named testRTC under your Tencent Cloud account. In addition to using audio/video services, the project also records and saves audio/video interactions through on-cloud recording. The usage is as follows:

**Recording 1**

Four users enter the channel and make a video call that lasts for 5,000 seconds. One on-cloud recording process is started, and 4 audio streams are recorded.

Usage statistics: 5,000 seconds of audio duration usage in total.

**Recording 2**

Four users enter the channel and make a video call that lasts for 5,000 seconds. Two on-cloud recording processes are started for single-stream recording and mix-stream recording respectively, and 4 audio streams are recorded in each process.

Usage statistics: 5,000 + 5,000 = 10,000 seconds of audio duration usage in total.

**Recording 3**

Four users enter the channel and make a video call that lasts for 3,500 seconds. One on-cloud recording process is started, and 4 audio/video streams are recorded, where each video stream has a resolution of 640 × 360.

Usage statistics: 3,500 seconds of HD video duration usage in total.

| Streams Subscribed                 |  Resolution Calculation                              | Aggregate Resolution  | Recording Usage Type |
| :--------------- | :--------------- | :------- | :----------- |
| Audio/Video streams of 4 anchors | 640 × 360 × 4    | 921,600  | HD    |

**Recording 4**

Three users enter the channel and interact over video for 1,800 seconds, and the video resolutions are 640 × 360, 1280 × 720, and 960 × 720 respectively. After 1,800 seconds, the fourth user enters the channel and joins the video interaction for 540 seconds, and the video resolution is 1920 × 1080. One on-cloud recording process is started to record the audio/video streams of all users throughout the process.

Usage statistics: 1,800 seconds of FHD video duration usage and 540 seconds of 2K+ video duration usage.

| Streams Subscribed                 |  Resolution Calculation                              | Aggregate Resolution  | Recording Usage Type |
| :--------------- | :----------------------------------------------- | :-------- | :----------- |
| Audio/Video streams of 3 anchors | 640 × 360 + 1280 × 720 + 960 × 720               | 1,843,200 | FHD |
| Audio/Video streams of 4 anchors | 640 × 360 + 1280 × 720 + 960 × 720 + 1920 × 1080 | 3,916,800 | 2K+          |

**Fees calculation**

| Billable Item (Recording Usage Type) | Total Duration Usage (Minutes) | Service Fees (USD) |
| :----------------------- | :----------------- | :------------------------- |
| Audio                     | 250                | (250/1000) × 1.49 = 0.3725 |
| HD               | 59                 | (59/1000) × 5.99 = 0.35341 |
| FHD            | 30                 | (30/1000) × 13.49 = 0.4047 |
| 2K+                      | 9                  | (9/1000) × 53.99 = 0.48591 |
| Total                     | -                  | 1.61652 ***\*≈\****1.62    |



## Notes

### Accuracy of durations

TRTC calculates durations in seconds and converts monthly cumulative seconds to minutes for billing. Specifically, it adds up the audio and video durations (in seconds) for a month and divides them by 60. The results are **rounded up** to the nearest whole number. For example, if your account generated 59 seconds of audio duration and 61 seconds of video duration a month, you would be billed for 1 minute of audio duration and 2 minutes of video duration. The margin of error for monthly durations is smaller than 1 minute.

