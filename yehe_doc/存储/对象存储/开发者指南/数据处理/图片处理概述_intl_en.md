## Overview

Image Processing is a set of image processing capabilities provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). It supports basic processing capabilities such as image cropping, format conversion, scaling, and watermarking, image downsizing capabilities such as Guetzli compression and AVIF transcoding and compression, blind watermarking for copyright protection, and AI-based recognition and analysis features such as image enhancement, tagging, scoring, and repair and image matting, meeting your image processing requirements in diverse business scenarios.

> !
> - Image Processing is available only in public cloud regions.
> - Image Processing is charged by CI. For detailed pricing, see **Basic image processing fee** in [Billing and Pricing](https://intl.cloud.tencent.com/document/product/1045/33431).
> - Currently, image processing is not supported for multi-AZ buckets.
>


<table>
<table>
   <tr>
      <th>Service</td>
      <th>Feature</td>
      <th>Description</td>
   </tr>
   <tr>
      <td rowspan=12>Basic Image Processing</td>
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
      <td><a href="https://intl.cloud.tencent.com/document/product/1045/33443">Setting styles</a></td>
      <td>Sets image styles to easily manage images for different purposes</td>
   </tr>
   <tr>
      <td rowspan=11>AI-Based Image Recognition</td>
      <td>Image repair</td>
      <td>Removes content like logos, objects, and watermarks from images and intelligently fills it with the background to repair certain areas in images effectively.</td>
   </tr>
   <tr>
      <td>Image matting</td>
      <td>Intelligently recognizes the body part in images and makes the remaining part transparent.</td>
   </tr>
   <tr>
      <td>Logo recognition</td>
      <td>Recognizes brand logos in images and returns information such as logo characters and positions in the images.</td>
   </tr>
   <tr>
      <td>QR code recognition</td>
      <td>Recognizes QR codes in images and returns their positions and content. Recognized QR codes can be pixelated.</td>
   </tr>
   <tr>
      <td>Image tagging</td>
      <td>Intelligently recognizes information such as scenes, objects, animals (including cats, dogs, and birds), and food (including fruits and vegetables) in images and adds corresponding tags. Thousands of tags in dozens of categories are supported.</td>
   </tr>
   <tr>
      <td>Image quality assessment</td>
      <td>Assesses the visual image quality in various dimensions and outputs objective definition scores and subjective aesthetic scores.</td>
   </tr>
   <tr>
      <td>Face recognition</td>
      <td>Detects the face positions, facial features, face quality information in given face images and supports various special effects, including beauty filters, portrait keying, age change, and gender swap.</td>
   </tr>
   <tr>
      <td>FaceID</td>
      <td>Provides capabilities like ID card recognition and face liveness detection.</td>
   </tr>
   <tr>
      <td>Vehicle recognition</td>
      <td>Detects vehicles in images and recognizes information such as vehicle brand, color, location, and license plate number.</td>
   </tr>
   <tr>
      <td>Text recognition</td>
      <td>Intelligently recognizes words in images and converts them into editable text.</td>
   </tr>
   <tr>
      <td>Search by image</td>
      <td>Creates image libraries in a bucket and quickly searches for the same and similar images in the specified image libraries.</td>
   </tr>
   <tr>
      <td rowspan=1>Others</td>
      <td>Abnormal image detection</td>
      <td>Detects images with abnormal and suspicious information such as images with TS video streams.</td>
   </tr>
</table>



## How to Use

#### Using COS console

You can perform basic image processing operations in the COS console as instructed in [Basic Image Processing](https://intl.cloud.tencent.com/document/product/436/36569).

#### Using RESTful APIs

You can perform basic image processing operations or AI-based recognition by using the APIs provided by COS as instructed in [Data Processing APIs](https://www.tencentcloud.com/document/product/436/36364).

## Restrictions

- Format: JPG, BMP, GIF, PNG, and WebP images can be processed, and HEIF images can be decoded and processed.
- Size: The input image cannot be larger than 32 MB, with its width and height not exceeding 30,000 pixels, and the total number of pixels not exceeding 250 million. The width and height of the output image cannot exceed 9,999 pixels. For an input animated image, the total number of pixels (Width x Height x Number of frames) cannot exceed 250 million pixels.
- Number of frames (for animated images): For GIF, the number of frames cannot exceed 300.
