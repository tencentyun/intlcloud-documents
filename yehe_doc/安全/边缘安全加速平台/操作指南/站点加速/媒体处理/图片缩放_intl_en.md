## Overview

EdgeOne can respond to the client with images in the specified size and format, and cache the processed images. The whole process is taken place on EdgeOne nodes.

## Use Cases

- Responds to the client with resized images. Only the original image is stored on the origin server, which reduces the image management costs.
- Compresses an image on the premise that the image quality is not visually degraded, which improves the page/image loading speed.

## Directions

1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Click **Site Acceleration** > **Media Processing** on the left sidebar.
2. On the page that appears, toggle **Image Resize** on.
   ![](https://qcloudimg.tencent-cloud.cn/raw/ff1e0bbba857aeab6e2552edd25b7204.png)

3. Concatenate `eo-img` parameters to the client request URL. Example: `https://www.example.com/foo.png?eo-img.resize=w/100`.
   The parameters are described as follows:
<table>
<thead>
<tr>
<th>Feature</th>
<th>Parameter</th>
<th>Value (type/pixel)</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td rowspan=5>Resize</td>
<td rowspan=5>eo-img.resize</td>
<td>w/100</td>
<td>Changes the width to the specified value. The height is automatically adjusted based on the aspect ratio.</td>
</tr>
<tr>
<td>h/100</td>
<td>Changes the height to the specified value. The width is automatically adjusted based on the aspect ratio.</td>
</tr>
<tr>
<td>w/100/h/100</td>
<td>Changes the width and height to the specified values.</td>
</tr>
<tr>
<td>l/100</td>
<td>Changes the long side of an image to the specified value. The short side is automatically adjusted based on the aspect ratio.</td>
</tr>
<tr>
<td>s/100</td>
<td>Changes the short side of an image to the specified value. The long side is automatically adjusted based on the aspect ratio.</td>
</tr>
<tr>
<td>Format conversion</td>
<td>eo-img.format</td>
<td>webp, heif, avif, guetzli, tpg, svg, jpg2000, or jpg-xr</td>
<td>Converts an image to the specified format.</td>
</tr>
</tbody></table>

## Limits
1. The original image cannot exceed 20 MB. For images over the limit, the original image is returned.
2. `eo-img.resize` and `eo-img.format` can be used at the same time. For example, `eo-img.resize=w/100&eo-img.format=webp` means to resize the image and convert the format.
3. The same parameter can only be specified once in a request URL. For example, `eo-img.resize=w/100&eo-img.resize=w/200` and `eo-img.resize=w/100&eo-img.format=webp&eo-img.resize=w/200` are not allowed. In this case, the parameter settings are invalid, and the original image is returned.
4. `width`/`height` and `long`/`short` parameters cannot be specified at the same time. For example, `w/300/s/200` is not allowed. In this case, the parameter settings are invalid, and the original image is returned.
5. If parameters are specified in an incorrect syntax, such as `eo-img.resize=w=100`, or are misspelled, the parameter settings are invalid, and the original image is returned.
6. If the **image resize** feature is disabled, `eo-img` parameters are processed as a common query string, and the original image is returned.

## Pricing and Billing
The image resize feature is billed based on the number of image resizing requests. For more information, see [Billing Overview](https://www.tencentcloud.com/document/product/1145/48705).

>? The image resize feature is currently free for a limited time. An announcement will be released when the free trial ends.

## Sample Configuration

In the following examples, the original image is 500 × 280 pixels in resolution and 500 KB in size.

1. Change the width to 200 pixels, and the height is automatically adjusted based on the aspect ratio.
Request URL: `http://www.example.com/foo.png?eo-img.resize=w/200`<br><img src="https://qcloudimg.tencent-cloud.cn/raw/fa35c9161cfcf7fd65fe164af13bdd38.png" width=500px>
2. Change the height to 200 pixels, and the width is automatically adjusted based on the aspect ratio.
Request URL: `http://www.example.com/foo.png?eo-img.resize=h/200`<br><img src="https://qcloudimg.tencent-cloud.cn/raw/f6c6cd2773c032705e4958d5c251754a.png" width=500px> 
3. Change the width to 300 pixels and the height to 200 pixels.
Request URL: `http://www.example.com/foo.png?eo-img.resize=w/300/h/200`
  >!If both the width and height are specified, the aspect ratio of the original image may not be retained.

   <img src="https://qcloudimg.tencent-cloud.cn/raw/6e3c142b4e878d1fa912d2839765f6a3.png" width=500px> 
4. Change the long side to 400 pixels, and the short side is automatically adjusted based on the aspect ratio.
   Request URL: `http://www.example.com/foo.png?eo-img.resize=l/400`<br><img src="https://qcloudimg.tencent-cloud.cn/raw/18cffd11fd3b4ce051c90b84e0c1ea17.png" width=500px> 
5. Change the short side to 200 pixels, and the long side is automatically adjusted based on the aspect ratio.
   Request URL: `http://www.example.com/foo.png?eo-img.resize=l/200`<br><img src="https://qcloudimg.tencent-cloud.cn/raw/e33ae53276eb9d611e9cd6633bdf71bb.png" width=500px> 
6. Convert the image to WebP format.
Request URL: `http://www.example.com/foo.png?eo-img.format=webp`
Output image format: WebP
7. Change the width to 200 pixels, with the height automatically adjusted based on the aspect ratio, and convert the format to WebP.
   Request URL: `http://www.example.com/foo.png?eo-img.resize=w/200&eo-img.format=webp`
