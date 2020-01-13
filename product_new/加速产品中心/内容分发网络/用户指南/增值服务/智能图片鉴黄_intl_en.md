## Feature Overview

Leveraging the deep learning image recognition technology of Tencent YouTu, CDN supports pornography detection to intelligently scan images distributed across the internet and identify pornographic information. This service protects your business from getting involved in distributing pornographic information. This service is currently in beta test.
The pornography detection service scans images distributed by CDN, scores each image based on its pornographic rating, and then classifies them as "suspicious images", "pornographic images", or "normal images".

> !
- Pornography detection service can keep the processing history of pornographic images for one month.
- Currently, pornography detection is only available to images distributed within Mainland China.

## Use Cases

#### Avoiding the risk of image violation
The pornography detection service intelligently scans the image resources distributed across the internet by CDN, mark and collect statistics on "suspicious images" and "pornographic images" for you to confirm and manage, helping you avoid the risk of getting involved in distributing pornographic images and ensuring business compliance.

## Operation Guide
1. Log into the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Pornography Detection** on the left sidebar to enter the  detection management page.
2. The **Suspicious Images** module is displayed by default in the console. You can switch to another module by clicking **Pornographic Images** or **Normal Images**.
   ![](https://main.qcloudimg.com/raw/dbacbda17404e1ee7333f8b49628bb39.png)

### Suspicious Images
> !When the pornography detection service scans and finds that your business resources contain suspected pornographic images, it will notify you via SMS, email, or internal message.
> 
1. The **Suspicious Images** module is displayed by default in the console. You can click the icon in the top-right corner to switch to thumbnail or list mode.
![](https://main.qcloudimg.com/raw/d674742535502d4db3942bd0b8683c09.png)
2. Manual Management
You can click **Normal Images** or **Pornographic Images** under an image and CDN will automatically mark it as a "normal" or "pornographic" image.
> CDN will also automatically block images classified as pornographic. If you want to unblock them, follow the steps in [Unblocking Images](#m1) below.
>
  ![](https://main.qcloudimg.com/raw/813ffd3c844a20a38fe4eda3c4d91097.png)
3. Automatic Management
   If you don't manually confirm a suspected pornographic image within 24 hours after the scan, CDN will automatically block it. You can click **Pornographic Images** on the top to switch to the "Pornographic Images" module and view the image. The blocking method is **Automatic**.

### Pornographic Images
> !When the pornography detection service of CDN scans and finds that your business resources contain pornographic images, it will directly block them to protect your business from getting involved in distributing pornographic information and your users will not be able to obtain them through CDN. You will be notified via SMS, email, or internal message.
> 
<span ID = "m1"></span>
1. The **Suspicious Images** module is displayed by default in the console. You can switch to another module by clicking **Pornographic Images**.
"Pornographic images" can be filtered by image status (not appealed, appeal in process, appeal rejected) and managed as needed.
![](https://main.qcloudimg.com/raw/b71d4e1c2c61c4af5405e0c1c3478b84.png)
2. Unblocking Images
  If you want to unblock an image, click **Appeal** at the bottom-right corner to initiate an appeal. The pornography detection service team of Tencent Cloud will manually verify the image. If it is incorrectly classified by CDN, the team will unblock it and notify you via SMS, email, or internal message.
  ![](https://main.qcloudimg.com/raw/376e9365647f582730d44044fc4fc0fd.png)

### Normal Images
If your business resources are classified as "normal images", CDN will not block them temporally. However, they will be manually verified by the service team and entered into the sample library to optimize the pornography detection algorithm.
The **Suspicious Images** module is displayed by default in the console. You can switch to another module by clicking **Normal Images**. You can view the confirmation status of each image in the "Normal Images" module.
![](https://main.qcloudimg.com/raw/175fae728a71f0e1877803390f453cb5.png)
