## Overview

The CI-launched Guetzli image compression feature is **visually lossless**. It compresses **JPG images** at a high ratio to reduce the downstream traffic and increase the download speed. By taking advantage of human beings’ insensitivity toward specific color gamuts and details, Guetzli discards specific details to reduce image sizes by 35% to 50% without changing the quality.


## Directions

1.  Log in to the [CI console](https://console.cloud.tencent.com/ci) and click **Bucket Management** on the left sidebar.
2.  Click the desired bucket to go to the bucket management page.
3.  Click **Image Processing** > **Image Compression** and find the **Image Guetzli Image Compression** area. Then, click **Edit**, set **Status** to **Enabled**, and click **Save**.
>?
>
>- After you enable Guetzli, **the original JPG image will be returned when you access the image for the first time**, and Guetzli will compress the image asynchronously. If you request the image again after the compression is complete, the compressed image will be returned.
>- Currently, Guetzli can process JPG images whose quality is greater than 70 and number of pixels is smaller than 16 million.
>- For the prices of Guetzli image compression, please see [Billing and Pricing](https://intl.cloud.tencent.com/document/product/1045/33431). CI provides a free tier of **3,000** images per month for each account. The exceeding part will be charged. If you don’t use up your free tier, it will not roll over to the next month.

## Guetzli Status Codes

After Guetzli image compression is enabled, `x-GuetzliState` will be added to the HTTP request headers for images in the bucket to indicate the Guetzli compression status, which is described as follows:

| `x-GuetzliState` Status Code | Description |
|:-|:-|
| < 0 | Unable to compress as the compression requirements are not met |
| 0 | Does not perform Guetzli compression |
| 1 | Guetzli compression request has been initiated |
| 2 | Guetzli compressing |
| 3 | Not processed yet as the input image cache has not expired |
| 100 | Compressed successfully |
