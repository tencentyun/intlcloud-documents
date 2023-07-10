CI offers flexible and powerful image processing features, such as rotation, cropping, transcoding, and scaling. It provides multiple image downsizing solutions like Guetzli compression, TPG transcoding, and HEIF transcoding, as well as diversified copyright protection solutions like image/text/blind watermarking. This meets your image processing needs in different business scenarios.



## Image Processing Fees

Image processing fees are divided into **basic image processing fees**, **image advanced compression fees**, **Guetzli image compression fees**, **blind watermark fees**, and **abnormal image detection fess**, as detailed below:

| Billable Item               | Description                                                   | Billing Cycle | Applicable Billing Mode                                         |
| :------------------- | :----------------------------------------------------------- | :------- | :------------- |
| Basic image processing fees | Fees incurred by image processing when you download or persistently store images. Such fees are charged by the processed data volume based on the **original image size**. | Monthly | Pay-as-you-go |
| Image advanced compression fees | Fees incurred by image conversion to formats with a high compression ratio, such as TPG, AVIF, and HEIF. Such fees are charged by the **number of uses**. |          |                |
| Guetzli image compression fees | Fees incurred by Guetzli lossless compression of JPG images. Such fees are charged by the **number of compression times**. |          |                |
| Blind watermark fees | Fees incurred by blind watermark operations performed on images, including **adding** and **extracting**. Such fees are charged by the **number of processing times**. |          |                |
| Abnormal image detection fees | Fees incurred by abnormal image detection. Such fees are charged by the **number of processing times**. |          |                |



## Image Processing Pricing

| Billable Item | Price |
| :--------------- | :-------------------------------------------------------- |
| Basic image processing     | ≤ 10 TB: Free of charge<br />> 10 TB: 0.01 USD/GB                     |
| Image advanced compression     | 0.015 USD/1,000 times                                            |
| Guetzli image compression | 0.15 USD/1,000 times                                             |
| Blind watermark           | Adding: 0.15 USD/1,000 times <br />Extracting: 0.15 USD/1,000 times |
| Abnormal image detection     | 0.01493 USD/1,000 times                                          |



## Billing Example

Suppose you upload a batch of images to a bucket, use CI's image cropping and advanced compression features to process the images in real time, and add blind watermarks during upload.

Usage statistics show that the basic image processing usage is 5 TB, the advanced compression feature is used 10,000 times, and the blind watermark feature is used 10,000 times.

The following can be concluded:

| Item | Free Tier | Unit Price | Billable Usage | Fees (Unit Price * Billable Usage) |
| :--------------- | :------- | :------------- | :------- | :------------------ |
| Basic image processing | 10 TB     | 0.01 USD/GB/month | 0 GB      | 0 USD               |
| Image advanced compression | None       | 0.015 USD/1,000 times | 10,000 times | 0.015 * 10 = 0.15 USD   |
| Blind watermark       | None       | 0.15 USD/1,000 times  | 10,000 times | 0.15 * 10 = 1.5 USD     |
| **Monthly fees**       | -        | -              | -        | **1.65 USD**        |

>?
>
> - CI doesn't bill inbound traffic, so uploading images for real-time processing doesn't incur traffic fees.
> - Storage fees are charged by COS.