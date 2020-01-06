## Description
With the **imageView2** API, Tencent Cloud CI provides common image processing templates. With this API, developers can generate the corresponding thumbnail simply by adding related parameters to the end of an image download URL based on their business requirements. Currently, this API is applicable to images with a size no greater than 20 MB and a length and width both less than 9,999 pixels.

## API Format

```
imageView2/<mode>/w/<Width>
                   /h/<Height>
                   /format/<Format>
                   /q/<Quality>
                   /rq/<Quality>
                   /lq/<Quality>			
```

> The quality conversion parameters are applicable only to images in **jpg** or **webp** format.


### Parameter description

| Parameter | Description |
| ----------------------------- | ------------------------------------------------------------ |
| download_url | The file access URL in the format of `<BucketName-APPID>.<picture region>.<domain>.com/<picture name>`, <br>for example, `examplebucket-1250000000.picsh.myqcloud.com/picture.jpeg`. |
| /1/w/&lt;Width>/h/&lt;Height> | This parameter specifies the minimum width and height of the thumbnail. In this mode, the image is proportionally scaled down until one direction reaches the set minimum value, and then the image is evenly cropped on both sides in the other direction. If only the value in one direction is specified, a square thumbnail is produced. For example, if the original image resolution is 1000 x 500 and this parameter is set to ?imageView2/1/w/500/h/400, the image is first proportionally scaled down to 800 x 400, and then 150 pixels are separately cropped from the left and right sides to obtain an image with a resolution of 500 x 400. |
| /2/w/&lt;Width>/h/&lt;Height> | This parameter specifies the maximum width and height of the thumbnail. In this mode, the image is proportionally scaled down until both the width and length are not greater than the set maximum values. For example, if the original image resolution is 1000 x 500 and this parameter is set to ?imageView2/2/w/500/h/400, the image is proportionally scaled down to 500 x 250.  If only the value in one direction is specified, the image is adapted in the other direction. |
| /3/w/&lt;Width>/h/&lt;Height> | This parameter specifies the minimum width and height of the thumbnail. In this mode, the image is proportionally scaled down until both the width and height are greater than the set minimum values. For example, if the original image resolution is 1000 x 500 and this parameter is set to ?imageView2/3/w/500/h/400, the image is proportionally scaled down to 800 x 400. If only the value in one direction is specified, a square thumbnail is produced. |
| /4/w/&lt;LongEdge>/h/&lt;ShortEdge> | This parameter specifies the minimum values of the long edge and short edge. In this mode, the image is proportionally scaled down. If only the value in one direction is specified, a square thumbnail is produced. |
| /5/w/&lt;LongEdge>/h/&lt;ShortEdge> | This parameter specifies the maximum values of the long edge and short edge of the thumbnail. In this mode, the image is proportionally scaled down, and then the image is evenly cropped on both sides. If only the value in one direction is specified, a square thumbnail is produced. After scaling, the extra part in the other direction will be cropped. |
| /format/&lt;Format> | The image format of the target thumbnail. Valid values: jpg, bmp, gif, png, and webp. The default value is the format of the original image. |
| /q/&lt;Quality> | Image quality. Value range: 0-100. The default value is the quality of the original image. The smaller value of the original image quality and the specified quality will be used. If &lt;Quality> is followed by an exclamation mark (**!**), the specified quality is used forcibly. |
| /rq/&lt;quality> | The relative quality of the image. Value range: 0-100. The value is subject to the original image quality. If the original image quality is 80 and `rquality` is set to 80, the quality of the processed image is 64 (that is, 80 x 80%). |
| /lq/&lt;quality> | The lowest quality of the image. Value range: 0-100. If the original image quality is 85 and lquality is set to 80, the quality of the processed image is 85. If the original image quality is 60 and `lquality` is set to 80, the quality of the processed image will be improved to 80. |


## Example
In this example, template style 1 is selected, the minimum width and height of the thumbnail are set to 400 x 600, and the absolute quality is set to 85:

```
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?imageView2/1/w/400/h/600/q/85
```

The resulting thumbnail is as follows:
![](https://main.qcloudimg.com/raw/281a2f6474ad29b430355f785f158a5c.jpeg)