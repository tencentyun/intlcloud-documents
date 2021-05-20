## Feature
COS uses the pipeline operator `|` in Tencent Cloud CI to perform multiple types of processing on images in a sequence. You can use the pipeline operator to separate multiple processing parameters so that different types of processing can be performed on an image in a single access. Currently, supported images are smaller than 20 MB in size and smaller than 9,999 pixels in length and width.

>! Image processing is a paid service, the fees of which are charged by Cloud Infinite. For detailed billing instructions, see Cloud Infinite’s [Billing and Pricing](https://intl.cloud.tencent.com/document/product/1045/33431).

## API Form
Following an image URL, the style separator `?` is used to connect processing styles that are separated with the pipeline operator `|` and executed in a sequence. Currently, up to ten layers of pipelines are supported.

## Examples

Th example below shows you how to scale an image by 50%, and then add to it the text watermark “Cloud Infinite” in the lower-right corner.

Assume that the URL of the image is
```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg
```

The original image: 
![](https://main.qcloudimg.com/raw/52e4147a6febbc589505c67973edb394.png)

#### Scaling

First, scale down the image using this URL:

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/!50p
```

The resulting image:
![](https://main.qcloudimg.com/raw/f6ab90d8bb2cc1faa1aa3467216c450d.jpg)

#### Adding a watermark

Use a pipeline operator to add the text watermark as processing style, and the final URL will be like:
```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/!50p|watermark/2/text/5pWw5o2u5LiH6LGh/fill/I0ZGRkZGRg==/fontsize/30/dx/20/dy/20
```

The final image: 
![](https://main.qcloudimg.com/raw/6a4864ac780db65742c04739f856fa47.jpg)
