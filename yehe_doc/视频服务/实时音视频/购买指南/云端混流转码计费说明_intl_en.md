>!
>- For accounts that created their first [application](https://intl.cloud.tencent.com/document/product/647/37714) in the TRTC console on or after November 1, 2020, billing starts from **November 1, 2020**.
>- For accounts that created their first [application](https://intl.cloud.tencent.com/document/product/647/37714) in the TRTC console before November 1, 2020, billing is postponed to **December 8, 2020**.
>- This document describes the relaying and transcoding fees for using [TRTC’s MCU cluster for On-Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618). If you relay TRTC streams to CSS and then mix the streams using the [live stream mixing](https://intl.cloud.tencent.com/document/product/267/37665) feature of CSS, CSS will charge you [live transcoding](https://intl.cloud.tencent.com/document/product/267/39604) fees.
>- If you push transcoded audio and video streams to CSS and [stream them to audience via CDNs](https://intl.cloud.tencent.com/document/product/647/35242), CSS will charge you based on the [traffic/bandwidth](https://intl.cloud.tencent.com/document/product/267/2818#.E6.B5.81.E9.87.8F.E5.B8.A6.E5.AE.BD) used.


<span id="Billing_items"></span>
## Usage Calculation

TRTC calculates your usage of the relaying and transcoding service by adding up the **durations** of the streams output by all applications under your account via the mixtranscoding MCU cluster. There are two types of durations: [video duration](#m_video) and [audio duration](#m_voice).

>!  A duration is calculated in seconds and daily cumulative seconds are converted to minutes for billing. A duration of less than one minute is calculated as one minute.

<span id="m_video"></span>
### Video duration
A video duration refers to the duration containing video images in a transcoding result. Videos are categorized by resolution as follows and billed accordingly:

| Category   | Output Resolution                   |
| ---------- | ---------------------------- |
| SD  | ≤ 640 × 480        |
| HD  | 640 × 480 - 1280 × 720       |
| FHD | > 1280 × 720     |

- If a segment of a transcoding result contains both video and audio, you will only pay for the video duration.
- A transcoded stream may contain video segments of different resolutions. TRTC checks the resolution at regular intervals (usually every 60 seconds) and updates its calculation when detecting a change in the resolution.

<span id="m_voice"></span>
### Audio duration

An audio duration refers to the duration containing only audio in a transcoding result.

<span id="Fixed_price"></span>
## Pricing
The TRTC On-Cloud MixTranscoding service is priced as follows:

| Codec | Item                   | Unit Price (USD/min)     |
| -------- | ------------------------ | ------------------- |
| Audio codec | Relaying and transcoding-audio            | 0.000799    |
| H.264    | Relaying and transcoding-H.264-SD    | 0.00228571  |
| H.264    | Relaying and transcoding-H.264-HD    | 0.00464286  |
| H.264    | Relaying and transcoding-H.264-FHD | 0.00899    |

<span id="Billing_method"></span>

## Billing Mode
TRTC On-Cloud MixTranscoding supports only **daily pay-as-you-go**. Fees for a day are deducted at 10 AM the next day.

<span id="Billing_examples"></span>
## Billing Example
>! The below example uses list prices. If you have signed a Tencent Cloud contract, prices specified in the contract will apply.

Assume that, on January 1, you used TRTC’s MCU cluster for On-Cloud MixTranscoding and output 1920 × 1080 and 640 × 360 videos of 100 minutes each using the H.264 codec, plus audio of 100 minutes using the audio codec.

**Analysis:**
- Video with a resolution of 1920 × 1080 falls under the FHD category and is therefore charged 0.00899 USD/min.
- Video with a resolution of 640 × 360 falls under the HD category and is therefore charged 0.00464286 USD/min.
- Audio is charged 0.000799 USD/min.

That means on January 2, you would be charged 0.00899 USD/min × 100 min + 0.00464286 USD/min × 100 min + 0.000799 USD/min × 100 min = 2.16 USD.

## References

- [Billing Overview](https://intl.cloud.tencent.com/document/product/647/34610)
- [Free Trial](https://intl.cloud.tencent.com/document/product/647/39784)
- [Billing of Interactive Live Audio Streaming](https://intl.cloud.tencent.com/document/product/647/39785)
- [Billing of Interactive Live Video Streaming](https://intl.cloud.tencent.com/document/product/647/39786)
- [Billing of Audio Calls](https://intl.cloud.tencent.com/document/product/647/39787)
- [Billing of Video Calls](https://intl.cloud.tencent.com/document/product/647/39788)
- [Billing of On-Cloud Recording](https://intl.cloud.tencent.com/document/product/647/38385)
- [Purchase Instructions](https://intl.cloud.tencent.com/document/product/647/35440)
- [FAQs](https://intl.cloud.tencent.com/document/product/647/39789)
