## Description
The pipeline operator **|** of Tencent Cloud CI allows you to perform multiple types of processing sequentially on an image. You can separate multiple processing parameters by using pipeline operators, to perform different types of processing sequentially on an image during a single access to the image. Currently, this feature is applicable to images of a size within 20 MB and of a width and a height both less than 9,999 pixels.


## API Format
You can add the style separator **?** to the end of the URL of an image to connect this URL with the processing styles. Multiple processing styles are separated by pipe operators **|**, and the styles are executed sequentially. Currently, up to three layers of pipeline operators are supported.

## Example
This example shows how to scale the original image to 50% and add the **CI** watermark in the lower-right corner of the image.

Assuming that the URL of the original image is:
```
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg
```

The original image is displayed as follows: 
![](https://main.qcloudimg.com/raw/52e4147a6febbc589505c67973edb394.png)

**Scale operation**
After the scale operation is performed, the URL is as follows:

```
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/!50p
```

The image is displayed as follows:
![](https://main.qcloudimg.com/raw/f6ab90d8bb2cc1faa1aa3467216c450d.jpg)

**Adding the watermark**
Use a pipeline operator to add the style processing of adding a text watermark. The resulting URL is as follows:
```
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/!50p|watermark/2/text/5pWw5o2u5LiH6LGh/fill/I0ZGRkZGRg==/fontsize/30/dx/20/dy/20
```

The final image processing effect is as follows: 
![](https://main.qcloudimg.com/raw/61567af609b9f9dd93fe49b22825d3d0.jpg)