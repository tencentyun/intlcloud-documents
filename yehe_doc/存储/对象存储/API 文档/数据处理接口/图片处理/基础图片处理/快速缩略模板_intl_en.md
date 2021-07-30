## Overview
COS uses the **imageView2** API provided by Cloud Infinite (CI) to generate a thumbnail. You can append parameters to the download URL to generate the desired thumbnail. The input image cannot be larger than 32 MB, with its width and height not exceeding 30,000 pixels and the total number of pixels not exceeding 250 million. The width and height of the output image cannot exceed 9,999 pixels. For an input animated image, the total number of pixels (Width x Height x Number of frames) cannot exceed 250 million.

>! Image Processing is charged by CI. For detailed pricing, please see **Basic image processing fee** in [Billing and Pricing](https://intl.cloud.tencent.com/document/product/1045/33431).
>

## API Format

```plaintext
imageView2/<mode>/w/<Width>
                 /h/<Height>
                 /format/<Format>
                 /q/<Quality>
                 /rq/<Quality>
                 /lq/<Quality>
```

>! Quality parameters apply only to images in **JPG** and **WebP** formats.
>


## Parameters

| Parameter | Description |
| ----------------------------- | ------------------------------------------------------------ |
| download_url | URL of the input image, formatted as `<BucketName-APPID>.cos.<Region>.myqcloud.com/<picture name>`<br>Example: `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |
| /1/w/&lt;Width>/h/&lt;Height> | Mode 1: specifies the minimum width and height of the thumbnail. <br>In this mode, the image is first scaled down until one of the minimum values set is reached. Then, the image will be centered and evenly cropped on both sides to meet the specified values. <br>If only one value is set, a square thumbnail will be generated. <br>For example, if the input image size is 1000x500 and this parameter is set to `?imageView2/1/w/500/h/400`, the image will be scaled down to 800x400 first. Then, 150 pixels will be cropped from the left and right sides respectively, outputting a 500x400 thumbnail. |
| /2/w/&lt;Width>/h/&lt;Height> | Mode 2: specifies the maximum width and height of the thumbnail. <br>In this mode, the image is scaled down until both the width and length are not greater than the maximum values set. <br>For example, if the input image size is 1000x500 and this parameter is set to `?imageView2/2/w/500/h/400`, the image is scaled down to 500x250. <br>If only one value is set, the image will be adapted. |
| /3/w/&lt;Width>/h/&lt;Height> | Mode 3: specifies the minimum width and height of the thumbnail. <br>In this mode, the image is scaled down until both the width and height are not smaller than the minimum values set. <br>For example, if the input image size is 1000x500 and this parameter is set to `??imageView2/3/w/500/h/400`, the image is scaled down to 800x400. <br>If only one value is set, a square thumbnail will be generated. |
| /4/w/&lt;LongEdge>/h/&lt;ShortEdge> | Mode 4: specifies the minimum values of the long edge and short edge of the thumbnail to scale down the image. <br>If only one value is set, a square thumbnail will be generated. |
| /5/w/&lt;LongEdge>/h/&lt;ShortEdge> | Mode 5: specifies the maximum values of the long edge and short edge of the thumbnail to scale down the image. The image will be then centered and cropped. <br>If only one value is set, a square thumbnail will be generated. <br>After the scaling, the excess will be cropped. |
| /format/<Format> | Format of the thumbnail, which can be JPG, BMP, GIF, PNG, or WebP. Default value: format of the input image |
| /q/&lt;Quality> | Absolute quality of the image. Value range: 0−100. Default value: quality of the input image. The smaller value between the input image quality and the specified quality will be used. If there is an exclamation mark (!) after `&lt;Quality>`, the specified quality will be used. |
| /rq/<quality> | Relative quality of the image, relative to that of the input image. Value range: 0−100. For example, if the input image quality is 80 and `rquality` is set to `80`, the quality of the output image is 64 (that is, 80 x 80%). |
| /lq/<quality> | The lowest quality of the output image. Value range: 0−100. <br>If the input image quality is 85 and `lquality` is set to `80`, the quality of the output image is 85.<br>If the input image quality is 60 and `lquality` is set to `80`, the quality of the output image will be improved to 80. |


## Examples
#### Using mode 1
The following example uses mode 1, and sets the minimum width and height of the thumbnail to 400x600, and the absolute quality to 85:

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageView2/1/w/400/h/600/q/85
```

Generated thumbnail:
![](https://main.qcloudimg.com/raw/281a2f6474ad29b430355f785f158a5c.jpeg)

#### Using mode 1 with a signature carried
This example processes the image in the same way as in the example above except that a signature is carried. The signature is joined with other processing parameters using an ampersand (&):

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=<signature>&imageView2/1/w/400/h/600/q/85
```

>? You can obtain the value of `<signature>` by referring to [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
>
