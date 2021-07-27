## Feature
This API **imageView2** from Tencent Cloud CI is used to provide common image processing templates in COS. You only need to add appropriate parameters to the downloading URL to generate thumbnails that you want. Currently, supported images are smaller than 20 MB in size and smaller than 9,999 pixels in length and width.

>!Image processing is a paid service, the fees of which are charged by Cloud Infinite. For detailed billing instructions, see Cloud Infinite’s [Billing and Pricing](https://intl.cloud.tencent.com/document/product/1045/33431).

## API Form

```plaintext
imageView2/<mode>/w/<Width>
                 /h/<Height>
                 /format/<Format>
                 /q/<Quality>
                 /rq/<Quality>
                 /lq/<Quality>			
```

>!Quality conversion parameters are only applicable to **jpg** and **webp** images.


## Parameter Description

| Parameter                         | Description                                                         |
| ----------------------------- | ------------------------------------------------------------ |
| download_url | URL that is used to access a file. Format: `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`,<br>such as `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |
| /1/w/&lt;Width>/h/&lt;Height> | Template 1: limits the minimum width and height of a thumbnail. This operation proportionally scales an image until one of its edges reaches the preset minimum value, and then centrally crops the other edge to the preset value. If only one edge is specified, it indicates a square with equal width and height.<br>For example, assume that the size of an original image is 1000 x 500. If this parameter is set to `?imageView2/1/w/500/h/400`, the image is proportionally scaled to 800 x 400 and then it is cropped by 150 on the left and right sides, resulting in an image of 500 x 400. |
| /2/w/&lt;Width>/h/&lt;Height> | Template 2: limits the maximum width and height of a thumbnail. This operation proportionally scales an image until its width and height are smaller than the preset maximum value. <br>For example, assume that the size of an original image is 1000 x 500. If this parameter is set to `?imageView2/2/w/500/h/400` the image is proportionally scaled to 500 x 250. If only one edge is specified, the other edge automatically adapts. |
| /3/w/&lt;Width>/h/&lt;Height> | Template 3: limits the minimum width and height of a thumbnail. This operation proportionally scales an image until its width and height are greater than the preset minimum value. <br>For example, assume that the size of an original image is 1000 x 500. If this parameter is set to `?imageView2/3/w/500/h/400`, the image is proportionally scaled to 800 x 400. If only one edge is specified, the other edge is set to the same value. |
| /4/w/&lt;LongEdge>/h/&lt;ShortEdge> | Template 4: limits the minimum values of the long edge and short edge of a thumbnail to `LongEdge` and `ShortEdge` respectively. This operation proportionally scales an image. If only one edge is specified, the other edge is set to the same value. |
| /5/w/&lt;LongEdge>/h/&lt;ShortEdge> | Template 5: limits the maximum values of the long edge and short edge of a thumbnail to `LongEdge` and `ShortEdge` respectively. This operation proportionally scales an image and centrally crops it. If only one edge is specified, it indicates a square with equal width and height. After the image is scaled, the extra part of the other edge will be cropped.
| /format/&lt;Format> | Indicates the format of the target thumbnail. Valid values: jpg, bmp, gif, png, and webp. Default value: original image format. |
| /q/&lt;Quality>                  | Absolute image quality. Value range: 0 - 100; default value: original image quality. Use the value of original image quality (default) or specified quality, whichever is smaller. If &lt;Quality> is followed by an English exclamation mark (!), a specified value must be used. |
| /rq/&lt;quality> | Indicates the relative image quality. Value range: 0 - 100. The value is subject to the original image quality. For example, assume that the original image quality is 80. If you set `rquality` to 80, the resulting image quality is 64 (80 x 80%). |
| /lq/&lt;quality> | Indicates the lowest image quality. Value range: 0 - 100. This value is the quality threshold for the resulting image. <br>For example, assume that the original image quality is 85. If you set `lquality` to 80, the resulting image quality is 85.<br>Assume that the original image quality is 60. If you set `lquality` to 80, the resulting image quality is improved to 80. |


## Examples
This example uses Template 1, setting the minimum width and height of a thumbnail to 400 x 600 and the absolute quality to 85.

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageView2/1/w/400/h/600/q/85
```

The final thumbnail:
![](https://main.qcloudimg.com/raw/281a2f6474ad29b430355f785f158a5c.jpeg)
