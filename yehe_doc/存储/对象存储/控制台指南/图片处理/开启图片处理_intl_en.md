## Overview

This document describes how to use COS Image Processing in the Console, with the following two methods available for you. For more information on image processing, see [Image Processing Overview] (https://cloud.tencent.com/document/product/436/42215).

- **Adding parameters to an image URL**: You can process an image by entering parameters behind the object URL of the image.
- **Using an image style**: You can save different processing results by creating styles, and use such styles to standardize your image processing. The style created is an assembled template designed to process parameters in real time when an image is downloaded.

>
> - This image processing feature is only supported for Public Cloud regions in mainland China.
> - Image Processing is a paid service, the fees of which are charged by Cloud Infinite. For detailed billing instructions, see Cloud Infinite’s [Billing and Pricing] (https://intl.cloud.tencent.com/document/product/1045/33431).

## Adding URL parameters

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5/bucket).
2. Locate the bucket that stores the image, and click the bucket name to enter the bucket management page.
3. In the right sidebar to the image file, click **Details** to enter the file details page.
4. Copy the **Object URL** and paste it into the address bar of your browser.
>To process an image, you need the write permission on objects. For object permissions setting, see [Setting Object Access Permission] (https://intl.cloud.tencent.com/document/product/436/13327).
5. In your address bar, enter parameters behind the object URL using the format below. For more image processing parameters and instructions, see the Cloud Infinite API documentation [Basic Image Processing] (https://cloud.tencent.com/document/product/460/6924).
```sh
Object URL?processing API name/processing operation name/processing parameter
```
> If the access permission on the image file is private read, you will need to add image processing parameters to the signed address.

**Example: scaling an image to 50% of its original size**
Suppose that the original image is displayed as below, the access permissions on the object are public read and private write, and the object URL is `https://examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/sample.jpeg`.
![img](https://main.qcloudimg.com/raw/3d4682ff8e622425ebd29913810a5c38.jpeg)

Next, add the following parameters in the URL link:

- Scaling API: imageMogr2
- Scaling operation name: thumbnail
- Processing parameter: !50p

Now, you obtain a new URL with added parameters `https://examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/!50p`. Paste this URL to you address bar, press Enter, and you will see a scaled image shown as below:
![](https://main.qcloudimg.com/raw/f48dba67ddfac797136a552dc6a14816.jpg)

## Using an image style

Image Style can help you present different processing parameters in the format of template to standardize your image processing. The style created is an assembled template designed to process parameters in real time when an image is downloaded. Now, let’s take **Image Style: width: 480px, height: 270px** as an example, and introduce how to use this feature:


1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5/bucket).
2. Locate the bucket that stores the image, and click the bucket name to enter the bucket management page.
3. In the left menu bar, click **Image Processing** to enter the **Style Management** page.
   **Separator**: Style separators are symbols that separates file names and processing styles, and include “-”, “_”, “/”, and “!”. Select “!” here and save.
4. Click **Add Style** to enter the **New Style** page where you can see configuration as follows:
	- **Style Name**: Enter your custom style name, such as “yunstyle”.
> 
> - Note that style names are case-sensitive and cannot be modified after being saved.
> - For the purpose of clarity, the separator you have enabled cannot appear in the processing style name.
	- **Edit Mode**: Select Basic.
  - Scale Mode: Select Scale Only.
  - Scale Option: Select Set Width/Height.
  - Scale Size: width: 480px, height: 270px.
  - Progressive Display: Once enabled, the images you access will be displayed progressively. It is disabled by default if you Save here.
  - Output Format: allows you to choose a format for outputting your image, with the original image retained by default.
5. Once your configuration is done, You can click the Preview button on the right for preview.
6. After the preview, click **Save**, and you will see that an image style named “yunstyle” has been added.
>
> - Up to 100 styles can be set in a single bucket.
> - It is set to take effect in 30 minutes on average.
> - Changing a separator requires clearing your cache, with the change taking effect across the entire work in at least 24 hours.
> - Removing a separator already in use may make some product features unable to work properly.
> - For more information on image styles, see [Setting Styles] (https://intl.cloud.tencent.com/document/product/1045/33443).
7. Go to the object details page, copy the object URL, and enter your separator and style name behind the URL in the following format:
```
Object URL + Separator + Processing style name
```
Now, you can obtain a final object URL `https://examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/sample.jpeg!yunstyle`. Paste it to your address bar, press Enter, and you will see a scaled image shown as below:
![](https://main.qcloudimg.com/raw/f48dba67ddfac797136a552dc6a14816.jpg)





