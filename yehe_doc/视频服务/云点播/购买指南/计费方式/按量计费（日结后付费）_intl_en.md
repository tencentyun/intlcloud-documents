## Notes:

- In the pay-as-you-go billing mode, fees are charged and postpaid based on the actual usage of each billable item, which can be viewed in the [VOD console](https://console.cloud.tencent.com/vod/overview).
- Overview:
  - Billing cycle: Between 12:00 and 18:00 each day, VOD calculates your usage of the previous day, generates a bill, and deducts the fees.
  - Settlement method: VOD settles fees daily by default. If you want to change to monthly settlement, [contact us](https://intl.cloud.tencent.com/contact-us).

Billable items:
- **Media asset storage**: The storage space taken up by the source video files uploaded to Tencent Cloud VOD and transcoded video files generated. This service is charged based on the storage space used and storage period.
- **Video transcoding**: General transcoding of source video files stored in Tencent Cloud VOD. This service is charged according to the specification and duration of output files. A duration less than 1 minute is counted as 1 minute. Each transcoding task is billed only once according to the specification. No fees will be charged for failed transcoding.
- **Tencent Extreme Speed High Definition (TESHD) transcoding**: Transcoding the source video files stored in the VOD into HD or FHD in TESHD. This service is charged according to the specification and duration of output files. A duration less than 1 minute is counted as 1 minute. Each transcoding task is billed only once according to the specification. No fees will be charged for failed transcoding.  
- **Video editing**: Using the [ComposeMedia](https://intl.cloud.tencent.com/document/product/266/34127) and [EditMedia](https://intl.cloud.tencent.com/document/product/266/34126) APIs to process source video files stored in VOD. This service is charged according to the specification and duration of output files. A duration less than 1 minute is counted as 1 minute. Each transcoding task is charged only once according to the specification. No fees will be charged for failed transcoding.  
- **Watermark removal**: Watermark removal of source video files stored in Tencent Cloud VOD. This service is charged according to the specification and duration of output files. A duration less than 1 minute is counted as 1 minute. Each transcoding task is billed only once according to the specification. No fees will be charged for failed transcoding.  
- **Video acceleration**: Using CDN for acceleration during video playback. This service is charged based on the downstream traffic.
- **Data retrieval:** for media assets stored in ARCHIVE or DEEP_ARCHIVE storage class, fees are charged based on the retrieval mode and retrieval volume.

## Media Asset Storage

### Pricing

<table>    
    <tr>         
        <th style="text-align:center">Storage Class</th>         
        <th style="text-align:center">Covered Regions</th>         
        <th style="text-align:center">Price (USD/GB/Day)</td> </tr>     
    <tr>         
        <td style="text-align:center" rowspan="2">STANDARD storage</td>         
        <td style="text-align:center">Chinese mainland</td>         
        <td style="text-align:center">0.0006</td> </tr>     
    <tr>         
        <td style="text-align:center">Outside the Chinese mainland (Silicon Valley, Hong Kong (China), Frankfurt, Moscow, Seoul, Virginia, Singapore, Mumbai, Toronto, Bangkok)</td>         
        <td style="text-align:center">0.0009</td>   </tr>     
    <tr>         
        <td style="text-align:center" rowspan="2">STANDARD_IA storage (for at least 30 days)</td>         
        <td style="text-align:center">Chinese mainland</td>         
        <td style="text-align:center">0.0004</td> </tr>     
    <tr>         
        <td style="text-align:center"> Outside the Chinese mainland (Silicon Valley, Hong Kong (China), Frankfurt, Moscow, Seoul, Virginia, Singapore, Mumbai, Toronto, Bangkok)</td>         
        <td style="text-align:center">0.0006</td> </tr>          
    <tr>         
        <td style="text-align:center" rowspan="2"> ARCHIVE storage (for at least 90 days)</td>         
        <td style="text-align:center">Chinese mainland</td>         
        <td style="text-align:center">0.0002</td> </tr>     
    <tr>         
        <td style="text-align:center">Outside the Chinese mainland (Silicon Valley, Hong Kong (China), Frankfurt, Moscow, Seoul, Virginia, Singapore, Mumbai, Toronto, Bangkok)</td>         
        <td style="text-align:center">0.0003</td>         </tr>    
    <tr>        
        <td style="text-align:center" rowspan="2">DEEP_ ARCHIVE storage (for at least 180 days)</td>        
        <td style="text-align:center">Chinese mainland</td>         <td style="text-align:center">0.00006</td> </tr>     
    <tr>         
        <td style="text-align:center">Outside the Chinese mainland (Silicon Valley, Hong Kong (China), Frankfurt, Moscow, Seoul, Virginia, Singapore, Mumbai, Toronto, Bangkok)</td>         
        <td style="text-align:center">0.0001</td>  </tr>      
 </table>

### Billing details

- Media asset storage is charged based on the actual content storage region and storage class. Media assets whose storage class is changed will be charged based on the new storage class.
- Rules: You are charged based on the actual storage class and daily peak storage space used **in the Chinese mainland and outside the Chinese mainland separately**.
- Billing formula: Daily storage space fee = Peak storage capacity in Chinese mainland (GB) x Storage class unit price (USD/GB/day) + Peak storage capacity outside Chinese mainland (GB) x Storage class unit price (USD/GB/day).

### Billing examples

Suppose you used the VOD storage service on January 1, where the peak STANDARD storage capacity in the Chinese mainland was 100 GB, and the peak STANDARD_IA storage capacity in Mumbai was 50 GB. You will need to pay the following fee on January 2:
VOD storage fee on January 1 = 100 (GB) x 0.0006 (USD/GB) + 50 (GB) x 0.0006 (USD/GB) = 0.06 (USD) + 0.03 (USD) = 0.09 (USD)

> !
> - You can delete stored files via the console to avoid incurring storage fees. Otherwise, storage fees will be incurred every day.
> - Minimum storage duration for STANDARD_IA files: 30 days
> - Minimum storage duration for ARCHIVE files: 90 days
> - Minimum storage duration for DEEP ARCHIVE files: 180 days

## Video Transcoding
VOD offers three types of video transcoding: General transcoding, TESHD transcoding, and [transcoding to adaptive bitrate streaming](https://intl.cloud.tencent.com/document/product/266/33942).

### General transcoding

#### Pricing

General transcoding is charged based on the duration and height (px) of the video generated after transcoding.

| Codec    | Resolution                            |  Unit Price (USD/min) |
| ---------  |:--------------------------------:|:---------------:|
| H.264      | 4K (height ≤ 2160 px)          | 0.0521           |
| H.264      | 2K (height ≤ 1440 px)           | 0.0242          |
| H.264      | FHD (height ≤ 1080 px)     | 0.0121          |
| H.264      | HD (height ≤ 720 px)        | 0.0061          |
| H.264      | SD (height ≤ 480 px)    | 0.003         |
| H.265      | 4K (height ≤ 2160 px)             |0.2521           |
| H.265      | 2K (height ≤ 1440 px)           | 0.126           |
| H.265      | FHD (height ≤ 1080 px)       | 0.063         |
| H.265      | HD (height ≤ 720 px)       |0.0315         |
| H.265      | SD (height ≤ 480 px)  | 0.0158          |
|Remuxing| -|0.0028|
|Audio transcoding|-|0.002|


#### Details

- Rules: You are charged based on the duration and specification of the video file generated after general transcoding. Video specification is determined by the codec used and height (px) of the video generated. Remuxing and audio transcoding are charged based on output video duration.
- Billing formula: Video transcoding fee = Output video duration (min) x Unit price as per codec and resolution (USD/min)

#### Billing example
Suppose you used the VOD to transcode a video whose codec is H.264 on January 1. You transcoded it into two outputs of 2560 x 1440 and 1280 x 640 respectively for 100 minutes, and also transcoded it into an audio file for 100 minutes. You will need to pay the following fee on January 2:
Transcoding fee on January 1 = 0.0242 (USD/min) x 100 (min) + 0.0061 (USD/min) x 100 (min) + 0.002 (USD/min) x 100 (min) = 3.23 (USD)

>? The 2560 x 1440 video falls under the category of 2K (height ≤ 1440 px), so the unit price is 0.0242 (USD/min); the 1280 x 640 video falls under the category of HD (480 px ≤ height ≤ 720 px), so the unit price is 0.0061 (USD/min); the unit price for audio transcoding is 0.002 (USD/min). The fee charged is the costs of the three tasks combined.

For more billing examples, see [Billing Examples](https://intl.cloud.tencent.com/document/product/266/38163).

### TESHD transcoding
To learn about TESHD transcoding, see [Video Transcoding Service](https://intl.cloud.tencent.com/document/product/266/7898#teshd).
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
>- Billing rules are the same as those for general transcoding.



### Transcoding to adaptive bitrate streaming

#### Pricing

Adaptive bitrate streaming is charged based on the duration and specification of the video generated after transcoding. Video specification is determined by the codec used and height (px) of the video generated.
#### Details

**Billing rules are the same as those of general transcoding**. Videos of different specifications in the output are charged separately according to their resolutions.
#### Billing example

Suppose you used VOD to transcode a video into outputs of adaptive bitrate streaming on January 1. The template contains three output specifications, namely, FHD (1920 x 1080), HD (1280 x 720), and SD (640 x 480), and the transcoded video duration of each output is 100 minutes. You will need to pay the following transcoding fee on January 2:
Transcoding fee on January 1 = 0.0121 (USD/min) x 100 (min) + 0.0061 (USD/min) x 100 (min) + 0.003 (USD/min) x 100 (min) = 2.21 (USD)

>? As the original video is transcoded into videos of three specifications, the overall transcoding fee is the sum of charges for the three videos.



## Video Editing

#### Pricing
- Video editing is billed according to the codec, duration, and resolution of the output file.
- The resolution-based unit prices for video editing are the same as those for [general transcoding](#p2).

#### Details
- Rules: You are charged based on the resolution and duration of the output file. **Each video editing task is billed once according to the specification**.
- Billing formula: Video editing fee = Output file duration (min) x Unit price (USD/min) as per resolution and codec

#### Billing example
Suppose you used the VOD editing feature to splice video A (10 min, 640 x 480) and video B (15 min, 1280 x 720) on January 1, and the output video is C (25 min, 1280 x 720). You will need to pay the following fee on January 2:
Video editing fee on January 1 = 0.0061 (USD/min) x 25 (min) = 0.1525 (USD)
>? The codec used in above example is H.264. For more information about video editing, see [ComposeMedia](https://intl.cloud.tencent.com/document/product/266/34127) and [EditMedia](https://intl.cloud.tencent.com/document/product/266/34126).

## Watermark Removal

#### Pricing

| Resolution                      | Unit Price (USD/min) |
| :-------------------------- | :---------------- |
| 8K (height ≤ 4320 px)         | 0.41              |
| 4K (height ≤ 2160 px)         | 0.21              |
| 2K (height ≤ 1440 px)         | 0.1               |
| FHD (height ≤ 1080 px) | 0.05              |
| HD (height ≤ 720 px)     | 0.03              |
| SD (height ≤ 480 px)     | 0.02              |

#### Details

- Watermark removal is billed based on the resolution and duration of the output video.
>- Rules: You are charged based on the duration and resolution of the video file generated after watermark removal. Video specification is determined by the height (px) of the video generated.

#### Billing example

Suppose you used the watermark removal service of VOD to output videos in 2560 x 1440 and 1280 x 640 respectively for 100 minutes. You will need to pay the following fee on January 2:

- For watermark removal from the video at 2560 x 1440 resolution, the video height 1440 px falls under the category of 2K (height ≤ 1440 px), so the unit price is 0.1 USD/min.
- For watermark removal from the video at 1280 x 640 resolution, the video height 640 px is below HD (≤ 720 px) but above SD (≤ 480 px), so the unit price is 0.03 USD/min.

Watermark removal fee on January 1 = 0.1 (USD/min) x 100 (min) + 0.03 (USD/min) x 100 (min) = 13 USD

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

| Traffic Tier (USD/GB) | Chinese Mainland |Asia Pacific Region 1|Asia Pacific Region 2|Asia Pacific Region 3|Middle East|Europe|North America|South America|Africa|
| ----------|--------|---------|----------|----------|----------|----------|----------|----------|----------|
|  0–500 GB (inclusive)   | 0.039    | 0.0748   | 0.1236   | 0.1138   | 0.1951 | 0.0715 | 0.0715 | 0.1675 | 0.1951 |
| 500 GB–2 TB (inclusive)   | 0.038    | 0.0699   | 0.1138   | 0.1041   | 0.1789 | 0.0634 | 0.0634 | 0.1593 | 0.1789 |
| 2–50 TB (inclusive)   | 0.036    | 0.0585   | 0.1057   | 0.0911   | 0.1675 | 0.0504 | 0.0504 | 0.1463 | 0.1675 |
| 50–100 TB (inclusive)     | 0.033    | 0.0504   | 0.0911   | 0.0813   | 0.1545 | 0.0325 | 0.0325 | 0.1382 | 0.1545 |
| > 100 TB         | 0.025    | 0.0455   | 0.0846   | 0.0715   | 0.1382 | 0.026  | 0.026  | 0.1301 | 0.1382 |


> ! For more information, see [Billing Examples](https://intl.cloud.tencent.com/document/product/266/38163#.E7.82.B9.E6.92.AD.E6.B5.81.E9.87.8F.E4.BD.BF.E7.94.A8.E9.A2.84.E4.BC.B0.E5.88.86.E6.9E.90).
#### Details

- Video acceleration is charged based on the accelerated downstream traffic and the acceleration region.
- Rules: You are charged daily based on the traffic accelerated by CDNs for video playback.
- Billing formula: Daily video acceleration fee = Video playback traffic (GB) x Traffic unit price (USD/GB) of the corresponding tier
- Billing example: Assume that you used the VOD acceleration service on January 1 to accelerate 550 GB of traffic for playback. On January 2, you would be charged:
  VOD traffic fee on January 1 = 0.038 (USD/GB) x 550 (GB)= 20.9 (USD)

## Data Retrieval

After you change the media asset storage class to ARCHIVE or DEEP_ARCHIVE, media assets cannot be directly accessed before they are retrieved. VOD supports different retrieval modes, and fees are charged based on the amount of data retrieved in the corresponding mode.

>! DEEP_ARCHIVE storage doesn't support expedited retrieval.

### Pricing

<table>
   <tr>
      <th width="0px" >Data Retrieval Type</td>
      <th width="0px"  >Data Retrieval Mode</td>
      <th width="0px" >	Covered Region</td>
      <th width="130px"  >Price (USD/GB)</td>
   </tr>
	   <tr>
    <td rowspan='6' >ARCHIVE storage</td>
      <td rowspan='2' >Bulk</td>
      <td >		Chinese mainland</td>
      <td >		0.0025</td>
   </tr>
	 	  <tr>
      <td >Outside the Chinese mainland (Silicon Valley, Hong Kong (China), Frankfurt, Moscow, Seoul, Virginia, Singapore, Mumbai, Toronto, Bangkok)</td>
      <td >	0.003</td>
   </tr>
	 	 	 <tr>
      <td rowspan='2' >Expedited</td>
      <td >		Chinese mainland</td>
				<td >		0.03</td>
   </tr>
	 	   <tr>
      <td >Outside the Chinese mainland (Silicon Valley, Hong Kong (China), Frankfurt, Moscow, Seoul, Virginia, Singapore, Mumbai, Toronto, Bangkok)</td>
      <td >	0.036</td>
   </tr>
	 	 	 <tr>
      <td rowspan='2' >Standard</td>
      <td >		Chinese mainland</td>
					<td >			0.01</td>
   </tr>
	 	   <tr>
      <td >Outside the Chinese mainland (Silicon Valley, Hong Kong (China), Frankfurt, Moscow, Seoul, Virginia, Singapore, Mumbai, Toronto, Bangkok)</td>
      <td >	0.012</td>
   </tr>
	   <tr>
    <td rowspan='4' >DEEP_ARCHIVE storage</td>
      <td rowspan='2' >Bulk</td>
      <td >		Chinese mainland</td>
      <td >			0.0026</td>
   </tr>
	 	  <tr>
      <td >Outside the Chinese mainland (Silicon Valley, Hong Kong (China), Frankfurt, Moscow, Seoul, Virginia, Singapore, Mumbai, Toronto, Bangkok)</td>
      <td >	0.00325</td>
   </tr>
      <td rowspan='2' >Standard</td>
      <td >		Chinese mainland</td>
      <td >			0.02</td>
   </tr>
	 	  <tr>
      <td >Outside the Chinese mainland (Silicon Valley, Hong Kong (China), Frankfurt, Moscow, Seoul, Virginia, Singapore, Mumbai, Toronto, Bangkok)</td>
      <td >	0.025</td>
   </tr>
</table>
  

### Billing details

- Data retrieval is charged based on the retrieval mode and usage.
- Rules: You are charged daily based on the actual retrieval mode and retrieval usage when the media asset storage class is changed from DEEP_ARCHIVE or ARCHIVE to STANDARD.
- Billing formula: Daily retrieval fee = Retrieval usage (GB) x Daily retrieval unit price (USD/GB).

### Billing examples

Suppose you used the VOD data retrieval service on January 1 to retrieve 100 GB of data from **DEEP_ARCHIVE storage** in the Chinese mainland in the **bulk retrieval mode**. You will need to pay the following fee:
VOD data fee = 100 (GB) x 0.0026 (USD/GB) = 0.26 USD

## Remarks

If you have a large-scale business (with over 1 PB of storage capacity or over 10 TB of daily traffic usage), a daily billing mode may not meet your needs. Please [contact us](https://intl.cloud.tencent.com/contact-us) for more flexible and cost-effective billing options.
