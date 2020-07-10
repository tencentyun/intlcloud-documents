## Style Separators
A style separator is a character that separates the file name from the processing style. It can be a hyphen (-), underscore (_), slash (/), or exclamation mark (!).

### Directions
1. Log in to the [CI Console](https://console.cloud.tencent.com/ci), click **Bucket Management**, and select the bucket for which to set the image style.
2. Click **Image Processing** in the left sidebar, and find the **Style Separator** section. Click **Edit**, and configure **Separator** to the exclamation mark (!). You can select one or more separators.
![](https://main.qcloudimg.com/raw/92c55ff1075bb647113f2de33ea64a61.png)
3. Click **Save**.

### Instructions
Format: http://[Domain name]/[File name] + [Separator] + [Style name]
For example, assume that the style separator is **!**, the style name is **yunstyle**, and the field of the original image is **sample.jpg**. The URL of the processed image is:
`http://space.image.com/sample.jpg!yunstyle`

>
- You can set a maximum of 100 styles for each bucket.
- To avoid ambiguity, do not use separators that are currently enabled to name processing styles.
- It takes an average of 30 minutes for settings to take effect.
- Changing separators requires purging the cache. It takes at least 24 hours for separator changes to take effect for both public and private networks.
- Canceling existing separators may cause product feature malfunctions.


## Setting Styles
Developers can set styles for images in the bucket to manage images for different purposes. The example style used here is an alias of the collection of real-time processing parameters during image downloading. The specific procedure is as follows:

1. Select a bucket, e.g. `imagetest1`, to open its configuration page.
2. Select the **Image Processing** tab and scroll down to **Style Management**.
3. Click **Add Styles** and enter the style name. You can set the resize mode, progressive display, output format, output effect, text watermark, image watermark, etc.
![](https://main.qcloudimg.com/raw/9f6c7cce07630253436a9d4eb8640d47.png)

>The style name is case-sensitive and can not be modified once saved.


### Instructions
#### Resize mode
CI supports three resize modes: [Scale + Crop](#st1), [Crop-only](#st2), and [Scale-only](#st3). The resize mode is optional, and you can also select **No-scaling** if you do not need to resize the image.


>CI’s scaling operation enlarges or shrinks images without stretching them.


<span id="st1"></span>

#### Scale + Crop
The **Scale + Crop** mode allows you to scale an image first, and then crop it into a smaller size. You can set the target width and height, and the crop position as well.
- **Proportional scaling**
Scales the image according to the size that you set without changing the aspect ratio of the original image.
- **Fixed width and height**
Scales the image to the exact size that you specify.
![Scale + Crop](https://main.qcloudimg.com/raw/ff573ce671721dfdac9ca554ba8831c2.png)

For example, if the original image resolution is 1200×900 and the thumbnail resolution is 600×600, the original image is first cropped by the aspect ratio of the thumbnail (that is, 600:600 or 1:1) to 900×900, then scaled down to the target resolution of 600×600.


<span id="st2"></span>
#### Crop-only
Use the “crop-only” method to crop the image according to the crop position and thumbnail size that you specify. Use the Crop Position grid to select the central position of cropping.
![Crop-only](https://main.qcloudimg.com/raw/7f0c3da4dfb5f6160ff1c83cf8068526.png)

For example, set the crop position to **center** and thumbnail resolution to 600×600. Then, the image is cropped starting from the center of the original image, then 300 pixels to each direction along the horizontal axis and vertical axis to form the 600×600 thumbnail.


<span id="st3"></span>
#### Scale-only
Use the “scale-only” method to scale the image according to the resolution that you specify.
- **Proportional scaling:** scales the image according to the resolution that you specify without changing the aspect ratio of the original image.
- **Fixed width and height:** scales the image to the exact resolution that you specify while ignoring the aspect ratio of the original image.

![Scale-only](https://main.qcloudimg.com/raw/189f1c74bbd5c3366951b25e16c82630.png)

### Text watermarks
Add a text watermark to the target image according to the text content, font, font size, font color, and transparency value that you specify. Use the Location grid to specify the watermark position.
![](https://main.qcloudimg.com/raw/b66c234e69fc2fc689e06387e13f631f.png)

### Image watermarks
Add an image watermark to the target image by using the image that you set. Use the Location grid to specify the watermark position.
![](https://main.qcloudimg.com/raw/e681ad02948366582d90b8b5b66e5547.png)

### Advanced settings
CI also provides advanced settings, which allow you to configure images by using parameters. For more information, see the [Basic Image Processing](https://intl.cloud.tencent.com/document/product/1045/33713) API document.
