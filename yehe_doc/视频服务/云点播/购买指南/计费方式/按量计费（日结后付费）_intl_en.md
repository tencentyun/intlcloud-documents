
Each day VOD will push your bill for resources consumed in the previous day to you and deduct corresponding fees. Daily billing cycle is the default mode. If you want to switch to monthly billing cycle, please contact sales. You can go to the [console](https://console.cloud.tencent.com/vod/overview) to view the actual VOD resource usage.
Daily billing cycle overview:
- Billing cycle: daily billing cycle. Fees generated in current day are billed and deducted between 12:00 and 18:00 (UTC+8) the next day.
- Payment method: postpaid.

VOD billable items:
- **Video storage**: the storage space taken up by the source video files and transcoded video files uploaded to Tencent Cloud VOD. This service is charged based on storage capacity and storage period.
- **Video transcoding**: basic transcoding of source video files stored in Tencent Cloud VOD. This service is charged according to specification and duration of output files. A duration less than 1 minute is counted as 1 minute. Each transcoding task is billed only once according to the specification. No fees will be charged for failed transcoding.
- **Top speed codec transcoding**: transcoding the video source files stored in the VOD into HD or FHD in top speed. This service is charged according to specifications and durations of output files. A duration less than 1 minute will be calculated as 1 minute. Each transcoding task is billed only once according to the specification. No fees will be charged for failed transcoding.  
- **Video Editing**: using [Video Composition](https://intl.cloud.tencent.com/document/product/266/34127) and [Video Editing](https://intl.cloud.tencent.com/document/product/266/34126) APIs to process source files stored in the VOD. Fees are calculated according to specifications and durations of output files. A duration less than 1 minute will be counted as 1 minute. Each trancoding task is only charged once according to the specification. No fees will be charged for failed transcoding.  
**Video acceleration**: using CDN for acceleration during video playback. Fees are charged based on the downstream traffic.

## Video Storage

#### Pricing
Fees for VOD video storage are charged differently in **Chinese Mainland** and **outside Chinese Mainland**.
Storage price in Chinese mainland: 0.0006 (USD/GB)
Storage price outside Chinese mainland: 0.0009 (USD/GB)

#### Billing overview

- Rules: Pay-as-you-go. The peak daily storage capacity is used for billing.
- Billing formula: daily storage fee = peak storage capacity (GB) x unit price of corresponding service region
- Billing example: let’s assume you used VOD storage service outside Chinese mainland on January 1 with a peak storage capacity of 100 GB.  Fee to pay on January 2 is as follow:
  VOD storage fee on January 1 = 100 (GB) x 0.0009 (USD/GB) = 0.09 (USD)

>! If you do not want to incur storage fees, you can delete the stored files via the console. Otherwise, storage fees will be incurred every day.

## Video Transcoding
VOD offers three types of video transcoding: basic transcoding, top speed codec transcoding and [transcoding to adaptive bitrate streaming](https://intl.cloud.tencent.com/document/product/266/33942).

### Basic transcoding

#### Pricing

Charges are made according to the duration of output files and the resolution range of video short side.

| Codec    | Resolution                            |  Unit Price (USD/min) |
| ---------  |:--------------------------------:|:---------------:|
| H.264      | 4K (Short side ≤ 2160 px）          | 0.0521           |
| H.264      | 2K (Short side ≤ 1440 px）           | 0.0242          |
| H.264      | FHD (Short side ≤ 1080 px）     | 0.0121          |
| H.264      | HD (short side ≤ 720 px)        | 0.0061          |
| H.264      | SD (short side ≤ 480 px)    | 0.003         |
| H.265      | 4K (Short side ≤ 2160 px）             |0.2521           |
| H.265      | 2K (Short side ≤ 1440 px）           | 0.126           |
| H.265      | FHD (Short side ≤ 1080 px）       | 0.063         |
| H.265      | HD (Short side ≤ 720 px)       |0.0315         |
| H.265      | SD (Short side ≤ 480 px)  | 0.0158          |
|Remuxing| -|0.0028|
|Audio transcoding|-|0.002|


#### Billing overview

- Rules: Fees are billed according to the codec, the length of video short side and the duration of output file. Each transcoding task is billed only once according to the specification.
- Billing formula: video transcoding fee = output video duration (min) × transcoding unit price as per codec and resolution (USD/min)

#### Billing example
Let’s assume you used the VOD to transcode a video whose codec is H.264 on January 1. You transcoded it into two outputs of 2560 × 1440 and 1280 × 640 respectively for 100 minutes, and also transcoded it into an audio file for 100 minutes. Fee to pay on January 2 is as follows:
Transcoding fees on January 1 = 0.0242 (USD/min) x 100 (min) + 0.0061 (USD/min) x 100 (min) + 0.002 (USD/min) x 100 (min) = 3.23 (USD)
>? For the output video with 2560 × 1440 resolution, the short side is in the range of 2K (≤ 1440 px) and the unit price is 0.0242 (USD/min ); for the output video with 1280 × 640 resolution, the short side is 640 px which is less than 720 px (HD) and greater than 480 px (SD), so the unit price is 0.0061 (USD/min); and unit price for audio transcoding is 0.002 (USD/Minute). The overall fee is the sum of charges for the three tasks.

For more billing examples, see [Billing Examples](https://intl.cloud.tencent.com/document/product/436/6241).

### THSHD

#### Pricing

Charges are based on the output file duration and the resolution range of the video short side.

|Codec|Resolution|Unit Price (USD/min)|
|----------|-----------|-----------|
|H.264|4K (short side ≤ 2160 px)  |0.1721|
|H.264|2K (short side ≤ 1440 px)|0.08|
|H.264|FHD(short side ≤ 1080 px)|0.04|
|H.264|HD(Short side ≤ 720 px)|0.02|
|H.264|HD(Short side ≤ 480 px)  |0.01 |
|H.265|4K (short side ≤ 2160 px)|0.8319 |
|H.265|2K (short side ≤ 1440 px)|0.416|
|H.265|FHD(short side ≤ 1080 px)   |0.208|
|H.265|HD(short side ≤ 720 px)  |0.104|
|H.265|SD(short side ≤ 480 px)|0.052|


>!
>- The listed prices are for the daily billing cycle. If you want to use monthly billing cycle, please contact sales for pricing.
>- Billing rules are the same as those for the basic transcoding.

### Transcoding to adaptive bitrate streaming

#### Pricing

Charges are based on the output file duration and the resolution range of the video short side.
#### Billing overview

**Billing rules are the same as those of the basic transcoding**. Output videos of adaptive bitrate streaming have three specifications and the charges differ as per specification.
#### Billing example

Let’s assume you used VOD to transcode a video into outputs of adaptive bitrate streaming on January 1. The template contains three output specifications, namely, FHD (1920 × 1080), HD (1280 × 720) and SD (640 × 480), and the transcoded video duration of each output is 100 minutes. Transcoding fee to pay on January 2 is as follows:
Transcoding fee on January 2 = 0.0121 (USD/min) x 100 (min) + 0.0061 (USD/min) x 100 (min) + 0.003 (USD/min) x 100 (min) = 2.21 (USD)

>As the original video is transcoded into videos of three specifications, the overall transcoding fee is the sum of charges for the three tasks.


## Video Editing
#### Pricing
- Charges are based on the codec, duration and resolution of the output file.
- The unit prices as per resolution is the same as those of the [transcoding](#p2).

#### Billing overview
- Rules: Charges are based on the resolution and duration of the output file, **Each video editing task is billed once according to the specification**.
- Billing formula: video editing fee = output file duration (min) × unit price (USD/min) as per resolution and codec

#### Billing example
Let’s assume you used VOD editing feature to concatenate video A (10 min, 640 × 480) and video B (15 min, 1280 × 720) on January 1, and the output video is C (25 min, 1280 × 720). Fee to pay for video editing on January 2 is as follows:
Video editing fee on January 1= 0.0061 (USD/min) x 25 (min) = 0.1525 (USD)
>Codec of all videos in above example is H.264. For more information, see [Video Composition](https://intl.cloud.tencent.com/document/product/266/34127) and [[Video Editing](https://intl.cloud.tencent.com/document/product/266/34126).


## Video Acceleration
Charges of VOD video acceleration differ in Chinese mainland and outside Chinese mainland.
In Chinese mainland, fees are charged uniformly without discrimination for all regions.
Outside Chinese mainland, there are eight billing regions determined according to locations of Tencent Cloud CDN node servers. The eight regions are Asia Pacific Region 1, Asia Pacific Region 2, Asia Pacific Region 3, Middle East, Europe, North America, South America, and Africa.

| Regions         | Countries and Places  |
| ----------      |----------------|
| Asia Pacific Region 1   | Hong Kong (China), Macau (China), Vietnam, Singapore, Thailand           |
| Asia Pacific Region 2   | Taiwan (China), Japan, South Korea, Malaysia, Indonesia           |
| Asia Pacific Region 3   | Philippines, India, Australia, other Asia-Pacific countries and regions             |
| Middle East     | Saudi Arabia, United Arab Emirates, Turkey        |
| Europe     |United Kingdom, Russia, Germany, Italy, Ireland, France, Netherlands, Spain  |
| North America| United States, Canada        |
| South America | Brazil|
| Africa| South Africa             |
- CDN service fees for Chinese mainland and regions outside Chinese mainland are paid separately based on corresponding unit prices and usages.

#### Pricing
> You can only use bill-by-traffic mode for postpaid daily billing cycle. If you want to use the monthly billing cycle with bill-by-bandwidth mode, please contact sales.

Tencent VOD traffic is billed on a daily basis with a tiered pricing. The more traffic you use on each day, the lower the billing tier. Detailed tiered unit prices are as follows:

| Traffic Tier (USD/GB) | Chinese Mainland |Asia Pacific Zone 1|Asia Pacific Zone 2|Asia Pacific Zone 3|Middle East|Europe|North America|South America|Africa|
| ----------  |----------------|----------------|----------------|----------------|----------------|----------------|----------------|----------------|----------------|
|  0 GB - 500 GB (inclusive)   | 0.039             |0.113|0.125|0.125|0.163|0.071|0.071|0.169|0.169|
| 500 GB - 2 TB (inclusive)   | 0.038             |0.038|0.105|0.105|0.159|0.064|0.064|0.161|0.161|
| 2 TB - 50 TB (inclusive)   | 0.036            |0.097|0.099|0.099|0.154|0.051|0.051|0.156|0.156|
| 50 TB - 100 TB (inclusive)     | 0.033             |0.084|0.092|0.092|0.145|0.033|0.033|0.15|0.15|
| 50 TB - 100 TB (inclusive)     | 0.033             |0.084|0.092|0.092|0.145|0.033|0.033|0.15|0.15|

>For more information, see [Examples of VOD Traffic Usage Estimation](https://intl.cloud.tencent.com/document/product/266/38163#.E7.82.B9.E6.92.AD.E6.B5.81.E9.87.8F.E4.BD.BF.E7.94.A8.E9.A2.84.E4.BC.B0.E5.88.86.E6.9E.90).
#### Billing overview
- Rules: daily billing cycle based on the downstream traffic generated when CDN acceleration is used during video playback.
- Billing formula: daily video traffic fee = video playback downstream traffic (GB) × tier traffic unit price (USD/GB)
- Billing example: let’s assume you used VOD acceleration service on January 1 and the downstream traffic is 550 GB. Acceleration fee to pay on January 2 is as follows:
  VOD traffic fee on January 1 = 0.038 (USD/GB) * 550 (GB)=14.85 (USD)

## Remarks
If your business volume is so large ( with storage capacity greater than 1 PB or daily traffic consumption over 10 TB) that daily billing cycle cannot meet your needs. You can contact sales to negotiate the billing modes and prices.
