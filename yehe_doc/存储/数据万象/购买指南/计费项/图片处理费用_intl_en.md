CI offers flexible and powerful image processing features, such as rotation, cropping, transcoding, and scaling. It provides multiple image downsizing solutions like Guetzli compression, TPG transcoding, and HEIF transcoding, as well as diversified copyright protection solutions like image/text/blind watermarking. This meets your image processing needs in different business scenarios.



## Image Processing Fees

Image processing fees are divided into **basic image processing fees**, **image advanced compression fees**, **Guetzli image compression fees**, and **blind watermark fees**, as detailed below:

| Billable Item               | Description                                                   | Billing Cycle | Applicable Billing Mode                                         |
| -------------------- | ------------------------------------------------------------ | -------- | ------------------------------------------------------ |
| Basic image processing fees | Fees incurred by image processing when you download or persistently store images. Such fees are charged by the processed data volume according to the **original image size**. | Monthly | Pay-as-you-go <br />Resource pack: Basic image processing resource pack |
| Image advanced compression fees | Fees incurred by image conversion to formats with a high compression ratio, such as TPG, AVIF, and HEIF. Such fees are charged by **uses**. | Monthly | Pay-as-you-go <br />Resource pack: Image compression resource pack |
| Guetzli image compression fees | Fees incurred by Guetzli lossless compression of JPG images. Such fees are charged by **compression times**. | Monthly | Pay-as-you-go <br />Resource pack: Image compression resource pack deducted at the ratio of 1:10 |
| Blind watermark fees | Fees incurred by blind watermark operations performed on images, including **adding** and **extracting**. Such fees are charged by **processing times**. | Monthly | Pay-as-you-go <br />Resource pack: Blind watermark resource pack |



## Image Processing Pricing

<table>
<thead>
<tr>
<th>Billable Item</th>
<th>Price</th>
</tr>
</thead>
<tbody><tr>
<td>Basic image processing</td>
<td>
<ul style="margin-bottom:0px">
<li>≤ 10 TB: Free of charge</li>
<li>> 10 TB: 0.025 CNY/GB</li>
</ul>
</td>
</tr>
<tr>
<td>Image advanced compression</td>
<td>
<ul style="margin-bottom:0px">
<li>TPG: 0.1 CNY/1,000 times</li>
<li>HEIF: 0.1 CNY/1,000 times</li>
<li>AVIF: 0.3 CNY/1,000 times</li>
</ul>
</td>
</tr>
<tr>
<td>Guetzli image compression</td>
<td>1 CNY/1,000 times</td>
</tr>
<tr>
<td>Blind watermark</td>
<td>Blind watermark adding: 1 CNY/1,000 times; blind watermark extracting: 1 CNY/1,000 times</td>
</tr>
</tbody></table>



## Billing Example

Suppose you upload a batch of images to a bucket, use CI's image cropping and Guetzli compression features to process the images in real time, and add blind watermarks during upload.

Usage statistics show that the basic image processing usage is 5 TB, the Guetzli compression feature is used 10,000 times, and the blind watermark feature is used 10,000 times. You purchased a 100,000-times image compression resource pack valid for 12 months in the Chinese mainland last month.

The following can be concluded:

| Item | Free Tier | Unit Price | Resource Pack | Billable Usage | Fees (Unit Price * Billable Usage) |
| ---------------- | -------- | ------------- | -------------------- | ------- | ------------------- |
| Basic image processing | 10 TB     | 0.025 CNY/GB/month | None                   | 0 GB     | 0 CNY                 |
| Guetzli compression  | None       | 1 CNY/1,000 times      | Resource pack of 100,000 image compressions | 0 times     | 0 CNY                 |
| Blind watermark       | None       | 1 CNY/1,000 times      | None                   | 10,000 times | 10 CNY                |
| **Monthly fees**       | -        |     -          |          -            |    -     | **10 CNY**            |

>?
> - CI doesn't bill inbound traffic, so uploading images for real-time processing doesn't incur traffic fees.
> - The deduction order of CI billable items is resource pack > pay-as-you-go. Guetzli compressions can be deducted from image compression resource packs and don't incur pay-as-you-go fees.
> - Storage fees are charged by COS.
