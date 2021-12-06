## Overview
In the [VOD console](https://console.cloud.tencent.com/vod/pics), you can perform image processing. This document introduces how to perform real-time image processing through image processing templates, and you can quickly get image processing results from image URLs.

## Directions
### Step 1. Upload images
1. Go to the [VOD console](https://console.cloud.tencent.com/vod/pics), select a non-admin application (primary application), click **Media Assets** > **[Image Management](https://console.cloud.tencent.com/vod/)** on the left sidebar, and click **Upload Image**.
![](https://qcloudimg.tencent-cloud.cn/raw/fed2ab4f8f9b94f15bae2c3c734a0f41.png)
2. Select the target image.
![](https://qcloudimg.tencent-cloud.cn/raw/592b99b27e42cb3734132ee8acc5f51e.png)
3. Click **Upload**.
![](https://qcloudimg.tencent-cloud.cn/raw/300743187dc0a04f37bfdbb839074a63.png)
4. After uploading, find the image in the **Uploaded** tab, and click **Manage**. You can see the URL of this image for acceleration.
![](https://qcloudimg.tencent-cloud.cn/raw/ac55111bc39488563f7abc3412cd9a54.png)

### Step 2. Create template

You can use VOD APIs to create a template for image processing, with more granular configurations.

1. For example, suppose you create a template for 240 x 240 thumbnail.
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
2. The image processing template number returned is `1009`.
```javascript
{
  "Response": {
    "Definition": 1009,
    "RequestId": "12ae8d8e-dce3-4151-9d4b-5594145287e1"
  }
}
```

### Step 3. Process the image

Process the image by URL, with the following formula:
#### URL of the processed image = URL of the original image + Space identifier + Image template ID + “.” + Output image format
  - URL of the original image: the acceleration URL generated after an image is uploaded to the [VOD](https://console.cloud.tencent.com/vod/pics) platform.
  - Space identifier: !
  - Output image format: JPG, JPEG, PNG


### Step 4. Process the image by type
Image processing supports scaling and cropping.

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
<td>Image long side: specified; image short side: auto-scaled</td>
</tr>
<tr>
<td>Image short side: specified; image long side: auto-scaled</td>
</tr>
<tr>
<td>Width: specified; height: specified</td>
</tr>
<tr>
<td rowspan="2">Cropping</td>
<td>Cropping to incircle, with the radius specified</td>
</tr>
<tr>
<td>Cropping to rectangle, with height and width specified</td>
</tr>
</tbody>
</Table>

#### Type 1. Scaling

- **Width: specified; height: auto-scaled**
 - Template: 10033; width: 700; output format: PNG
 - URL of the output image: `http://1500003022.vod2.myqcloud.com/6c99162fvodcq1500003022/8215ff285285890811169205193/FcbdNXl2pswA.jpg!10033.PNG`
 - Result:
![](https://main.qcloudimg.com/raw/abf6f0699647efe9bef7f22d8f3fb939.png)

- **Height: specified; width: auto-scaled**
 - Template: 10034; height: 700; output format: PNG
 - URL of the output image: `http://1500003022.vod2.myqcloud.com/6c99162fvodcq1500003022/8215ff285285890811169205193/FcbdNXl2pswA.jpg!10034.PNG`
 - Result:
![](https://main.qcloudimg.com/raw/df5c784021a55910a67bd3fcf1be1ac8.png)

- **Image long side: specified; image short side: auto-scaled**
 - Template: 10035; image long side: 300; output format: PNG
 - URL of the output image: `http://1500003022.vod2.myqcloud.com/6c99162fvodcq1500003022/8215ff285285890811169205193/FcbdNXl2pswA.jpg!10035.PNG`
 - Result:
![](https://main.qcloudimg.com/raw/fca36a5152c013ec9f111923f1f37b97.png)

- **Image short side: specified; image long side: auto-scaled**
 - Template: 10036; image short side: 300; output format: PNG
 - URL of the output image: `http://1500003022.vod2.myqcloud.com/6c99162fvodcq1500003022/8215ff285285890811169205193/FcbdNXl2pswA.jpg!10036.PNG`
 - Result:
![](https://main.qcloudimg.com/raw/e3f9bd39fe92b57758d8954d44715d93.png)

- **Width: specified; height: specified**
 - Template: 10037; height: 300; width: 300; output format: PNG
 - URL of the output image: `http://1500003022.vod2.myqcloud.com/6c99162fvodcq1500003022/8215ff285285890811169205193/FcbdNXl2pswA.jpg!10037.PNG`
 - Result:
![](https://main.qcloudimg.com/raw/4225aa7986ac5f2f58b6cf061b51f64d.png)

#### Type 2. Cropping
- **Cropping to incircle**
 - Template: 10038; output circle radius: 300; output format: PNG
 - URL of the output image: `http://1500003022.vod2.myqcloud.com/6c99162fvodcq1500003022/8215ff285285890811169205193/FcbdNXl2pswA.jpg!10038.PNG`
 - Result:
![](https://main.qcloudimg.com/raw/e62ef7791ff9b129259bd3fa04afd6d2.png)

- **Cropping to rectangle**
 - Template: 10039; output image height: 300; output image width: 300; output format: PNG
 - URL of the output image: `http://1500003022.vod2.myqcloud.com/6c99162fvodcq1500003022/8215ff285285890811169205193/FcbdNXl2pswA.jpg!10039.PNG`
 - Result:
![](https://main.qcloudimg.com/raw/433ea68294a8b8af47bae088e7a89508.png)

