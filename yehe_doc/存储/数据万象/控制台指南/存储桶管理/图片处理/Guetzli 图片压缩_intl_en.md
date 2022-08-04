## Overview

CI's Guetzli image compression feature is a **visually lossless** compression service. It compresses **JPG images** at a high ratio to reduce the downstream traffic usage and accelerate downloads. By leveraging human eyes' insensitivity to specific color gamuts and details, Guetzli discards specific details to reduce the image size by 35% to 50% without changing the quality.


## Directions

1. Log in to the [CI console](https://console.cloud.tencent.com/ci/bucket).
2. Click **Bucket Management** on the left sidebar to enter the bucket management page.
3. Click the name of the target bucket.
4. On the left sidebar, click **Image Processing**.
5. Find the **Guetzli Image Compression** configuration item and click **Edit** to change its status to **Enabled**.
6. Click **Save**.
>?
>- After you enable Guetzli, **the original JPG image will be returned if you access the image for the first time**, and Guetzli will compress the image asynchronously. If you request the image again after the compression is completed, the compressed image will be returned.
>- Currently, Guetzli can process JPG images with the quality being greater than 70 and the number of pixels being smaller than 16 million.
>- Guetzli is a paid feature. For billing details, see [Billing Overview](https://intl.cloud.tencent.com/document/product/1045/33431).
>

## Guetzli Status Codes

After Guetzli image compression is enabled, `x-GuetzliState` will be added to the HTTP request headers for images in the bucket to indicate the Guetzli compression status as described below:

| x-GuetzliState Status Code | Description |
|:-|:-|
| < 0 | The image cannot be processed as the compression requirements are not met. |
| 0 | Guetzli compression is not performed. |
| 1 | The Guetzli compression request has been initiated. |
| 2 | Guetzli compressing is in progress. |
| 3 | The image is not processed as the input image cache has not expired. |
| 100 | Compressed successfully. |
