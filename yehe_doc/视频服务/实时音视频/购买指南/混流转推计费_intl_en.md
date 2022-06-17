This document describes the billing of MixTranscoding and relay to CDN.

If you have a contract with TRTC, the billing details in the contract will apply.

## Billable Items
To deliver content to viewers via a CDN, you need to relay TRTC streams to the CDN.
 ![img](https://qcloudimg.tencent-cloud.cn/raw/73a5c751bc87e73b28be8d3edf056796.png)

1. The anchor and co-anchoring audience members publish audio/video streams in a call or live stream.
2. The MixTranscoding server subscribes to the streams (UDP).
3. The MixTranscoding server mixes and transcodes the streams it receives.
4. The MixTranscoding server sends the result to a CDN.

Step 1 incurs TRTC basic service fees. For details, see [Billing of TRTC Basic Services](https://intl.cloud.tencent.com/document/product/647/42734).

Step 2 is not charged. Step 3 incurs MixTranscoding fees, and step 4 incurs relaying fees.

>! Special offer:
> In addition to making step 2 free, TRTC also waives relaying fees if you relay to Tencent Cloud’s live streaming system. This means you will only be charged MixTranscoding fees.

At the end of each month, TRTC adds up the total audio and video MixTranscoding durations (minutes) as well as the bandwidth (Mbps) used for relaying streams to third-party platforms or CDNs for all projects under your [account](https://console.intl.cloud.tencent.com/trtc). Note that video MixTranscoding durations are classified into eight categories based on aggregate resolution and are priced differently. Your monthly MixTranscoding fee is the MixTranscoding durations multiplied by their unit prices, and your monthly relaying fee is the bandwidth used for relaying multiplied by its unit price.

Cost formula:

**Monthly fee** = **MixTranscoding fee** + **Relaying fee**

### MixTranscoding fees
Mixing and transcoding audio and video streams will incur MixTranscoding fees.

A MixTranscoding duration is the duration during which streams are mixed. It does not change with the number of streams mixed. For example, if the video streams of user A and user B are mixed in a MixTranscoding task for five minutes, then the billable MixTranscoding duration will be five minutes, which will be charged according to the aggregate resolution of the task.

If multiple MixTranscoding tasks are started in a room, the durations of all tasks will be added up.

Cost formula:

**Monthly MixTranscoding fee** = **Audio duration** x **Unit price of audio MixTranscoding duration** + **Video durations of different categories** x **Unit price of the corresponding category**

>? If both audio-only streams and video streams are transcoded and mixed during a time period in a MixTranscoding task, the period will only be billed as a video MixTranscoding duration.

#### Pricing
The table below lists the unit prices of audio and video MixTranscoding durations:

<table>
     <tr>
         <th style="text-align:center">Category</th>
         <th style="text-align:center">Video Category</th>
         <th style="text-align:center">Price (USD/1,000 Min)</th>
 </tr>
     <tr>
         <td style="text-align:center">Audio</td>
         <td style="text-align:center">None</td>
         <td style="text-align:center">1.99</td>
 </tr>
  <tr>
         <td style="text-align:center" rowspan="4">H.264 video</td>
         <td style="text-align:center">HD</td>
         <td style="text-align:center">5.99</td>
 </tr>
     <tr>
         <td style="text-align:center">FHD</td>
         <td style="text-align:center">13.99</td>
 </tr>
     <tr>
         <td style="text-align:center">2K</td>
         <td style="text-align:center">25.99</td>
 </tr>
     <tr>
         <td style="text-align:center">2K+</td>
         <td style="text-align:center">69.99</td>
   <tr>
         <td style="text-align:center" rowspan="4">H.265 video</td>
         <td style="text-align:center">HD</td>
         <td style="text-align:center">17.99</td>
 </tr>
     <tr>
         <td style="text-align:center">FHD</td>
         <td style="text-align:center">37.99</td>
 </tr>
     <tr>
         <td style="text-align:center">2K</td>
         <td style="text-align:center">69.99</td>
 </tr>
     <tr>
         <td style="text-align:center">2K+</td>
         <td style="text-align:center">189.99</td>       
 </tr> 
</table>

According to the sum of the resolutions of all videos mixed, TRTC classifies the resolution of video MixTranscoding durations into the following four categories:

| Resolution | Range |
| :---------------- | :----------------------------------------------------------- |
| HD        | Aggregate resolution ≤ 921,600 (1280 x 720)                           |
| FHD | 921,600 (1280 × 720) ＜ aggregate resolution ≤ 2,073,600 (1920 × 1080) |
| 2K                | 2,073,600 (1920 x 1080) < Aggregate resolution ≤ 3,686,400 (2560 x 1440) |
| 2K+               | 3,686,400 (2560 x 1440) < Aggregate resolution ≤ 8,847,360 (4096 x 2160) |

For example, if a MixTranscoding task mixes two 960 x 720 video streams, the aggregate resolution is 960 x 720 + 960 x 720 = 1,382,400, which falls in the FHD category.

#### Billing examples
**Audio live streaming**

An anchor streamed audio-only content for 30 minutes and then co-anchored with someone for 30 minutes, during which the two anchors’ streams were mixed and then published to Tencent Cloud’s live streaming system.

In the first 30 minutes, because there was only one anchor, no MixTranscoding fees would be charged. In the 30 minutes afterward, there were two anchors who communicated over audio, so audio MixTranscoding fees would be charged.

MixTranscoding fee = 1.99 x 30/1,000 = 0.0597 USD

**Video live streaming**

Anchor A streamed video content at a resolution of 1920 x 1080 for 30 minutes and then co-anchored with anchor B over video for 10 minutes. Anchor B’s video resolution was 1280 x 720. The two anchors’ streams were mixed and then published to Tencent Cloud’s live streaming system.

For anchor A, his or her own video was displayed as the big image, and anchor B’s video appeared in a small window in the top right corner. The resolution of the video viewed by anchor A was 1920 x 1080. For anchor B, his or her own video was displayed in the large video window, and anchor A’s video appeared in a small window in the top right corner. The resolution of the video viewed by anchor B was 1280 x 720.

In the first 30 minutes, because there was only one anchor, no MixTranscoding fees would be charged. In the 10 minutes afterward, two anchors communicated over video, and two MixTranscoding tasks were started, which would be charged separately. The aggregate resolution of both tasks was 1920 x 1080 + 1280 x 720 = 2,995,200, and the H.264 codec was used, so the H.264 2K category would apply. Note that the applicable video category is not determined by the resolution of the output video.

MixTranscoding fee = 25.99 x 10/1,000 + 25.99 x 10/1,000 = 0.5198 USD

### Relaying fees
If you publish to Tencent Cloud’s live streaming system, we will not charge you relaying fees. If you publish to a third-party platform or CDN, relaying fees will be charged based on the bandwidth used.

Cost formula:

**Relaying fees** = **Monthly peak bandwidth** x **Unit price of relaying**

#### Pricing
The bandwidth used for relaying is priced as follows:

| Category | Price (USD/Mbps/Month) |
| :------- | :------------------- |
| Monthly peak bandwidth | 18.99               |

#### Billing examples
Suppose the bitrate of a stream you published to third-party platforms was 500 Kbps (the sum of the audio bitrate and video bitrate), and there were 10 relaying tasks at the peak on that day.
Daily peak bandwidth = 500 (Kbps) x 10 = 5,000 (Kbps) = 5 Mbps.

Suppose you used the relaying feature in June 2022, and the bandwidth used for relaying reached 5 Mbps at the peak.
Your relaying fee for June 2022 = 18.99 (USD/Mbps/month) x 5 (Mbps) = 94.95 USD.
