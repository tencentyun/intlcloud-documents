
VOD will generate a bill daily for resources consumed the previous day, and the corresponding fees will be deducted at the same time. The default billing mode is daily pay-as-you-go. If you want to switch to monthly billing cycle, please contact sales. You can go to the [console](https://console.cloud.tencent.com/vod/overview) to view the actual VOD resource usage.
Overview:
- Billing cycle: Between 12:00 and 18:00 each day, VOD calculates your usage of the previous day, generates a bill, and deducts the fees.
- Billing mode: By default, VOD charges you on a daily basis. To switch to monthly billing, please contact sales.

Billable items:
- **Video storage**: the storage space taken up by the source video files and transcoded video files uploaded to Tencent Cloud VOD. This service is charged based on the storage space used and storage period.
- **Video transcoding**: basic transcoding of source video files stored in Tencent Cloud VOD. This service is charged according to the specification and duration of output files. A duration less than 1 minute is counted as 1 minute. Each transcoding task is billed only once according to the specification. No fees will be charged for failed transcoding.
- **Tencent Extreme Speed High Definition (TESHD)**: transcoding the source video files stored in the VOD into HD or FHD in TESHD. This service is charged according to the specification and duration of output files. A duration less than 1 minute is counted as 1 minute. Each transcoding task is billed only once according to the specification. No fees will be charged for failed transcoding.  
- **Video editing**: using the [ComposeMedia](https://intl.cloud.tencent.com/document/product/266/34127) and [EditMedia](https://intl.cloud.tencent.com/document/product/266/34126) APIs to process source video files stored in VOD. This service is charged according to the specification and duration of output files. A duration less than 1 minute is counted as 1 minute. Each transcoding task is charged only once according to the specification. No fees will be charged for failed transcoding.  
- **Video acceleration**: using CDN for acceleration during video playback. This service is charged based on the downstream traffic.

## Video Storage

#### Pricing
Video storage is priced differently **in and outside the Chinese mainland**.
Chinese mainland: 0.0006 (USD/GB/day)
Outside the Chinese mainland: 0.0009 (USD/GB/day)

#### Details

- Rules: You are charged for your daily peak storage usage in a service region.
- Billing formula: Daily storage fee = Peak storage usage (GB) × Unit price of the corresponding service region
- Billing example: Assume that you used the VOD storage service outside the Chinese mainland on January 1 and your usage reached 100 GB at the peak. On January 2, you would be charged:
  VOD storage fee on January 1 = 100 (GB) × 0.0009 (USD/GB) = 0.09 (USD)

>! You can delete stored files via the console to avoid incurring storage fees. Otherwise, storage fees will be incurred every day.

## Video Transcoding
VOD offers three types of video transcoding: basic transcoding, TESHD and [transcoding to adaptive bitrate streaming](https://intl.cloud.tencent.com/document/product/266/33942).

### Basic transcoding

#### Pricing

Basic transcoding is charged based on the duration and height (px) of the video generated after transcoding.

| Codec    | Resolution                            |  Unit Price (USD/min) |
| ---------  |:--------------------------------:|:---------------:|
| H.264      | 4K (height ≤ 2160 px）          | 0.0521           |
| H.264      | 2K (height ≤ 1440 px）           | 0.0242          |
| H.264      | FHD (height ≤ 1080 px）     | 0.0121          |
| H.264      | HD (height ≤ 720 px)        | 0.0061          |
| H.264      | SD (height ≤ 480 px)    | 0.003         |
| H.265      | 4K (height ≤ 2160 px）             |0.2521           |
| H.265      | 2K (height ≤ 1440 px）           | 0.126           |
| H.265      | FHD (height ≤ 1080 px）       | 0.063         |
| H.265      | HD (height ≤ 720 px)       |0.0315         |
| H.265      | SD (height ≤ 480 px)  | 0.0158          |
|Remuxing| -|0.0028|
|Audio transcoding|-|0.002|


#### Details

- Rules: You are charged based on the duration and specification of the video file generated after basic transcoding. Video specification is determined by the codec used and height (px) of the video generated. Remuxing and audio transcoding are charged based on output video duration.
- Billing formula: Video transcoding fee = Output video duration (min) × Unit price as per codec and resolution (USD/min)

#### Billing example
Suppose you used the VOD to transcode a video whose codec is H.264 on January 1. You transcoded it into two outputs of 2560 × 1440 and 1280 × 640 respectively for 100 minutes, and also transcoded it into an audio file for 100 minutes. You will need to pay the following fee on January 2:
Transcoding fees on January 1 = 0.0242 (USD/min) × 100 (min) + 0.0061 (USD/min) × 100 (min) + 0.002 (USD/min) × 100 (min) = 3.23 (USD)

>? The 2560 × 1440 video falls under the category of 2K (height ≤ 1440 px), so the unit price is 0.0242 (USD/min); the 1280 × 640 video falls under the category of HD (480 px ≤ height ≤ 720 px), so the unit price is 0.0061 (USD/min); the unit price for audio transcoding is 0.002 (USD/min). The fee charged is the costs of the three tasks combined.

For more billing examples, see [Billing Examples](https://intl.cloud.tencent.com/document/product/266/38163).

### Tencent Extreme Speed High Definition (TESHD)
To learn about TESHD, see [Video Transcoding Service](https://intl.cloud.tencent.com/document/product/266/7898#teshd).
#### Pricing

TESHD transcoding is charged based on the duration and height (px) of the video generated after transcoding.

|Codec|Resolution|Unit Price (USD/min)|
|----------|-----------|-----------|
|H.264|4K (height ≤ 2160 px)  |0.1721|
|H.264|2K (height ≤ 1440 px)|0.08|
|H.264|FHD(height ≤ 1080 px)|0.04|
|H.264|HD(height ≤ 720 px)|0.02|
|H.264|HD(height ≤ 480 px)  |0.01 |
|H.265|4K (height ≤ 2160 px)|0.8319 |
|H.265|2K (height ≤ 1440 px)|0.416|
|H.265|FHD(height ≤ 1080 px)   |0.208|
|H.265|HD(height ≤ 720 px)  |0.104|
|H.265|SD(height ≤ 480 px)|0.052|


>!
>- TESHD transcoding is billed according to the resolution and duration of the output video.
>- Rules: You are charged based on the duration and specification of the video file generated after TESHD transcoding. Video specification is determined by the codec used and height (px) of the video generated.
>- Prices are listed according to the daily billing cycle. If you want to use monthly billing cycle, please contact sales for pricing.
>- Billing rules are the same as those for the basic transcoding.



### Adaptive bitrate streaming

#### Pricing

Adaptive bitrate streaming is charged based on the duration and specification of the video generated after transcoding. Video specification is determined by the codec used and height (px) of the video generated.
#### Details

**Billing rules are the same as those of basic transcoding**. Videos of different specifications in the output are charged separately according to their resolutions.
#### Billing example

Suppose you used VOD to transcode a video into outputs of adaptive bitrate streaming on January 1. The template contains three output specifications, namely, FHD (1920 × 1080), HD (1280 × 720) and SD (640 × 480), and the transcoded video duration of each output is 100 minutes. You will be required to pay the following transcoding fee on January 2:
Transcoding fee on January 1 = 0.0121 (USD/min) × 100 (min) + 0.0061 (USD/min) × 100 (min) + 0.003 (USD/min) × 100 (min) = 2.21 (USD)

>? As the original video is transcoded into videos of three specifications, the overall transcoding fee is the sum of charges for the three videos.



## Video Editing

#### Pricing
- Video editing is billed according to the codec, duration, and resolution of the output file.
- The resolution-based unit prices for video editing are the same as those for [basic transcoding](#p2).

#### Details
- Rules: Charges are based on the resolution and duration of the output file. **Each video editing task is billed once according to the specification**.
- Billing formula: Video editing fee = Output file duration (min) × Unit price (USD/min) as per resolution and codec

#### Billing example
Suppose you used the VOD editing feature to splice video A (10 min, 640 × 480) and video B (15 min, 1280 × 720) on January 1, and the output video is C (25 min, 1280 × 720). You will need to pay the following fee on January 2:
Video editing fee on January 1 = 0.0061 (USD/min) × 25 (min) = 0.1525 (USD)
>? The codec used in above example is H.264. For more information about video editing, see [ComposeMedia](https://intl.cloud.tencent.com/document/product/266/34127) and [EditMedia](https://intl.cloud.tencent.com/document/product/266/34126).


## Video Acceleration
Charges of video acceleration differ in and outside the Chinese mainland.
- In the Chinese mainland, fees are the same for all regions.
- Regions outside the Chinese mainland are divided into eight billing regions according to the location of Tencent Cloud CDN node servers, namely Asia Pacific Region 1, Asia Pacific Region 2, Asia Pacific Region 3, Middle East, Europe, North America, South America, and Africa, as shown below:

| Region         | Countries and Places  |
| ----------      |----------------|
| Asia Pacific Region 1   | Hong Kong (China), Macao (China), Vietnam, Singapore, Thailand           |
| Asia Pacific Region 2   | Taiwan (China), Japan, South Korea, Malaysia, Indonesia           |
| Asia Pacific Region 3   | Philippines, India, Australia, other Asia-Pacific countries and regions             |
| Middle East     | Saudi Arabia, United Arab Emirates, Turkey        |
| Europe     |United Kingdom, Russia, Germany, Italy, Ireland, France, Netherlands, Spain  |
| North America| United States, Canada        |
| South America | Brazil|
| Africa| South Africa             |
> ! CDN service fees for the Chinese mainland and regions outside the Chinese mainland are charged separately based on corresponding unit prices and usages.

#### Pricing
>? The daily pay-as-you-go mode supports only bill-by-traffic. If you want to pay monthly by bandwidth, please contact sales.

Video acceleration is billed daily based on a volume pricing model. The more traffic you use a day, the lower unit price you get. The pricing tiers are as follows:

| Traffic Tier (USD/GB) | Chinese Mainland |Asia Pacific Zone 1|Asia Pacific Zone 2|Asia Pacific Zone 3|Middle East|Europe|North America|South America|Africa|
| ----------|--------|---------|----------|----------|----------|----------|----------|----------|----------|
| 0 GB - 500 GB (inclusive)    | 0.038 |0.072|0.119|0.110|0.188|0.069|0.069|0.161|0.188|
| 500 GB - 2 TB (inclusive)    | 0.036 |0.067|0.110|0.100|0.172|0.061|0.061|0.154|0.172|
| 2 TB - 50 TB (inclusive)     | 0.034 |0.056|0.102|0.088|0.161|0.049|0.049|0.141|0.161|
|50 TB - 100 TB (inclusive)    | 0.031 |0.049|0.088|0.078|0.149|0.031|0.031|0.133|0.149|
| > 100 TB                     | 0.024 |0.044|0.081|0.069|0.133|0.025|0.025|0.125|0.133|


> ! For more information, see [Billing Examples](https://intl.cloud.tencent.com/document/product/266/38163#.E7.82.B9.E6.92.AD.E6.B5.81.E9.87.8F.E4.BD.BF.E7.94.A8.E9.A2.84.E4.BC.B0.E5.88.86.E6.9E.90).
#### Details

- Video acceleration is charged based on the accelerated downstream traffic and the acceleration region.

- Rules: You are charged daily based on the traffic accelerated by CDNs for video playback.
- Billing formula: Daily video acceleration fee = Video playback traffic (GB) × Traffic unit price (USD/GB) of the corresponding tier
- Billing example: Assume that you used the VOD acceleration service on January 1 to accelerate 550 GB of traffic for playback. On January 2, you would be charged:
  VOD traffic fee on January 1 = 0.038 (USD/GB) × 550 (GB)= 20.9 (USD)

## Remarks
If you have a large business volume (storage usage greater than 1 PB or daily traffic consumption over 10 TB), you can [contact sales](https://intl.cloud.tencent.com/contact-us) for more flexible and cost-effective billing options.
