## Overview

Tencent Cloud COS has integrated the professional All-in-One media solutions of [Cloud Infinite](https://intl.cloud.tencent.com/document/product/1045), covering image processing, moderation, recognition, and many more. See the table below for details. You can process your media data with the Upload and Process APIs in COS.

<table>
   <tr>
      <th>Service</td>
      <th>Feature</td>
      <th>Description</td>
   </tr>
   <tr>
      <td rowspan=12>Basic image processing service</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/1045/33713">Scaling</a></td>
      <td>Proportional scaling, scale an image based on the target width and height, and more</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/1045/33714">Cropping</a></td>
      <td>Cut (regular cropping), crop (scaling and cropping), iradius (inscribed circle cropping), and scrop (smart cropping)</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/1045/33715">Rotation</a></td>
      <td>Adaptive rotation and common rotation</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/1045/33716">Format conversion</a></td>
      <td>Format conversion, GIF format optimization, and progressive display</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/1045/33717">Quality conversion</a></td>
      <td>Perform quality conversion on images in JPG and WEBP formats</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/1045/33718">Gaussian blurring</a></td>
      <td>Blur images</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/1045/33719">Sharpening</a></td>
      <td>Sharpen images</td>
   </tr>
   <tr>
      <td>Watermarking</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/1045/33720"> image watermarks</a>、<a href="https://intl.cloud.tencent.com/document/product/1045/33721">text watermarks</a></td>
   </tr>
   <tr>
      <td>Obtaining image information</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/1045/33722">Basic information</a>、<a href="https://intl.cloud.tencent.com/document/product/1045/33723">EXIF information</a>、<a href="https://intl.cloud.tencent.com/document/product/1045/33724">average hue</a></td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/1045/33725">Removing meta information</a></td>
      <td>Including EXIF information</td>
   </tr>
   <tr>
      <td><a href="https://cloud.tencent.com/document/product/460/6929">Quick thumbnail template</a></td>
      <td>Perform quick format conversion, scaling, and cropping to generate thumbnails</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/1045/33443">Setting styles</a></td>
      <td>Set image styles to manage images for different purposes</td>
   </tr>
      <td rowspan="6">Value-added image services</td>
      <td><a href="https://cloud.tencent.com/document/product/460/19017">Blind watermarking</a></td>
      <td>Add an invisible watermark to the original image without affecting its quality</td>
   </tr>
   <tr>
      <td>Content detection</td>
      <td>Detect obscene, political, violence, and advertising content</td>
   </tr>
   <tr>
      <td><a href="https://cloud.tencent.com/document/product/460/37513">QR code recognition</a></td>
      <td>Recognize and override (if necessary) the position and content of a valid QR code in an image</td>
   </tr>
      <td><a href="https://cloud.tencent.com/document/product/460/39082">Image tag</a></td>
      <td>Identify the main content in an image and return its tag information</td>
   </tr>
</table>




## Directions

#### Using the COS Console

You can set image processing in the COS Console. For more information, please see [Enabling Image Processing](https://intl.cloud.tencent.com/document/product/436/35278).

>
> - This image processing feature is only supported for Public Cloud regions in mainland China.
> - Image Processing is a paid service, the fees of which are charged by Cloud Infinite. For detailed billing instructions, see Cloud Infinite’s [Billing and Pricing](https://intl.cloud.tencent.com/document/product/1045/33431).

#### Using REST API

You can configure image processing with the Cloud Infinite API. For more information, see the Cloud Infinite API documentation Basic Image Processing.

