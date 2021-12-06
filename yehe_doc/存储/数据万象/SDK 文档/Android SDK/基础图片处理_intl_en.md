## Overview

CI provides the ResponsiveTransformation (auto processing) and CITransformation (custom processing) image processing methods.

>? 
- Format: Currently, JPG, BMP, GIF, PNG, and WebP images can be processed, and HEIF images can be decoded and processed.
- Size: The input image cannot be larger than 32 MB, with its width and height not exceeding 30,000 pixels, and the total number of pixels not exceeding 250 million. The width and height of the output image cannot exceed 9,999 pixels. For an input animated image, the total number of pixels (Width x Height x Number of frames) cannot exceed 250 million pixels.
- Number of frames (for animated images): For GIF, the number of frames cannot exceed 300.


#### ResponsiveTransformation

ResponsiveTransformation includes format conversion (converting formats according to OS versions) and scaling (scaling images according to the imageView control sizes and ScaleType) and is described as follows:
1. ResponsiveTransformation refers to processing images automatically.
2. Image sizes are automatically adjusted according to the imageView control sizes and ScaleType.
3. Images are automatically converted to the format most suitable for the OS version. For an OS earlier than Android 4.3, the original format is used. For Android 4.3 to 10.0, WebP is used. For Android 10.0 and later, HEIC is used.
```
    ResponsiveTransformation transformation = new ResponsiveTransformation(imageview);
```

#### CITransformation

The CITransformation class in the cloud-infinite SDK has encapsulated the following basic image processing features of CI:

- [Scaling](#ci_suofang)
- [Cropping](#ci_caijian)
- [Rotating](#ci_xuanzhuan)
- [Format Conversion](#ci_geshizhuanhuan)
- [Quality Change](#ci_zhiliangbianhuan)
- [Gaussian Blurring](#ci_gaosimohua)
- [Sharpening](#ci_ruihua)
- [Watermarking](#ci_shuiyin)
- [Removing Image Metadata](#ci_yuanxinxi)
- [Combined Operations](#ci_zuhe)

Before using the basic image processing features of CI, instantiate the CITransformation class first as follows. Note that instantiation is required for all the operations described below.

```
CITransformation transform = new CITransformation();
```

<div id="ci_suofang"></div>


## Scaling

>? For the API documentation, please see [Scaling](https://intl.cloud.tencent.com/document/product/1045/33713).
>

#### Scaling by percentage

```plaintext
// Scale the image’s width to 50% without changing the height.
transform.thumbnailByWidthScale(50);
// Scale the image’s height to 50% without changing the width.
transform.thumbnailByHeightScale(50);
// Scale both the image’s width and height to 50%.
transform.thumbnailByScale(50);
```

#### Scaling with specified width and height

```plaintext
// Scale the image’s width to 50 with the height scaled automatically.
transform.thumbnailByWidth(50);
// Scale the image’s height to 50 with the width scaled automatically.
transform.thumbnailByHeight(50);
// Set both the minimum width and height of the output image to 50 to scale the image.
transform.thumbnailByMinWH(50, 50);
// Set both the maximum width and height of the output image to 50 to scale the image.
transform.thumbnailByMaxWH(50, 50);
// Scale both the image’s width and height to 50 with the original aspect ratio ignored. Note that the image might be distorted.
transform.thumbnailByWH(50, 50);
```

#### Proportional scaling

This feature scales images by limiting the resolution of the output image (the total number of pixels cannot exceed the specified value).

```
// Scale the image proportionally by limiting the total number of pixels of the output image to 1,000.
transform.thumbnailByPixel(1000);
```

<div id="ci_caijian"></div>


## Cropping

>? For the API documentation, please see [Cropping](https://intl.cloud.tencent.com/document/product/1045/33714).
>

#### Regular cropping

```plaintext
// Crop the image to the specified width and height (vertical and horizontal offsets relative to the upper-left vertex).
transform.cut(100, 300, 30, 30);
```

#### Inscribed circle cropping

`radius` specifies the radius of the inscribed circle. The value of `radius` should be an integer greater than 0 but smaller than half the length of the input image’s shorter side. The center of the inscribed circle is the center of the input image. This operation is not available for GIF images.

```
// Set the radius to 100.
transform.iradius(100);
```

#### Rounded corner cropping

`radius` specifies the radius of the rounded corners of an image. The value of `radius` should be an integer greater than 0 but smaller than half the length of the input image’s shorter side. The two sides of the input image are the tangent lines of the rounded corner. This operation is not available for GIF images.

```
// Set the corner radius to 100.
transform.rradius(100);
```

#### Scaling and cropping 

>? For more information about the 3x3 grid position diagram, please see [gravity](https://intl.cloud.tencent.com/document/product/1045/33714#.E4.B9.9D.E5.AE.AB.E6.A0.BC.E6.96.B9.E4.BD.8D.E5.9B.BE).
>

```
// Scale and crop the input image to the target width and height.
transform.cropByWH(100, 100);
// Scale and crop the input image to the target width and height with the reference point (CIGravity) specified.
transform.cropByWH(100, 100, CIGravity.CENTER);
// Scale and crop the input image to the target width.
transform.cropByWidth(100);
// Scale and crop the input image to the target width with the reference point (CIGravity) specified.
transform.cropByWidth(100, CIGravity.CENTER);
// Scale and crop the input image to the target height.
transform.cropByHeight(100);
// Scale and crop the input image to the target height with the reference point (CIGravity) specified.
transform.cropByHeight(100, CIGravity.CENTER);
```

#### Smart cropping

Scale and crop an image based on the face position in the image. The width and height of the target image are specified by `Width` and `Height` respectively.

``` 
// Crop the face from the image and scale both the width and height to 100.
transform.scrop(100, 100);
```

<div id="ci_xuanzhuan"></div>


## Rotating

>? For the API documentation, please see [Rotating](https://intl.cloud.tencent.com/document/product/1045/33715).
>

#### Rotating an image by a specified angle

Rotate an image clockwise by a specified angle (0−360 degrees). By default, the image is not rotated.

```
// Rotate the image by 45 degrees.
transform.rotate(45);
```

#### Rotating an image automatically

Rotate an image automatically according to the EXIF data of the input image.

```
transform.rotate();
```

<div id="ci_geshizhuanhuan"></div>


## Format Conversion

>? For the API documentation, please see [Converting Format](https://intl.cloud.tencent.com/document/product/1045/33716).
>

The target format can be TPG, JPG, BMP, GIF, PNG, HEIC, YJPEG (optimized by CI based on JPEG and is essentially JPG), and more. By default, the image format is not converted.

```
// Convert an image into JPEG.
 transform.format(CIImageFormat.JPEG, CIImageLoadOptions.LoadTypeUrlFooter);
```

**CIImageLoadOptions**

```
// Loading option 1: Include the accept header (accept:image/xxx).
LoadTypeAcceptHeader,

// Loading option 2: Append imageMogr2/format/xxx to the URL.
LoadTypeUrlFooter,
```

>?
> - To use the WebP format, ensure the version is Android 4.3 or later.
> - To use the HEIC format, ensure the version is Android 10 or later.
> - Converting GIF into HEIF is not supported.
> - If you pass in parameters using `LoadTypeAcceptHeader` and have specified other image processing rules, the header will not take effect. Instead, the SDK will use footer automatically.
>

To convert an image into TPG format, the TPG SDK is needed as follows:
```
    implementation 'com.tencent.qcloud:tpg:1.3.1'	
```

When installing TPG, the .so libraries will be included automatically. You are advised to use the “abiFilter” configuration of the NDK in the module’s `build.gradle` file to set the .so library frameworks that are supported.

```
defaultConfig {
    ndk {
       // Set the .so library frameworks that are supported.
        abiFilters 'armeabi' //, 'x86', 'armeabi-v7a', 'x86_64', 'arm64-v8a'
    }
}
```

#### GIF optimization

This feature only optimizes GIF images to reduce frames and image colors.
    FrameNumber=1: cuts the input GIF to the default number of frames (30). If the original number of frames is greater than 30, the exceeded frames will be cut.
    FrameNumber=(1,100]: compresses the image to the specified number of frames (`FrameNumber`).

```
transform.gifOptimization(50);
```

#### Progressive mode of the output JPG image

This operation is only available if the output format is JPG. Otherwise, this operation will be ignored.

```
transform.jpegInterlaceMode(true);
```

<div id="ci_zhiliangbianhuan"></div>


## Quality Change


CI supports three modes (absolute, relative, and lowest quality) to change the quality of an image. For the API documentation, please see [Quality Change](https://intl.cloud.tencent.com/document/product/1045/33717).


```
// Set the absolute quality of the image. Value range: 0−100. By default, the smaller value between the original image quality and the specified quality will be used.
transform.quality(90);
// Set the lowest quality of the output image. Value range: 0−100.
// If the input image quality is 85 and `lquality` is set to 80, the quality of the output image is 85.
// If the input image quality is 60 and `lquality` is set to 80, the quality of the output image will be improved to 80.
transform.lowestQuality(90);
// Set the relative quality of the image, relative to that of the input image. Value range: 0−100. For example, if the input image quality is 80 and `rquality` is set to `80`, the quality of the output image is 64 (that is, 80 x 80%).
transform.relativelyQuality(80);
```

>? This operation is only available for JPG and WebP images.
>

<div id="ci_gaosimohua"></div>


## Gaussian Blurring

Gaussian blurring supports a blur radius ranging from 1 to 50, and the standard deviation of the normal distribution must be greater than 0. For the API documentation, please see [Gaussian Blurring](https://intl.cloud.tencent.com/document/product/1045/33718).


```
// Set the blur radius to 20 and the standard deviation of the normal distribution to 20.
transform.blur(20, 20);
```

>? This operation is not available for GIF images.
>

<div id="ci_ruihua"></div>


## Sharpening


The sharpening value can be an integer ranging from 10 to 300 (70 is recommended). The greater the value, the more obvious the sharpening. For the API documentation, please see [Sharpening](https://intl.cloud.tencent.com/document/product/1045/33719).

```
// Set the sharpening value to 70.
transform.sharpen(70);
```

<div id="ci_shuiyin"></div>


## Watermarking

>?
> - For the API documentation, plesae see [Image Watermarking](https://intl.cloud.tencent.com/document/product/1045/33720) and [Text Watermarking](https://intl.cloud.tencent.com/document/product/1045/33721).
> - For more information about the 3x3 grid position diagram, please see [gravity](https://intl.cloud.tencent.com/document/product/1045/33721#1).
> 

#### Image watermark

```
WatermarkImageTransform watermarkImageTransform = new WatermarkImageTransform
        // Set the URL of the image watermark.
        .Builder(imageurl)
        // Set the reference point in the 3x3 grid position diagram.
        .setGravity(CIGravity.CENTER)
        // Set the adaptation mode for an image watermark that is larger than the input image.
        .setBlogo(1)
        // Set the horizontal offset.
        .setDistanceX(10)
        // Set the vertical offset.
        .setDistanceY(10)
        .builder();
transform.watermarkImage(watermarkImageTransform);
```

>? An image watermark must:
> 1. Be stored in the same bucket as the input image.
> 2. Have a URL containing a COS domain name (a CDN acceleration domain name such as `examplebucket-1250000000.file.myqcloud.com/shuiyin_2.png` is unsupported) and be accessible. If the image watermark is set to private-read, it must carry a signature.
> 3. Have a URL starting with `http://`. Note that "http://" cannot be omitted or changed to "https://". For example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/shuiyin_2.png` and `https://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/shuiyin_2.png` are invalid watermark URLs.
> 

#### Text watermark

```
WatermarkTextTransform watermarkImageTransform = new WatermarkTextTransform
        // Set the watermark text.
        .Builder("Watermark")
        // Set the reference point in the 3x3 grid position diagram.
        .setGravity(CIGravity.CENTER)
        // Set the font.
        .setFont("tahoma.ttf")
        // Set the font size.
        .setFontSize(13)
        // Set the text color.
        .setFill("#FF0000")
        // Set the opacity of the watermark.
        .setDissolve(80)
        // Set the horizontal offset.
        .setDistanceX(10)
        // Set the vertical offset.
        .setDistanceY(10)
        // Enable text watermark tiling to tile the watermark across the image.
        .openBatch()
        // Rotate the watermark.
        .rotate(45)
        .builder();
transform.watermarkText(watermarkImageTransform);
```

<div id="ci_yuanxinxi"></div>


## Removing Image Metadata

CI uses the `imageMogr2` API to remove image metadata, including the EXIF data. For the API documentation, please see [Removing Image Metadata](https://intl.cloud.tencent.com/document/product/1045/33725).

```
transform.strip();
```

<div id="ci_zuhe"></div>


## Combined Operations

`Transform` can be used to perform multiple operations in order.

```
transform
        .thumbnailByScale(80)
        .iradius(100)
        .blur(20,20)
        .strip();
```
