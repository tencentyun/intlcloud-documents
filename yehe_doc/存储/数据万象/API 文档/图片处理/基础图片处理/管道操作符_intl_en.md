## Overview
CI allows you to use pipeline operators (|) to separate multiple image processing parameters. In this way, multiple operations can be performed in sequence in a single request. The input image cannot be larger than 32 MB, with its width and height not exceeding 30,000 pixels, and the total number of pixels not exceeding 250 million. The width and height of the output image cannot exceed 9,999 pixels. For an input animated image, the total number of pixels (Width x Height x Number of frames) cannot exceed 250 million pixels.

## API Format
You can append a style separator (?) to the end of an image URL and then add processing operations. Use pipeline operators (|) to separate multiple operations (up to 10 operations are supported). These operations will be performed in sequence.

## Examples
This example scales the input image to 50% and then adds a text watermark in the lower-right corner.

Assume that the URL of the input image is as follows:
```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg
```

Input image: 
![](https://main.qcloudimg.com/raw/52e4147a6febbc589505c67973edb394.png)

#### Scaling the image

Add the scaling operation:

```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/!50p
```

The scaled image is as follows:
![](https://main.qcloudimg.com/raw/f6ab90d8bb2cc1faa1aa3467216c450d.jpg)

#### Adding a watermark

Append a pipeline operator (|) and then add the text watermarking operation:
```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/!50p|watermark/2/text/5pWw5o2u5LiH6LGh/fill/I0ZGRkZGRg==/fontsize/30/dx/20/dy/20
```

Output image: 
![](https://main.qcloudimg.com/raw/61567af609b9f9dd93fe49b22825d3d0.jpg)

#### Using pipeline operators with a signature carried

This example processes the image in the same way as in the example above except that a signature is carried. The signature is joined with other processing parameters using an ampersand (&):

```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=<signature>&imageMogr2/thumbnail/!50p|watermark/2/text/5pWw5o2u5LiH6LGh/fill/I0ZGRkZGRg==/fontsize/30/dx/20/dy/20
```

>? You can obtain the value of `<signature>` by referring to [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
>
