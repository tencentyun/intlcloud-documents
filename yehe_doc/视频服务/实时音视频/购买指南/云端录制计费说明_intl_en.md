
>!
>- For Tencent Cloud accounts that created their first TRTC applications on or after July 1, 2020, on-cloud recording fees will be charged according to the billing rules described in this document.
>- For Tencent Cloud accounts that created TRTC applications before July 1, 2020, on-cloud recording fees will be charged according to the billing rules described in [CSS > CSS Recording](https://intl.cloud.tencent.com/document/product/267/39605).
>- This document only describes the billing rules for TRTC on-cloud recording. Recording files are saved on the VOD platform by default, which will charge **storage fees** and **viewing fees** based on your usage. For more information, please see [On-cloud Recording and Playback > Applicable Fees](https://intl.cloud.tencent.com/document/product/647/35426).
>- If you use the [On-Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618) feature before enabling on-cloud recording, additional transcoding fees will be incurred. For details, see [On-Cloud MixTranscoding Billing](https://intl.cloud.tencent.com/document/product/647/38929).

[](id:Billing_items)
## Usage Calculation Method

Tencent Cloud calculates an account’s on-cloud recording usage by adding up the **duration** of all recording files under the account. There are two types of recording durations: **video duration** and **audio duration**.

>!  Duration is calculated in seconds and daily cumulative seconds are converted to minutes for billing. A duration of less than one minute is calculated as one minute.


### Video duration
A video duration refers to the duration containing videos in a recording output file. Video durations are categorized by the following resolutions and billed accordingly.

|Video Type|Resolution|
|-------|--------|
|SD| ≤ 640 × 480|
|HD|640 × 480 - 1280 × 720|
|FHD| > 1280 × 720|


- If a duration contains both video and audio, it will be charged as a video duration.
- The resolutions of different durations in an output file may vary with the input resolutions. TRTC refreshes the resolution every five seconds and records the durations of different resolutions separately.


### Audio duration
An audio duration refers to the duration containing only audio in a recording output file.

[](id:Fixed_price)
## Service Pricing

Prices for TRTC on-cloud recording are listed below:

|Billable Item|Unit Price (USD/thousand minutes)|
|---|---|
|Audio|0.499|
|SD|0.99|
|HD|1.99|
|FHD|7.499|

[](id:Billing_method)
## Billing Mode
Only **pay-as-you-go daily billing** is supported. Fees incurred on a day are deducted at 10 AM the next day.

>!On-cloud recording works only when **CSS** and **VOD** are activated. Therefore, if your CSS or VOD service is suspended due to overdue payments, your on-cloud recording task will fail.

[](id:Billing_examples)
## Billing Examples
>!
>- The examples below use list prices. However, if you have signed a contract with Tencent Cloud sales, the prices specified in the contract will be applied instead.
>- By default, the audio and video streams of each user in a TRTC room are recorded as a separate file. You can also use the [On-Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618) feature to record the videos of multiple users in one file, for which you will be charged additional fees. For details, see [On-Cloud MixTranscoding Billing](https://intl.cloud.tencent.com/document/product/647/38929).

Suppose user A, B and C make a TRTC call for 10 minutes and the entire call is recorded. Below are the types and resolutions of the streams pushed.

|User|Stream Type|Resolution|Billable Item|
|---|---|---|---|
|A|Audio-only|None|Audio|
|B|Video+audio|640 × 360|SD|
|C|Video-only|1280 × 720|HD|

### Recording without stream mixing
If On-Cloud MixTranscoding is disabled, Tencent Cloud will generate three separate recording output files for A, B, and C, and the total recording fee for this call will be:
>A's recording fee + B's recording fee + C's recording fee = unit price of audio duration × A's audio duration + unit price of SD video duration × B's SD video duration + unit price of HD video duration × C's HD video duration = 0.499 USD/thousand minutes x 10 minutes/1,000 + 0.99 USD/thousand minutes × 10 minutes/1,000 + 1.99 USD/thousand minutes × 10 minutes/1,000 = 0.03479 USD.

### Recording after stream mixing

If On-Cloud MixTranscoding is enabled, the streams of A, B, and C will be mixed and recorded in one file, and the output video resolution will be 1280 × 720. The recording fee for this call will be:
> Unit price of HD video duration × HD video duration = 1.99 USD/thousand minutes × 10 minutes/1,000 = 0.0199 USD.

An additional fee will be charged for the use of On-Cloud MixTranscoding. For details, see [On-Cloud MixTranscoding Billing](https://intl.cloud.tencent.com/document/product/647/38929).

## Documentation
- [Billing Overview](https://intl.cloud.tencent.com/document/product/647/34610)
- [Basic Service Fees](https://intl.cloud.tencent.com/document/product/647/34610)
- [Value-added Service Fees](https://intl.cloud.tencent.com/document/product/647/34610)
- [On-Cloud Recording Billing](https://intl.cloud.tencent.com/document/product/647/38385)
- [On-Cloud MixTranscoding Billing](https://intl.cloud.tencent.com/document/product/647/38929)
- [Notes for Overdue Payment Processing](https://intl.cloud.tencent.com/document/product/647/34611)
