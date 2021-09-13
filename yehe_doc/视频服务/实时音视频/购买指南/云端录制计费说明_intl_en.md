
>!
>- For Tencent Cloud accounts that created their first TRTC applications on or after July 1, 2020, on-cloud recording fees will be charged according to the billing rules described in this document.
>- For Tencent Cloud accounts that created TRTC applications before July 1, 2020, on-cloud recording fees will be charged according to the billing rules described in [CSS > Live Recording](https://intl.cloud.tencent.com/document/product/267/39605).
>- This document only describes the billing rules for TRTC on-cloud recording. Recording files are saved in VOD by default, which will charge **storage fees** and **playback fees** based on your usage. For more information, please see [On-Cloud Recording and Playback > Billing](https://intl.cloud.tencent.com/document/product/647/35426).
>- If you use the [On-Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618) feature before on-cloud recording, you will incur additional transcoding fees. For details, see [Billing of On-Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/38929).

[](id:Billing_items)
## Usage Calculation

Tencent Cloud calculates an account’s on-cloud recording usage by adding up the **durations** of all recording files under the account. There are two types of recording durations: **video duration** and **audio duration**.

>!  A duration is calculated in seconds and daily cumulative seconds are converted to minutes for billing. A duration of less than one minute is calculated as one minute.


### Video duration
A video duration refers to the duration containing video in a recording output file. Video durations are categorized and billed based on resolution, as shown below.

|Video Type|Resolution|
|-------|--------|
|SD| ≤ 640 × 480|
|HD|640 × 480 - 1280 × 720|
|FHD| > 1280 × 720|


- If a duration contains both video and audio, it will be charged as a video duration.
- The resolutions of different durations in an output file may vary with the input resolutions. TRTC refreshes the resolution every five seconds and records durations of different resolutions separately.


### Audio duration
An audio duration refers to the duration containing only audio in a recording output file.

[](id:Fixed_price)
## Pricing

The prices of TRTC on-cloud recording are listed below:

|Billable Item|Unit Price (USD/1,000 min)|
|---|---|
|Audio|0.499|
|SD|0.99|
|HD|1.99|
|FHD|7.499|

[](id:Billing_method)
## Billing Mode
The on-cloud recording feature supports only **daily pay-as-you-go**. Fees for a day are deducted at 10 AM the next day.

>!On-cloud recording works only when **CSS** and **VOD** are activated. Therefore, if your CSS or VOD service is suspended due to overdue payments, your on-cloud recording task will fail.

[](id:Billing_examples)
## Billing Example
>!
>- The below examples use list prices. If you have signed a Tencent Cloud contract, prices specified in the contract will apply.
>- By default, the audio/video stream of each user in a TRTC room is recorded into a separate file. You can also use the [On-Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618) feature to record the videos of multiple users into one file, for which you will be charged additional fees. For details, see [Billing of On-Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/38929).

Assume that users A, B and C were in a TRTC call for 10 minutes and the entire call was recorded. Below are the types and resolutions of the streams pushed.

|User|Stream Type|Resolution|Billable Item|
|---|---|---|---|
|A|Audio-only|None|Audio|
|B|Video+audio|640 × 360|SD|
|C|Video-only|1280 × 720|HD|

### Recording without stream mixing
If On-Cloud MixTranscoding is disabled, Tencent Cloud will generate three separate recording output files for A, B, and C, and the total recording fee for this call will be:
>A's recording fee + B's recording fee + C's recording fee = Unit price of audio duration × A's audio duration + Unit price of SD video duration × B's SD video duration + Unit price of HD video duration × C's HD video duration = 0.499 USD/1,000 minutes × 10 minutes ÷ 1,000 + 0.99 USD/1,000 minutes × 10 minutes ÷ 1,000 + 1.99 USD/1,000 minutes × 10 minutes ÷ 1,000 = 0.03479 USD.

### Recording after stream mixing

If On-Cloud MixTranscoding is enabled, the streams of A, B, and C will be mixed and recorded into one file. Assume that the output resolution is 1280 × 720. The recording fee for this call will be:
> Unit price of HD video duration × HD video duration = 1.99 USD/1,000 minutes × 10 minutes ÷ 1,000 = 0.0199 USD

An additional fee will be charged for the use of On-Cloud MixTranscoding. For details, see [On-Cloud MixTranscoding Billing](https://intl.cloud.tencent.com/document/product/647/38929).

## References
- [Billing Overview](https://intl.cloud.tencent.com/document/product/647/34610)
- [Free Trial](https://intl.cloud.tencent.com/document/product/647/39784)
- [Billing of Interactive Live Audio Streaming](https://intl.cloud.tencent.com/document/product/647/39785)
- [Billing of Interactive Live Video Streaming](https://intl.cloud.tencent.com/document/product/647/39786)
- [Billing of Audio Calls](https://intl.cloud.tencent.com/document/product/647/39787)
- [Billing of Video Calls](https://intl.cloud.tencent.com/document/product/647/39788)
- [Billing of On-Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/38929)
- [Purchase Instructions](https://intl.cloud.tencent.com/document/product/647/35440)
- [FAQs](https://intl.cloud.tencent.com/document/product/647/39789)
