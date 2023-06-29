
## Overview
When distributing mass images with Tencent Cloud CDN, you can enable image optimization. This feature can compress images that meet specified requirements into WebP, Guetzli, and TPG formats, while drastically reducing downstream traffic and costs. 

## Directions
Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar. Click **Manage** on the right of a domain name configured with a COS origin. On the page that appears, select **Image Optimization**.
- Only domain names that are configured with a COS V5 origin are supported.
- If the CI service is not yet activated before this feature is enabled, you can quickly complete the activation in the CDN console.
- If the CI service is already activated, you can use this feature directly.

>?[Tencent Cloud CI](https://intl.cloud.tencent.com/products/ci) provides you a secure, stable and efficient cloud data processing service. When images (Webp, Guetzli, TPG) are processed, charges for the CI service will be incurred. For more billing details, see [Billing Overview](https://intl.cloud.tencent.com/document/product/1045/33431).

### WebP adaptation
When WebP adaptation is enabled, images that meet the following compression requirements will be processed and returned. If these requirements are not met, the original images will be returned.
- The HTTP Accept header contains `image/webp`. 
- The image is in JPG, JPEG, BMP, GIF, or PNG format.

>! 
>- The charges incurred are included in the billable item "Basic Image Processing" of your CI bill.
>- The image to be processed should not be larger than 20 MB, with the width and height not exceeding 30,000 pixels and the total number of pixels not exceeding 100 million. The width and height of the output image should not exceed 9,999 pixels.
>- For an input animated image, the total number of pixels (Width x Height x Number of frames) cannot exceed 100 million pixels (GIF frame limit: 300).

### Guetzli adaptation
The CI-launched Guetzli image compression feature is visually lossless. It compresses JPG images at a high ratio to reduce the downstream traffic and increase the download speed. By taking advantage of human beings’ insensitivity toward specific color gamuts and details, Guetzli discards specific details to reduce download traffic by 35% to 50% without changing quality.

When Guetzli adaptation is enabled, images that meet the following compression requirements will be processed and returned.
- The HTTP Accept header contains `image/guetzli`.
- The image is in JPG or JPEG format.

> !
>- The charges incurred are included in the billable item "Guetzli Compression" of your CI bill.
>- After you enable Guetzli, the original JPG image will be returned when you access the image for the first time, and Guetzli will compress the image asynchronously. If you request the image again after the compression is complete, the compressed image will be returned.
>- Currently, Guetzli can process JPG images whose quality is greater than 70 and number of pixels is smaller than 4 million.

### TPG adaptation

TPG adaption is a CI-launched advanced image compression feature. It converts images into TPG format with smaller image size, greatly reducing the download traffic and improving the page load speed.

When TPG adaption is enabled, images that meet the following compression requirements will be processed and returned.
- The HTTP Accept header contains `image/tpg`.
- The image is in JPG, JPEG, BMP, GIF, PNG, or WebP format.

>! The charges incurred are included in the billable item "Image Advanced Compression" of your CI bill.

## Must-knows
After image optimization is enabled, the cache key of the request URL will change and conflict with the configured cache key rules. In this case, the cache key rules take higher priority.
For example, when image optimization is enabled for JPG files, the request URL `http://www.test.com/a.jpg?colour=red` changes to `http://www.test.com/a.jpgxxxxxx ?colour=red`, which conflicts with the configured cache key rule that ignores all parameters for all files. In this case, the rule will be executed, and the request URL will eventually change to `http:/ /www.test.com/a.jpgxxxxxx`.




