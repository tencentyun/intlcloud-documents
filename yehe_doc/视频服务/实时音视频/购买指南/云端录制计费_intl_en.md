This documents describes the billing mode of TRTC's [on-cloud recording feature](https://intl.cloud.tencent.com/document/product/647/45169).

If you have a contract with TRTC, the billing details in the contract will apply.



## Billable Items

TRTC calculates the total audio and video recording durations of all projects under your [account](https://console.intl.cloud.tencent.com/trtc) at the end of each month. Note that video recording durations are classified into four categories based on resolution and are priced differently. TRTC offers each account a [10,000-minute free package per month](https://intl.cloud.tencent.com/document/product/647/42735), which will be deducted from your total monthly duration. The remaining recording durations multiplied by their unit prices are your total monthly cost.

Cost formula:

**Monthly cost** = **Audio duration** × **Unit price of audio duration** + **Video durations of different categories** × **Unit price of the corresponding category**


### Duration

The duration usage of the TRTC on-cloud recording service is calculated from the start of recording to the end of recording. If both audio and video streams are recorded simultaneously, only video fees will be charged.

Video duration usage = total duration of all recording processes in the TRTC room

Audio duration usage = total duration of all recording processes in the TRTC room − video duration. During recording, a duration when video is not recorded will be calculated as audio recording duration regardless of whether audio is recorded.

The duration calculation is not related to the number of audio/video streams that are recorded. For example, if a recording process is started to simultaneously record the video streams of anchors A and B for 5 minutes, the duration billed will be 5 minutes, and fees will be charged based on the aggregate resolution of the two anchors.

The duration calculation is related to the number of recording processes. If multiple recording processes are started in the room concurrently, the duration of each process is calculated and included in the total usage of the month.

<br>

Recording service refers to the service on-cloud recording offers. A recording process is a task that is started and stopped using on-cloud recording APIs.

Please note that audio/video durations may be generated during recording because the recording server subscribes to audio and video streams in the room.

<br>


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

Video usage in TRTC is categorized into the following four types according to the aggregate resolution of all videos recorded in a recording task. The fees for each type are calculated separately:

| Video Usage Type | Aggregate Resolution of Recorded Videos |
| :---------------- | :----------------------------------------------------------- |
| HD        | Aggregate resolution ≤ 921,600 (1280 × 720)                           |
| FHD | 921,600 (1280 × 720) ＜ aggregate resolution ≤ 2,073,600 (1920 × 1080) |
| 2K                | 2,073,600 (1920 × 1080) < Aggregate resolution ≤ 3,686,400 (2560 × 1440) |
| 2K+               | 3,686,400 (2560 × 1440) < Aggregate resolution ≤ 8,847,360 (4096 × 2160) |

For example, if a recording process simultaneously records two video streams with a resolution of 960 × 720 each, the aggregate resolution will be 960 × 720 + 960 × 720 = 1,382,400, and the recording fees will be charged according to the FHD unit price.



## Billing Examples

This section describes how TRTC calculates aggregate resolution, durations, and costs.



Suppose you have a project named testRTC under your Tencent Cloud account. In addition to using audio/video services, the project also records and saves audio/video interactions through on-cloud recording. The usage is as follows:

**Example 1**

On February 11, 2022, four users made a video call that lasted for 5,000 seconds. One on-cloud recording process was started to record four audio streams.

Usage statistics: 5,000 seconds of audio duration usage in total.

**Example 2**

On February 12, 2022, four users made a video call that lasted for 5,000 seconds. Two on-cloud recording processes were started, one for single-stream recording and the other mixed-stream recording. Four audio streams were recorded in each process.

Usage statistics: 5,000 + 5,000 = 10,000 seconds of audio duration usage in total.

**Example 3**

On February 13, 2022, four users made a video call that lasted for 3,500 seconds. One on-cloud recording process was started to record four audio and video streams. Each video stream had a resolution of 640 × 360.

Usage statistics: 3,500 seconds of HD video duration usage in total.

| Streams Subscribed     | Resolution Calculation | Aggregate Resolution | Recording Usage Type |
| :--------------- | :--------------- | :------- | :----------- |
| Audio/Video streams of 4 anchors | 640 × 360 × 4    | 921,600  | HD    |

**Example 4**

On February 14, 2022, three users interacted over video for 1,800 seconds, and their video resolutions were 640 × 360, 1280 × 720, and 960 × 720 respectively. After 1,800 seconds, the fourth user entered the room and interacted for 540 seconds, and the user’s video resolution was 1920 × 1080. One on-cloud recording process was started to record the audio and video streams of all users throughout the process.

Usage statistics: 1,800 seconds of FHD video duration usage and 540 seconds of 2K + video duration usage.

| Streams Subscribed     | Resolution Calculation | Aggregate Resolution | Recording Usage Type |
| :--------------- | :----------------------------------------------- | :-------- | :----------- |
| Audio/Video streams of 3 anchors | 640 × 360 + 1280 × 720 + 960 × 720               | 1,843,200 | FHD |
| Audio/Video streams of 4 anchors | 640 × 360 + 1280 × 720 + 960 × 720 + 1920 × 1080 | 3,916,800 | 2K+          |

**Fee calculation**

| Billable Item (Recording Usage Type) | Total Duration Usage (Minutes) | Service Fees (USD) |
| :----------------------- | :----------------- | :------------------------- |
| Audio                     | 250                | (250/1000) × 1.49 = 0.3725 |
| HD               | 59                 | (59/1000) × 5.99 = 0.35341 |
| FHD            | 30                 | (30/1000) × 13.49 = 0.4047 |
| 2K+                      | 9                  | (9/1000) × 53.99 = 0.48591 |
| Total                     | -                  | 1.61652 ≈ 1.62             |



## Notes

### Accuracy of durations

TRTC calculates durations in seconds and converts monthly cumulative seconds to minutes for billing. Specifically, it adds up the audio and video durations (in seconds) for a month and divides them by 60. The results are **rounded up** to the nearest whole number. For example, if your account generated 59 seconds of audio duration and 61 seconds of video duration a month, you would be billed for 1 minute of audio duration and 2 minutes of video duration. The margin of error for monthly durations is smaller than 1 minute.

