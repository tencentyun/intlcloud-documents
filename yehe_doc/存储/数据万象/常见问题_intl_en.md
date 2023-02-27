### What image processing features does CI support?
CI supports scaling, cropping, transcoding, watermarking, and more to meet your image processing needs.

### Which image formats can be processed by CI?
Currently, CI supports JPG, BMP, GIF, PNG, and WebP, as well as HEIF decoding and processing. For more information, see [Rules and Limits](https://intl.cloud.tencent.com/document/product/1045/33425).

### What are the limits of the image processing feature of CI?

The size of an input image cannot be larger than 32 MB, its width and height cannot exceed 30,000 pixels, and the total number of pixels cannot exceed 250 million. The width and height of the output image cannot exceed 9,999 pixels. For a source animated image, Width x Height x Number of frames cannot exceed 250 million pixels.

### Where is CI data stored?
CI uses Tencent Cloud Object Storage (COS) to store data. You can process images during the upload and store the results persistently in COS, or process images during the download.

### Why is "Permission denied" prompted when I use the processing feature?

"Permission denied" is prompted generally because no CI roles are bound. You can go to the [Service Authorization](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https://console.cloud.tencent.com/ci) page and click **Grant** to bind a CI role.
If you use a sub-account, this problem may be because the required operation permission is not granted. You can grant it as instructed in [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

### How do I migrate existing images to Tencent Cloud?
You can use COS Migration Tool or Migration Service Platform (MSP).
>?Source bucket names and the corresponding List permissions are required for the migration.

### How do I switch to Tencent Cloud CI without affecting use of images in the production environment network?
Use the mirroring-based origin-pull feature of COS to bind the COS bucket to your origin and switch the image processing domain name to the CI domain name (CI will pull the original image from the origin and process it, and COS will pull it asynchronously). This method can be used to migrate images, but only those requested.

### Does a CDN acceleration domain support image processing?

Yes. All you need to do is add the processing parameters at the end of the CDN file URL.

### Can I process an image multiple times with one request?
Yes. You can do this simply by using style separators. For example, `url?imageMorg2/cut/400x400|watermark/1/xxx` can both crop and add a watermark to the image.

### How is image processing billed?
For billing details of basic image processing (e.g., cropping, scaling, transcoding, and watermarking) and value-added services (e.g., content recognition, blind watermarking, and Guetzli), see [Billing Overview](https://intl.cloud.tencent.com/document/product/1045/33431).

### Will processed images be stored?
Images processed through an API during download won't be stored in your storage space.

### Can I process images when uploading or downloading them?
Yes. You can also process images already stored in COS buckets.

### Do image processing URLs support encrypted access?
Yes. You can encrypt URLs based on our encoding and decoding rules. Encrypted access is a customized feature. If you want to use it, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

### How do I perform multiple processing operations on an image?
For example, to crop and add a watermark to an image at the same time, you can use the pipeline operator "|" to concatenate the processing parameters so as to perform the processing operations sequentially on the image.

### What do I do if the WeChat Mini Program ignores the multi-processing rule?
Take the pipeline operator (|) as an example. It will be escaped or truncated by the WeChat Mini Program. Therefore, you need to redefine it.
You can:
- Use a style.
- Replace pipeline operators (|) with `%7C`.

### Why are the image quality and size unchanged no matter which parameters are added?
One possible cause is that the EXIF information of the original image accounts for the majority of the image size. If the image size shows little change after you adjust the image resolution, use the `Strip` parameter to remove the EXIF information as instructed in [Removing Image Metadata](https://intl.cloud.tencent.com/document/product/1045/33725).

### Why does the watermark not take effect?
The possible causes are as follows:
- The image watermark is not stored in the same bucket as the input image.
- The URL format of the image watermark is incorrect. For example, the URL must begin with `http://`. In this case, `http` cannot be omitted or replaced with `https`.
- The URL of the image watermark must use a CI endpoint. Do not use a CDN acceleration endpoint or other endpoints.


<span id="urlbase"></span>

### What is Base64 URL-safe encoding?

Many parameters of CI’s image processing (e.g., text, color, and font of the text watermark, as well as the URL of the image watermark) need to be Base64 URL-safe encoded. The rules are as follows:
1. Plus signs (+) in normal Base64-encoded results are replaced with hyphens (-).
2. Slashes (/) in the encoded results are replaced with underscores (_).
3. Remove `=` from the encoded results.


### What will be returned if the input image is larger than 32 MB?
CI will return 302 and redirect you to the URL of the image in COS for you to download the original image.


### What do I do if the enabled Guetzli does not take effect?

Guetzli is an image compression feature with no visual quality loss launched by CI. Once Guetzli is enabled, images in the bucket will be compressed with Guetzli upon the download, and `x-GuetzliState` will be added to the HTTP header of the request to indicate the compression status. If Guetzli does not take effect, you can:

1. Check whether [Guetzli Image Compression](https://intl.cloud.tencent.com/document/product/1045/42359) is enabled via the CI console.
2. Check whether the image to process is a JPG image (currently, Guetzli supports only JPG images).
3. Check whether the image to process meets the following requirements: q > 70; Number of pixels ＜ 4 million
4. Initiate another request again. If this is your first time accessing the image after Guetzli is enabled, the original JPG image will be returned, while Guetzli compression will be performed asynchronously. Therefore, when you initiate another request after the compression is completed, the compressed image will be returned.
5. Use a CI endpoint such as `examplebucket-1250000000.picgz.myqcloud.com` and try again. Currently, using COS endpoints (format: `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com`) for processing is not supported for some users.


### How do I configure if "Non-business domain names cannot be opened" is prompted when I use the document-to-HTML preview service in the mini program?

If you need to use the document-to-HTML preview service in the mini program, "Non-business domain names cannot be opened" may be prompted when you use the service for the first time. In this case, you can configure as follows:

1. Log in to the mini program backend and select **Development** > **Development Management** on the left sidebar.

2. Click **Development Settings** and locate the **Business Domain Name** section.

3. Click **Start Configuration**. In the pop-up window, add `https://prvsh.myqcloud.com` and your COS bucket domain name such as `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com`, click **Download Verification File**. Then, [contact us](https://intl.cloud.tencent.com/contact-sales) and provide the verification file for configuration.



