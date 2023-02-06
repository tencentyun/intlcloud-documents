## Overview

COS has integrated [Cloud Infinite](https://www.tencentcloud.com/document/product/1045) (CI), a one-stop professional multimedia solution that offers the image processing features outlined below. For more information, see [Image Processing Overview](https://intl.cloud.tencent.com/document/product/436/35280).

| Feature | Description |
| ------------- |  ---------------------- |
| [Scaling](https://intl.cloud.tencent.com/document/product/436/36366) | Scales an image proportionally or to the target width and height. |
| [Cropping](https://intl.cloud.tencent.com/document/product/436/36367) | Performs regular cropping, cropping and scaling, cropping to circle, or smart face cropping. |
| [Rotation](https://intl.cloud.tencent.com/document/product/436/36368) | Performs adaptive rotation or regular rotation. |
| [Format conversion](https://intl.cloud.tencent.com/document/product/436/36369) | Converts the format of an image, optimizes the GIF format, and performs progressive display. |
| [Quality change](https://intl.cloud.tencent.com/document/product/436/36370) | Changes the quality of images in JPG and WEBP formats. |
| [Gaussian blurring](https://intl.cloud.tencent.com/document/product/436/36371) | Blurs an image by a Gaussian function. |
| [Brightness](https://intl.cloud.tencent.com/document/product/436/41159) | Adjusts the image brightness. |
| [Contrast](https://intl.cloud.tencent.com/document/product/436/41160) | Adjusts the image contrast. |
| [Sharpening](https://intl.cloud.tencent.com/document/product/436/36372) | Sharpens an image. |
| [Grayscale image](https://intl.cloud.tencent.com/document/product/436/44884) | Sets an image to a grayscale image. |
| [Image watermark](https://intl.cloud.tencent.com/document/product/436/36373) | Processes an image watermark. |
| [Text watermark](https://intl.cloud.tencent.com/document/product/436/36374) | Processes a text watermark. |
| [Basic image information acquisition](https://intl.cloud.tencent.com/document/product/436/36375) | Queries the basic information of an image, such as format, width, and height. |
| [Image EXIF data acquisition](https://intl.cloud.tencent.com/document/product/436/36376) | Gets the EXIF data of an image. |
| [Image average hue acquisition](https://intl.cloud.tencent.com/document/product/436/36377) | Gets the average hue of an image. |
| [Metadata removal](https://intl.cloud.tencent.com/document/product/436/36378) | Removes the image metadata, including the EXIF data. |
| [Quick thumbnail template](https://intl.cloud.tencent.com/document/product/436/36379) | Performs quick format conversion, scaling, and cropping to generate thumbnails. |
| [Image size limiting](https://intl.cloud.tencent.com/document/product/436/42704) | Limits the size of an output image, such as a scaled or compressed image. |
| [Pipeline operator](https://intl.cloud.tencent.com/document/product/436/36380) | Performs multiple operations on images in sequence |


## Scaling

#### Feature description

CI uses the **imageMogr2** API to scale images. The input image cannot be larger than 32 MB, with its width and height not exceeding 30,000 pixels, and the total number of pixels not exceeding 250 million. The width and height of the output image cannot exceed 9,999 pixels. For an input animated image, the total number of pixels (Width x Height x Number of frames) cannot exceed 250 million pixels.

#### Sample codes

```php
<?php

require dirname(__FILE__, 2) . '/vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; // Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol, which is `http` by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
try {
    // Image processing - scaling. For more information, visit https://cloud.tencent.com/document/product/460/36540.
    $imageRule = new Qcloud\Cos\ImageParamTemplate\ImageMogrTemplate();
    $imageRule->thumbnailByScale(50); // /thumbnail/!<Scale>p
    $imageRule->thumbnailByWidthScale(50); // /thumbnail/!<Scale>px
    $imageRule->thumbnailByHeightScale(50); // /thumbnail/!x<Scale>p
    $imageRule->thumbnailByWidth(60); // /thumbnail/<Width>x
    $imageRule->thumbnailByHeight(60); // /thumbnail/x<Height>
    $imageRule->thumbnailByMaxWH(100, 100); // /thumbnail/<Width>x<Height>
    $imageRule->thumbnailByMinWH(30, 30); // /thumbnail/!<Width>x<Height>r
    $imageRule->thumbnailByWH(50, 50); // /thumbnail/<Width>x<Height>!
    $imageRule->thumbnailByPixel(10000); // /thumbnail/<Area>@
    $imageRule->thumbnailEqualRatioReduceByWH(300, 300); // /thumbnail/<Width>x<Height>>
    $imageRule->thumbnailEqualRatioEnlargeByWH(300, 300); // /thumbnail/<Width>x<Height><
    $imageRule->pad(1); // /pad/1
    $imageRule->color('#3D3D3D'); // /color/IzNEM0QzRA
    $imageRule->ignoreError(); // /ignore-error/1

    $picOperations = new Qcloud\Cos\ImageParamTemplate\PicOperationsTransformation();
    $picOperations->setIsPicInfo(1); // is_pic_info
    $picOperations->addRule($imageRule, "output.png"); // rules

    // -------------------- 1. Processing during download -------------------- //
//    $downloadUrl = $cosClient->getObjectUrl('examplebucket-1250000000', 'xxx.jpg'); // Get the download URL
    $downloadUrl = 'https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/xxx.jpg'; // Private images can be processed in the same way as detailed above, except that a signature is carried. The signature is concatenated with other processing parameters by an ampersand (&).
    $rule = $imageRule->queryString();
    echo "{$downloadUrl}?{$rule}";
//    echo "{$downloadUrl}&{$rule}"; // The URL of an image with a signature is concatenated by "&".
    // -------------------- 1. Processing during download -------------------- //

    // -------------------- 2. Processing during upload -------------------- //
    $result = $cosClient->putObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Key' => 'object.jpg',
        'Body' => fopen('/tmp/local.jpg', 'rb'), // Local file
        'PicOperations' => $picOperations->queryString(),
    ));
    // Request succeeded
    print_r($result);
    // -------------------- 2. Processing during upload -------------------- //

    // -------------------- 3. Processing in-cloud data -------------------- //
    $result = $cosClient->ImageProcess(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Key' => 'test.png',
        'PicOperations' => $picOperations->queryString(),
    ));
    // Request succeeded
    print_r($result);
    // -------------------- 3. Processing in-cloud data -------------------- //
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameters

Operation: thumbnail

| Parameter | Description |
| :------------------------------- | :----------------------------------------------------------- |
| ObjectKey  | Object name, such as `folder/sample.jpg`.                           |
| /thumbnail/!&lt;Scale&gt;p             | Scales an image to `Scale%` of its original width and height.                             |
| /thumbnail/!&lt;Scale&gt;px            | Scales an image to `Scale%` of its original width while keeping the height unchanged.                     |
| /thumbnail/!x&lt;Scale&gt;p            | Scales an image to `Scale%` of its original height while keeping the width unchanged.                     |
| /thumbnail/&lt;Width&gt;x              | Specifies the target image width as `Width`, with the height proportionally scaled.                    |
| /thumbnail/x&lt;Height&gt;             | Specifies the target image height as `Height`, with the width proportionally scaled.                   |
| /thumbnail/&lt;Width&gt;x&lt;Height&gt;      | Specifies the maximum width and height of a thumbnail as `Width` and `Height` respectively for proportional scaling. |
| /thumbnail/&lt;Width&gt;x&lt;Height&gt;**>** | Specifies the maximum width and height of a thumbnail as `Width` and `Height` respectively for proportional scaling down. The smaller value between the width scale ratio and height scale ratio will be used as the scale ratio. If both the output width and height are greater than the input width and height, the image will not be scaled. |
| /thumbnail/&lt;Width&gt;x&lt;Height&gt;**<** |  Specifies the maximum width and height of a thumbnail as `Width` and `Height` respectively for proportional scaling up. The smaller value between the width scale ratio and height scale ratio will be used as the scale ratio. If both the output width and height are less than the input width and height, the image will not be scaled. |
| /thumbnail/!&lt;Width&gt;x&lt;Height&gt;r    | Specifies the minimum width and height of a thumbnail as `Width` and `Height` respectively for proportional scaling. |
| /thumbnail/&lt;Width&gt;x&lt;Height&gt;!     | Forces image scaling with the specified `Width` and `Height`, which may cause deformation of the target image. |
| /thumbnail/&lt;Area&gt;@               | Proportionally scales an image so that the total number of its pixels does not exceed `Area`. |
| /pad/ | Pads the blank area with the color specified by `color` after the input image is scaled as large as possible in a rectangle with the specified `Width` and `Height`, with the image centered. Valid values: `0` (not to pad), `1` (to pad). |
| /color/ | Fill color. The value must be in hexadecimal format, such as `#FF0000`. For format conversion, see [RGB Color Codes Chart](https://www.rapidtables.com/web/color/RGB_Color.html). The value must be URL-safe Base64-encoded as described in [FAQs](https://intl.cloud.tencent.com/document/product/1045/33430). Default value: `#FFFFFF` (white). |
| /ignore-error/1 | If this parameter is carried and the image fails to be processed because the image is too large or a parameter value exceeds the limit, the input image will be returned with no error reported. |



## Cropping

#### Feature description

CI uses the `imageMogr2` API to crop images, such as regular cropping, scaling and cropping, inscribed circle cropping, rounded corner cropping, and smart cropping.

#### Sample codes

```php
<?php

require dirname(__FILE__, 2) . '/vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; // Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol, which is `http` by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
try {
    // Image processing - cropping. For more information, visit https://cloud.tencent.com/document/product/460/36541.
    $imageRule = new Qcloud\Cos\ImageParamTemplate\ImageMogrTemplate();
    $imageRule->cut(400, 400, 100, 100); // Parameters for regular cropping /cut/<width>x<height>x<dx>x<dy>
    $imageRule->cropByWidth(400, 'center'); // Parameters for scaling and cropping /crop/<Width>x
    $imageRule->cropByHeight(400, 'center'); // Parameters for scaling and cropping /crop/x<Height>
    $imageRule->cropByWH(400, 400, 'center'); // Parameters for scaling and cropping /crop/<Width>x<Height>
    $imageRule->iradius(30); // Parameters for cropping to circle /iradius/<radius>
    $imageRule->rradius(30); // Parameters for rounded corner cropping /rradius/<radius>
    $imageRule->scrop(30, 30); // Parameters for smart face cropping /scrop/<Width>x<Height>
    $imageRule->ignoreError(); // /ignore-error/1

    $picOperations = new Qcloud\Cos\ImageParamTemplate\PicOperationsTransformation();
    $picOperations->setIsPicInfo(1); // is_pic_info
    $picOperations->addRule($imageRule, "output.png"); // rules

    // -------------------- 1. Processing during download -------------------- //
//    $downloadUrl = $cosClient->getObjectUrl('examplebucket-1250000000', 'xxx.jpg'); // Get the download URL
    $downloadUrl = 'https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/xxx.jpg'; // Private images can be processed in the same way as detailed above, except that a signature is carried. The signature is concatenated with other processing parameters by an ampersand (&).
    $rule = $imageRule->queryString();
    echo "{$downloadUrl}?{$rule}";
//    echo "{$downloadUrl}&{$rule}"; // The URL of an image with a signature is concatenated by "&".
    // -------------------- 1. Processing during download -------------------- //

    // -------------------- 2. Processing during upload -------------------- //
    $result = $cosClient->putObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Key' => 'object.jpg',
        'Body' => fopen('/tmp/local.jpg', 'rb'), // Local file
        'PicOperations' => $picOperations->queryString(),
    ));
    // Request succeeded
    print_r($result);
    // -------------------- 2. Processing during upload -------------------- //

    // -------------------- 3. Processing in-cloud data -------------------- //
    $result = $cosClient->ImageProcess(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Key' => 'test.png',
        'PicOperations' => $picOperations->queryString(),
    ));
    // Request succeeded
    print_r($result);
    // -------------------- 3. Processing in-cloud data -------------------- //
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameters

| Parameter | Description |
| :-------------- | :----------------------------------------------------------- |
| /ignore-error/1 | If this parameter is carried and the image failed to be processed because the image size or the parameter value is too large, the input image will be returned with no error reported. |

##### Parameters for regular cropping

Operation: cut

| Parameter | Description |
| :------- | :-------------------------------- |
| &lt;width&gt;  | Width of the output image |
| &lt;height&gt; | Height of the output image |
| &lt;dx&gt;     | Horizontal offset relative to the top-left vertex |
| &lt;dy&gt;     | Vertical offset relative to the top-left vertex |

>?
>
> The values should be greater than 0 and smaller than the width/height of the input image.

##### Parameters for scaling and cropping

Operation: crop

| Parameter | Description |
| :--------------------- | :----------------------------------------------------------- |
| /crop/&lt;Width&gt;x         | Width of the output image with the height unchanged. The value must be greater than 0 and smaller than the width of the input image. |
| /crop/x&lt;Height&gt;        | Height of the output image with the width unchanged. The value must be greater than 0 and smaller than the height of the input image. |
| /crop/&lt;Width&gt;x&lt;Height&gt; | Width and height of the output image. The values of width and height should be greater than 0 and smaller than those of the input image, respectively. |

When performing scaling and cropping, you can also use the `gravity` parameter to specify the start position of the operation. For more information, see [Cropping](https://intl.cloud.tencent.com/document/product/1045/33714).

##### Parameters for cropping to circle

Operation: iradius

| Parameter | Description |
| :---------------- | :----------------------------------------------------------- |
| /iradius/&lt;radius&gt; | Crops to a circle. `radius` specifies the radius of the inscribed circle, which should be an integer greater than zero and less than half of the shorter side of the input image. The center of the inscribed circle is the center of the image. This operation is not supported for GIF images. |

##### Parameters for rounded corner cropping

Operation: rradius

| Parameter | Description |
| :---------------- | :----------------------------------------------------------- |
| /rradius/&lt;radius&gt; | Crops with round corners. `radius` specifies the radius of the rounded corner of the image, which should be an integer greater than zero and less than half of the shorter side of the input image. The two sides of the image are the tangent lines of the rounded corner. This operation is not supported for GIF images. |

##### Parameters for smart face cropping

Operation: scrop

| Parameter | Description |
| :---------------------- | :----------------------------------------------------------- |
| /scrop/&lt;Width&gt;x&lt;Height&gt; | Scales and crops an image based on the face position in the image. The width and height of the target image are specified by `Width` and `Height` respectively. |



## Rotating

#### Feature description

CI uses the **imageMogr2** API to rotate an image by a specified angle or automatically.

#### Sample codes

```php
<?php

require dirname(__FILE__, 2) . '/vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; // Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol, which is `http` by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
try {
    // Image processing - rotation. For more information, visit https://cloud.tencent.com/document/product/460/36542.
    $imageRule = new Qcloud\Cos\ImageParamTemplate\ImageMogrTemplate();
    $imageRule->rotate(90); // /rotate/<rotateDegree>
    $imageRule->autoOrient(); // /auto-orient
    $imageRule->flip('vertical'); // /flip/<flip>
    $imageRule->ignoreError(); // /ignore-error/1

    $picOperations = new Qcloud\Cos\ImageParamTemplate\PicOperationsTransformation();
    $picOperations->setIsPicInfo(1); // is_pic_info
    $picOperations->addRule($imageRule, "output.png"); // rules

    // -------------------- 1. Processing during download -------------------- //
//    $downloadUrl = $cosClient->getObjectUrl('examplebucket-1250000000', 'xxx.jpg'); // Get the download URL
    $downloadUrl = 'https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/xxx.jpg'; // Private images can be processed in the same way as detailed above, except that a signature is carried. The signature is concatenated with other processing parameters by an ampersand (&).
    $rule = $imageRule->queryString();
    echo "{$downloadUrl}?{$rule}";
//    echo "{$downloadUrl}&{$rule}"; // The URL of an image with a signature is concatenated by "&".
    // -------------------- 1. Processing during download -------------------- //

    // -------------------- 2. Processing during upload -------------------- //
    $result = $cosClient->putObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Key' => 'object.jpg',
        'Body' => fopen('/tmp/local.jpg', 'rb'), // Local file
        'PicOperations' => $picOperations->queryString(),
    ));
    // Request succeeded
    print_r($result);
    // -------------------- 2. Processing during upload -------------------- //

    // -------------------- 3. Processing in-cloud data -------------------- //
    $result = $cosClient->ImageProcess(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Key' => 'test.png',
        'PicOperations' => $picOperations->queryString(),
    ));
    // Request succeeded
    print_r($result);
    // -------------------- 3. Processing in-cloud data -------------------- //
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameters

| Parameter | Description |
| :--------------------- | :----------------------------------------------------------- |
| /rotate/&lt;rotateDegree&gt; | Rotates an image clockwise by a specified angle. The value can be 0−360. By default, the image is not rotated. |
| /auto-orient              | Rotates an image automatically according to its EXIF data.         |
| /flip/&lt;flip&gt;            | Flips an image. Valid values: `vertical`, `horizontal`. |
| /ignore-error/1 | If this parameter is carried and the image fails to be processed because the image is too large or a parameter value exceeds the limit, the input image will be returned with no error reported. |



## Format Conversion

#### Feature description

CI uses the `imageMogr2` API to perform format conversion, GIF optimization, and progressive display.

#### Sample codes

```php
<?php

require dirname(__FILE__, 2) . '/vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; // Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol, which is `http` by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
try {
    // Image processing - format conversion. For more information, visit https://cloud.tencent.com/document/product/460/36543.
    $imageRule = new Qcloud\Cos\ImageParamTemplate\ImageMogrTemplate();
    $imageRule->format('jpg'); // Format conversion /format/<Format>
    $imageRule->gifOptimization(1); // GIF optimization /cgif/<FrameNumber>
    $imageRule->jpegInterlaceMode(1); // Progressive mode of the output JPG image, where `Mode` can be `0` or `1`. /interlace/<Mode>
    $imageRule->ignoreError(); // /ignore-error/1

    $picOperations = new Qcloud\Cos\ImageParamTemplate\PicOperationsTransformation();
    $picOperations->setIsPicInfo(1); // is_pic_info
    $picOperations->addRule($imageRule, "output.png"); // rules

    // -------------------- 1. Processing during download -------------------- //
//    $downloadUrl = $cosClient->getObjectUrl('examplebucket-1250000000', 'xxx.jpg'); // Get the download URL
    $downloadUrl = 'https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/xxx.jpg'; // Private images can be processed in the same way as detailed above, except that a signature is carried. The signature is concatenated with other processing parameters by an ampersand (&).
    $rule = $imageRule->queryString();
    echo "{$downloadUrl}?{$rule}";
//    echo "{$downloadUrl}&{$rule}"; // The URL of an image with a signature is concatenated by "&".
    // -------------------- 1. Processing during download -------------------- //

    // -------------------- 2. Processing during upload -------------------- //
    $result = $cosClient->putObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Key' => 'object.jpg',
        'Body' => fopen('/tmp/local.jpg', 'rb'), // Local file
        'PicOperations' => $picOperations->queryString(),
    ));
    // Request succeeded
    print_r($result);
    // -------------------- 2. Processing during upload -------------------- //

    // -------------------- 3. Processing in-cloud data -------------------- //
    $result = $cosClient->ImageProcess(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Key' => 'test.png',
        'PicOperations' => $picOperations->queryString(),
    ));
    // Request succeeded
    print_r($result);
    // -------------------- 3. Processing in-cloud data -------------------- //
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameters

| Parameter | Description |
| :------------------ | :----------------------------------------------------------- |
| /format/&lt;Format&gt;    | Converts the image format. The target format can be JPG, BMP, GIF, PNG, WebP, or YJPEG (which is optimized based on JPEG and is essentially JPG). The default format is the format of the input image. |
| /cgif/&lt;FrameNumber&gt;  | Optimizes images in the GIF format by reducing frames and colors of images. There are two cases: FrameNumber=1: Cut the input GIF to the default number of frames (30). If the original number of frames is greater than 30, excessive frames will be cut. FrameNumber=(1,100]: Compress the image to the specified number of frames (`FrameNumber`). |
| /interlace/&lt;Mode&gt;   | Progressive mode of the output JPG image. Valid values: `0` (default): Disables the progressive mode; `1`: Enables the progressive mode. This parameter takes effect only when the output image is in JPG format. |
| /ignore-error/1 | If this parameter is carried and the image fails to be processed because the image is too large or a parameter value exceeds the limit, the input image will be returned with no error reported. |



## Quality Change

#### Feature description

CI uses the `imageMogr2` API to adjust the quality of an image.

#### Sample codes

```php
<?php

require dirname(__FILE__, 2) . '/vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; // Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol, which is `http` by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
try {
    // Image processing - quality change. For more information, https://cloud.tencent.com/document/product/460/36544.
    $imageRule = new Qcloud\Cos\ImageParamTemplate\ImageMogrTemplate();
    $imageRule->quality(90, 1); // Absolute quality /quality/<Quality>
    $imageRule->lowestQuality(90); // Lowest quality /lquality/<quality>
    $imageRule->relativelyQuality(90); // Relative quality /rquality/<quality>
    $imageRule->ignoreError(); // /ignore-error/1

    $picOperations = new Qcloud\Cos\ImageParamTemplate\PicOperationsTransformation();
    $picOperations->setIsPicInfo(1); // is_pic_info
    $picOperations->addRule($imageRule, "output.png"); // rules

    // -------------------- 1. Processing during download -------------------- //
//    $downloadUrl = $cosClient->getObjectUrl('examplebucket-1250000000', 'xxx.jpg'); // Get the download URL
    $downloadUrl = 'https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/xxx.jpg'; // Private images can be processed in the same way as detailed above, except that a signature is carried. The signature is concatenated with other processing parameters by an ampersand (&).
    $rule = $imageRule->queryString();
    echo "{$downloadUrl}?{$rule}";
//    echo "{$downloadUrl}&{$rule}"; // The URL of an image with a signature is concatenated by "&".
    // -------------------- 1. Processing during download -------------------- //

    // -------------------- 2. Processing during upload -------------------- //
    $result = $cosClient->putObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Key' => 'object.jpg',
        'Body' => fopen('/tmp/local.jpg', 'rb'), // Local file
        'PicOperations' => $picOperations->queryString(),
    ));
    // Request succeeded
    print_r($result);
    // -------------------- 2. Processing during upload -------------------- //

    // -------------------- 3. Processing in-cloud data -------------------- //
    $result = $cosClient->ImageProcess(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Key' => 'test.png',
        'PicOperations' => $picOperations->queryString(),
    ));
    // Request succeeded
    print_r($result);
    // -------------------- 3. Processing in-cloud data -------------------- //
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameters

Operation: quality

| Parameter | Description |
| :------------------ | :----------------------------------------------------------- |
| /quality/&lt;Quality&gt;  | Absolute quality of the image. The value can be 0–100. Use the value of the original image quality (default) or the specified quality, whichever is smaller. If there is an exclamation mark (!) after <Quality> (such as `90!`), the specified quality value is forcibly used. |
| /rquality/&lt;quality&gt; | Image quality relative to that of the input image. The value can be 0−100. For example, if the input image quality is 80 and `rquality` is set to `80`, the quality of the output image will be 64 (80 * 80%). |
| /lquality/&lt;quality&gt; | Minimum quality of the image. Value range: 0−100. If the input image quality is 85 and `lquality` is set to 80, the quality of the output image will be 85. If the input image quality is 60 and `lquality` is set to 80, the quality of the output image will be improved to 80. |
| /ignore-error/1 | If this parameter is carried and the image fails to be processed because the image is too large or a parameter value exceeds the limit, the input image will be returned with no error reported. |



## Gaussian Blurring

#### Feature description

CI uses the **imageMogr2** API to blur an image.

#### Sample codes

```php
<?php

require dirname(__FILE__, 2) . '/vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; // Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol, which is `http` by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
try {
    // Image processing - Gaussian blurring. For more information, visit https://cloud.tencent.com/document/product/460/36545.
    $imageRule = new Qcloud\Cos\ImageParamTemplate\ImageMogrTemplate();
    $imageRule->blur(8, 5); // Gaussian blurring /blur/<radius>x<sigma>
    $imageRule->ignoreError(); // /ignore-error/1

    $picOperations = new Qcloud\Cos\ImageParamTemplate\PicOperationsTransformation();
    $picOperations->setIsPicInfo(1); // is_pic_info
    $picOperations->addRule($imageRule, "output.png"); // rules

    // -------------------- 1. Processing during download -------------------- //
//    $downloadUrl = $cosClient->getObjectUrl('examplebucket-1250000000', 'xxx.jpg'); // Get the download URL
    $downloadUrl = 'https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/xxx.jpg'; // Private images can be processed in the same way as detailed above, except that a signature is carried. The signature is concatenated with other processing parameters by an ampersand (&).
    $rule = $imageRule->queryString();
    echo "{$downloadUrl}?{$rule}";
//    echo "{$downloadUrl}&{$rule}"; // The URL of an image with a signature is concatenated by "&".
    // -------------------- 1. Processing during download -------------------- //

    // -------------------- 2. Processing during upload -------------------- //
    $result = $cosClient->putObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Key' => 'object.jpg',
        'Body' => fopen('/tmp/local.jpg', 'rb'), // Local file
        'PicOperations' => $picOperations->queryString(),
    ));
    // Request succeeded
    print_r($result);
    // -------------------- 2. Processing during upload -------------------- //

    // -------------------- 3. Processing in-cloud data -------------------- //
    $result = $cosClient->ImageProcess(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Key' => 'test.png',
        'PicOperations' => $picOperations->queryString(),
    ));
    // Request succeeded
    print_r($result);
    // -------------------- 3. Processing in-cloud data -------------------- //
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameters

Operation: blur

| Parameter | Description |
| :-------------- | :----------------------------------------------------------- |
| radius&lt;radius&gt;  | Blurring radius. Value range: 1–50. |
| sigma&lt;sigma&gt;    | Standard deviation of normal distribution. The value must be greater than 0. |
| /ignore-error/1 | If this parameter is carried and the image failed to be processed because the image size or the parameter value is too large, the input image will be returned with no error reported. |



## Adjusting Brightness

#### Feature description

CI uses the **imageMogr2** API to adjust the brightness of an image.

#### Sample codes

```php
<?php


require dirname(__FILE__, 2) . '/vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; // Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol, which is `http` by default
        'credentials' => array(
            'secretId'  => $secretId,
            'secretKey' => $secretKey)));
try {
    // Image processing - brightness. For more information, visit https://cloud.tencent.com/document/product/460/51808.
    $imageRule = new Qcloud\Cos\ImageParamTemplate\ImageMogrTemplate();
    $imageRule->bright(70); // Image brightness adjustment /bright/<value>
    $imageRule->ignoreError(); // /ignore-error/1

    $picOperations = new Qcloud\Cos\ImageParamTemplate\PicOperationsTransformation();
    $picOperations->setIsPicInfo(1); // is_pic_info
    $picOperations->addRule($imageRule, "output.png"); // rules

    // -------------------- 1. Processing during download -------------------- //
//    $downloadUrl = $cosClient->getObjectUrl('examplebucket-1250000000', 'xxx.jpg'); // Get the download URL
    $downloadUrl = 'https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/xxx.jpg'; // Private images can be processed in the same way as detailed above, except that a signature is carried. The signature is concatenated with other processing parameters by an ampersand (&).
    $rule = $imageRule->queryString();
    echo "{$downloadUrl}?{$rule}";
//    echo "{$downloadUrl}&{$rule}"; // The URL of an image with a signature is concatenated by "&".
    // -------------------- 1. Processing during download -------------------- //

    // -------------------- 2. Processing during upload -------------------- //
    $result = $cosClient->putObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Key' => 'object.jpg',
        'Body' => fopen('/tmp/local.jpg', 'rb'), // Local file
        'PicOperations' => $picOperations->queryString(),
    ));
    // Request succeeded
    print_r($result);
    // -------------------- 2. Processing during upload -------------------- //

    // -------------------- 3. Processing in-cloud data -------------------- //
    $result = $cosClient->ImageProcess(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Key' => 'test.png',
        'PicOperations' => $picOperations->queryString(),
    ));
    // Request succeeded
    print_r($result);
    // -------------------- 3. Processing in-cloud data -------------------- //
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameters

Operation: bright

| Parameter | Description |
| :-------------- | :----------------------------------------------------------- |
| /bright/&lt;value&gt; | Adjusts the brightness of an image. The value must be an integer in the range of [-100, 100]. `value` < 0: Reduces the image brightness. `value` = 0: Does not adjust the image brightness. `value` > 0: Increases the image brightness. |
| /ignore-error/1 | If this parameter is carried and the image failed to be processed because the image size or the parameter value is too large, the input image will be returned with no error reported. |



## Adjusting Contrast

#### Feature description

CI uses the **imageMogr2** API to adjust an image’s contrast, which is the difference in luminance between the brightest and darkest points in an image (i.e., the contrast in grayscale).

#### Sample codes

```php
<?php


require dirname(__FILE__, 2) . '/vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; // Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol, which is `http` by default
        'credentials' => array(
            'secretId'  => $secretId,
            'secretKey' => $secretKey)));
try {
    // Image processing - contrast. For more information, visit https://cloud.tencent.com/document/product/460/51809.
    $imageRule = new Qcloud\Cos\ImageParamTemplate\ImageMogrTemplate();
    $imageRule->contrast(-70); // Image contrast adjustment /contrast/<value>
    $imageRule->ignoreError(); // /ignore-error/1

    $picOperations = new Qcloud\Cos\ImageParamTemplate\PicOperationsTransformation();
    $picOperations->setIsPicInfo(1); // is_pic_info
    $picOperations->addRule($imageRule, "output.png"); // rules

    // -------------------- 1. Processing during download -------------------- //
//    $downloadUrl = $cosClient->getObjectUrl('examplebucket-1250000000', 'xxx.jpg'); // Get the download URL
    $downloadUrl = 'https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/xxx.jpg'; // Private images can be processed in the same way as detailed above, except that a signature is carried. The signature is concatenated with other processing parameters by an ampersand (&).
    $rule = $imageRule->queryString();
    echo "{$downloadUrl}?{$rule}";
//    echo "{$downloadUrl}&{$rule}"; // The URL of an image with a signature is concatenated by "&".
    // -------------------- 1. Processing during download -------------------- //

    // -------------------- 2. Processing during upload -------------------- //
    $result = $cosClient->putObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Key' => 'object.jpg',
        'Body' => fopen('/tmp/local.jpg', 'rb'), // Local file
        'PicOperations' => $picOperations->queryString(),
    ));
    // Request succeeded
    print_r($result);
    // -------------------- 2. Processing during upload -------------------- //

    // -------------------- 3. Processing in-cloud data -------------------- //
    $result = $cosClient->ImageProcess(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Key' => 'test.png',
        'PicOperations' => $picOperations->queryString(),
    ));
    // Request succeeded
    print_r($result);
    // -------------------- 3. Processing in-cloud data -------------------- //
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameters

Operation: contrast

| Parameter | Description |
| :---------------- | :----------------------------------------------------------- |
| /contrast/&lt;value&gt; | Adjusts the contrast of an image. The value must be an integer in the range of [-100, 100]. `value` < 0: Reduces the contrast. `value` = 0: Does not adjust the contrast. `value` > 0: Increases the contrast. |
| /ignore-error/1 | If this parameter is carried and the image fails to be processed because the image is too large or a parameter value exceeds the limit, the input image will be returned with no error reported. |



## Sharpening

#### Feature description

CI uses the **imageMogr2** API to sharpen an image.

#### Sample codes

```php
<?php


require dirname(__FILE__, 2) . '/vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; // Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol, which is `http` by default
        'credentials' => array(
            'secretId'  => $secretId,
            'secretKey' => $secretKey)));
try {
    // Image processing - sharpening. For more information, visit https://cloud.tencent.com/document/product/460/36546.
    $imageRule = new Qcloud\Cos\ImageParamTemplate\ImageMogrTemplate();
    $imageRule->sharpen(70); // Image sharpening /sharpen/<value>
    $imageRule->ignoreError(); // /ignore-error/1

    $picOperations = new Qcloud\Cos\ImageParamTemplate\PicOperationsTransformation();
    $picOperations->setIsPicInfo(1); // is_pic_info
    $picOperations->addRule($imageRule, "output.png"); // rules

    // -------------------- 1. Processing during download -------------------- //
//    $downloadUrl = $cosClient->getObjectUrl('examplebucket-1250000000', 'xxx.jpg'); // Get the download URL
    $downloadUrl = 'https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/xxx.jpg'; // Private images can be processed in the same way as detailed above, except that a signature is carried. The signature is concatenated with other processing parameters by an ampersand (&).
    $rule = $imageRule->queryString();
    echo "{$downloadUrl}?{$rule}";
//    echo "{$downloadUrl}&{$rule}"; // The URL of an image with a signature is concatenated by "&".
    // -------------------- 1. Processing during download -------------------- //

    // -------------------- 2. Processing during upload -------------------- //
    $result = $cosClient->putObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Key' => 'object.jpg',
        'Body' => fopen('/tmp/local.jpg', 'rb'), // Local file
        'PicOperations' => $picOperations->queryString(),
    ));
    // Request succeeded
    print_r($result);
    // -------------------- 2. Processing during upload -------------------- //

    // -------------------- 3. Processing in-cloud data -------------------- //
    $result = $cosClient->ImageProcess(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Key' => 'test.png',
        'PicOperations' => $picOperations->queryString(),
    ));
    // Request succeeded
    print_r($result);
    // -------------------- 3. Processing in-cloud data -------------------- //
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameters

Operation: sharpen

| Parameter | Description |
| :--------------- | :----------------------------------------------------------- |
| /sharpen/&lt;value&gt; | Sharpens an image, where `value` controls the strength of the sharpening effect. The value must be an integer ranging from 10 to 300 (70 is recommended). The greater the value, the more obvious the sharpening effect. |
| /ignore-error/1 | If this parameter is carried and the image fails to be processed because the image is too large or a parameter value exceeds the limit, the input image will be returned with no error reported. |



## Grayscale Image

#### Feature description

COS uses CI’s **imageMogr2/grayscale** API to set an image to be a grayscale image.

#### Sample codes

```php
<?php


require dirname(__FILE__, 2) . '/vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; // Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol, which is `http` by default
        'credentials' => array(
            'secretId'  => $secretId,
            'secretKey' => $secretKey)));
try {
    // Image processing - grayscale image. For more information, visit https://cloud.tencent.com/document/product/460/66519.
    $imageRule = new Qcloud\Cos\ImageParamTemplate\ImageMogrTemplate();
    $imageRule->grayscale(1); // Conversion of the image to grayscale image /grayscale/<value>
    $imageRule->ignoreError(); // /ignore-error/1

    $picOperations = new Qcloud\Cos\ImageParamTemplate\PicOperationsTransformation();
    $picOperations->setIsPicInfo(1); // is_pic_info
    $picOperations->addRule($imageRule, "output.png"); // rules

    // -------------------- 1. Processing during download -------------------- //
//    $downloadUrl = $cosClient->getObjectUrl('examplebucket-1250000000', 'xxx.jpg'); // Get the download URL
    $downloadUrl = 'https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/xxx.jpg'; // Private images can be processed in the same way as detailed above, except that a signature is carried. The signature is concatenated with other processing parameters by an ampersand (&).
    $rule = $imageRule->queryString();
    echo "{$downloadUrl}?{$rule}";
//    echo "{$downloadUrl}&{$rule}"; // The URL of an image with a signature is concatenated by "&".
    // -------------------- 1. Processing during download -------------------- //

    // -------------------- 2. Processing during upload -------------------- //
    $result = $cosClient->putObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Key' => 'object.jpg',
        'Body' => fopen('/tmp/local.jpg', 'rb'), // Local file
        'PicOperations' => $picOperations->queryString(),
    ));
    // Request succeeded
    print_r($result);
    // -------------------- 2. Processing during upload -------------------- //

    // -------------------- 3. Processing in-cloud data -------------------- //
    $result = $cosClient->ImageProcess(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Key' => 'test.png',
        'PicOperations' => $picOperations->queryString(),
    ));
    // Request succeeded
    print_r($result);
    // -------------------- 3. Processing in-cloud data -------------------- //
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameters

Operation: grayscale

| Parameter | Description |
| :----------------- | :----------------------------------------------------------- |
| /grayscale/&lt;value&gt; | Whether to set an image to be a grayscale image. Valid values of the `value` field: `0` (no), `1` (yes). |
| /ignore-error/1 | If this parameter is carried and the image fails to be processed because the image is too large, the input image will be returned with no error reported. |



## Image Watermark

#### Feature description

COS implements image watermarking using the **watermark** API provided by CI, and thus only images stored in CI-bound buckets can be processed. For the restrictions on Basic Image Processing (including watermarking), please see [Rules and Limits](https://intl.cloud.tencent.com/document/product/1045/33425).

#### Sample codes

```php
<?php


require dirname(__FILE__, 2) . '/vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; // Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol, which is `http` by default
        'credentials' => array(
            'secretId'  => $secretId,
            'secretKey' => $secretKey)));
try {
    // Image processing - image watermark. For more information, visit https://cloud.tencent.com/document/product/460/6930.
    $imageWatermarkRule = new Qcloud\Cos\ImageParamTemplate\ImageWatermarkTemplate();
    $imageWatermarkRule->setImage('https://www.xxx.com/xxx.jpg'); // Watermark image address
    $imageWatermarkRule->setGravity('SouthEast'); // Image watermark position
    $imageWatermarkRule->setDx(10); // Horizontal offset in px. Default value: `0`.
    $imageWatermarkRule->setDy(10); // Vertical offset in px. Default value: `0`.
    $imageWatermarkRule->setBlogo(1); // Adaptation mode for an image watermark that is larger than the input image
    $imageWatermarkRule->setScatype(1); // Scale the image watermark to the size of the input image
    $imageWatermarkRule->setSpcent(200); // Use together with `scatype`
    $imageWatermarkRule->setDissolve(70); // Image watermark opacity
    $imageWatermarkRule->setBatch(1); // Tile the image watermark
    $imageWatermarkRule->setDegree(90); // Set the angle to rotate the image watermark. This parameter will take effect only when `/batch/` is set to `1`.

    $picOperations = new Qcloud\Cos\ImageParamTemplate\PicOperationsTransformation();
    $picOperations->setIsPicInfo(1); // is_pic_info
    $picOperations->addRule($imageWatermarkRule, "output.png"); // rules

    // -------------------- 1. Processing during download -------------------- //
//    $downloadUrl = $cosClient->getObjectUrl('examplebucket-1250000000', 'xxx.jpg'); // Get the download URL
    $downloadUrl = 'https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/xxx.jpg'; // Private images can be processed in the same way as detailed above, except that a signature is carried. The signature is concatenated with other processing parameters by an ampersand (&).
    $rule = $imageWatermarkRule->queryString();
    echo "{$downloadUrl}?{$rule}";
//    echo "{$downloadUrl}&{$rule}"; // The URL of an image with a signature is concatenated by "&".
    // -------------------- 1. Processing during download -------------------- //

    // -------------------- 2. Processing during upload -------------------- //
    $result = $cosClient->putObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Key' => 'object.jpg',
        'Body' => fopen('/tmp/local.jpg', 'rb'), // Local file
        'PicOperations' => $picOperations->queryString(),
    ));
    // Request succeeded
    print_r($result);
    // -------------------- 2. Processing during upload -------------------- //

    // -------------------- 3. Processing in-cloud data -------------------- //
    $result = $cosClient->ImageProcess(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Key' => 'test.png',
        'PicOperations' => $picOperations->queryString(),
    ));
    // Request succeeded
    print_r($result);
    // -------------------- 3. Processing in-cloud data -------------------- //
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameters

In the code above, `watermark` is the operation name and the number `1` indicates that the watermark is an image.

| Parameter       | Description                                                                                                                                        |
| :--------- | :----------------------------------------------------------- |
| /image/      | Image watermark URL, which must be [URL-safe Base64-encoded](https://intl.cloud.tencent.com/document/product/1045/33430). For example, if the image watermark URL is `http://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/shuiyin_2.png`, you should set this parameter to `aHR0cDovL2V4YW1wbGVidWNrZXQtMTI1MDAwMDAwMC5jb3MuYXAtc2hhbmdoYWkubXlxY2xvdWQuY29tL3NodWl5aW5fMi5wbmc`.  |
| /gravity/    | Position of the image watermark, which is a square in a [3x3 grid](https://intl.cloud.tencent.com/document/product/436/36373#1). Default value: `SouthEast`. |
| /dx/         | Horizontal offset in px. Default value: `0`.                      |
| /dy/         | Vertical offset in px. Default value: `0`.                      |
| /blogo/      | Adaptation mode for an image watermark that is larger than the input image. Valid values: `1` (scales the image watermark to the size of the input image); `2` (crops the image watermark to the size of the input image). |
| /scatype/    | Scaling mode for the image watermark (relative to the input image). Valid values: `1` (scales by width); `2` (scales by height); `3` (scales by area). |
| /spcent/     | Scale ratio of the image watermark in permillage. This parameter must be used together with `scatype`. Value range: 1−1000 (if `scatype` is set to `1`); 1−1000 (if `scatype` is set to `2`); 1−250 (if `scatype` is set to `3`). Example: `http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?watermark/1/image/xxxxxxx/scatype/3/spcent/250` |
| /dissolve/ | Opacity of the image watermark. Value range: 1−100. Default value: `90` (meaning 90% opacity) |
| /batch/ | Whether to tile the image watermark. If this parameter is set to `1`, the image watermark will be tiled across the input image. |
| /degree/ | Angle to rotate the image watermark. This parameter will take effect only when `/batch/` is set to `1`. Value range: 0−360. Default value: `0`. |

>!
>
> An image watermark must:
>
> - Be stored in the same bucket as the input image.
> - Have a URL containing a COS domain name (a CDN acceleration domain name such as `examplebucket-1250000000.file.myqcloud.com/shuiyin_2.png` is unsupported) and be accessible (if the image watermark is set to private-read, it must carry a signature).
> - Have a URL starting with `http://`. Note that "http://" cannot be omitted or changed to "https://". For example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/shuiyin_2.png` and `https://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/shuiyin_2.png` are invalid watermark URLs.



## Text Watermark

#### Feature description

COS uses the **watermark** API provided by CI to add text watermarks in real time. An input image cannot be larger than 32 MB, with its width and height not exceeding 30,000 pixels and the total number of pixels not exceeding 250 million. The width and height of the output image cannot exceed 9,999 pixels. For an input animated image, its total number of pixels (Width x Height x Number of frames) cannot exceed 250 million.

#### Sample codes

```php
<?php


require dirname(__FILE__, 2) . '/vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; // Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol, which is `http` by default
        'credentials' => array(
            'secretId'  => $secretId,
            'secretKey' => $secretKey)));
try {
    // Image processing - text watermark. For more information, visit https://cloud.tencent.com/document/product/460/6951.
    $textWatermarkRule = new Qcloud\Cos\ImageParamTemplate\TextWatermarkTemplate();
    $textWatermarkRule->setText('Watermark content'); // Watermark content
    $textWatermarkRule->setFont('tahoma.ttf'); // Watermark font
    $textWatermarkRule->setFontsize(13); // Watermark text font size
    $textWatermarkRule->setFill('#3D3D3D'); // Font color. The value must be in hexadecimal RGB format, such as `#FF0000`. Default value: `#3D3D3D` (gray).
    $textWatermarkRule->setDissolve(90); // Text opacity. Value range: 1−100. Default value: `90` (meaning 90% opacity).
    $textWatermarkRule->setGravity('SouthEast'); // Position of the text watermark in the 3x3 grid position diagram. Default value: `SouthEast`.
    $textWatermarkRule->setDx(10); // Horizontal offset in px. Default value: `0`.
    $textWatermarkRule->setDy(10); // Vertical offset in px. Default value: `0`.
    $textWatermarkRule->setBatch(1); // Whether to tile the text watermark. If this parameter is set to `1`, the text watermark will be tiled across the input image.
    $textWatermarkRule->setDegree(10); // Angle to rotate the text watermark. This parameter will take effect only when `/batch/` is set to `1`. Value range: 0−360. Default value: `0`.
    $textWatermarkRule->setShadow(10); // Text shadow effect. Value range: 0−100. Default value: `0` (no shadow).

    $picOperations = new Qcloud\Cos\ImageParamTemplate\PicOperationsTransformation();
    $picOperations->setIsPicInfo(1); // is_pic_info
    $picOperations->addRule($textWatermarkRule, "output.png"); // rules

    // -------------------- 1. Processing during download -------------------- //
//    $downloadUrl = $cosClient->getObjectUrl('examplebucket-1250000000', 'xxx.jpg'); // Get the download URL
    $downloadUrl = 'https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/xxx.jpg'; // Private images can be processed in the same way as detailed above, except that a signature is carried. The signature is concatenated with other processing parameters by an ampersand (&).
    $rule = $textWatermarkRule->queryString();
    echo "{$downloadUrl}?{$rule}";
//    echo "{$downloadUrl}&{$rule}"; // The URL of an image with a signature is concatenated by "&".
    // -------------------- 1. Processing during download -------------------- //

    // -------------------- 2. Processing during upload -------------------- //
    $result = $cosClient->putObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Key' => 'object.jpg',
        'Body' => fopen('/tmp/local.jpg', 'rb'), // Local file
        'PicOperations' => $picOperations->queryString(),
    ));
    // Request succeeded
    print_r($result);
    // -------------------- 2. Processing during upload -------------------- //

    // -------------------- 3. Processing in-cloud data -------------------- //
    $result = $cosClient->ImageProcess(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Key' => 'test.png',
        'PicOperations' => $picOperations->queryString(),
    ));
    // Request succeeded
    print_r($result);
    // -------------------- 3. Processing in-cloud data -------------------- //
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameters

In the code above, `watermark` is the operation name and the number `2` indicates that the watermark is a text.

| Parameter       | Description                                                                                                                                        |
| :--------- | :----------------------------------------------------------- |
| /text/  | Watermark text, which must be [URL-safe Base64-encoded](https://intl.cloud.tencent.com/document/product/1045/33430). |
| /font/ | Font of the text, which must be [URL-safe Base64-encoded](https://intl.cloud.tencent.com/document/product/1045/33430). Default font: Tahoma.ttf (see [Supported Fonts](https://intl.cloud.tencent.com/document/product/1045/40681)). |
| /fontsize/ | Font size, in pt. Default value: `13`. To scale the text watermark proportionally based on the original image, convert the text watermark to a PNG image. For more configuration information, see [Image Watermarking](https://intl.cloud.tencent.com/document/product/436/36373)                     |
| /fill/ | Font color. The value must be in hexadecimal format, for example, `#FF0000`. For format conversion, see [RGB Color Codes Chart](https://www.rapidtables.com/web/color/RGB_Color.html). The value must be [URL-safe Base64-encoded](https://intl.cloud.tencent.com/document/product/1045/33430). Default value: `#3D3D3D` (gray). |
| /dissolve/ | Text opacity. Value range: 1−100. Default value: `90` (meaning 90% opacity) |
| /gravity/    | Position of the text watermark, which is a square in a [3x3 grid](https://intl.cloud.tencent.com/document/product/436/36374#1). Default value: `SouthEast`. |
| /dx/         | Horizontal offset in px. Default value: `0`.                      |
| /dy/         | Vertical offset in px. Default value: `0`.                      |
| /batch/ | Whether to tile the text watermark. If this parameter is set to `1`, the text watermark will be tiled across the input image. |
| /degree/ | Angle to rotate the text watermark. This parameter will take effect only when `/batch/` is set to `1`. Value range: 0−360. Default value: `0`. |
| /shadow/|  Text shadow effect. Value range: 0−100. Default value: `0` (no shadow).   |



## Basic Image Information Acquisition

#### Feature description

COS uses the **imageInfo** API provided by CI to query an image’s basic information such as its format, width, and height.

#### Sample codes

```php
<?php

require dirname(__FILE__, 2) . '/vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; // Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol, which is `http` by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
try {
    $result = $cosClient->ImageInfo(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Key' => 'exampleobject',
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameters

**Operation**: imageInfo

| Parameter       | Description                                                                                                                                        |
| :--- | :----------------------------------- |
| Key  | Object name, such as `folder/sample.jpg`.                           |

#### Response parameters

| Parameter | Description |
| :---------- | :-------------------------------------- |
| format | Image type, such as PNG and GIF. |
| width       | Image width in px.           |
| height      | Image height in px.          |
| size        | Image size in bytes.                |
| md5         | Image MD5 value.                           |
| frame_count | Number of frames. For static images, this value is `1`. |



## Image EXIF Data Acquisition

#### Feature description

Exchangeable Image File (EXIF) records the camera settings, thumbnails, and other attributes of digital images. COS uses the **exif** API provided by CI to obtain EXIF data. An input image cannot be larger than 32 MB, with its width and height not exceeding 30,000 pixels and the total number of pixels not exceeding 250 million. The width and height of an output image cannot exceed 9,999 pixels. For an input animated image, the total number of pixels (Width x Height x Number of frames) cannot exceed 250 million.

#### Sample codes

```php
<?php

require dirname(__FILE__, 2) . '/vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; // Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol, which is `http` by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
try {
    $result = $cosClient->ImageExif(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Key' => 'exampleobject',
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameters

**Operation**: exif

| Parameter       | Description                                                                                                                                        |
| :--- | :----------------------------------- |
| Key  | Object name, such as `folder/sample.jpg`.                           |



## Image Average Hue Acquisition

#### Feature description

COS uses the **imageAve** API provided by CI to obtain the average hue of an image. The input image cannot be larger than 32 MB, with its width and height not exceeding 30,000 pixels, and the total number of pixels not exceeding 250 million. The width and height of the output image cannot exceed 9,999 pixels. For an input animated image, the total number of pixels (Width x Height x Number of frames) cannot exceed 250 million pixels.

#### Sample codes

```php
<?php

require dirname(__FILE__, 2) . '/vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; // Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol, which is `http` by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
try {
    $result = $cosClient->ImageAve(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Key' => 'exampleobject',
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameters

**Operation**: imageAve

| Parameter       | Description                                                                                                                                        |
| :--- | :----------------------------------- |
| Key  | Object name, such as `folder/sample.jpg`.                           |



## Removing Image Metadata

#### Feature description

COS uses the **imageMogr2** API provided by CI to remove image metadata, including EXIF data.

#### Sample codes

```php
<?php


require dirname(__FILE__, 2) . '/vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; // Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol, which is `http` by default
        'credentials' => array(
            'secretId'  => $secretId,
            'secretKey' => $secretKey)));
try {
    // Image processing - metadata removal. For more information, visit https://cloud.tencent.com/document/product/460/36547.
    $imageRule = new Qcloud\Cos\ImageParamTemplate\ImageMogrTemplate();
    $imageRule->strip(); // Remove the image metadata, including EXIF data.  /strip
    $imageRule->ignoreError(); // /ignore-error/1

    $picOperations = new Qcloud\Cos\ImageParamTemplate\PicOperationsTransformation();
    $picOperations->setIsPicInfo(1); // is_pic_info
    $picOperations->addRule($imageRule, "output.png"); // rules

    // -------------------- 1. Processing during download -------------------- //
//    $downloadUrl = $cosClient->getObjectUrl('examplebucket-1250000000', 'xxx.jpg'); // Get the download URL
    $downloadUrl = 'https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/xxx.jpg'; // Private images can be processed in the same way as detailed above, except that a signature is carried. The signature is concatenated with other processing parameters by an ampersand (&).
    $rule = $imageRule->queryString();
    echo "{$downloadUrl}?{$rule}";
//    echo "{$downloadUrl}&{$rule}"; // The URL of an image with a signature is concatenated by "&".
    // -------------------- 1. Processing during download -------------------- //

    // -------------------- 2. Processing during upload -------------------- //
    $result = $cosClient->putObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Key' => 'object.jpg',
        'Body' => fopen('/tmp/local.jpg', 'rb'), // Local file
        'PicOperations' => $picOperations->queryString(),
    ));
    // Request succeeded
    print_r($result);
    // -------------------- 2. Processing during upload -------------------- //

    // -------------------- 3. Processing in-cloud data -------------------- //
    $result = $cosClient->ImageProcess(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Key' => 'test.png',
        'PicOperations' => $picOperations->queryString(),
    ));
    // Request succeeded
    print_r($result);
    // -------------------- 3. Processing in-cloud data -------------------- //
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameters

Operation: strip

| Parameter | Description |
| :-------------- | :----------------------------------------------------------- |
| /ignore-error/1 | If this parameter is carried and the image failed to be processed because it is too large, the input image will be returned with no error reported. |



## Quick Thumbnail Template

#### Feature description

COS uses the **imageView2** API of Cloud Infinite (CI) to provide a common image processing template. You can append parameters to the download URL to generate the desired thumbnail. The input image cannot be larger than 32 MB, with its width and height not exceeding 30,000 pixels and the total number of pixels not exceeding 250 million. The width and height of the output image cannot exceed 9,999 pixels. For an input animated image, the total number of pixels (width x height x number of frames) cannot exceed 250 million (GIF frame limit: 300).

#### Sample codes

```php
<?php


require dirname(__FILE__, 2) . '/vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; // Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol, which is `http` by default
        'credentials' => array(
            'secretId'  => $secretId,
            'secretKey' => $secretKey)));
try {
    // Image processing - quick thumbnail template. For more information, visit https://cloud.tencent.com/document/product/460/6929.
    $imageViewRule = new Qcloud\Cos\ImageParamTemplate\ImageViewTemplate();
    $imageViewRule->setMode(1); // /<mode>
    $imageViewRule->setWidth(400); // /w/<Width>
    $imageViewRule->setHeight(600); // /h/<Height>
    $imageViewRule->setFormat('jpg'); // /format/<Format>
    $imageViewRule->setQuality(1, 85); // 1-/q/<Quality>; 2-/rq/<quality>; 3-/lq/<quality>
    $imageViewRule->ignoreError(); // /ignore-error/1

    $picOperations = new Qcloud\Cos\ImageParamTemplate\PicOperationsTransformation();
    $picOperations->setIsPicInfo(1); // is_pic_info
    $picOperations->addRule($imageViewRule, "output.png"); // rules

    // -------------------- 1. Processing during download -------------------- //
//    $downloadUrl = $cosClient->getObjectUrl('examplebucket-1250000000', 'xxx.jpg'); // Get the download URL
    $downloadUrl = 'https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/xxx.jpg'; // Private images can be processed in the same way as detailed above, except that a signature is carried. The signature is concatenated with other processing parameters by an ampersand (&).
    $rule = $imageViewRule->queryString();
    echo "{$downloadUrl}?{$rule}";
//    echo "{$downloadUrl}&{$rule}"; // The URL of an image with a signature is concatenated by "&".
    // -------------------- 1. Processing during download -------------------- //

    // -------------------- 2. Processing during upload -------------------- //
    $result = $cosClient->putObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Key' => 'object.jpg',
        'Body' => fopen('/tmp/local.jpg', 'rb'), // Local file
        'PicOperations' => $picOperations->queryString(),
    ));
    // Request succeeded
    print_r($result);
    // -------------------- 2. Processing during upload -------------------- //

    // -------------------- 3. Processing in-cloud data -------------------- //
    $result = $cosClient->ImageProcess(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Key' => 'test.png',
        'PicOperations' => $picOperations->queryString(),
    ));
    // Request succeeded
    print_r($result);
    // -------------------- 3. Processing in-cloud data -------------------- //
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameters

| Parameter | Description |
| :---------------------------- | :----------------------------------------------------------- |
| /1/w/&lt;Width&gt;/h/&lt;Height&gt;       | Specifies the minimum width and height of the thumbnail. In this mode, the image will be first scaled down until one of the minimum values set is reached. Then, the image will be centered and evenly cropped on both sides to meet the specified values. If only one value is set, a square thumbnail will be generated. For example, if the input image size is 1000x500 and this parameter is set to `?imageView2/1/w/500/h/400`, the image will be scaled down to 800x400 first. Then, 150 pixels will be cropped from the left and right sides respectively, outputting a 500x400 thumbnail. |
| /2/w/&lt;Width&gt;/h/&lt;Height&gt;       | Specifies the maximum width and height of the thumbnail. In this mode, the image is scaled down until both the width and length are not greater than the maximum values set. For example, if the input image size is 1000x500 and this parameter is set to `?imageView2/2/w/500/h/400`, the image is scaled down to 500x250. If only one value is set, the image will be adapted. |
| /3/w/&lt;Width&gt;/h/&lt;Height&gt;       | Specifies the minimum width and height of the thumbnail. In this mode, the image will be scaled down until both the width and height are not smaller than the minimum values set. For example, if the input image size is 1000x500 and this parameter is set to `?imageView2/3/w/500/h/400`, the image will be scaled down to 800x400. If only one value is set, a square thumbnail will be generated. |
| /4/w/&lt;LongEdge&gt;/h/&lt;ShortEdge&gt; | Specifies the minimum values of the long edge and short edge of the thumbnail to scale down the image. If only one value is set, a square thumbnail will be generated. |
| /5/w/&lt;LongEdge&gt;/h/&lt;ShortEdge&gt; | Specifies the maximum values of the long edge and short edge of the thumbnail to scale down the image. The image will be centered and cropped. If only one value is set, a square thumbnail will be generated. After the scaling, the excess will be cropped. |
| /format/&lt;Format&gt;              | Format of the thumbnail, which can be JPG, BMP, GIF, PNG, or WebP. Default value: Format of the input image. |
| /q/&lt;Quality&gt;                  | Image quality. The value can be 0–100. Use the value of the original image quality (default) or the specified quality, whichever is smaller. If there is an exclamation mark (!) after <Quality>, the specified quality value is forcibly used. |
| /rq/&lt;quality&gt;                 | Image quality relative to that of the input image. The value can be 0−100. For example, if the input image quality is 80 and `rquality` is set to `80`, the quality of the output image will be 64 (80 * 80%). |
| /lq/&lt;quality&gt;                 | Minimum quality of the image. Value range: 0−100. If the input image quality is 85 and `lquality` is set to 80, the quality of the output image will be 85. If the input image quality is 60 and `lquality` is set to 80, the quality of the output image will be improved to 80. |



## Image Size Limiting

#### Feature description

COS uses the **imageMogr2/size-limit** API provided by CI to limit the size of an image processed (e.g., scaled or compressed).

#### Sample codes

```php
<?php


require dirname(__FILE__, 2) . '/vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; // Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol, which is `http` by default
        'credentials' => array(
            'secretId'  => $secretId,
            'secretKey' => $secretKey)));
try {
    // Image processing - image size limiting. For more information, visit https://cloud.tencent.com/document/product/460/56732.
    $imageRule = new Qcloud\Cos\ImageParamTemplate\ImageMogrTemplate();
    $imageRule->sizeLimit(15, 1); // Limit the size of an output image, such as a scaled or compressed image /size-limit/<value>!
    $imageRule->ignoreError(); // /ignore-error/1

    $picOperations = new Qcloud\Cos\ImageParamTemplate\PicOperationsTransformation();
    $picOperations->setIsPicInfo(1); // is_pic_info
    $picOperations->addRule($imageRule, "output.png"); // rules

    // -------------------- 1. Processing during download -------------------- //
//    $downloadUrl = $cosClient->getObjectUrl('examplebucket-1250000000', 'xxx.jpg'); // Get the download URL
    $downloadUrl = 'https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/xxx.jpg'; // Private images can be processed in the same way as detailed above, except that a signature is carried. The signature is concatenated with other processing parameters by an ampersand (&).
    $rule = $imageRule->queryString();
    echo "{$downloadUrl}?{$rule}";
//    echo "{$downloadUrl}&{$rule}"; // The URL of an image with a signature is concatenated by "&".
    // -------------------- 1. Processing during download -------------------- //

    // -------------------- 2. Processing during upload -------------------- //
    $result = $cosClient->putObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Key' => 'object.jpg',
        'Body' => fopen('/tmp/local.jpg', 'rb'), // Local file
        'PicOperations' => $picOperations->queryString(),
    ));
    // Request succeeded
    print_r($result);
    // -------------------- 2. Processing during upload -------------------- //

    // -------------------- 3. Processing in-cloud data -------------------- //
    $result = $cosClient->ImageProcess(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Key' => 'test.png',
        'PicOperations' => $picOperations->queryString(),
    ));
    // Request succeeded
    print_r($result);
    // -------------------- 3. Processing in-cloud data -------------------- //
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameters

Operation: size-limit

| Parameter | Description |
| :-------------- | :----------------------------------------------------------- |
| size-limit | Limits the size of the output image. The unit can be `k` (KB) or `m` (MB). 1. Only JPG images are supported. 2. Appending an exclamation mark (!) means to compare the sizes of the input and output images. If the output image is smaller, the output image will be returned; otherwise, the input image will be returned; for example,  `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpg?imageMogr2/size-limit/15k!`. 3. We recommend you use this parameter together with `strip` to remove redundant image metadata, for example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpg?imageMogr2/strip/format/png/size-limit/15k!`. |
| /ignore-error/1 | If this parameter is carried and the image failed to be processed because it is too large, the input image will be returned with no error reported. |



## Pipeline Operator

#### Feature description

COS uses the pipeline operators (|) provided by CI to separate multiple image processing parameters. In this way, multiple operations can be performed in sequence in a single request. The input image cannot be larger than 32 MB, with its width and height not exceeding 30,000 pixels, and the total number of pixels not exceeding 250 million. The width and height of the output image cannot exceed 9,999 pixels. For an input animated image, the total number of pixels (Width x Height x Number of frames) cannot exceed 250 million pixels.

#### Sample codes

```php
<?php


require dirname(__FILE__, 2) . '/vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; // Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol, which is `http` by default
        'credentials' => array(
            'secretId'  => $secretId,
            'secretKey' => $secretKey)));
try {
    // Image processing - pipeline operator. For more information, visit https://cloud.tencent.com/document/product/460/15293.
    $imageMogrRule = new Qcloud\Cos\ImageParamTemplate\ImageMogrTemplate();
    $imageMogrRule->thumbnailByScale(50);
    $imageMogrRule->rotate(50);
    $imageViewRule = new Qcloud\Cos\ImageParamTemplate\ImageViewTemplate();
    $imageViewRule->setMode(1);
    $imageViewRule->setWidth(400);
    $imageViewRule->setHeight(600);
    $imageViewRule->setQuality(1, 85);
    $ciParamChannel = new Qcloud\Cos\ImageParamTemplate\CIParamTransformation();
    $ciParamChannel->addRule($imageMogrRule); // Multiple processing methods connected by "|"
    $ciParamChannel->addRule($imageViewRule); // Multiple processing methods connected by "|"

    $picOperations = new Qcloud\Cos\ImageParamTemplate\PicOperationsTransformation();
    $picOperations->setIsPicInfo(1); // is_pic_info
    $picOperations->addRule($ciParamChannel, "output.png"); // rules

    // -------------------- 1. Processing during download -------------------- //
//    $downloadUrl = $cosClient->getObjectUrl('examplebucket-1250000000', 'xxx.jpg'); // Get the download URL
    $downloadUrl = 'https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/xxx.jpg'; // Private images can be processed in the same way as detailed above, except that a signature is carried. The signature is concatenated with other processing parameters by an ampersand (&).
    $rule = $ciParamChannel->queryString();
    echo "{$downloadUrl}?{$rule}";
//    echo "{$downloadUrl}&{$rule}"; // The URL of an image with a signature is concatenated by "&".
    // -------------------- 1. Processing during download -------------------- //

    // -------------------- 2. Processing during upload -------------------- //
    $result = $cosClient->putObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Key' => 'object.jpg',
        'Body' => fopen('/tmp/local.jpg', 'rb'), // Local file
        'PicOperations' => $picOperations->queryString(),
    ));
    // Request succeeded
    print_r($result);
    // -------------------- 2. Processing during upload -------------------- //

    // -------------------- 3. Processing in-cloud data -------------------- //
    $result = $cosClient->ImageProcess(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Key' => 'test.png',
        'PicOperations' => $picOperations->queryString(),
    ));
    // Request succeeded
    print_r($result);
    // -------------------- 3. Processing in-cloud data -------------------- //
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameters

Multiple processing styles are separated by the pipeline operator `|` and executed in sequence. Currently, there can be a maximum of 10 pipelines.
