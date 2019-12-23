Blind watermarking is an exclusive watermarking service provided by Cloud Infinite (CI), which can embed invisible watermarks in the frequency domain of images. After an image is exploited, you can extract the watermark from the image for authentication and accountability.

Once activated in the console, this feature can add blind watermarks to uploaded images or during image uploading and downloading through the persistence processing API. When you need to detect images, extract blind watermarks through the extraction API.

>Blind watermarking is a paid service. For information on its pricing, see the [Purchase Guide](https://intl.cloud.tencent.com/document/product/1045/33431).

## Activating the Service in the Console
Log in to [CI Console](https://console.cloud.tencent.com/ci). On the **Bucket Management** page, select the bucket for which you want to activate the service (for example, buckettest). Click **Style**, toggle on **Status**, and click **Save**.
![](https://main.qcloudimg.com/raw/bb7f1c67596ec0ac49f621c99c898ba3.png)


>
- When using the blind watermark feature, ensure that the width and height of the watermark image do not exceed 1/8 of those of the original image.
- To ensure the proper effect of the blind watermark, use a white image on a black background as the watermark image.