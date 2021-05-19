>!
>- For accounts that created their first [application](https://intl.cloud.tencent.com/document/product/647/37714) on the TRTC console on or after November 1, 2020, billing will start from **November 1, 2020**.
>- For accounts that created their first [application](https://intl.cloud.tencent.com/document/product/647/37714) on the TRTC console before November 1, 2020, billing is postponed to **December 8, 2020**.
>- This document describes billing for relayed transcoding of [On-Cloud MixTranscoding through the MCU cluster provided by TRTC](https://intl.cloud.tencent.com/document/product/647/34618). If you use the relayed push feature to push TRTC audio and video streams to LVB before using the [On-Cloud MixTranscoding feature provided by LVB](https://intl.cloud.tencent.com/document/product/267/37665), you will be charged [LVB transcoding](https://intl.cloud.tencent.com/zh/document/product/267/2818#.E5.9B.BD.E9.99.85.2F.E6.B8.AF.E6.BE.B3.E5.8F.B0.E5.B8.A6.E5.AE.BD.E8.AE.A1.E8.B4.B9) fees.
>- If you push transcoded audio and video streams to LVB and enable [CDN relayed live streaming](https://intl.cloud.tencent.com/document/product/647/35242) for viewers, you will be charged [traffic/bandwidth](https://intl.cloud.tencent.com/zh/document/product/267/2818#.E6.B5.81.E9.87.8F.E5.B8.A6.E5.AE.BD) fees.


<span id="Billing_items"></span>
## Usage Calculation Method

TRTC calculates your usage of the relayed transcoding service by adding up the **duration** of the streams produced through MCU On-Cloud MixTranscoding by all the applications in your Tencent Cloud account. Depending on the encoding methods and transcoding results, the duration is classified into [video duration](#m_video) and [audio duration](#m_voice).

>!  The duration is calculated in seconds and daily cumulative seconds are converted to minutes for billing. Duration shorter than one minute will be calculated as one minute.

<span id="m_video"></span>
### Video duration
A video duration refers to the duration containing video images in a transcoding result. Videos are categorized by resolution as follows and billed accordingly:

| Category   | Output Resolution                   |
| ---------- | ---------------------------- |
| Standard definition (SD)  | 640×480 or lower        |
| High definition (HD)  | 640×480-1280×720       |
| Full high definition (FHD) | Higher than 1280×720     |

- If a stream in a transcoding result contains both video and audio, you will only pay for the video duration.
- A transcoded stream may contain video segments of different resolutions. TRTC checks the resolution at regular intervals (usually every 60 seconds) and updates its calculation when detecting a change in the resolution.

<span id="m_voice"></span>
### Audio duration

An audio duration refers to the duration containing only audio in a transcoding result.

<span id="Fixed_price"></span>
## Pricing
The TRTC On-Cloud MixTranscoding service is priced as follows:

| Codec | Item                   | Unit Price (USD/min)     |
| -------- | ------------------------ | ------------------- |
| Audio codec | Relayed transcoding-audio            | 0.000799 USD/min   |
| H.264    | Relayed transcoding-H264-SD    | 0.00228571 USD/min |
| H.264    | Relayed transcoding-H264-HD    | 0.00464286 USD/min |
| H.264    | Relayed transcoding-H264-FHD | 0.00899 USD/min    |

<span id="Billing_method"></span>

## Billing Method
TRTC On-Cloud MixTranscoding supports only **pay-as-you-go daily billing**. Fees for the day will be deducted at 10 AM the next day.

<span id="Billing_examples"></span>
## Billing Examples
>!The below example uses list prices. If you have signed a Tencent Cloud contract, prices specified in the contract will apply.

You used the On-Cloud MixTranscoding service through the MCU cluster provided by TRTC on January 1, which produced 1920×1080 and 640×360 videos using the H.264 codec, each totaling 100 minutes, plus 100-minute audio using the audio codec.

**Analysis:**
- Video with a resolution of 1920×1080 falls under the FHD category and is therefore charged 0.00899 USD/min.
- Video with a resolution of 640×360 falls under the HD category and is therefore charged 0.00464286 USD/min.
- Audio is charged 0.000799 USD/min.

That means on January 2, the amount deducted from your payment account would be 0.00899 USD/min x 100 min + 0.00464286 USD/min x 100 min + 0.000799 USD/min x 100 min, which amounts to 2.16 USD.

## References

- [Billing Overview](https://intl.cloud.tencent.com/document/product/647/34610)
- [Basic Service Fees](https://intl.cloud.tencent.com/document/product/647/34610)
- [Value-added Service Fees](https://intl.cloud.tencent.com/document/product/647/34610)
- [On-Cloud Recording Billing Overview](https://intl.cloud.tencent.com/document/product/647/38385)
- [Notes for Arrears Processing](https://intl.cloud.tencent.com/document/product/647/34611)
