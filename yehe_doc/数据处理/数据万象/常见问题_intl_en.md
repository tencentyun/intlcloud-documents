### What image processing features does Cloud Infinite (CI) provide?
CI offers a myriad of image processing features such as zoom, crop, transcoding, watermarks, and content moderation.

### What image formats does CI support?
CI supports images in JPG, BMP, GIF, PNG, and WEBP. It can also decode and process HEIF images.

### What are the limits for images that need processing in CI?
The maximum image size is limited to 20 MB, with both the height and width less than 9,999 pixels.

### Where does CI store my data?
CI uses buckets based on Tencent Cloud Object Storage (COS) to store data. You can choose to process images when uploading them and store the results in the cloud or do so while downloading them.

### How can I migrate my images to Tencent Cloud?
You can use the COS Migration Tool or Migration Service Platform (MSP).
> You need to provide the name of the source bucket and give COS Migration Tool or MSP listing permission.

### How can I switch to Tencent Cloud CI without interrupting the use of images on my website?
You can use image origin-pull to bind COS buckets to your origin server, then replace the image processing domain name with the CI domain name (CI pulls original images from the origin server and then processes them, while COS pulls images asynchronously.) You can use this feature to migrate your images, but only requested resources are migrated.

### Do CDN domain names support image processing?
CI supports image processing through CDN domain names. You can enable CDN acceleration in the CI Console. Alternatively, in the CDN Console, set the acceleration domain name origin server to the CI domain name (by selecting **Own origin** and entering the CI domain name).

### Can I perform multiple operations with one request?
Yes. You can achieve this by using style separators. For example, with url?imageMorg2/cut/400x400|watermark/1/xxx, you can crop an image and add a watermark at the same time.

### How is CI billed?
- Refer to [Billing and Pricing](https://intl.cloud.tencent.com/document/product/1045/33431) for more information.

### Will images be stored after being processed?
Images processed when they are downloaded using APIs are not stored in the buckets.

### Can I process images during uploading or downloading?
Yes, you can. You can also process images already stored in COS buckets.

### Do image processing URLs support encrypted access?
Yes. You can encrypt URLs based on our encoding and decoding rules. Encrypted access is a customized feature, if you want to use it, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply.

### How can I perform multiple operations on an image at the same time?
Take cropping + watermarking as an example, use the pipeline operator **l** to connect respective processing parameters, and then both operations will be performed in sequence.

### What should I do if many processing rules are invalid in WeChat Mini Programs?
Take the pipeline operator **|** as an example. The pipeline operator **|** is replaced or truncated in WeChat Mini Programs, so you need to redefine the operator.
The solution is as follows:
- Use styles.
- Replace **|** with **%7C**.

### Why do the quality and size of the image stay the same no matter which parameters I use?
One possible cause is that original image contains too much EXIF information, which accounts for the majority of the image size. If the image size shows little change after adjusting the image resolution, use the **strip** parameter to remove the EXIF information. For instructions, refer to [Removing Meta Information](https://intl.cloud.tencent.com/document/product/1045/33725).

### Why does the watermark not take effect?
This issue may result from the following reasons:
- The watermarked image and the original image are not in the same bucket.
- The format of the URL of the watermarked image is incorrect. For example, the URL must begin with **http://**. In this case, do not omit the HTTP string and do not use HTTPS.
- The URL of the watermarked image must use the CI domain. Do not use the CDN acceleration domain name or other domain names.

### Can I sync my hotlink protection configuration from CI to COS?
Each hotlink protection configuration is bound to a specific domain name. CI and COS have different domain names, and therefore their hotlink protection configurations are independent of each other.
