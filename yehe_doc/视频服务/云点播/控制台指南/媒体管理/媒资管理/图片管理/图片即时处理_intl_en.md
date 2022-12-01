## Overview
This document shows you how to create a template in the [VOD console](https://console.cloud.tencent.com/vod/pics) to process images in real time. The processing is based on URLs, which allows quick image generation.
>? The original image cannot be larger than 32 MB. Its dimensions cannot exceed 30,000 pixels and its resolution cannot exceed 250 million pixels. The dimensions of the output image cannot exceed 9,999 pixels.

## Directions
### Step 1. Upload images
1. Log in to the [VOD console](https://console.cloud.tencent.com/vod) and select **Application Management** on the left sidebar.
2. Find the target application and click its name.
3. By default, you will be directed to **Media Assets > Video/Audio Management > Uploaded**.
4. Select **Image Management** on the left sidebar and click **Upload Image** to upload an image.

### Step 2. Create a template
1. Select **Media Processing > Template Settings** on the left sidebar and click **Image Processing Template**.
2. In addition to the preset templates listed on the page, you can also create your own template. The screenshots below show how to create a template to generate 240 x 240 thumbnails.
![](https://qcloudimg.tencent-cloud.cn/raw/79eb769ca9593f0924a9247e2da07e80.png)
![](https://qcloudimg.tencent-cloud.cn/raw/828297905d8d08e7363a0bd683491df5.png)
3. After a template is created successfully, it will appear in the template list, and a template ID will be generated for it.
![](https://qcloudimg.tencent-cloud.cn/raw/35893ec11a0e762466bdce3083e1b865.png)

You can also call an API of VOD to create an image processing template. For details, see [CreateImageProcessingTemplate](https://cloud.tencent.com/document/product/266/48901).

### Step 3. Learn about URL-based image processing

VOD processes images based on URLs.
#### URL of the processed image = URL of the original image + Separator + Image template ID + “.” + Output image format
  - URL of the original image: The accelerated URL generated after an image is uploaded to [VOD](https://console.cloud.tencent.com/vod/pics).
  - Separator: !
  - Output image format: JPG, JPEG, PNG


### Step 4. Learn about the processing types
There are two processing types: scaling and cropping.

<Table>
<tbody>
<tr>
<th>Type</th>
<th>Operation</th>
</tr>
<tr>
<td rowspan=5>Scaling</td>
<td>Width: Specified; height: Auto-scaled</td>
</tr>
<tr>
<td>Height: Specified; width: Auto-scaled</td>
</tr>
<tr>
<td>Long side: Specified; short side: Auto-scaled</td>
</tr>
<tr>
<td>Short side: Specified; long side: Auto-scaled</td>
</tr>
<tr>
<td>Width: Specified; height: Specified</td>
</tr>
<tr>
<td rowspan="2">Cropping</td>
<td>Cropping to circle, with the radius specified</td>
</tr>
<tr>
<td>Cropping to rectangle, with height and width specified</td>
</tr>
</tbody>
</Table>

#### Examples for scaling

- **Width: Specified; height: Auto-scaled**
 - Template ID: 13290; width: 700; output format: PNG.
 - The URL of the processed image is: `https://1500012191.vod2.myqcloud.com/6caaa776vodcq1500012191/0f9d472c387702299328320141/Cov1ATJ3AYYA.jpg!13290.PNG`
 - Result:
![](https://main.qcloudimg.com/raw/abf6f0699647efe9bef7f22d8f3fb939.png)

- **Height: Specified; width: Auto-scaled**
 - Template ID: 13291; height: 700; output format: PNG
 - The URL of the processed image is: `http://1500012191.vod2.myqcloud.com/6caaa776vodcq1500012191/0f9d472c387702299328320141/Cov1ATJ3AYYA.jpg!13291.PNG`
 - Result:
![](https://main.qcloudimg.com/raw/df5c784021a55910a67bd3fcf1be1ac8.png)

- **Long side: Specified; short side: Auto-scaled**
 - Template ID: 13292; long side: 300; output format: PNG
 - The URL of the processed image is: `https://1500012191.vod2.myqcloud.com/6caaa776vodcq1500012191/0f9d472c387702299328320141/Cov1ATJ3AYYA.jpg!13292.PNG`
 - Result:
![](https://main.qcloudimg.com/raw/fca36a5152c013ec9f111923f1f37b97.png)

- **Short side: Specified; long side: Auto-scaled**
 - Template ID: 13293; short side: 300; output format: PNG
 - The URL of the processed image is: `https://1500012191.vod2.myqcloud.com/6caaa776vodcq1500012191/0f9d472c387702299328320141/Cov1ATJ3AYYA.jpg!13293.PNG`
 - Result:
![](https://main.qcloudimg.com/raw/e3f9bd39fe92b57758d8954d44715d93.png)

- **Width: Specified; height: Specified**
 - Template ID: 13294; height: 300; width: 300; output format: PNG
 - The URL of the processed image is: `https://1500012191.vod2.myqcloud.com/6caaa776vodcq1500012191/0f9d472c387702299328320141/Cov1ATJ3AYYA.jpg!13294.PNG`
 - Result:
![](https://main.qcloudimg.com/raw/4225aa7986ac5f2f58b6cf061b51f64d.png)

#### Examples for cropping
- **Cropping to circle**
 - Template ID: 13295; radius: 300; output format: PNG
 - The URL of the processed image is: `http://1500012191.vod2.myqcloud.com/6caaa776vodcq1500012191/182b0f2a387702299461251102/EOy4fI1V8gQA.jpg!13295.PNG`
 - Result:
![](https://main.qcloudimg.com/raw/e62ef7791ff9b129259bd3fa04afd6d2.png)

- **Cropping to rectangle**
 - Template ID: 13296; output height: 300; output width: 300; output format: PNG
 - The URL of the processed image is: `http://1500012191.vod2.myqcloud.com/6caaa776vodcq1500012191/23c473bb387702299461744409/HVSbBfQq3JgA.jpg!13296.PNG`
 - Result:
![](https://main.qcloudimg.com/raw/433ea68294a8b8af47bae088e7a89508.png)