## Overview

Tencent Cloud COS has integrated the professional All-in-One media solutions of [Cloud Infinite](https://intl.cloud.tencent.com/document/product/1045), covering image processing, moderation, recognition, and many more. See the table below for details. You can process your media data with the Upload and Process APIs in COS.

> !
> - This image processing feature is only supported for Public Cloud regions.
> - Image processing is a paid service, the fees of which are charged by Cloud Infinite. For detailed billing instructions, see Cloud Infinite’s [Billing and Pricing](https://intl.cloud.tencent.com/document/product/1045/33431).



<table>
   <tr>
      <th>Service</td>
      <th>Feature</td>
      <th>Description</td>
   </tr>
   <tr>
      <td rowspan=12>Image Processing-Basic Services</td>
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
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36370">Changing quality</a></td>
      <td>Changes the quality of images in JPG and WEBP formats</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36371">Gaussian blur</a></td>
      <td>Blurs images</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36372">Sharpening</a></td>
      <td>Sharpens images</td>
   </tr>
   <tr>
      <td>Watermarking</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36373">Adds image watermarks</a>,<a href="https://intl.cloud.tencent.com/document/product/436/36374">Adds text watermarks</a></td>
   </tr>
   <tr>
      <td>Obtaining image information</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36375">Gets the basic information</a>,<a href="https://intl.cloud.tencent.com/document/product/436/36376">EXIF data </a>,<a href="https://intl.cloud.tencent.com/document/product/436/36377">average hue of an image</a></td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36378">Removing metadata</a></td>
      <td>Including EXIF data</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36379">Quick thumbnail template</a></td>
      <td>Performs quick format conversion, scaling, and cropping to generate thumbnails</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/1045/33443#.E6.A0.B7.E5.BC.8F.E7.AE.A1.E7.90.86">Setting styles</a></td>
      <td>Sets image styles to easily manage images for different purposes</td>
   </tr>
</table>



## Directions

#### Using the COS console

Set image processing in the COS console. For more information, see [Enabling Image Processing](https://intl.cloud.tencent.com/document/product/436/35278).

#### Using REST API

Set image processing using the API provided in COS.

