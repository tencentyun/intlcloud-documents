## Overview

COS has integrated [Cloud Infinite](https://intl.cloud.tencent.com/document/product/1045) (CI), a one-stop professional multimedia solution that offers the image processing features outlined below. For more information, please see [Image Processing Overview](https://intl.cloud.tencent.com/document/product/436/35280).


<table>
   <tr>
      <th>Service</td>
      <th>Feature</td>
      <th>Description</td>
   </tr>
   <tr>
      <td rowspan=14>Image Processing-Basic Services</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36366">Scaling</a></td>
      <td>Proportional scaling, scaling image to target width and height, and more</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36367">Cropping</a></td>
      <td>Cut (regular cropping), crop (scaling and cropping), iradius (inscribed circle cropping), and scrop (smart cropping)</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36368">Rotation</a></td>
      <td>Adaptive rotation and common rotation</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36369">Format conversion</a></td>
      <td>Format conversion, GIF optimization, and progressive display</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36370">Quality conversion</a></td>
      <td>Changes the quality of images in JPG and WEBP formats</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36371">Gaussian blurring</a></td>
      <td>Blurs images</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/1045/40647">Adjusting brightness</a></td>
      <td>Adjusts image brightness</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/1045/40648">Adjusting contrast</a></td>
      <td>Adjusts contrast</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36372">Sharpening</a></td>
      <td>Sharpens images</td>
   </tr>
   <tr>
      <td>Watermarking</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36373">Image watermarks</a>, <a href="https://intl.cloud.tencent.com/document/product/436/36374">text watermarks</a></td>
   </tr>
   <tr>
      <td>Obtaining image information</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36375">Basic information</a>, <a href="https://intl.cloud.tencent.com/document/product/436/36376">EXIF data</a>, <a href="https://intl.cloud.tencent.com/document/product/436/36377">average hue</a></td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36378">Removing metadata</a></td>
      <td>Includes EXIF data</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36379">Quick thumbnail template</a></td>
      <td>Performs quick format conversion, scaling, and cropping to generate thumbnails</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36380">Pipeline operator</a></td>
      <td>Performs multiple types of processing on images in a sequence</td>
   </tr>
</table>




## Instantiating Templates

Before using a basic image processing feature, you need to instantiate the template class and call the method to generate CI image processing parameters that are to be passed in when obtaining file resources.

#### Sample code

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is http by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));

try {
        $imageMogrTemplate = new Qcloud\Cos\ImageParamTemplate\ImageMogrTemplate(); //Create an instance of the basic image processing parameter template
        $imageMogrTemplate->thumbnailByScale(50); //Scale an image to 50% of its original width and height
        $result = $cosClient->getObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
        'ImageHandleParam' => $imageMogrTemplate->queryString(), //Generate basic image processing parameters
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter | Type | Description | Required |
| -------------------- | ----------- | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key | String | Uniquely identifies an object in a bucket. For example, if the object access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg`.  | Yes |
| ImageHandleParam      | String      | CI image processing parameters, such as `imageMogr2/thumbnail/!50p`      | Yes        |

#### Sample response

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [Body] => 
            [RequestId] => NWQwOGRkNDdfMjJiMjU4NjRfNzVjXzEwNmVjY2M=
            [ContentLength] => 100
            [CacheControl] => max-age=2592000
            [ContentType] => image/jpeg
            [Key] => exampleobject
            [Bucket] => examplebucket-1250000000
            [Location] => examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject
        )

)

```

#### Response description

| Parameter | Type | Description | Parent Node |
| -------------------- | ----------- | ------------------------------------------------- | ------ |
| Body | File/String | Downloaded content                                                   | None |
| RequestId             | String      | Request ID                                | None     |
| CacheControl | String | Cache policy. Sets `Cache-Control`. | None |
| ContentType | String | Content type. Sets `Content-Type` | None |
| ContentLength | Int | Length of the response body | None |
| Key                  | String      | Object key                                    | None     |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | None |
| Location             | String      | Address of the requested resource                                 | None     |

## Scaling

### Scaling by percentage

```php
$imageMogrTemplate->thumbnailByScale(50); //Scale an image to 50% of its original width and height
$imageMogrTemplate->thumbnailByWidthScale(50); //Scale an image to 50% of its original width while keeping the height unchanged
$imageMogrTemplate->thumbnailByHeightScale(50); //Scale an image to 50% of its original height while keeping the width unchanged
```

### Scaling with specified width and height

```php
$imageMogrTemplate->thumbnailByWidth(50); //Specify the target image width as 50, with the height proportionally scaled down
$imageMogrTemplate->thumbnailByHeight(50); //Specify the target image height as 50, with the width proportionally scaled down
$imageMogrTemplate->thumbnailByMaxWH(50, 50); //Specify the maximum width and height of a thumbnail as 50 and 50 respectively for proportional scaling
$imageMogrTemplate->thumbnailByMinWH(50, 50);//Specify the minimum width and height of a thumbnail as 50 and 50 respectively for proportional scaling
$imageMogrTemplate->thumbnailByWH(50, 50); //Force image scaling with the specified width (50) and height (50), which may cause deformation of the target image
```

### Proportional scaling

```php
$imageMogrTemplate->thumbnailByPixel(1000); //Proportionally scale an image so that the total number of its pixels does not exceed 1,000
```

## Cropping


### Regular cropping

```php
$imageMogrTemplate->cut(100, 300, 30, 30); //Perform cropping based on the specified target width, height, and horizontal offset and vertical offset relative to the upper-left vertex of the output image
```

### Scaling and cropping

For information on 3x3 grid position diagrams, see [3x3 Grid Position Diagram](https://intl.cloud.tencent.com/document/product/436/36367).

```php
$imageMogrTemplate->cropByWidth(100); //Perform scaling and cropping based on the specified target width
$imageMogrTemplate->cropByWidth(100, 'center'); //Perform scaling and cropping based on the specified target width and operation start point
$imageMogrTemplate->cropByHeight(100); //Perform scaling and cropping based on the specified target height
$imageMogrTemplate->cropByHeight(100, 'center'); //Perform scaling and cropping based on the specified target height and operation start point
$imageMogrTemplate->cropByWH(100, 100); //Perform scaling and cropping based on the specified target width and height
$imageMogrTemplate->cropByWH(100, 100, 'center'); //Perform scaling and cropping based on the specified target width and height, as well as the operation start point
```

### Inscribed circle cropping

`radius` specifies the radius of the inscribed circle. The value of `radius` should be an integer greater than 0 but smaller than half the length of the input image’s shorter side. The center of the inscribed circle is the center of the input image. This operation is not available for GIF images.

```php
$imageMogrTemplate->iradius(100); //Specify radius as 100 in this example
```

### Rounded corner cropping

`radius` specifies the radius of the rounded corners of an image. The value of `radius` should be an integer greater than 0 but smaller than half the length of the input image’s shorter side. The two sides of the input image are the tangent lines of the rounded corner. This operation is not available for GIF images.

```php
$imageMogrTemplate->rradius(1000); // Specify radius as 100 in this example
```

### Smart cropping

Scale and crop an image based on the face position in the image. The width and height of the target image are specified by `Width` and `Height` respectively.

```php 
$imageMogrTemplate->scrop(100, 100); //Scale and crop an image to 100x100 based on the face position in the image in this example
```

## Rotating


### Common rotation

Rotate an image clockwise by a specified angle. Value range: 0−360. By default, the image is not rotated.

```php
$imageMogrTemplate->rotate(45); //This example rotates an image by 45 degrees clockwise
```

### Adaptive rotation

Rotate an image automatically according to the EXIF data of the input image.

```php
$imageMogrTemplate->autoOrient();
```

## Format Conversion


### Common conversion

The target format can be JPG, BMP, GIF, PNG, WebP, or YJPEG (optimized based on JPEG and is essentially JPG). The default format is the format of the input image.

```php
$imageMogrTemplate->format('png'); //Convert an image to the PNG format
```

### GIF optimization

This feature is used to optimize only images whose original images are in the GIF format. It can reduce frames and colors of images. There are two situations, depending on the value of `FrameNumber`:
- FrameNumber=1: cut the input GIF to the default number of frames (30). If the original number of frames is greater than 30, the exceeded frames will be cut.
- FrameNumber=(1,100]: compress the image to the specified number of frames (`FrameNumber`).

```php
$imageMogrTemplate->gifOptimization(50); //Compress the image to 50 frames
```

### Progressive mode of the output JPG image

The `Mode` parameter is used to specify whether to enable or disable the progressive mode. This parameter takes effect only when the output image is in JPG format. Otherwise, this parameter will be ignored. The parameter value can be 0 (disable the progressive mode) or 1 (enable the progressive mode). The default value is 0.

```php
$imageMogrTemplate->jpegInterlaceMode(1); //Enable the progressive mode
```

## Quality Change

The quality conversion feature supports conversion to three types of quality: absolute, relative, and lowest image quality. The feature applies only to JPG and WEBP images.

### Conversion to absolute image quality

Set the absolute quality of the image. Value range: 0−100. Use the value of the original image quality (default) or specified quality, whichever is smaller.
Specify whether to use the specified quality by force. The value can be 0 (no) or 1 (yes). The default value is 0.

```php
$imageMogrTemplate->quality(90, 1); //Use the specified quality 90 by force
```

### Conversion to relative image quality

Set the relative quality of the image, relative to that of the input image. Value range: 0−100. For example, if the input image quality is 80 and `rquality` is set to `80`, the quality of the output image is 64 (that is, 80 x 80%).

```php
$imageMogrTemplate->relativelyQuality(80);
```

### Conversion to lowest image quality

Set the lowest quality of the output image. Value range: 0−100.
- If the input image quality is 85 and `lquality` is set to 80, the quality of the output image is 85.
- If the input image quality is 60 and `lquality` is set to 80, the quality of the output image will be improved to 80.

```php
$imageMogrTemplate->lowestQuality(90);
```

## Gaussian Blurring

The blur radius must range from 1 to 50. The standard deviation of normal distribution must be greater than 0. GIF images do not support Gaussian blurring.

```php
$imageMogrTemplate->blur(20, 20); //The blur radius is 20 and the standard deviation of normal distribution is 20 in this example
```

## Adjusting Brightness

Adjust the brightness of an image. The value must be an integer in the range of [−100, 100].

```php
//Value < 0: reduce the image brightness
//Value = 0: do not adjust the image brightness
//Value > 0: increase the image brightness
$imageMogrTemplate->bright(50); //Increase the image brightness by 50
```

## Adjusting Contrast

Adjust the contrast of an image. The value must be an integer in the range of [−100, 100].

```php
//Value < 0: reduce the image contrast
//Value = 0: do not adjust the image contrast
//Value > 0: increase the image contrast
$imageMogrTemplate->contrast(50); //Increase the image contrast by 50
```

## Sharpening

Sharpen an image. The sharpening value must be an integer ranging from 10 to 300 (70 is recommended). The greater the value, the more obvious the sharpening effect.

```php
$imageMogrTemplate->sharpen(70); //Sharpen an image with the sharpening value of 70
```

## Adding Watermarks

For information on 3x3 grid position diagrams, see [3x3 Grid Position Diagram](https://intl.cloud.tencent.com/document/product/436/36374).

### Image watermarks

An image watermark must:
1. Be stored in the same bucket as the input image.
2. Have a URL containing a COS domain name (a CDN acceleration domain name such as `examplebucket-1250000000.file.myqcloud.com/shuiyin_2.png` is unsupported) and be accessible. If the image watermark is set to private-read, it must carry a signature.
3. Have a URL starting with `http://`. Note that "http://" cannot be omitted or changed to "https://". For example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/shuiyin_2.png` and `https://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/shuiyin_2.png` are invalid watermark URLs.

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is http by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));

try {
        $imageWatermarkTemplate = new Qcloud\Cos\ImageParamTemplate\ImageWatermarkTemplate(); //Create an image watermark parameter template instance
        $imageWatermarkTemplate->setImage("imageurl"); //Set the watermark image address
        $imageWatermarkTemplate->setGravity('center'); //Set the position of the watermark in the 3x3 grid position diagram
        $imageWatermarkTemplate->setDx(10); //Set the horizontal offset
        $imageWatermarkTemplate->setDy(10); //Set the vertical offset
        $imageWatermarkTemplate->setBlogo(1); //Set the adaptation mode for an image watermark that is larger than the input image. Valid values: 1 (scale the image watermark to the size of the input image), 2 (crop the image watermark to the size of the input image)
        $imageWatermarkTemplate->setScatype(1); //Set the scaling mode for the image watermark (relative to the input image). Valid values: 1 (scale by width), 2 (scale by height), 3 (scale by area)
        $imageWatermarkTemplate->setSpcent(100); //Set the scale ratio of the image watermark (relative to the input image), in permillage, to 100/1000. Value range: [1,1000]. By default, the image watermark is not scaled.
        $result = $cosClient->getObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
        'ImageHandleParam' => $imageWatermarkTemplate->queryString(), //Generate image watermark parameters
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}

```

### Text watermarks

COS provides real-time text watermarking. For the list of watermark fonts supported, see [Supported Fonts](https://intl.cloud.tencent.com/document/product/1045/40681). For the list of font colors supported, see [RGB Color Codes Chart](https://www.rapidtables.com/web/color/RGB_Color.html).

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is http by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));

try {
        $textWatermarkTemplate = new Qcloud\Cos\ImageParamTemplate\TextWatermarkTemplate(); //Create a text watermark parameter template instance
        $textWatermarkTemplate->setText("test"); //Set the watermark text
        $textWatermarkTemplate->setFont("tahoma.ttf"); //Set the font of the watermark text. Default value: `tahoma.ttf`
        $textWatermarkTemplate->setFontsize(30); //Set the watermark text font size, in pounds. Default value: `13`
        $textWatermarkTemplate->setFill("#3D3D3D"); //Set the font color. The value must be in hexadecimal RGB format, for example, `#FF0000`. Default value: `#3D3D3D` (gray)
        $textWatermarkTemplate->setDissolve(90); //Set the text opacity. Value range: 1−100. Default value: `90` (meaning 90% opacity)
        $textWatermarkTemplate->setGravity('center'); //Set the position of the text watermark in the 3x3 grid position diagram. Default value: `southeast`
        $textWatermarkTemplate->setDx(10); //Set the horizontal offset in pixels. Default value: `0`
        $textWatermarkTemplate->setDy(10); //Set the vertical offset in pixels. Default value: `0`
        $textWatermarkTemplate->setBatch(1); //Set whether to tile the text watermark. If this parameter is set to `1`, the text watermark will be tiled across the input image.
        $textWatermarkTemplate->setDegree(45); //Set the angle to rotate the text watermark. Value range: 0−360. Default value: `0`
        $result = $cosClient->getObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
        'ImageHandleParam' => $textWatermarkTemplate->queryString(), //Generate text watermark parameters
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```


## Obtaining Image Information

### Obtaining basic image information

Query basic image information.

#### Sample code

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is http by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));

try {
        $result = $cosClient->ImageInfo(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter | Type | Description | Required |
| -------------------- | ----------- | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key | String | Uniquely identifies an object in a bucket. For example, if the object access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg`.  | Yes |

#### Sample response

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [Body] => 
            [RequestId] => NWQwOGRkNDdfMjJiMjU4NjRfNzVjXzEwNmVjY2M=
            [ContentLength] => 100
            [ContentType] => application/json
            [Key] => exampleobject
            [Bucket] => examplebucket-1250000000
            [Location] => examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject
            [Data] => {"format": "jpeg", "width": "400", "height": "400"}
        )
)

```

#### Response description

| Parameter | Type | Description | Parent Node |
| -------------------- | ----------- | ------------------------------------------------- | ------ |
| Body                 | File/String | Response body                                    | None     |
| RequestId             | String      | Request ID                                | None     |
| ContentType | String | Content type. Sets `Content-Type` | None |
| ContentLength | Int | Length of the response body | None |
| Key                  | String      | Object key                                    | None     |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | None |
| Location             | String      | Address of the requested resource                                 | None     |
| Data                 | Json/String      | Basic image information                            | None     |

### Obtaining image EXIF

Obtain image EXIF data. If an image does not have EXIF data, `{"error" : "no exif data"}` will be returned.

#### Sample code

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is http by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));

try {
        $result = $cosClient->ImageExif(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter | Type | Description | Required |
| -------------------- | ----------- | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key | String | Uniquely identifies an object in a bucket. For example, if the object access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg`.  | Yes |

#### Sample response

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [Body] => 
            [RequestId] => NWQwOGRkNDdfMjJiMjU4NjRfNzVjXzEwNmVjY2M=
            [ContentLength] => 32
            [ContentType] => application/json
            [Key] => exampleobject
            [Bucket] => examplebucket-1250000000
            [Location] => examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject
            [Data] => {"error" : "no exif data"}
        )
)

```

#### Response description

| Parameter | Type | Description | Parent Node |
| -------------------- | ----------- | ------------------------------------------------- | ------ |
| Body                 | File/String | Response body                                    | None     |
| RequestId             | String      | Request ID                                | None     |
| ContentType | String | Content type. Sets `Content-Type` | None |
| ContentLength | Int | Length of the response body | None |
| Key                  | String      | Object key                                    | None     |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | None |
| Location             | String      | Address of the requested resource                                 | None     |
| Data                 | Json/String      | Image EXIF data                            | None     |

### Obtaining image's average hue

Obtain the average hue of an image.

#### Sample code

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is http by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));

try {
        $result = $cosClient->ImageAve(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter | Type | Description | Required |
| -------------------- | ----------- | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key | String | Uniquely identifies an object in a bucket. For example, if the object access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg`.  | Yes |

#### Sample response

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [Body] => 
            [RequestId] => NWQwOGRkNDdfMjJiMjU4NjRfNzVjXzEwNmVjY2M=
            [ContentLength] => 19
            [ContentType] => application/json
            [Key] => exampleobject
            [Bucket] => examplebucket-1250000000
            [Location] => examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject
            [Data] => {"RGB": "0x483519"}
        )
)

```

#### Response description

| Parameter | Type | Description | Parent Node |
| -------------------- | ----------- | ------------------------------------------------- | ------ |
| Body                 | File/String | Response body                                    | None     |
| RequestId             | String      | Request ID                                | None     |
| ContentType | String | Content type. Sets `Content-Type` | None |
| ContentLength | Int | Length of the response body | None |
| Key                  | String      | Object key                                    | None     |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | None |
| Location             | String      | Address of the requested resource                                 | None     |
| Data                 | Json/String      | Average hue of the image                             | None     |



## Removing Image Metadata

Remove image metadata, including EXIF data.

```php
$imageMogrTemplate->strip(); //Remove image metadata
```

## Quick Thumbnail Template

Provide common image processing templates to help you generate desired thumbnails.

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is http by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));

try {
        $imageViewTemplate = new Qcloud\Cos\ImageParamTemplate\ImageViewTemplate(); //Create a parameter template instance for the quick thumbnail template
        $imageViewTemplate->setMode(1); //Set the thumbnail mode. Value range: [1,5]. Mode 1: specify the minimum width and height of the thumbnail. In this mode, the image is first scaled down until one of the minimum values set is reached. Then, the image will be centered and evenly cropped on both sides to meet the specified values. If only one value is set, a square thumbnail will be generated. Mode 2: specify the maximum width and height of the thumbnail. In this mode, the image is scaled down until both the width and length are not greater than the maximum values set. Mode 3: specify the minimum width and height of the thumbnail. In this mode, the image is scaled down until both the width and height are not smaller than the minimum values set. Mode 4: specify the minimum values of the long edge and short edge of the thumbnail to scale down the image. If only one value is set, a square thumbnail will be generated. Mode 5: specify the maximum values of the long edge and short edge of the thumbnail to scale down the image. Then the image will be centered and cropped. If only one value is set, a square thumbnail will be generated. After the scaling, the excess will be cropped.
        $imageViewTemplate->setWidth(400); //Set the thumbnail width
        $imageViewTemplate->setHeight(600); //Set the thumbnail height
        $imageViewTemplate->setFormat(); //Set the thumbnail format, which can be JPG, BMP, GIF, PNG, or WebP. Default value: format of the input image
        $imageViewTemplate->setQuality(1, 85); //Set the image quality type, which can be `1` (absolute quality), `2` (relative quality), or `3` (lowest quality)
        $imageViewTemplate->setQuality(1, 85, 1); //If the image quality type is set to absolute quality, the specified quality will be used by force
        $result = $cosClient->getObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
        'ImageHandleParam' => $imageViewTemplate->queryString(), //Generate quick thumbnail template parameters
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```


## Pipeline Operator

CIParamTransformation supports multiple operation groups.

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is http by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
            
try {
    $ciParamTransformation = new Qcloud\Cos\ImageParamTemplate\CIParamTransformation(); //Create a pipeline parameter template instance
    $ciParamTransformation = new Qcloud\Cos\ImageParamTemplate\CIParamTransformation("#"); //If the pipeline operator is not `|`, it must be specified during instance creation
    $ciParamTransformation->addRule($imageMogrTemplate); //Set basic image processing parameters
    $ciParamTransformation->addRule($imageWatermarkTemplate); //Set image watermark processing parameters
    $ciParamTransformation->addRule($textWatermarkTemplate); //Set text watermark processing parameters
    $ciParamTransformation->addRule($imageViewTemplate); //Set quick thumbnail template parameters
$result = $cosClient->getObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
        'ImageHandleParam' => $ciParamTransformation->queryString(), //Generate pipeline splicing parameters
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

