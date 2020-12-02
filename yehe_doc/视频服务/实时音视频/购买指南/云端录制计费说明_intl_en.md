
>!
- On-cloud recording fees will be charged according to the billing rules described in this document for Tencent Cloud accounts that created apps on the TRTC console on or after July 1, 2020. 
- For Tencent Cloud accounts that created apps on the TRTC console before July 1, 2020, on-cloud recording fees will be charged according to billing rules described in [Billing Details > LVB Recording](https://intl.cloud.tencent.com/zh/document/product/267/2818#.E7.9B.B4.E6.92.AD.E5.BD.95.E5.88.B6).
- This document only describes billing rules for TRTC on-cloud recording. VOD will charge **storage fees** and **viewing fees** of the recording output files saved on VOD platform based on your usage. For more information, please see [On-cloud Recording > Pricing](https://intl.cloud.tencent.com/document/product/647/35426).
- If you used LVB On-Cloud MixTranscoding feature before enabling on-cloud recording, additional fees for [LVB Transcoding > Standard transcoding](https://intl.cloud.tencent.com/zh/document/product/267/2818#.E7.9B.B4.E6.92.AD.E8.BD.AC.E7.A0.81) will be incurred.

<span id="Billing_items"></span>
## Usage Calculation Method

Tencent Cloud will charge the total **recording duration** of the output files of all on-cloud recordings under one Tencent Cloud account. There are two types of recording duration: **video duration** and **audio duration**, depending on your recording outputs.

>!  The duration will be calculated in seconds and daily cumulative seconds will be converted to minutes for billing. Duration less than one minute will be calculated as one minute.


### Video duration
A video duration refers to the duration containing video images in a recording output file. Videos will be categorized based on resolutions and will be billed accordingly. The categorization rules are as follows:
 
|Video Type|Resolution|
|-------|--------|
|SD| ≤ 640 × 480 (inclusive)|
|HD|640 × 480 - 1280 × 720 (inclusive)|
|FHD| > 1280 × 720|


- If both video and audio output files are generated for one recording task, you will only pay for the video duration.
- Resolutions of different durations in one output file may differ as the input resolutions may be modified during the recording. TRTC will record durations for billing in segments and refresh the resolution data every five seconds.


### Audio duration
An audio duration refers to the duration containing only audio in a recording output file.

<span id="Fixed_price"></span>
## Service Pricing

Fees for TRTC on-clouding recording are listed as follows:

|Billable Item|Unit Price (USD/thousand minutes)|
|---|---|
|Audio|0.499|
|SD|0.99|
|HD|1.99|
|FHD|7.499|

<span id="Billing_method"></span>
## Billing Mode
Only **pay-as-you-go daily billing** is supported. Fees for the day will be deducted at 10 AM the next day.

>!On-cloud recording only works when **LVB** feature is activated. Therefore, if the LVB service is suspended due to arrears, the on-cloud recording task will fail.

<span id="Billing_examples"></span>
## Billing Examples
>!
>- The below examples uses list prices.
>- By default, each user’s audio and video streams in one TRTC room will be recorded as separate files. If you want to record videos of multiple users in one room in one file, you can merge multiple video images into one using [On-Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618).

Suppose user A, B and C made a call in a TRTC room for 10 minutes and the entire call was recorded with push types and resolutions as follows:

|User|Upstream Push Type|Resolution|Billable Item|
|---|---|---|---|
|A|Audio-only|None|Audio|
|B|Video+audio|640 × 360|SD|
|C|Video-only|1280 × 720|HD|

### Billing example (without On-Cloud MixTranscoding usage)
Since on-Cloud MixTranscoding was not used, Tencent Cloud generated three separate recording output files for A, B, and C. The total recording fee for this call includes:
>A's recording fee + B's recording fee + C's recording fee = unit price of audio duration x A's audio duration + unit price of SD video duration × B's SD video duration + unit price of HD video duration × C's HD video duration = 0.499 USD/thousand minutes x 10 minutes/1,000 + 0.99 USD/thousand minutes × 10 minutes/1,000 + 1.99 USD/thousand minutes × 10 minutes/1,000 = 0.03479 USD.

### Billing example (with On-Cloud MixTranscoding usage)

When On-Cloud MixTranscoding is used, streams of A, B, and C will be mixed and recorded in one file, and the output video resolution will be 1280 × 720. The recording fee for this call will be:
> Unit price of HD video duration × HD video duration = 1.99 USD/thousand minutes × 10 minutes/1,000 = 0.0199 USD.

