## Overview
The real-time image processing feature of VOD supports scaling and cropping operations, which are detailed below:
<melo-data data-src="" data-version="2.1.0"></melo-data><table ><colgroup><col  width="301px"><col  width="301px"></colgroup>
<tbody>
<tr>
<th   colspan="1" rowspan="1" align="" valign=""><p>Operation Type</p></td>
 <th   colspan="1" rowspan="1" align="" valign=""><p>Detailed Operation</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="5" align="" valign=""><p>Scaling</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>The width is adjusted to the specified value, and the height changes with it proportionally.</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>The height is adjusted to the specified value, and the width changes with it proportionally.</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>The long sides are adjusted to the specified length, and the short sides change with them proportionally.</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>The short sides are adjusted to the specified length, and the long sides change with them proportionally.</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>The image is forcibly scaled to the specified width and height.</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="2" align="" valign=""><p>Cropping</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>A circle with the specified radius is inscribed from the image.</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>A rectangle with the specified height and width is inscribed from the image.</p></td>
</tr>
</tbody>
</table>

 Compared with traditional image editing, VOD's real-time image processing feature has the following strengths:
<melo-data data-src="{}" data-version="2.1.0"></melo-data><table ><colgroup><col  width="201px"><col  width="201px"><col  width="201px"></colgroup>
<tbody>
<tr>
<th   colspan="1" rowspan="1" align="" valign=""><p>Dimension</p></td>
 <th   colspan="1" rowspan="1" align="" valign=""><p>Traditional Image Editing</p></td>
 <th   colspan="1" rowspan="1" align="" valign=""><p>Real-Time Image Processing of VOD</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>Processing steps</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>Multiple steps are required, including download, editing, and upload, which are time-consuming and laborious.</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>You can directly complete all image editing processes in the cloud with no need to upload and download images.</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>Operation method</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>Image editing software is difficult to use and requires a mastery of certain image editing skills.</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>You can specify the image editing parameters in the URL in real time, which is easy to get started with.</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>Access speed</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>Image access and download through cloud storage URLs are slow, affecting the user experience.</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>VOD uses CDN to accelerate global image delivery, so that you can get the processed images in very little time.</p></td>
</tr>
</tbody>
</table>

## Use Cases
<melo-data data-src="{}" data-version="2.1.0"></melo-data><table ><colgroup><col  width="301px"><col  width="301px"></colgroup>
<tbody>
<tr>
<th   colspan="1" rowspan="1" align="" valign=""><p>Use Case</p></td>
 <th   colspan="1" rowspan="1" align="" valign=""><p>Description</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>User profile photo</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>User profile photos are generally round or square images with the same resolution. You can use scaling and cropping to generate them.</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>Identity document photos</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>When a photo of an identity document is taken, it may need to be cropped to retain only the identity information part of the document.</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>Image close-up</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>When the key part in an image requires a close-up, it needs to be cropped from the image.</p></td>
</tr>
</tbody>
</table>

## Directions
For more information, see [Real-Time Image Processing](https://intl.cloud.tencent.com/document/product/266/42094).

