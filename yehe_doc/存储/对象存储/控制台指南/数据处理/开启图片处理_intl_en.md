## Overview

This document describes how to use image processing in the COS Console with the following two methods. For more information, see [Image Processing Overview](https://intl.cloud.tencent.com/document/product/436/35280).

- **Adding parameters to an image URL**: you can process an image by adding parameters to its object URL.
- **Using an image style**: you can save different processing results as image styles, which can be used to standardize your image processing. Such a style is an assembled template designed to process parameters in real time when an image is downloaded.

>!
> - This image processing feature is only supported for Public Cloud regions.
> - Image processing is a paid service, the fees of which are charged by Cloud Infinite. For detailed billing instructions, see Cloud Infinite’s [Billing and Pricing](https://intl.cloud.tencent.com/document/product/1045/33431).

## Adding URL Parameters

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5/bucket).
2. Locate the bucket that stores the image, and click the bucket name to enter the bucket details page.
3. Find the image file, and click **Details** under the **Actions** column.
4. Copy the **Object Address** and paste it into the address bar of your browser.
>!To process an image object, you need the write permission for it. For object permissions setting, see [Setting Object Access Permission](https://intl.cloud.tencent.com/document/product/436/13327).
5. In your address bar, add parameters behind the object URL using the format below. For more image processing parameters and instructions, see the Cloud Infinite API documentation [Basic Image Processing](https://intl.cloud.tencent.com/document/product/1045/33713).
```sh
Object URL?API name/operation name/processing parameters
```
>!If the image is private read, you need to add image processing parameters to a signed URL.

**Example: scaling an image to 50% of its original size**
Suppose that the original image is public read and private write in COS, with an object URL `https://examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/sample.jpeg`:
![img](https://main.qcloudimg.com/raw/3d4682ff8e622425ebd29913810a5c38.jpeg)

Next, add the following parameters to the URL:

- API: imageMogr2
- Operation: thumbnail
- Processing parameters: !50p

Now, you obtain a new URL `https://examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/!50p`. Paste this URL to you address bar, press Enter, and you will see a scaled image as shown below:
![](https://main.qcloudimg.com/raw/f48dba67ddfac797136a552dc6a14816.jpg)

## Using an Image Style

An image style is a template that combines real-time processing parameters for image download, and can be used to standardize image processing. The following example shows you how it works by using an image style of **target width 480 px, and target height 270 px**:


1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5/bucket).
2. Locate the bucket that stores the image, and click the bucket name to enter the bucket details page.
3. In the left menu bar, click **Image Processing** to enter the **Styles Management** page.
   **Separator**: a symbol that separates the file name and processing style, including “-”, “_”, “/”, and “!”. Select “!” here and save.
4. Click **Add Style** to configure the following:
	- **Style Name**: enter a custom style name, such as “yunstyle”.
> ! 
> - Note that style names are case-sensitive and cannot be modified once saved.
> - For the purpose of clarity, the separator you have enabled cannot be used in the style name.
	- **Edit Mode**: select Basic.
  - Scale Mode: select Scale Only.
  - Scale Option: select Target Width/Height.
  - Scale Size: width: 480 px, height: 270 px.
  - Progressive Display: once enabled, the images you access will be displayed progressively. Leave the default **Off** here.
  - Output Format: image output format. Use the default original format here.
5. Once completed, you can click the **Preview** button on the right.
6. Click **Save**, and you will see that an image named “yunstyle” has been added.
> ?
> - Up to 100 styles can be set for a single bucket.
> - A new style takes effect in 30 minutes on average.
> - Changing a separator requires clearing your cache, with the change taking effect across the entire network in at least 24 hours.
> - Removing a separator already in use may make some features unable to work properly.
> - For more information on image styles, see [Setting Styles](https://intl.cloud.tencent.com/document/product/1045/33443).
7. Go to the object details page, copy the object URL, and enter your separator and style name behind the URL in the following format:
```
Object URL + separator + style name
```
Now, you get a final object URL `https://examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/sample.jpeg!yunstyle`. Paste it to your address bar, press Enter, and you will see a scaled image as shown below:
![](https://main.qcloudimg.com/raw/f48dba67ddfac797136a552dc6a14816.jpg)





