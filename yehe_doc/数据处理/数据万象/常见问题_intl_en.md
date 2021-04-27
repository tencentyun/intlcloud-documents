### What image processing features does Cloud Infinite (CI) provide?
CI supports scaling, cropping, transcoding, watermarking, and more to meet your image processing needs.

### What image formats can CI process?
Currently, CI supports JPG, BMP, GIF, PNG, and WebP, as well as HEIF decoding and processing. For more information, please see [Rules and Limits](https://intl.cloud.tencent.com/document/product/1045/33425).

### What is the maximum size of an input image?

The size of an input image cannot be larger than 20 MB, its width and height cannot exceed 30,000 pixels, and the total number of pixels cannot exceed 250 million. The width and height of the output image cannot exceed 9,999 pixels. For a source animated image, Width x Height x Number of frames cannot exceed 250 million pixels.

### Where does CI store my data?
CI uses Tencent Cloud Object Storage (COS) to store data. You can process images during the upload and store the results persistently in COS, or process images during the download.

### How can I migrate my images to Tencent Cloud?
You can use COS Migration Tool or Migration Service Platform (MSP).
>?Source bucket names and the corresponding List permissions are required for the migration.

### How can I switch to Tencent Cloud CI without interrupting the use of images by my current website?
You can use the image origin-pull feature of COS to bind COS buckets to your origin server, then replace the image processing domain name with the CI domain name (CI pulls original images from the origin server and then processes them, while COS pulls images asynchronously.) In this method, only resources that you request will be migrated.

### Do CDN domain names support image processing?

Yes. All you need to do is add the processing parameters in the CDN file URL.

### Can I perform several operations with one request?
Yes, you can achieve this by using style separators. For example, with url?imageMorg2/cut/400x400|watermark/1/xxx, you can crop an image and add a watermark at the same time.

### How is CI billed?
Basic image processing (e.g., scaling, cropping, transcoding, and watermarking) is charged at 0.01 USD/GB. Advanced features (e.g., content recognition, blind watermarking, and Guetzli) are charged additionally. For detailed pricing, please see [Billing and Pricing](https://intl.cloud.tencent.com/document/product/1045/33431).

### Will processed images be stored?
Processed images will be stored through APIs. Images processed during downloading will not be stored in customers’ storage.

### Can I process images during uploading or downloading?
Yes. You can also process images already stored in COS buckets.

### Do image processing URLs support encrypted access?
Yes. You can encrypt URLs based on our encoding and decoding rules. Encrypted access is a customized feature. If you want to use it, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

### How can I perform several operations on an image at the same time?
Take cropping + watermarking as an example, use the pipeline operator **l** to connect respective processing parameters, and then both operations will be performed in sequence.

### What do I do if the WeChat Mini Program ignores the multi-processing rule?
Take the pipeline operator (|) as an example. It will be escaped or truncated by the WeChat Mini Program. Therefore, you need to redefine it.
You can:
- Use a style.
- Replace pipeline operators (|) with `%7C`.

### Why do the quality and size of the image stay the same no matter which parameters I use?
One possible cause is that the EXIF information of the input image accounts for the majority of the image size. If the image size shows little change after you adjust the image resolution, use the **strip** parameter to remove the EXIF information. For instructions, see [Removing Meta Information](https://intl.cloud.tencent.com/document/product/1045/33725).

### Why does the watermark not take effect?
The possible causes are as follows:
- The image watermark is not stored in the same bucket as the input image.
- The URL format of the image watermark is incorrect. For example, the URL must begin with `http://`. In this case, HTTP cannot be omitted and HTTPS cannot be used.
- The URL of the image watermark must use a CI endpoint. Do not use a CDN acceleration endpoint or other endpoints.


<span id="urlbase"></span>

### What is Base64 URL-safe encoding?

Many parameters of CI’s image processing (e.g., text, color, and font of the text watermark, as well as the URL of the image watermark) need to be Base64 URL-safe encoded. The rules are as follows:
1. Plus signs (+) in normal Base64-encoded results are replaced with hyphens (-).
2. Slashes (/) in the encoded results are replaced with underscores (_).
3. All equal signs (=) appended to the encoded results are retained.


### What will be returned if the input image is larger than 20 MB?
CI will return 302 and redirect you to the URL of the image in COS for you to download the input image.


### What do I do if the enabled Guetzli does not take effect?

Guetzli is an image compression feature with no visual quality loss launched by CI. Once Guetzli is enabled, images in the bucket will be compressed with Guetzli upon the download, and `x-GuetzliState` will be added to the HTTP header of the request to indicate the compression status. If Guetzli does not take effect, you can:

1. Check whether [Guetzli Image Compression](https://intl.cloud.tencent.com/document/product/1045/33443) is enabled via the CI console.
2. Check whether the image to process is a JPG image (currently, Guetzli supports only JPG images).
3. Check whether the image to process meets the following requirements: q > 70; Number of pixels ＜ 4 million
4. Initiate another request again. If this is your first time accessing the image after Guetzli is enabled, the original JPG image will be returned, while Guetzli compression will be performed asynchronously. Therefore, when you initiate another request after the compression is completed, the compressed image will be returned.
5. Use a CI endpoint such as `examplebucket-1250000000.picgz.myqcloud.com` and try again. Currently, using COS endpoints (format: `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com`) for processing is not supported for some users.


