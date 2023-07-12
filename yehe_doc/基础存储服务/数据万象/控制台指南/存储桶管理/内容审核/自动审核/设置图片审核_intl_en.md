## Overview
**This document describes how to use the image moderation feature in the console. After you enable image moderation, new images uploaded to a bucket will be automatically moderated, and the identified non-compliant content can be automatically blocked (by denying public read access to the content).**

The incremental image moderation feature can check image content for **pornographic**, **illegal**, and **advertising** information.

After you configure image moderation, new images uploaded to a bucket will be automatically moderated **during upload**, and the identified non-compliant content can be automatically blocked (by denying public read access to the content).

You can also scan **historical** image files in COS to detect pornographic, illegal, and advertising content. For more information, see Setting Historical Data Moderation Task and [Moderating Image](https://intl.cloud.tencent.com/document/product/1045/49320).

>? 
> - Supported image formats: PNG, JPEG, JPG, BMP, WEBP, GIF.
> - Supported image file size: < 32 MB. To moderate images larger than 5 MB in size, you need to enable the large image moderation feature.
> - Supported image dimensions: > 20 * 20 px (width * height).
>

## Operation Process
<img style="width:418px; max-width: inherit;" src="https://staticintl.cloudcachetci.com/yehe/backend-news/3YaP402_PRELIM__%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1_%E4%BA%A7%E5%93%81%E7%9B%AE%E5%BD%95_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US-1.png" />


## Directions

1. Log in to the [CI console](https://console.cloud.tencent.com/ci). On the **Bucket Management** page, select the target bucket to enter the bucket management page.
2. On the left sidebar, select **Sensitive Content Moderation** > **Automatic Moderation Configuration** and click **Image Moderation**.
3. Click **Add Automatic Image Moderation Configuration** and set the following configuration items:
 - **Moderation Scope**: You can select **The whole bucket** or **Specified Range**.
    - **Path**: If you select **Specified Range**, enter the path of the images to be moderated. <br>Example 1: To moderate files in the test directory, set this field to `test/`.<br>Example 2: To moderate files prefixed with `123`, set this field to `123`.
>!You can add multiple moderation configurations, but the paths cannot be duplicate or have inclusion relationships. If you have configured to moderate the entire bucket, you cannot add a moderation configuration for a specific path in the bucket.
>
 - **Moderation Suffix**: The following image formats can be moderated: JPG, JPEG, PNG, BMP, WEBP, and GIF. Two options are supported: **Smart** and **Without suffix**.
>?**Smart**: After you select this option, the system will intelligently determine whether a file is an image based on its file extension and content.
>
 - **Moderation Policy**: Select a moderation policy. You can create different policies for refined moderation. Moderation scene options include **Pornographic**, **Illegal**, and **Advertisement**, and you can select one or multiple options. For detailed directions on how to configure a moderation policy, see [Setting Moderation Policy](https://intl.cloud.tencent.com/document/product/1045/52107).
 - **Moderation Scene**: It displays the default scene or the scene that you configure in the moderation policy. You can select the target scene as needed.
 - **Restricted File Block**: You can enable this service to authorize CI to perform automatic or manual moderation and block the identified non-compliant files by denying public read access to them.
 - **Block Type**: You can select a block type and mechanism. **Machine moderation and block** is selected by default. If you select **Manual review freeze**, TenDI's professional team will review suspiciously sensitive images identified during machine moderation. You can select the image score range for blocking (by specifying an integer between 60 and 100; the greater the score, the more sensitive the image).


 - **Callback**: After callback is enabled, you will receive image moderation results. You need to select the moderation type, callback content, callback URL, and image domain name. If you select **Custom Callback Threshold**, you need to set the score range of the images for callback. After the callback URL is set, CI will send the default callback message to the set URL to check whether it can receive callback messages normally. For more information on callback, see [Viewing Image Moderation Callback Content](https://intl.cloud.tencent.com/document/product/436/48540).
4. After completing the configuration, click **Save**. Images uploaded subsequently will be moderated.


<span id=2></span>
## Notes

1. Image moderation adopts a scoring mechanism, with a score between 0 and 100 returned for each image.
2. The **confirmed part** refers to the images that are confirmed to be normal or sensitive (with a score in the range of [0,60] or (90,100]). For such images, no manual intervention is required.
3. The **uncertain part** refers to the images that are suspected to be sensitive (with a score in the range of (60,90]). For such images, manual moderation is recommended.
