> !
>
>- This document describes the relaying and transcoding fees for using [TRTC’s MCU cluster for On-Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618). If you relay TRTC streams to CSS and then mix the streams using the [live stream mixing](https://intl.cloud.tencent.com/document/product/267/37665) feature of CSS, CSS will charge you [live transcoding](https://intl.cloud.tencent.com/document/product/267/39604) fees.
>- If you push transcoded audio and video streams to CSS and [stream them to audience via CDNs](https://intl.cloud.tencent.com/document/product/647/35242), CSS will charge you based on the [traffic/bandwidth](https://intl.cloud.tencent.com/document/product/267/2818#.E6.B5.81.E9.87.8F.E5.B8.A6.E5.AE.BD) used.
>- If you have a contract with TRTC, the billing details in the contract will apply.

<span id="Billing_items"></span>

## Pricing

The TRTC On-Cloud MixTranscoding service is priced as follows:

| Codec | Billable Item                   | Unit Price (USD/1,000 Min, rounded to 3 decimals) |
| -------- | ------------------------ | --------------------------------------------- |
| Audio | Relaying & transcoding-audio            | 0.799                                         |
| H.264    | Relaying & transcoding-H.264-SD    | 2.296                                         |
| H.264    | Relaying & transcoding-H.264-HD    | 4.643                                         |
| H.264    | Relaying & transcoding-H.264-FHD    | 8.990                                         |

<span id="Billing_method"></span>

## Usage Calculation

TRTC calculates your usage of the relaying and transcoding service by adding up the **durations** of the streams output by all applications under your [account](https://console.intl.cloud.tencent.com/trtc) via the mixtranscoding MCU cluster. There are two types of durations: [video duration](#m_video) and [audio duration](#m_voice).

>! A duration is calculated in seconds and daily cumulative seconds are converted to minutes for billing. A duration less than 1 minute is calculated as 1 minute.

<span id="m_video"></span>

### Video duration

A video duration refers to the duration containing video images in a transcoding result. Videos are categorized by resolution as follows and billed accordingly:

| Category           | Output Resolution                                                |
| ------------------ | --------------------------------------------------------- |
| SD        | Resolution ≤ 307,200 (640 × 480)                         |
| HD        | 307,200 (640 × 480) < Resolution ≤ 921,600 (1280 × 720) |
| FHD | Resolution > 921,600 (1280 × 720)                        |

- If a segment of a transcoding result contains both video and audio, you will only pay for the video duration.
- A transcoded stream may contain video segments of different resolutions. TRTC checks the resolution at regular intervals (usually every 60 seconds) and updates its calculation when detecting a change in the resolution.

<span id="m_voice"></span>

### Audio duration

An audio duration refers to the duration containing only audio in a transcoding result.

<span id="Fixed_price"></span>

## Billing Example

Assume that, on January 1, user A used TRTC’s MCU cluster for On-Cloud MixTranscoding and output 1920 × 1080 and 640 × 360 videos of 100 minutes each using the H.264 codec, plus audio of 100 minutes.

Then on January 2, user A would be charged as follows:

<table>
     <tr>
         <th style="text-align:center">Output Resolution</th>
         <th style="text-align:center">Category</th>
         <th style="text-align:center">Duration (Min)</th>
         <th style="text-align:center">Unit Price (USD/1,000 Min)</th>
         <th style="text-align:center">Cost by Category (USD)</th>
         <th style="text-align:center">Total Cost (USD, rounded to 2 decimals)</th>
     </tr>
     <tr>
         <td style="text-align:center">1920 × 1080</td>
         <td style="text-align:center">FHD</td>
         <td style="text-align:center">100</td>
         <td style="text-align:center">8.990</td>
         <td style="text-align:center" >0.899</td>
         <td style="text-align:center" rowspan="3">1.44</td>
     </tr>
     <tr>
         <td style="text-align:center">640 × 360</td>
         <td style="text-align:center">HD</td>
         <td style="text-align:center">100</td>
         <td style="text-align:center">4.643</td>
         <td style="text-align:center">0.464</td>
     </tr>
     <tr>
         <td style="text-align:center">Audio</td>
         <td style="text-align:center">Audio</td>
         <td style="text-align:center">100</td>
         <td style="text-align:center">0.799</td>
         <td style="text-align:center">0.0799</td>
     </tr>
</table>

## Notes

This section provides extra information on the billing of On-Cloud MixTranscoding.

### Daily pay-as-you-go

TRTC On-Cloud MixTranscoding supports only **daily pay-as-you-go**. Fees for a day are deducted at 10 AM the next day.

<span id="Billing_examples"></span>
