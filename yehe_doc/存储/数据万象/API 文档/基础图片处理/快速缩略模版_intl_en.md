## Feature
This API is used to provide common image processing templates in Tencent Cloud CI. You only need to add corresponding parameters to the download URL to generate corresponding thumbnails. Currently, images smaller than 20 MB in size and smaller than 9,999 pixels in length and width are supported.

## API Form

```shell
imageView2/<mode>/w/<Width>
                 /h/<Height>
                 /format/<Format>
                 /q/<Quality>
                 /rq/<Quality>
                 /lq/<Quality>			
```

> Quality conversion parameters are only applicable to **jpg** and **webp** images.


## Parameter Description

| Parameter | Description |
| ----------------------------- | ------------------------------------------------------------ |
| download_url | URL that is used to access a file. The URL form is `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`, <br>for example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg`. |
| /1/w/&lt;Width>/h/&lt;Height> | Limits the minimum width and height of a thumbnail. This operation proportionally scales an image until one of its edges reaches the preset minimum value, and then centrally crops the other edge to the preset value. If only one edge is specified, it indicates a square with equal width and height. <br>For example, assume that the size of an original image is 1000x500. If this parameter is set to ?imageView2/1/w/500/h/400, the image is proportionally scaled to 800x400 and then it is cropped by 150 on the left and right sides, resulting in an image of 500x400. |
| /2/w/&lt;Width>/h/&lt;Height> | Limits the maximum width and height of a thumbnail. This operation proportionally scales an image until its width and height are smaller than the preset maximum value. <br>For example, assume that the size of an original image is 1000x500. If this parameter is set to imageView2/2/w/500/h/400, the image is proportionally scaled to 500x250. If only one edge is specified, the other edge is automatically adapted. |
| /3/w/&lt;Width>/h/&lt;Height> | Limits the minimum width and height of a thumbnail. This operation proportionally scales an image until its width and height are greater than the preset minimum value. <br>For example, assume that the size of an original image is 1000x500. If this parameter is set to ?imageView2/3/w/500/h/400, the image is proportionally scaled to 800x400. If only one edge is specified, the other edge is set to the same value. |
| /4/w/&lt;LongEdge>/h/&lt;ShortEdge> | Limits the minimum values of the long edge and short edge of a thumbnail to LongEdge and ShortEdge respectively. This operation proportionally scales an image. If only one edge is specified, the other edge is set to the same value. |
| /5/w/&lt;LongEdge>/h/&lt;ShortEdge> | Limits the maximum values of the long edge and short edge of a thumbnail to LongEdge and ShortEdge respectively. This operation proportionally scales an image and centrally crops it. If only one edge is specified, it indicates a square with equal width and height. After the image is scaled, the extra part of the other edge will be cropped.
| /format/&lt;Format> | Indicates the format of the target thumbnail. Valid values: jpg, bmp, gif, png, and webp. Default value: original image format. |
| /q/&lt;Quality> | Indicates the image quality. Value range: 0 - 100. The default value is the quality of the original image. Obtain the minimum value from the original image quality and the specified quality. If &lt;Quality> is followed by an exclamation mark (!), a specified value is used forcibly. |
| /rq/&lt;quality> | Indicates the relative image quality. Value range: 0 - 100. The value is based on the original image quality. For example, assume that the original image quality is 80. If you set rquality to 80, the resulting image quality is 64 (80x80%). |
| /lq/&lt;quality> | Indicates the lowest image quality. Value range: 0 - 100. The value is set to the minimum value of the quality parameter for the resulted image. <br>For example, assume that the original image quality is 85. If you set lquality to 80, the resulted image quality is 85. <br>For example, assume that the original image quality is 60. If you set lquality to 80, the resulting image quality is improved to 80. |


## Example
This example uses template style 1, and limits the minimum width and height of a thumbnail to 400x600 and the absolute quality to 85.

```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageView2/1/w/400/h/600/q/85
```

The effect of the thumbnail is as follows:
![](https://main.qcloudimg.com/raw/281a2f6474ad29b430355f785f158a5c.jpeg)
