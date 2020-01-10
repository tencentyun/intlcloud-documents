## Style Separators
A style separator is a character that separates the file name from the processing style. This separator can be a hyphen (-), underscore (_), slash (/), or exclamation mark (!).

### Directions
1. Log in to [CI Console](https://console.cloud.tencent.com/ci). In the left sidebar, click **Bucket Management** and click the bucket for which you want to set the style to go to the bucket configuration page.
2. On the bucket configuration page, click **Style** on the top and locate **Style Management**. Change **Separator** to the exclamation mark (**!**). In this case, you can select one or more separators.
![](https://main.qcloudimg.com/raw/6f6c238f1e809b0a944b977476ca155f.png)

### Instructions
Format: http://[Domain name]/[File name] + [Separator] + [Style name]
For example, assume that the style separator is **!**, the style name is **yunstyle**, and the fileid of the original image is **sample.jpg**. The URL of the processed image is:
`http://space.image.com/sample.jpg!yunstyle`.

>
- You can set a maximum of 100 styles for each bucket.
- To avoid ambiguity, do not use separators that are currently enabled to name processing styles.
- It takes an average of 30 minutes for settings to take effect.
- Changing separators requires purging the cache. It takes at least 24 hours for separator changes to take effect for both public and private networks.
- Canceling existing separators may cause product feature malfunctions.


## Setting Styles
Developers can set styles for images in the bucket to manage images for different purposes. The example style used here is an alias of the collection of real-time processing parameters during image downloading. The specific procedure is as follows:

1. Select a bucket (for example, imagetest1) and go to the **Style** page. Then, click **Add Style**.
![Add style](https://main.qcloudimg.com/raw/749118d5bf657fb727f94d6c61432721.png)
2. Go to the style editing page and enter the style name. You can set the thumbnail method, progressive effect, output format, output effect, and text watermark or image watermark.
![Style 2](https://main.qcloudimg.com/raw/4e1951a61bec4279f4d0c0a725223586.png)

>The style name is case-sensitive and can not be modified once saved.


### Instructions
#### Thumbnail method
CI supports three thumbnail methods: crop + scale, crop-only, and scale-only. The thumbnail method is optional, and you can also select **No thumbnail**.


>CI’s scaling operation enlarges or shrinks images without stretching them.

- **crop + scale**
When the original image is large and the target image is small and has a different aspect ratio, use **crop + scale** to scale the image to the thumbnail size, then crop it according to the crop position and the width and height that you set. Use the Sudoku orientation chart to select the central position of cropping.

- **Scale proportionally**
Scale the image according to the size that you set without changing the aspect ratio of the original image.

- **Scale to fixed width and height**
Scale the image to the exact resolution that you specify.
![crop + scale](https://main.qcloudimg.com/raw/0e9b659e1c11955e00c69ba7abe5b34e.png)

For example, if the original image resolution is 1200×900 and the thumbnail resolution is 600×600, the original image is first cropped by the aspect ratio of the thumbnail (that is, 600:600 or 1:1) to 900×900, then scaled down to the target resolution of 600×600.

#### Crop-only
Use the “crop-only” method to crop the image according to the crop position and thumbnail size that you specify. Use the Sudoku orientation chart to select the central position of cropping.
![crop-only](https://main.qcloudimg.com/raw/5c884d7ede2c8a38f538108b38a100ec.png)

For example, set the crop position to **center** and thumbnail resolution to 600×600. Then, the image is cropped starting from the center of the original image, then 300 pixels to each direction along the horizontal axis and vertical axis to form the 600×600 thumbnail.

#### Scale-only
Use the “scale-only” method to scale the image according to the resolution that you specify.
***Scale proportionally:** Scale the image according to the resolution that you specify without changing the aspect ratio of the original image.
**Scale to fixed width and height:** Scale the image to the exact resolution that you specify, and ignore the aspect ratio of the original image.

![scale-only](https://main.qcloudimg.com/raw/d65bc5a6b68316eb5316019f5f41de07.png)

### Text watermarks
Add a text watermark to the target image according to the text content, font, font size, font color, and transparency value that you specify. Use the Sudoku orientation chart to specify the watermark position.
![Text watermark](https://main.qcloudimg.com/raw/4ca38256668ee716271b582c5c526095.png)

### Image watermarks
Add an image watermark to the target image by using the image that you set. Use the Sudoku orientation chart to specify the watermark position.
![Image watermark](https://main.qcloudimg.com/raw/767136b69920bf54a4d122216a9ec8ff.png)

### Advanced settings
CI also provides advanced settings, which allow you to configure images by using parameters. For more information, see the [Basic Image Processing](https://intl.cloud.tencent.com/document/product/1045/33713) API document.