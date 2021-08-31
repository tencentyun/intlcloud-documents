## Feature Overview
The pipeline operator `|` in Tencent Cloud CI can be used to perform multiple types of processing on images in a sequence. You can use the pipeline operator to separate multiple processing parameters so that different types of processing can be performed on an image in a single access. Currently, images smaller than 20 MB in size and smaller than 9,999 pixels in length and width are supported.


## API Form
Following an image URL, the style separator `?` is used to connect processing styles that are separated with the pipeline operator `|` and executed in a sequence. Currently, up to three layers of pipelines are supported.

## Example
This example shows you how to scale an original image by 50% and then add the text watermark “CI” in the lower-right corner.

Assume that the URL of the original image is as follows:
```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg
```

The original image is as follows: 
![](https://main.qcloudimg.com/raw/52e4147a6febbc589505c67973edb394.png)

#### Scaling operations

Add a scaling operation. Then, the URL is as follows:

```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/!50p
```

The image is as follows:
![](https://main.qcloudimg.com/raw/f6ab90d8bb2cc1faa1aa3467216c450d.jpg)

#### Adding a watermark

Use a pipeline operator and then add the text watermark for style processing. The final URL is as follows:
```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/!50p|watermark/2/text/5pWw5o2u5LiH6LGh/fill/I0ZGRkZGRg==/fontsize/30/dx/20/dy/20
```

The final image is as follows: 
![](https://main.qcloudimg.com/raw/8c44c8e3cda5f6311ebdd7e5b33b0480.jpg)
