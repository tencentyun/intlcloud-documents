## Feature Overview
COS uses the **imageView2** API of CI to provide common image processing templates. You only need to add corresponding parameters to the downloading URL to generate corresponding thumbnails.

An image can be processed:

- Upon download
- Upon upload
- In cloud

>! Image Processing is charged by CI. For detailed pricing, see **Basic image processing fee** in [Billing and Pricing](https://www.tencentcloud.com/document/product/1045/45582).
>

## Restrictions

- Format: JPG, BMP, GIF, PNG, and WebP images can be processed, and HEIF images can be decoded and processed.
- Static image size: The input image cannot be larger than 32 MB. Its dimensions cannot exceed 50,000 pixels and its resolution cannot exceed 250 million pixels. The dimensions of the output image cannot exceed 50,000 pixels.
- WebP image size: The input image cannot be larger than 32 MB. Its dimensions cannot exceed 16,383 pixels and its resolution cannot exceed 250 million pixels. The dimensions of the output image cannot exceed 16,383 pixels.
- Animated image size: For the input or output image, the total number of pixels (width x height x number of frames) cannot exceed 250 million pixels.
- Number of frames (for animated images): For GIF, the number of frames cannot exceed 300.


## API Format

#### 1. Processing upon download

```plaintext
GET /<ObjectKey>?imageView2/<mode>/w/<Width>
                 /h/<Height>
                 /format/<Format>
                 /q/<Quality>
                 /rq/<Quality>
                 /lq/<Quality> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
```

>! Quality parameters apply only to images in **JPG** and **WebP** formats.

#### 2. Processing upon upload

```plaintext
PUT /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
Pic-Operations: 
{
  "is_pic_info": 1,
  "rules": [{
      "fileid": "exampleobject",
      "rule": "imageView2/<mode>/w/<Width>
                 /h/<Height>
                 /format/<Format>
                 /q/<Quality>
                 /rq/<Quality>
                 /lq/<Quality>"
  }]
}
```

>? `Pic-Operations` is a JSON string. Its parameters are as described in [Persistent Image Processing](https://www.tencentcloud.com/document/product/1045/33695).
>

#### 3. Processing in-cloud data

```plaintext
POST /<ObjectKey>?image_process HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-length: Size
Authorization: Auth String
Pic-Operations: 
{
  "is_pic_info": 1,
  "rules": [{
      "fileid": "exampleobject",
      "rule": "imageView2/<mode>/w/<Width>
                 /h/<Height>
                 /format/<Format>
                 /q/<Quality>
                 /rq/<Quality>
                 /lq/<Quality>"
  }]
}
```

>? 
> - Authorization: Auth String (see [Request Signature](https://www.tencentcloud.com/document/product/436/7778) for more information)
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://www.tencentcloud.com/document/product/1045/49896).
> 

## Parameters

| Parameter       | Description                                                                                                                                        |
| ----------------------------- | ------------------------------------------------------------ |
| ObjectKey  | Object name, such as `folder/sample.jpg`.                           | 
| /1/w/&lt;Width>/h/&lt;Height> | Mode 1: specifies the minimum width and height of the thumbnail. <br>In this mode, the image is first scaled down until one of the minimum values set is reached. Then, the image will be centered and evenly cropped on both sides to meet the specified values. <br>If only one value is set, a square thumbnail will be generated. <br>For example, if the input image size is 1000 x 500 and this parameter is set to `?imageView2/1/w/500/h/400`, the image will be scaled down to 800 x 400 first. Then, 150 pixels will be cropped from the left and right sides respectively, outputting a 500 x 400 thumbnail. |
| /2/w/&lt;Width>/h/&lt;Height> | Mode 2: specifies the maximum width and height of the thumbnail. <br>In this mode, the image is scaled down until both the width and length are not greater than the maximum values set. <br>For example, if the input image size is 1000 x 500 and this parameter is set to `?imageView2/2/w/500/h/400`, the image is scaled down to 500 x 250. <br>If only one value is set, the image will be adapted. |
| /3/w/&lt;Width>/h/&lt;Height> | Mode 3: specifies the minimum width and height of the thumbnail. <br>In this mode, the image is scaled down until both the width and height are not smaller than the minimum values set. <br>For example, if the input image size is 1000 x 500 and this parameter is set to `??imageView2/3/w/500/h/400`, the image is scaled down to 800 x 400. <br>If only one value is set, a square thumbnail will be generated. |
| /4/w/&lt;LongEdge>/h/&lt;ShortEdge> | Mode 4: specifies the minimum values of the long edge and short edge of the thumbnail to scale down the image. <br>If only one value is set, a square thumbnail will be generated. |
| /5/w/&lt;LongEdge>/h/&lt;ShortEdge> | Mode 5: specifies the maximum values of the long edge and short edge of the thumbnail to scale down the image. The image will be then centered and cropped. <br>If only one value is set, a square thumbnail will be generated. <br>After the scaling, the excess will be cropped. |
| /format/&lt;Format> | Format of the thumbnail, which can be JPG, BMP, GIF, PNG, or WebP. Default value: format of the input image |
| /q/&lt;Quality> | Image quality. Value range: 0−100. Default value: quality of the input image. The smaller value between the input image quality and the specified quality will be used. If there is an exclamation mark (!) after `&lt;Quality>`, the specified quality will be used. |
| /rq/&lt;quality> | Relative quality of the image, relative to that of the input image. Value range: 0−100. For example, if the input image quality is 80 and `rquality` is set to `80`, the quality of the output image is 64 (that is, 80 x 80%). |
| /lq/&lt;quality> | Minimum quality of the image. Value range: 0−100. <br>If the input image quality is 85 and `lquality` is set to `80`, the quality of the output image is 85.<br>If the input image quality is 60 and `lquality` is set to `80`, the quality of the output image will be improved to 80. |


## Examples

>? **Processing upon download** is used as an example here, which does not store the output image in a bucket. If you need to store the output image, see [Persistent Image Processing](https://www.tencentcloud.com/document/product/436/40592) and use **Processing upon upload** or **Processing in-cloud data**.


#### Example 1: Using mode 1
The following example uses mode 1, and sets the minimum width and height of the thumbnail to 400x600, and the absolute quality to 85:

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageView2/1/w/400/h/600/q/85
```

Generated thumbnail:
![](https://main.qcloudimg.com/raw/281a2f6474ad29b430355f785f158a5c.jpeg)

#### Example 2: Using mode 1 with a signature carried
This example processes the image in the same way as in the example above except that a signature is carried. The signature is joined with other processing parameters using an ampersand (&):

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=<signature>&imageView2/1/w/400/h/600/q/85
```

>? You can obtain the value of `<signature>` by referring to [Request Signature](https://www.tencentcloud.com/document/product/436/7778).
>

## Notes

To prevent unauthorized users from accessing or downloading the input image by using a URL that does not contain any processing parameter, you can add the processing parameters to the request signature, making the processing parameters the key of the parameter with the value left empty. The following is a simple example for your reference (it might not be valid or accessible anymore). For more information, please see [Request Signature](https://www.tencentcloud.com/document/product/436/14114).


```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=sha1&q-ak=AKID********************&q-sign-time=1593342360;1593342720&q-key-time=1593342360;1593342720&q-header-list=&q-url-param-list=watermark%252f1%252fimage%252fahr0cdovl2v4yw1wbgvzlteyntewmdawmdqucgljc2gubxlxy2xvdwquy29tl3nodwl5aw4uanbn%252fgravity%252fsoutheast&q-signature=26a429871963375c88081ef60247c5746e834a98&watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAwMDQucGljc2gubXlxY2xvdWQuY29tL3NodWl5aW4uanBn/gravity/southeast
```




