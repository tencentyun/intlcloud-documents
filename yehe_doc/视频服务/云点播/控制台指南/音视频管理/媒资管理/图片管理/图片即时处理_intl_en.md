## Overview
This document shows you how to create a template in the [VOD console](https://console.cloud.tencent.com/vod/pics) to process images in real time. The processing is based on URLs, which allows quick image generation.

## Directions
### Step 1. Upload images
1. Log in to the [VOD console](https://console.cloud.tencent.com/vod) and select **Application Management** on the left sidebar.
2. Find the target application and click its name.
3. By default, you will enter the **Media Assets > Video Management > Uploaded ** page.
4. Select **Image Management** on the left sidebar and click **Upload Image**.

### Step 2. Create a template

You can create a real-time image processing template by calling a VOD API.

1. For example, to create a template for 240 x 240 thumbnails, use the request URL below:
```shell
https://vod.tencentcloudapi.com/?Action=CreateImageProcessingTemplate
&Operations.0.Type=Scale
&Operations.0.Scale.Type=ShortEdgeFirst
&Operations.0.Scale.ShortEdge=240
&Operations.1.Type=CenterCut
&Operations.1.CenterCut.Type=Rectangle
&Operations.1.CenterCut.Width=240
&Operations.1.CenterCut.Height=240
&<Common request parameters>
```
2. The template ID returned by the API is `1009`.
```javascript
{
  "Response":{
    "Definition": 1009,
    "RequestId": "12ae8d8e-dce3-4151-9d4b-5594145287e1"
  }
}
```

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
<td>Width: specified; height: auto-scaled</td>
</tr>
<tr>
<td>Height: specified; width: auto-scaled</td>
</tr>
<tr>
<td>Long side: specified; short side: auto-scaled</td>
</tr>
<tr>
<td>Short side: specified; long side: auto-scaled</td>
</tr>
<tr>
<td>Width: specified; height: specified</td>
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

#### Type 1. Scaling

- **Width: specified; height: auto-scaled**
 - Template ID: 13290; width: 700; output format: PNG.
 - The URL of the processed image is: `https://1500012191.vod2.myqcloud.com/6caaa776vodcq1500012191/0f9d472c387702299328320141/Cov1ATJ3AYYA.jpg!13290.PNG`
 - Result:
![](https://main.qcloudimg.com/raw/abf6f0699647efe9bef7f22d8f3fb939.png)

- **Height: specified; width: auto-scaled**
 - Template ID: 13291; height: 700; output format: PNG
 - The URL of the processed image is: `http://1500012191.vod2.myqcloud.com/6caaa776vodcq1500012191/0f9d472c387702299328320141/Cov1ATJ3AYYA.jpg!13291.PNG`
 - Result:
![](https://main.qcloudimg.com/raw/df5c784021a55910a67bd3fcf1be1ac8.png)

- **Long side: specified; short side: auto-scaled**
 - Template ID: 13292; long side: 300; output format: PNG
 - The URL of the processed image is: `https://1500012191.vod2.myqcloud.com/6caaa776vodcq1500012191/0f9d472c387702299328320141/Cov1ATJ3AYYA.jpg!13292.PNG`
 - Result:
![](https://main.qcloudimg.com/raw/fca36a5152c013ec9f111923f1f37b97.png)

- **Short side: specified; long side: auto-scaled**
 - Template ID: 13293; short side: 300; output format: PNG
 - The URL of the processed image is: `https://1500012191.vod2.myqcloud.com/6caaa776vodcq1500012191/0f9d472c387702299328320141/Cov1ATJ3AYYA.jpg!13293.PNG`
 - Result:
![](https://main.qcloudimg.com/raw/e3f9bd39fe92b57758d8954d44715d93.png)

- **Width: specified; height: specified**
 - Template ID: 13294; height: 300; width: 300; output format: PNG
 - The URL of the processed image is: `https://1500012191.vod2.myqcloud.com/6caaa776vodcq1500012191/0f9d472c387702299328320141/Cov1ATJ3AYYA.jpg!13294.PNG`
 - Result:
![](https://main.qcloudimg.com/raw/4225aa7986ac5f2f58b6cf061b51f64d.png)

#### Type 2. Cropping
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

