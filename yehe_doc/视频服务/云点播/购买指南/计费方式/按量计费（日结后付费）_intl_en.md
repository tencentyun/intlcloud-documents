## Notes

- In the pay-as-you-go billing mode, fees are charged based on the actual usage of each billable item, which you can view in the [VOD console](https://console.cloud.tencent.com/vod/overview).
- About daily billing:
  - Billing time: Between 12:00 and 18:00 each day, VOD calculates your usage of the previous day, generates a bill, and deducts the fees.
  - Billing period: By default, VOD deducts fees on a daily basis. If you want to change to monthly billing, please [contact us](https://intl.cloud.tencent.com/contact-us).

Billable items:
- **Storage**: Saving the files you upload to Tencent Cloud VOD as well as the files generated after transcoding. Storage fees are charged based on the storage space used and storage period.
- **Video transcoding**: General transcoding of video files stored in Tencent Cloud VOD. This service is charged according to the specification and duration of output files. A duration less than 1 minute is counted as 1 minute. Each transcoding task is billed only once according to the specification. No fees will be charged if transcoding fails.
- **Top Speed Codec (TSC)**: Transcoding video files stored in VOD according to TSC standards. This service is charged according to the specification and duration of output files. A duration less than 1 minute is counted as 1 minute. Each transcoding task is billed only once according to the specification. No fees will be charged for if transcoding fails.  
- **Video editing**: Using the [ComposeMedia](https://intl.cloud.tencent.com/document/product/266/34127) and [EditMedia](https://intl.cloud.tencent.com/document/product/266/34126) APIs to process video files stored in VOD. This service is charged according to the specification and duration of output files. A duration less than 1 minute is counted as 1 minute. Each transcoding task is charged only once according to the specification. No fees will be charged if transcoding fails.  
- **Watermark removal**: Removing watermarks from videos stored in VOD. This service is charged according to the specification and duration of output files. A duration less than 1 minute is counted as 1 minute. Each watermark removal task is billed only once according to the specification. No fees will be charged if a task fails.  
- **Video acceleration**: Using CDN for acceleration during video playback. This service is charged based on the downstream traffic consumed.
- **Data retrieval:** Retrieving media from ARCHIVE or DEEP_ARCHIVE. This service is charged based on the retrieval mode and size of the file retrieved.
- **Media AI:** Using AI capabilities (content analysis and recognition) on media files stored in VOD. This service is charged based on the duration of output files. Each task is billed only once. No fees will be charged if a task fails.
- **Copyright protection:** Using VOD’s copyright protection capabilities (digital watermark extraction and DRM encryption) on media stored in VOD. For the billing details, see [Media Encryption and Protection](https://intl.cloud.tencent.com/document/product/266/33965). 

## Storage[](id:media_storage)
### Pricing
<table>
   <tr>
      <th width="150px" >Storage Class</td>
      <th width="0px" >Region</td>
      <th width="0px"  >Price (USD/GB/Day)</td>
   </tr>
	   <tr>
    <td rowspan='2' >STANDARD</td>
      <td>Chinese mainland</td>
      <td >0.0006</td>
   </tr>
	 	   <tr>
      <td >Outside the Chinese mainland (Silicon Valley, Hong Kong (China), Frankfurt, Moscow, Seoul, Virginia, Singapore, Mumbai, Toronto, Bangkok)</td>
      <td>0.0009</td>
   </tr>
	 	   <tr>
    <td rowspan='2' >STANDARD_IA<br>(at least 30 days)</td>
      <td>Chinese mainland</td>
      <td >0.0004</td>
   </tr>
	 	   <tr>
      <td >Outside the Chinese mainland (Silicon Valley, Hong Kong (China), Frankfurt, Moscow, Seoul, Virginia, Singapore, Mumbai, Toronto, Bangkok)</td>
      <td >0.0006</td>
   </tr>
	 	 	   <tr>
    <td rowspan='2' >ARCHIVE<br>(at least 90 days)</td>
      <td>Chinese mainland</td>
      <td >0.0002</td>
   </tr>
	 	   <tr>
      <td >Outside the Chinese mainland (Silicon Valley, Hong Kong (China), Frankfurt, Moscow, Seoul, Virginia, Singapore, Mumbai, Toronto, Bangkok)</td>
      <td >0.0003</td>
   </tr>
	 	 	 	   <tr>
    <td rowspan='2' >DEEP_ ARCHIVE<br>(at least 180 days)</td>
      <td>Chinese mainland</td>
      <td >0.00006</td>
   </tr>
	 	   <tr>
      <td >Outside the Chinese mainland (Silicon Valley, Hong Kong (China), Frankfurt, Moscow, Seoul, Virginia, Singapore, Mumbai, Toronto, Bangkok)</td>
      <td >0.0001</td>
   </tr>
</table>

### Billing details

- Prices vary with storage region and storage class. If you change the storage class of a media file, the price for the new storage class will apply.
- Rules: Storage fees are charged based on the storage class and peak storage space used per day. **Storage fees for regions inside and outside the Chinese mainland are charged separately**.
- Billing formula: Daily storage fee = Peak storage space used in the Chinese mainland (GB) x Unit price (USD/GB/day) + Peak storage space used outside the Chinese mainland (GB) x Unit price (USD/GB/day).

### Examples

Assume that on January 1, you stored media files in STANDARD in the Chinese mainland and the peak storage usage was 100 GB. You also stored media files in STANDARD_IA in Mumbai and the peak storage usage was 50 GB. On January 2, the storage fee billed for January 1 would be as follows:
100 (GB) x 0.0006 (USD/GB) + 50 (GB) x 0.0006 (USD/GB) = 0.06 (USD) + 0.03 (USD) = 0.09 (USD)

> !
>- You can delete files in the console to avoid incurring storage fees.
>- Minimum storage duration for STANDARD_IA files: 30 days. Storage fees for 30 days will be charged even if a file is stored for shorter than the period.
>- Minimum storage duration for ARCHIVE files: 90 days. Storage fees for 90 days will be charged even if a file is stored for shorter than the period.
>- Minimum storage duration for DEEP ARCHIVE files: 180 days. Storage fees for 180 days will be charged even if a file is stored for shorter than the period.

## Media Processing
VOD offers media processing capabilities including general transcoding, TSC transcoding, [adaptive bitrate streaming](https://intl.cloud.tencent.com/document/product/266/33942), and video editing.

### General transcoding

#### Pricing

General transcoding is charged based on the duration and short side (px) of the video generated after transcoding.

| Codec    | Resolution                            |  Unit Price (USD/min) |
| ---------  |:--------------------------------:|:---------------:|
| H.264      | 4K (short side ≤ 2160 px）          | 0.0521           |
| H.264      | 2K (short side ≤ 1440 px）           | 0.0242          |
| H.264      | FHD (short side ≤ 1080 px）     | 0.0121          |
| H.264      | HD (short side ≤ 720 px)        | 0.0061          |
| H.264      | SD (short side ≤ 480 px)    | 0.003         |
| H.265      | 4K (short side ≤ 2160 px）             |0.2521           |
| H.265      | 2K (short side ≤ 1440 px）           | 0.126           |
| H.265      | FHD (short side ≤ 1080 px）       | 0.063         |
| H.265      | HD (short side ≤ 720 px)       |0.0315         |
| H.265      | SD (short side ≤ 480 px)  | 0.0158          |
|Remuxing| -|0.0028|
|Audio transcoding|-|0.002|


#### Billing details

- Rules: General transcoding fees are charged based on the duration and specification of the video file generated. Video specification is determined by the codec used and short side (px) of the video generated. Remuxing and audio transcoding are charged based on the output video duration.
- Billing formula: Video transcoding fee = Output video duration (min) x Unit price as per codec and resolution (USD/min)

#### Example
Assume that you transcoded a video file of 100 minutes into 2560 x 1440 and 1280 x 640 respectively using the H.264 codec on January 1, as well as an audio file of 100 minutes. On January 2, the transcoding fee billed for January 1 would be as follows:
0.0242 (USD/min) x 100 (min) + 0.0061 (USD/min) x 100 (min) + 0.002 (USD/min) x 100 (min) = 3.23 (USD)

>? The 2560 x 1440 video falls under the category of 2K (short side ≤ 1440 px), so the unit price is 0.0242 USD/min; the 1280 x 640 video falls under the category of HD (480 px ≤ short side ≤ 720 px), so the unit price is 0.0061 USD/min; the unit price for audio transcoding is 0.002 USD/min. The fee charged is the costs of the three tasks combined.

For more billing examples, see [Billing Examples](https://intl.cloud.tencent.com/document/product/266/38163).

### TSC transcoding
To learn more about TSC transcoding, see [Video Transcoding Service](https://intl.cloud.tencent.com/document/product/266/7898).
#### Pricing

TSC transcoding is charged based on the duration and short side (px) of the video generated after transcoding.

|Codec|Resolution|Unit Price (USD/min)|
|----------|-----------|-----------|
|H.264|4K (short side ≤ 2160 px)  |0.1721|
|H.264|2K (short side ≤ 1440 px)|0.08|
|H.264|FHD (short side ≤ 1080 px)|0.04|
|H.264|HD (short side ≤ 720 px)|0.02|
|H.264|HD (short side ≤ 480 px)  |0.01 |
|H.265|4K (short side ≤ 2160 px)|0.8319 |
|H.265|2K (short side ≤ 1440 px)|0.416|
|H.265|FHD (short side ≤ 1080 px)   |0.208|
|H.265|HD (short side ≤ 720 px)  |0.104|
|H.265|SD (short side ≤ 480 px)|0.052|


>!
>- TSC transcoding is billed according to the resolution and duration of transcoded video.
>- Rules: TSC transcoding fees are based on the duration and specification of the video file generated after TSC transcoding. Video specification is determined by the codec used and short side (px) of the video generated.
>- The prices above apply only to daily billing. If you are billed monthly, please contact your sales rep to learn about the billing details.
>- The billing rules are the same as those for general transcoding.



### Adaptive bitrate streaming

#### Pricing

Adaptive bitrate streaming is charged based on the duration and specification of the video generated after transcoding. Video specification is determined by the codec used and short side (px) of the video generated.
#### Billing details

**The billing rules are the same as those for general transcoding**. Output videos of different resolutions are charged separately.
#### Example

Assume that on January 1, you used VOD’s adaptive bitrate streaming service to transcode a video of 100 minutes into three resolutions: FHD (1920 x 1080), HD (1280 x 720), and SD (640 x 480). On January 2, the fee billed for January 1 would be as follows:
0.0121 (USD/min) x 100 (min) + 0.0061 (USD/min) x 100 (min) + 0.003 (USD/min) x 100 (min) = 2.21 (USD)

>? Because the video is transcoded into three specifications, each specification is charged and the fee is the sum of the three.



### Video editing

#### Pricing
- Video editing is billed according to the codec, duration, and resolution of the output file.
- The resolution-specific unit prices for video editing are the same as those for [general transcoding](#p2).

#### Billing details
- Rules: Charges are based on the resolution and duration of the output file. **Each video editing task is billed once according to the specification**.
- Billing formula: Video editing fee = Output file duration (min) x Unit price (USD/min) as per resolution and codec

#### Example
Assume that on January 1, you used the VOD editing feature to splice video A (10 min, 640 x 480) and video B (15 min, 1280 x 720) into video C (25 min, 1280 x 720). On January 2, the fee billed for January 1 would be as follows:
0.0061 (USD/min) x 25 (min) = 0.1525 (USD)
>? The codec used in the above examples is H.264. For more information about video editing, see [ComposeMedia](https://intl.cloud.tencent.com/document/product/266/34127) and [EditMedia](https://intl.cloud.tencent.com/document/product/266/34126).

### Watermark removing

#### Pricing

| Resolution                      | Unit Price (USD/min) |
| :-------------------------- | :---------------- |
| 8K (short side ≤ 4320 px)         | 0.41              |
| 4K (short side ≤ 2160 px)         | 0.21              |
| 2K (short side ≤ 1440 px)         | 0.1               |
| FHD (short side ≤ 1080 px) | 0.05              |
| HD (short side ≤ 720 px）     | 0.03              |
| SD (short side ≤ 480 px）     | 0.02              |

#### Billing details

- Watermark removal is billed based on the resolution and duration of the output video.
- Rules: Watermark removal fees are based on the duration and resolution of the video file generated. Video specification is determined by the short side (px) of the video generated.

#### Example

Assume that you used the watermark removal service of VOD on January 1. Two videos were generated, each 100 minutes long, and their resolutions were 2560 x 1440 and 1280 x 640 respectively. On January 2, the fee billed for January 1 would be as follows:

- For the 2560 x 1440 video, the unit price for 2K (short side ≤ 1440 px) applies, which is 0.1 USD/min.
- For the 1280 x 640 video, the unit price for HD (480 px ≤ short side ≤ 720 px) applies, which is 0.03 USD/min.

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

>! CDN service fees for the Chinese mainland and regions outside the Chinese mainland are charged separately based on corresponding unit prices and usages.

#### Pricing
>? The daily pay-as-you-go mode supports only bill-by-traffic. If you want to pay monthly by bandwidth, please contact sales.

Video acceleration is billed daily based on a volume pricing model. The more traffic you use a day, the lower the unit price will be. The pricing tiers are as follows:

| Traffic Tier (USD/GB) | Chinese Mainland |Asia Pacific Region 1|Asia Pacific Region 2|Asia Pacific Region 3|Middle East|Europe|North America|South America|Africa|
| ----------|--------|---------|----------|----------|----------|----------|----------|----------|----------|
|  0 GB - 500 GB (inclusive)   | 0.039    | 0.0748   | 0.1236   | 0.1138   | 0.1951 | 0.0715 | 0.0715 | 0.1675 | 0.1951 |
| 500 GB - 2 TB (inclusive)   | 0.038    | 0.0699   | 0.1138   | 0.1041   | 0.1789 | 0.0634 | 0.0634 | 0.1593 | 0.1789 |
| 2 TB - 50 TB (inclusive)   | 0.036    | 0.0585   | 0.1057   | 0.0911   | 0.1675 | 0.0504 | 0.0504 | 0.1463 | 0.1675 |
| 50 TB - 100 TB (inclusive)     | 0.033    | 0.0504   | 0.0911   | 0.0813   | 0.1545 | 0.0325 | 0.0325 | 0.1382 | 0.1545 |
| > 100 TB         | 0.025    | 0.0455   | 0.0846   | 0.0715   | 0.1382 | 0.026  | 0.026  | 0.1301 | 0.1382 |


>! For more information, see [Billing Examples](https://intl.cloud.tencent.com/document/product/266/38163#.E7.82.B9.E6.92.AD.E6.B5.81.E9.87.8F.E4.BD.BF.E7.94.A8.E9.A2.84.E4.BC.B0.E5.88.86.E6.9E.90).

#### Billing details

- Video acceleration is charged based on the accelerated downstream traffic and the acceleration region.
- Rules: Video acceleration fees are charged daily based on the traffic accelerated by CDNs for video playback.
- Billing formula: Daily video acceleration fee = Video playback traffic (GB) x Traffic unit price (USD/GB) of the corresponding tier
- Billing example: Assume that you used the VOD acceleration service on January 1 to accelerate 550 GB of traffic for playback. On January 2, the fee billed for January 1 would be as follows:
  0.038 (USD/GB) x 550 (GB)= 20.9 (USD)

## Data Retrieval

To access media assets stored in ARCHIVE or DEEP_ARCHIVE, you must retrieve them first. VOD supports different retrieval modes. Retrieval fees are charged based on the size of the files retrieved.

>! DEEP_ARCHIVE storage doesn't support expedited retrieval.

### Pricing

<table>
   <tr>
      <th width="0px" >Storage Class</td>
      <th width="0px"  >Retrieval Mode</td>
      <th width="0px" >Region</td>
      <th width="130px"  >Price (USD/GB)</td>
   </tr>
	   <tr>
    <td rowspan='6' >ARCHIVE</td>
      <td rowspan='2' >Bulk</td>
      <td>Chinese mainland</td>
      <td>0.0025</td>
   </tr>
	 	  <tr>
      <td >Outside the Chinese mainland (Silicon Valley, Hong Kong (China), Frankfurt, Moscow, Seoul, Virginia, Singapore, Mumbai, Toronto, Bangkok)</td>
      <td>0.003</td>
   </tr>
	 	 	 <tr>
      <td rowspan='2' >Expedited</td>
      <td>Chinese mainland</td>
				<td>0.03</td>
   </tr>
	 	   <tr>
      <td >Outside the Chinese mainland (Silicon Valley, Hong Kong (China), Frankfurt, Moscow, Seoul, Virginia, Singapore, Mumbai, Toronto, Bangkok)</td>
      <td >	0.036</td>
   </tr>
	 	 	 <tr>
      <td rowspan='2' >Standard</td>
      <td>Chinese mainland</td>
					<td>0.01</td>
   </tr>
	 	   <tr>
      <td >Outside the Chinese mainland (Silicon Valley, Hong Kong (China), Frankfurt, Moscow, Seoul, Virginia, Singapore, Mumbai, Toronto, Bangkok)</td>
      <td>0.012</td>
   </tr>
	   <tr>
    <td rowspan='4' >DEEP_ARCHIVE</td>
      <td rowspan='2' >Bulk</td>
      <td>Chinese mainland</td>
      <td >			0.0026</td>
   </tr>
	 	  <tr>
      <td >Outside the Chinese mainland (Silicon Valley, Hong Kong (China), Frankfurt, Moscow, Seoul, Virginia, Singapore, Mumbai, Toronto, Bangkok)</td>
      <td >	0.00325</td>
   </tr>
      <td rowspan='2' >Standard</td>
      <td>Chinese mainland</td>
      <td>0.02</td>
   </tr>
	 	  <tr>
      <td >Outside the Chinese mainland (Silicon Valley, Hong Kong (China), Frankfurt, Moscow, Seoul, Virginia, Singapore, Mumbai, Toronto, Bangkok)</td>
      <td >	0.025</td>
   </tr>
</table>


### Billing details

- Data retrieval is charged based on the retrieval mode and the size of the files retrieved.
- Rules: Data retrieval fees are charged daily based on the retrieval mode and the size of the files retrieved from DEEP_ARCHIVE or ARCHIVE to STANDARD.
- Billing formula: Daily retrieval fee = File size (GB) x Retrieval unit price (USD/GB).

### Examples

Assume that on January 1, you retrieved 100 GB of data from **DEEP_ARCHIVE storage** in the **bulk retrieval mode** in the Chinese mainland. On January 2, the retrieval fee billed for January 1 would be as follows:
100 (GB) x 0.0026 (USD/GB) = 0.26 USD

## Media AI

Media AI services include content moderation, content analysis, and content recognition.

### Content analysis

The video analysis feature is billed monthly in the pay-as-you-go mode. We calculate the fee by multiplying the minutes analyzed by the unit price.

#### Pricing

Billable items:

- Intelligent highlights generation and video segmentation: Splitting videos into shots or scenes. This feature can be optimized for your needs. **Highlights generation and video segmentation use different APIs and are billed separately**.
- Intelligent labeling and classification: Intelligent face, speech, and optical character recognition; automatically generating labels, categories, and synopses. **Video labeling and classification use different APIs and are billed separately**.
- Intelligent thumbnail generation: Capturing one or more frames from a video to use as the thumbnail.

The unit price is as follows:

| Item       | Billed By                 | Price (USD/Min) |
| :----------- | :----------------------- | :---------------- |
| Highlights generation | The duration of the source video for which highlights are generated | 0.0572            |
| Video segmentation | The duration of the source video segmented | 0.0572            |
| Video labeling | The duration of the source video labeled | 0.0572            |
| Video classification | The duration of the source video classified | 0.0572            |
| Thumbnail generation | The duration of the source video for which thumbnails are generated | 0.0572            |

#### Example

**User A called the video labeling and classification APIs to analyze video B, whose length is 100 minutes.
The fee incurred = 100 x 0.0572 + 100 x 0.0572 = 11.4 USD**

>!
>- Currently, the content analysis feature is only offered to customers billed monthly. To change from daily to monthly billing, please contact sales.
>- Video duration is rounded up to the nearest minute.

### Content recognition

The video content recognition feature of VOD leverages AI technologies to recognize faces and text in video images, opening and closing video segments, and speech, helping you manage your media assets more accurately and efficiently.

#### Pricing

| Billable Item     | Billed By                               | Price             |
| :----------- | :------------------------- | :-------------- |
| Content recognition | The duration of the video recognized | 0.0572 USD/min |

#### Example

User A used VOD’s content recognition feature on video B, whose length was 60 minutes. The fee incurred would be 60 (minutes) x 0.0572 (USD/min) = 3.432 (USD).

## Copyright Protection

VOD offers digital watermark and DRM encryption capabilities to help protect your content. 

### Digital watermark

VOD offers watermark solutions with high protection and low costs to protect your content against piracy. Using a digital watermark, you can extract a user ID from a video to find the user responsible for distributing it without authorization. This deters piracy and allows you to take action against copyright infringement.

#### Pricing

| Billable Item       | Billed By                                   | Price          |
| :----------- | :----------------------------------------- | :------------ |
| Digital watermark extraction | The duration of the video tracked (only pay-as-you-go supported) | 0.22 USD/min |

#### Billing details

- Billable item: Digital watermark extraction
- Rules: In case of unauthorized distribution of your video, you can [submit a ticket](https://intl.cloud.tencent.com/zh/account/login?s_url=https%3A%2F%2Fconsole.intl.cloud.tencent.com%2Fworkorder) to extract the user ID of the user who distributed a video containing a digital watermark. This will incur digital watermark extraction fees.

#### Example

Assume that you found your video (length: 60 minutes; resolution: 2560 x 1440) distributed by someone without your authorization, and you submitted a ticket to VOD to extract the distributor’s user ID from the video’s digital watermark. The output video was 60 minutes long and had a resolution of 1280 x 720. The digital watermark extraction fee incurred would be as follows:

- The unit price of the digital watermark extraction service is 0.22 USD/min.

Digital watermark extraction fee = 0.22 x 60 (minutes) = 13.2 USD

>?
>- No fees will be charged if digital watermark extraction fails.
>- When you add a digital watermark to a video, the video will be transcoded, which will incur transcoding fees. For details, see [Media Processing](#media-processing).
>- Transcoded streams take up storage space, which incurs storage fees. For details, see [Storage](#storage).

### DRM encryption

VOD uses established DRM solutions to encrypt videos during transcoding. If you enable DRM encryption, the encryption cost will be included in your transcoding fee. If you play DRM-encrypted videos to viewers, DRM playback fees will be charged based on the number of license requests.

#### Pricing

| Billable Item                        | Billed By     | Price          |
| :--------------- | :--------------------------- | :------------ |
| DRM license | The number of license requests (only pay-as-you-go supported) | 0.0012 USD/request |

#### Billing details

- Billable item: The number of license requests to play DRM-encrypted videos
- Rules: Transcoding fees are incurred for encrypting videos with DRM solutions, and DRM playback fees are charged based on the number of license requests.
- DRM fees = DRM encryption (transcoding) fees + DRM playback fees (based on the number of license requests)

#### Example

Assume that on January 1, you transcoded a video (length: 10 minutes; resolution: 2560 x 1440) using the H.264 codec and used VOD’s DRM encryption feature to encrypt it. The video generated was 10 minutes long and had a resolution of 1280 x 720, and there were 50 license requests to play it. On January 2, the DRM playback fee billed for January 1 would be as follows:

- The unit price of DRM playback is 0.0012 USD/request.

DRM playback fee on January 1 = 50 (requests) x 0.0012 (USD/request) = 0.06 USD

>?
>- DRM transcoding is billed in the same way as general transcoding. DRM transcoding fees are incurred each time you encrypt a video.
>- Encrypted videos take up storage space, which incurs storage fees. For details, see [Storage](#storage).

## Others

If you have a large-scale business (storage usage over 1 PB or daily traffic consumption over 10 TB), daily billing may not meet your needs. You can [contact us](https://intl.cloud.tencent.com/contact-us) for other billing options.
