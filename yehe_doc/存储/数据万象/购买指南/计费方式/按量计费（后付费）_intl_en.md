CI is pay-as-you-go (postpaid) by default in all regions as described in [Regions and Domain Names](https://www.tencentcloud.com/zh/document/product/1045/33423). Fees are charged monthly by the actual usage of traffic and basic image processing.



## Pricing

For detailed **CI** pricing, see [Pricing | Cloud Infinite](https://buy.cloud.tencent.com/price/ci).



## Billable Items

CI billable items are as described below:

| Billable Item       |                      | Description                                                   |
| :----------- | :------------------- | ------------------------------------------------------------ |
| Image processing fees | Basic image processing fees | Fees incurred by image processing when you download or persistently store images. Such fees are charged by the monthly processing usage. |
|              | Image advanced compression fees     | Fees incurred by image conversion to formats with a high compression ratio, such as TPG, AVIF, and HEIF. Such fees are charged by the monthly number of uses. |
|              | Guetzli image compression fees | Fees incurred by Guetzli lossless compression of JPG images. Such fees are charged by the monthly number of compression times. |
|              | Blind watermark fees           | Fees incurred by blind watermark operations performed on images, including adding and extracting. Such fees are charged by the monthly number of processing times. |
| Media processing fees | Audio/Video transcoding fees | Fees incurred by using audio/video transcoding services, including standard transcoding, video-to-animated image conversion, and audio/video splicing. Such fees are charged by the output video duration at different prices for different resolutions. |
|              | Top speed codec transcoding fees     | Fees incurred by using the top speed codec transcoding service. Such fees are charged by the output video duration at different prices for different resolutions. |
|              | Video montage fees         | Fees incurred by using the video montage service. Such fees are charged by the input video duration at different prices for different resolutions. |
|              | Video enhancement fees     | Fees incurred by using the video enhancement service. Such fees are charged by the input video duration at different prices for different resolutions. |
|              | Super resolution fees     | Fees incurred by using the super resolution service, including basic edition and enhanced edition. Such fees are charged by the output video duration at different prices for different resolutions. |
|              | SDR-to-HDR fees     | Fees incurred by using the SDR-to-HDR service. Such fees are charged by the output video duration based on dynamic range conversion. |
|              | Voice/Sound separation fees         | Fees incurred by using the voice/sound separation service. Such fees are charged by the output file duration. |
|              | Video tagging fees     | Fees incurred by using the video tagging service. Such fees are charged by the input video duration. Failed recognitions will not be billed. |
|              | Video metadata acquisition fees     | Fees incurred by using the video metadata acquisition service. Such fees are charged by the number of uses. |
|              | Video frame capturing fees     | Fees incurred by using the video frame capturing service. Such fees are charged by the number of uses. |
|              | Intelligent thumbnail fees         |  Fees incurred by using the intelligent thumbnail service. Such fees are charged by the input video duration. |
|              | Digital watermark fees     | Fees incurred by using the digital watermark service. Such fees are charged by the output video duration. |
|              | Text-to-speech fees         | Fees incurred by using the text-to-speech service. Such fees are charged by the number of input characters. |
|              | Audio noise cancellation fees         | Fees incurred by using the audio noise cancellation service. Such fees are charged by the audio processing duration. |
|              | Video quality scoring fees     | Fees incurred by using the video quality scoring service. Such fees are charged by the input video duration. |
| File processing fees | File-to-image conversion fees       | Fees incurred by file-to-image conversion in the file preview service. Such fees are charged by the number of successfully converted file pages.  |
|              | File-to-HTML conversion fees     | Fees incurred by file-to-HTML conversion in the file preview service. Such fees are charged by the number of successful conversions. |
|              | Privacy protection fees     | Fees incurred by detection of privacy data contained in files, such as identity card numbers, license plate numbers, and mobile numbers. Such fees are charged by the size of successfully detected files. |
| Traffic fees     | CDN origin-pull traffic fees         | Fees incurred by the origin-pull traffic generated during access to CI over CDN.        |
|              | Public network outbound traffic fees           | Fees incurred by the traffic generated during access to CI at CI domain names.               |

## Billing Cycle

CI billable items are billed **monthly**. Amounts are deducted and the bill for the previous month is generated on the first day of each month.



## Example

You operate an online image website. Visitors can upload their local images to the website for online image processing and then download the output images. You store the website content in a COS bucket in **Guangzhou region**, use the **CI** service, and enable the CDN acceleration service.

The monthly basic image processing volume is 100 GB, generating CDN origin-pull traffic of 100 GB, Guetzli compression operations of 10,000 times, and blind watermark operations of 10,000 times.

### Monthly fees calculation

| Item | Free Tier | Unit Price | Billable Usage | Fees (Unit Price * Billable Usage) |
| :--------------- | :------- | :------------- | :----------------- | :--------------------- |
| Basic image processing | 10 TB     | 0.01 USD/GB/month | 0 GB                | 0 USD                 |
| Guetzli compression | 3,000 times   | 0.15 USD/1,000 times  | (10000 - 3000) times  | 1.05 USD              |
| Blind watermark | 3,000 times   | 0.15 USD/1,000 times  | (10000 - 3000) times  | 1.05 USD              |
| CDN origin-pull traffic | 10 GB     | 0.02 USD/GB    | (100 - 10) GB     | 1.8 USD               |
| Monthly fees           | -        | -              | -                  | **3.9 USD**           |