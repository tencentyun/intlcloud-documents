## Overview
COS uses the pipeline operators (|) provided by CI to separate multiple image processing parameters. In this way, multiple operations can be performed in sequence in a single request. The input image cannot be larger than 32 MB, with its width and height not exceeding 30,000 pixels, and the total number of pixels not exceeding 250 million. The width and height of the output image cannot exceed 9,999 pixels. For an input animated image, the total number of pixels (Width x Height x Number of frames) cannot exceed 250 million pixels.

>! Image processing is charged by CI. For detailed pricing, please see the image processing prices of CI.
>

## API Format
You can append a style separator (?) to the end of an image URL and then add processing operations. Use pipeline operators (|) to separate multiple operations (up to 10 operations are supported). These operations will be performed in sequence.

## Examples

This sample scales the input image to 50% and then adds a text watermark in the lower-right corner.

Assume that the URL of the input image is as follows:
```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg
```

Input image: 
![](https://main.qcloudimg.com/raw/52e4147a6febbc589505c67973edb394.png)

#### Example 1: scaling and adding watermark

Add the scaling operation:

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/!50p
```

The scaled image is as follows:
![](https://main.qcloudimg.com/raw/f6ab90d8bb2cc1faa1aa3467216c450d.jpg)

Append a pipeline operator (|) and then add the text watermarking operation:
```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/!50p|watermark/2/text/5pWw5o2u5LiH6LGh/fill/I0ZGRkZGRg==/fontsize/30/dx/20/dy/20
```

Output image: 
![](https://main.qcloudimg.com/raw/61567af609b9f9dd93fe49b22825d3d0.jpg)

#### Example 2: using pipeline operators with a signature carried

This example processes the image in the same way as in the example above except that a signature is carried. The signature is joined with other processing parameters using an ampersand (&):

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=<signature>&imageMogr2/thumbnail/!50p|watermark/2/text/5pWw5o2u5LiH6LGh/fill/I0ZGRkZGRg==/fontsize/30/dx/20/dy/20
```

>? You can obtain the value of `<signature>` by referring to [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
>

## Notes

To prevent unauthorized users from accessing or downloading the input image by using a URL that does not contain any processing parameter, you can add the processing parameters to the request signature, making the processing parameters the key of the parameter with the value left empty. The following is a simple example for your reference (it might have expired or become inaccessible). For more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/14114).


```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=sha1&q-ak=AKID********************&q-sign-time=1593342360;1593342720&q-key-time=1593342360;1593342720&q-header-list=&q-url-param-list=watermark%252f1%252fimage%252fahr0cdovl2v4yw1wbgvzlteyntewmdawmdqucgljc2gubxlxy2xvdwquy29tl3nodwl5aw4uanbn%252fgravity%252fsoutheast&q-signature=26a429871963375c88081ef60247c5746e834a98&watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAwMDQucGljc2gubXlxY2xvdWQuY29tL3NodWl5aW4uanBn/gravity/southeast
```

