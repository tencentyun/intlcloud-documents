CI provides a rich set of basic video processing services, such as video frame capturing, video-to-animated image conversion, file transcoding, video metadata acquisition, and audio/video splicing. In addition, by leveraging Tencent Cloud's advanced AI technologies, it can analyze video content to intelligently select the optimal key frame as the video thumbnail, which can effectively improve the video click rate and visual experience.



## Media Processing Fees

Media processing fees refer to fees incurred by using video frame capturing, video metadata acquisition, video-to-animated image conversion, audio/video transcoding, and other media processing features as detailed below. For more information, see [Media Processing Service](https://www.tencentcloud.com/document/product/1045/46980).

| Billable Item               | Description                                                   | Billing Cycle | Applicable Billing Mode                                         |
| :----------------- | :----------------------------------------------------------- | :------- | :------------- |
| Audio/Video transcoding fees     | Fees incurred by using audio/video transcoding services, including standard transcoding, video-to-animated image conversion, and audio/video splicing. Such fees are charged by the **output video duration** at different prices for different resolutions. | Monthly | Pay-as-you-go       |
| Top speed codec transcoding fees   | Fees incurred by using the top speed codec transcoding service. Such fees are charged by the **output video duration** at different prices for different resolutions. |          |                |
| Video montage fees       | Fees incurred by using the video montage service. Such fees are charged by the **input video duration** at different prices for different resolutions. |          |                |
| Video enhancement fees       | Fees incurred by using the video enhancement service. Such fees are charged by the **input video duration** at different prices for different resolutions. |          |                |
| Super resolution fees       | Fees incurred by using the super resolution service, including basic edition and enhanced edition. Such fees are charged by the **output video duration** at different prices for different resolutions. |          |                |
| SDR-to-HDR fees     | Fees incurred by using the SDR-to-HDR service. Such fees are charged by the **output video duration** based on dynamic range conversion. |          |                |
| Video tagging fees       | Fees incurred by using the video tagging service. Such fees are charged by the **input video duration**. Failed recognitions will not be billed. |          |                |
| Video metadata acquisition fees | Fees incurred by using the video metadata acquisition service. Such fees are charged by the **number of uses**.   |          |                |
| Video frame capturing fees       | Fees incurred by using the video frame capturing service. Such fees are charged by the **number of uses**.         |          |                |
| Intelligent thumbnail fees       | Fees incurred by using the intelligent thumbnail service. Such fees are charged by the **input video duration**.     |          |                |
| Digital watermark fees       | Fees incurred by using the digital watermark service. Such fees are charged by the **output video duration**.     |          |                |
| Video quality scoring fees   | Fees incurred by using the video quality scoring service. Such fees are charged by the **input video duration**. |          |                |



## Media Processing Pricing

### Audio/Video transcoding pricing

Prices vary by region, codec, and audio/video transcoding type (standard transcoding, video-to-animated image conversion, or audio/video splicing) as follows: 

| Codec | Resolution | Chinese Mainland (USD/Min) | Silicon Valley, Virginia (USD/Min) | Mumbai, Seoul, Bangkok, Moscow, Hong Kong (China), Tokyo, Toronto, Frankfurt, Singapore (USD/Min) |
| :------- | :-------------------------- | :--------------------- | :--------------------------- | :----------------------------------------------------------- |
| Remuxing   | -                           | 0.001                  | 0.002                        | 0.00295                                                      |
| Pure audio   | -                           | 0.0008                 | 0.00149                      | 0.0019                                                       |
| H.264    | SD (short side ≤ 480 px)     | 0.0023                 | 0.0023                       | 0.00707                                                      |
|          | HD (short side ≤ 720 px)     | 0.0046                 | 0.0049                       | 0.01                                                         |
|          | FHD (short side ≤ 1080 px) | 0.0094                 | 0.0095                       | 0.0219                                                       |
|          | 2K (short side ≤ 1440 px)         | 0.02                   | 0.0206                       | 0.0339                                                       |
|          | 4K  (short side ≤ 2160 px)         | 0.04088                | 0.0427                       | 0.0458                                                       |
| VP8      | SD  (short side ≤ 480 px)     | 0.00268                | 0.00269                      | 0.07                                                         |
|          | HD (short side ≤ 720 px)     | 0.00507                | 0.0052                       | 0.01                                                         |
|          | FHD (short side ≤ 1080 px) | 0.0097                 | 0.00985                      | 0.0223                                                       |
|          | 2K (short side ≤ 1440 px)         | 0.0194                 | 0.02                         | 0.0358                                                       |
|          | 4K (short side ≤ 2160 px)         | 0.0432                 | 0.046                        | 0.0507                                                       |
| VP9      | SD (short side ≤ 480 px)     | 0.0036                 | 0.00365                      | 0.00365                                                      |
|          | HD (short side ≤ 720 px)     | 0.00588                | 0.00588                      | 0.00588                                                      |
|          | FHD (short side ≤ 1080 px) | 0.01                   | 0.012                        | 0.012                                                        |
|          | 2K (short side ≤ 1440 px)         | 0.0264                 | 0.0265                       | 0.0265                                                       |
|          | 4K (short side ≤ 2160 px)         | 0.0485                 | 0.0486                       | 0.0486                                                       |
| H.265    | SD (short side ≤ 480 px)     | 0.012                  | 0.012                        | 0.0428                                                       |
|          | HD (short side ≤ 720 px)     | 0.022                  | 0.023                        | 0.0577                                                       |
|          | FHD (short side ≤ 1080 px) | 0.0457                 | 0.0471                       | 0.1174                                                       |
|          | 2K (short side ≤ 1440 px)         | 0.1                    | 0.11                         | 0.177                                                        |
|          | 4K (short side ≤ 2160 px)         | 0.197                  | 0.2032                       | 0.2368                                                       |

### Top speed codec transcoding pricing

| Codec | Resolution | Chinese Mainland (USD/Min) | Silicon Valley, Virginia (USD/Min) | Mumbai, Seoul, Bangkok, Moscow, Hong Kong (China), Tokyo, Toronto, Frankfurt, Singapore (USD/Min) |
| :-------- | :-------------------------- | :--------------------- | :--------------------------- | :----------------------------------------------------------- |
| **H.264** | SD (short side ≤ 480 px)     | 0.0097                 | 0.0233                       | 0.027                                                        |
|           | HD (short side ≤ 720 px)     | 0.0147                 | 0.0314                       | 0.0363                                                       |
|           | FHD (short side ≤ 1080 px) | 0.0291                 | 0.0624                       | 0.0724                                                       |
|           | 2K (short side ≤ 1440 px)         | 0.0627                 | 0.0935                       | 0.107                                                        |
|           | 4K (short side ≤ 2160 px)         | 0.125                  | 0.1273                       | 0.1401                                                       |
| **H.265** | SD (short side ≤ 480 px)     | 0.0488                 | 0.1227                       | 0.1362                                                       |
|           | HD (short side ≤ 720 px)     | 0.0729                 | 0.1587                       | 0.1711                                                       |
|           | FHD (short side ≤ 1080 px) | 0.1459                 | 0.3299                       | 0.3627                                                       |
|           | 2K (short side ≤ 1440 px)         | 0.313                  | 0.481                        | 0.549                                                        |
|           | 4K (short side ≤ 2160 px)         | 0.626                  | 0.648                        | 0.7229                                                       |

### Video montage pricing

| Resolution | Price (USD/Min) |
| :-------------------------- | :---------------- |
| SD (short side ≤ 480 px)     | 0.033             |
| HD (short side ≤ 720 px)     | 0.045             |
| FHD (short side ≤ 1080 px) | 0.05              |
| 2K (short side ≤ 1440 px)         | 0.072             |
| 4K (short side ≤ 2160 px)         | 0.088             |

### Video enhancement pricing

| Resolution | Price (USD/Min) |
| :------- | :---------------- |
| Color enhancement | 0.06              |
| Detail enhancement | 0.06              |

### Super resolution pricing

**Basic edition**

| Resolution (R) | Frame Rate (F) | Price (USD/Min) |
| :---------- | :-------- | :---------------- |
| R ≤ 1080p   | F < 30   | 0.36              |
| R ≤ 1080p   | F ≥ 30    | 0.72              |
| R > 1080p  | F < 30   | 0.5               |
| R > 1080p  | F ≥ 30    | 1.45              |

**Enhanced version (digital remastering)**

| Resolution (R) | Frame Rate (F) | Price (USD/Min) |
| :-------------- | :-------- | :---------------- |
| 2K < R ≤ 2160p | F ≤ 30    | 2.2               |
| 2K < R ≤ 2160p | F > 30   | 3.5               |
| 720p < R ≤ 2K  | F ≤ 30    | 0.95              |
| 720p < R ≤ 2K  | F > 30   | 1.76              |
| R ≤ 720p        | F ≤ 30    | 0.588             |
| R ≤ 720p        | F > 30   | 1.1               |

### Digital watermark pricing

| Resolution | Price (USD/Min) |
| :-------------------------- | :---------------- |
| SD (short side ≤ 480 px)     | 0.38              |
| HD (short side ≤ 720 px)     | 0.4               |
| FHD (short side ≤ 1080 px) | 0.43              |
| 2K (short side ≤ 1440 px)         | 0.46              |
| 4K (short side ≤ 2160 px)         | 0.5               |
| Watermark extracting                    | 0.85              |



### Pricing of other features

| Features | Price |
| :------------- | :--------------- |
| SDR-to-HDR     | 0.06 USD/min |
| Video tagging       | 0.00784 USD/min |
| Video metadata acquisition | 0.015 USD/1,000 times   |
| Video frame capturing       | 0.015 USD/1,000 times   |
| Intelligent thumbnail       | 0.026 USD/min |
| Video quality scoring   | 0.01463 USD/min |

## Billing Example

You operate an online video website. Visitors can upload their own videos to the website for online media processing and then download output videos. You store the website content in a COS bucket, use the **CI** service, and enable the CDN acceleration service.

### Demand

The monthly basic video processing volume is 100 GB, generating CDN origin-pull traffic of 100 GB, H.264 1080p transcoding of 2,000 minutes, and video frame capturing of 10,000 times.

### Monthly Fees Calculation

| Item | Free Tier | Unit Price | Billable Usage | Fees (Unit Price * Billable Usage) |
| :--------------- | :------- | :----------------------------------------------- | :--------- | :--------------------- |
| Transcoding         | 0        | H.264 FHD (short side ≤ 1080 px) - 0.0094 USD/min | 2,000 minutes | 2,000 * 0.0094 = 18.8 USD |
| Video frame capturing         | 0        | 0.015 USD/1,000 times                                   | 10,000 times   | 10 * 0.015 = 0.15 USD      |
| CDN origin-pull traffic | 0        | 0.02 USD/GB                                      | 100 GB      | 100 * 0.02 = 2 USD         |
| **Monthly fees**       | -        | -                                                | -          | **26.35 USD**          |