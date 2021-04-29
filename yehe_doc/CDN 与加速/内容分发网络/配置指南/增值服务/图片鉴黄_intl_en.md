## Feature Overview

Leveraging the deep learning image recognition technology of Tencent YouTu, CDN supports pornography detection to intelligently scan images distributed across the internet and identify pornographic content. This service protects your business from the risk of distributing pornographic content. This service is currently in beta.
The pornography detection service spot checks and scans images distributed by CDN, scores each image based on its pornographic rating, and then classifies them as "suspicious images", "pornographic images", or "normal images".

> !
>- Pornography detection service can keep the processing history of pornographic images for one month.
>- Currently, pornography detection is only available to images distributed in the Chinese mainland.

## Use Cases

#### Avoiding image violation
The pornography detection service intelligently scans the image resources distributed across the internet by CDN, mark and collect statistics on "suspicious images" and "pornographic images" for you to confirm and manage, helping you avoid the risk of distributing pornographic images and ensuring business compliance.

## Operation Guide
1. Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Pornography Detection** on the left sidebar to enter the detection management page.
2. The **Suspicious Images** tab is displayed by default in the console. You can switch to another tab by clicking **Pornographic Images** or **Normal Images**.
   ![](https://main.qcloudimg.com/raw/6a5032ae03e9d818de743ab729e49540.png)

### Suspicious images
> !When the pornography detection service scans and finds that your business resources contain suspected pornographic images, it will notify you via SMS, email and the console Message Center.

1. The **Suspicious Images** tab is displayed by default in the console. You can click the icon in the top-right corner to switch to thumbnail or list mode.
![](https://main.qcloudimg.com/raw/e563618d7e2a1db33c590f186490f545.png)
2. Manual management
You can click **Normal Images** or **Pornographic Images** under an image and CDN will automatically mark it as a "normal" or "pornographic" image.
>? CDN will also automatically block images classified as pornographic. If you want to unblock them, follow the steps in [Unblocking Images](#m1) below.

3. Automatic management
   If you do not manually confirm a suspected pornographic image within 24 hours after the scan, CDN will automatically block it. You can click **Pornographic Images** to switch to the "Pornographic Images" tab and view the image. These images will be blocked automatically.

### Pornographic images
> !When the pornography detection service of CDN scans and finds that your business resources contain pornographic images, it will directly block them to protect your business from running the risk of distributing pornographic content. Your users will not be able to receive these images through CDN. You will be notified via SMS, email and the console Message Center.

<span ID = "m1"></span>
1. The **Suspicious Images** tab is displayed by default in the console. Click **Pornographic Images** to view the **Pornographic Images** tab.
**Pornographic Images** can be filtered by image status and managed as needed. Filters include `not appealed`, `appeal in process` and `appeal rejected`.
![](https://main.qcloudimg.com/raw/e68168dd147f828144414116afa5d489.png)
2. Unblocking images
If you want to unblock an image, click **Appeal** at the bottom-right corner to initiate an appeal. The Tencent Cloud pornography detection service team will manually verify the image. If it is incorrectly classified by CDN, the team will unblock it and notify you via SMS, email and the console Message Center.
![](https://main.qcloudimg.com/raw/cb039e15fe71b426bbd946cfbb7ad03f.png)

### Normal images
If your business resources are classified as "normal images", they will not be blocked by CDN. However, they will be manually verified by the service team and entered into the sample library to optimize the pornography detection algorithm.
The **Suspicious Images** tab is displayed by default in the console. Click **Normal Images** to view images and their individual confirmation status in the "Normal Images" tab.
![](https://main.qcloudimg.com/raw/accc286fec2374675e1f86f7e588132d.png)
