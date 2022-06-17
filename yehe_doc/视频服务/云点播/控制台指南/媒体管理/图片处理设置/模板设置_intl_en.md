1. Log in to the [VOD console](https://console.cloud.tencent.com/vod) and select **Application Management** on the left sidebar.
2. Select the target application.
3. Select **Video Processing > Template Settings** on the left sidebar.


## Image Processing Template

Select **Image Processing Template** and click **Create Image Processing Template** to create a custom template.
+ Template name: Up to 64 characters; supports Chinese characters, letters, digits, spaces, underscores (_), hyphens (-), and periods (.).
+ How to process: Scale or crop.
+ Scale:
	+ Width: Specify the output width (pixels). Value range: 1-9999. **Do not select** this if you want the width to be scaled proportionally.
	+ Height: Specify the output height (pixels). Value range: 1-9999. **Do not select** this if you want the height to be scaled proportionally.
+ Crop:
	+ Crop to circle
		+ Radius: Specify the radius (greater than 0) of the output circle.
	+ Crop to rectangle
		+ Target size: Specify the width (pixels) and height (pixels) of the output rectangle. Value range: 1-9999.

#### Preset templates
For information about preset image processing templates, see [Preset Templates - Image Processing](https://intl.cloud.tencent.com/document/product/266/47373).
