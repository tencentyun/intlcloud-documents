### Overview
imageMogr2 is a simple yet powerful advanced image processing API provided by CI for developers. It has various functions such as rotation, smart cropping, EXIF information extraction and format conversion. Currently, this supports processing images with a size of less than 20 MB and a length x width of less than 9,999 pixels.

### API Form

>**Note:**
Please ignore the line breaks in the following API.

```
  download_url?imageMogr2/auto-orient
                         /thumbnail/
                         /strip
                         /gravity/
						 /cut/
                         /crop/
                         /rotate/
                         /format/
                         /quality/
                         /cgif/
                         /interlace/
                         /radius/
						 /rquality/
                         /lquality/
				         /sharpen/		
						 /scrop/
```												 
												 
### Parameter Descriptions

| Parameter                                      | Meaning                                       |
| --------------------------------------- | ---------------------------------------- |
| download_url | Access link of the file which is structured as &lt;bucket id&gt;-&lt;appid&gt;.&lt;picture region&gt;.&lt;domain&gt;.com/&lt;picture name&gt;, for example, examples-1251000004.picsh.myqcloud.com/sample.jpeg |
| /auto-orient | Automatically rotate the original image back to the positive position according to the EXIF information of the image |
| /strip | Remove meta information from the image, including EXIF information |
| /sharpen/&lt;value&gt; | Image sharpening function; the value is the sharpening parameter value, which is an integer between 10 and 300. The larger the parameter value, the more obvious the sharpening effect. 70 is recommended |
| /thumbnail/&lt;imageSizeAndOffsetGeometry&gt; | See the operation parameter table for scaling below |
|/cut/&lt;imageSizeAndOffsetGeometry&gt;| See the operation parameter table for cutting below; no cutting by default |
| /crop/&lt;imageSizeAndOffsetGeometry&gt; | See the operation parameter table for cutting below; no cutting by default |
| /rotate/&lt;rotateDegree&gt; | Image rotation angle between 0 and 360°; no rotation by default |
| /format/&lt;Format&gt; | Format of the target thumbnail; values include .jpg, .bmp, .gif, .png, .webp and .yjpeg; .yjpeg is CI's optimization of .jpeg and it is essentially in .jpg format; original image format is used by default |
| /quality/&lt;Quality&gt; | Image quality; value range: 0-100; original image quality by default; the original image quality or the specified quality value (whichever is smaller) is used; if ! is added after &lt;Quality>, it means the specified value will be used forcibly, for example, 90! |
| /cgif/&lt;FrameNumber&gt; | This is to optimize original images in .gif format by reducing the frame and color gamut. This is divided into the following two cases: if FrameNumber = 1, the image is processed according to the default number of frames (30) and excessive frames are cut off; if FrameNumber = (1,100], the image is compressed to the specified number of frames (FrameNumber) |
| /interlace/&lt;Mode&gt; | The output is in progressive .jpg format. Mode can be 0 or 1; 0 means "progressive" is disabled, while 1 means it is enabled. This parameter is only valid when the output image is in .jpg format. If a non-jpg image is output, this parameter will be ignored. The default value is 0 |
|/blur/&lt;radius&gt;x&lt;sigma&gt;|	Gaussian blur function; radius is the blur radius (value range: 1-50); sigma is the standard deviation of the normal distribution and must be greater than 0. This parameter is not supported if the image format is .gif. |
|/iradius/&lt;radius&gt;|	Incircle cutting function; radius is the radius of the incircle and its value can be an integer greater than 0 but less than half of the original image's smallest edge. The center of the incircle is the center of the image. This parameter is not supported if the image format is .gif. |
|/rquality/&lt;quality&gt; | The relative quality of the image; value range: 0-100; the value is based on the original image quality, for example, if the original image quality is 80 and rquality is set to 80, the image quality of the resulting image is 64 (80x80%) |
|/lquality/&lt;quality&gt;| Minimum quality of the image; value range: 0-100; this is to set the minimum value of the quality parameter for the resulting image. For example, if the original image quality is 85 and lquality is set to 80, the quality of the resulting image is 85; if the original image quality is 60 and lquality is set to 80, the quality of the resulting image will be increased to 80 |
|/scrop/&lt;Width&gt;x&lt;Height&gt; | Smart face cropping function, which scales and crops the image based on the face position in it. The width of the target image is Width and the height is Height |


### Scaling Operations
| Parameter                                  | Meaning                                       |
| ----------------------------------- | ---------------------------------------- |
| /thumbnail/!&lt;Scale&gt;p | Specify the width and height of the target image as Scale% of the original image |
| /thumbnail/!&lt;Scale&gt;px | Specify the width of the target image as Scale% of the original image and keep the height unchanged |
| /thumbnail/!x&lt;Scale&gt;p | Specify the height of the target image as Scale% of the original image and keep the width unchanged |
| /thumbnail/&lt;Width&gt;x | Specify the width of the target image as Width and scale the height pro rata |
| /thumbnail/x&lt;Height&gt; | Specify the height of the target image as Height and scale the width pro rata |
| /thumbnail/&lt;Width&gt;x&lt;Height&gt; | Limit the maximum width and height of the thumbnail to Width and Height respectively and scale the image pro rata |
| /thumbnail/!&lt;Width&gt;x&lt;Height&gt;r | Limit the minimum width and height of the thumbnail to Width and Height respectively and scale the image pro rata |
| /thumbnail/&lt;Width&gt;x&lt;Height&gt;! | Ignore the aspect ratio of the original image, specify the width of the image as Width and the height as Height, and force scale the image, which may cause target image distortion |
| /thumbnail/&lt;Area&gt;@ | Scale the image pro rata; the total number of pixels of the resulting image should not exceed Area |

### Cutting Operation
**Table for ordinary cutting operation (cut)**

| Parameter                                  | Meaning                                       |
| ----------------------------------- | ---------------------------------------- |
|/cut/&lt;width&gt;x&lt;height&gt;x&lt;dx&gt;x&lt;dy&gt;| Specify the width and height of the target image as width and height. The value of width and height should be greater than 0 but less than the width and height of the original image. dx and dy are used to adjust the cutting position; specifically, it is to offset dx horizontally to the right and dy vertically downward relatively to the offset position (which is the upper left vertex of the image if gravity is not set) and then performs cutting based on the specified width and height; the value of dx and dy should be greater than 0 but less than the width and height of the original image.


### Cropping Operation
**Table for ordinary cropping operation (crop)**

| Parameter                     | Meaning                                       |
| ---------------------- | ---------------------------------------- |
| /crop/&lt;Width&gt;x         | Specify the width of the target image as Width and keep the height unchanged. The value of Width should be greater than 0 but less than the original image width |
| /crop/x&lt;Height&gt;       | Specify the height of the target image as Height and keep the height unchanged. The value of Height should be greater than 0 but less than the original image width |
| /crop/&lt;Width&gt;x&lt;Height&gt; | Specify the width and height of the target image as Width and Height respectively. The value of width and height should be greater than 0 but less than the width and height of the original image |

<pre>
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?imageMogr2/crop/300x400
</pre>

### Example
#### Scaling Operation
<pre>
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/!50p
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/!50px
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/!x50p
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/200x
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/200x400!
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/35000@
</pre>

#### Cutting Operation
<pre>
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?imageMogr2/crop/!600x600a20a20
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?imageMogr2/crop/!600x600-20a20
</pre>

#### Sharpening Operation
<pre>
http://snsimg-10000538.picsh.myqcloud.com/b994c449-ee08-4631-8c05-f5006adf47a4?imageMogr2/sharpen/1
</pre>

#### Gaussian Blur Operation
<pre>
http://test-1252081001.picsh.myqcloud.com/2018-01-10/example.jpg?imageMogr2/blur/8x5
</pre>



### Grid Position Diagram
The grid position diagram provides a location reference for various operations on the image. The red dots are the origins of each zone position (if the gravity parameter is set to select the zones, the offsetting operation will use the corresponding origins as reference).
![](https://main.qcloudimg.com/raw/25596a911919e464d5edf4c84b829fbe.png)
