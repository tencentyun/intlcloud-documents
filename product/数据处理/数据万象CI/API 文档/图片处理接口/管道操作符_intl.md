## Overview
The pipe operator "|" enables CI to execute multiple operations in sequence on an image. Multiple processing parameters can be separated with pipe operators, so that the image can be processed in different ways in one single access. Currently, this supports processing images with a size of less than 20 MB and a length x width of less than 9,999 pixels.

## API Form
A style separator "?" can be added after the image's url to connect it with processing styles, and multiple processing styles can be separated with pipe operators "|". Then, the styles will be executed in sequence. Currently, up to three pipes are supported.

## Example
````
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/!50p|watermark/2/text/Q0xPVUQgSU1BR0U=/gravity/southeast/fontsize/30/fill/IzAwMDAwMA==
````

This example will first scale the original image by 50% and then add the text watermark "Cloud Data Processing" in the lower right corner.
First, the original image url is: 
````
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg
````

The image is as follows:
![](https://main.qcloudimg.com/raw/77a16fa70e2eba652fb42e8a639c52f2.jpg)

After the scaling operation is added, the url becomes:
````
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/!50p
````

The image is as follows:
![](https://main.qcloudimg.com/raw/88304b1ca69938f579225e3e76e290cb.jpg)

Then, use the pipeline operator to add the style of text watermark, and the url becomes:

````
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/!50p|watermark/2/text/5pWw5o2u5LiH6LGh/fill/I0ZGRkZGRg==/fontsize/30/dx/20/dy/20
````

The resulting image is as follows:
![](https://main.qcloudimg.com/raw/9bc40115f6d6e0b0800f42a5bd02ef5a.jpeg)
