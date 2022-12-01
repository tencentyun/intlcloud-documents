Image scaling and cropping have many use cases. For example, images may be scaled to generate thumbnails for media files, and cropping is needed to make square or circular user profile photos. When images are stored in the cloud, traditional editing methods such as locally run software and online editing tools have many disadvantages, for example:
- The process of downloading, editing, and uploading is complicated.
- Manual editing is not efficient and prone to errors.

These pain points can be addressed by VOD’s real-time image processing feature.

<Table>
<tbody>
<tr>
<th>Aspect</th>
<th>Traditional Image Editing</th>
<th>VOD Image Processing</th>
</tr>
<tr>
<td>Process</td>
<td>You need to download the images, edit them, and then upload them. The process is complicated and time-consuming.</td>
<td>All operations are performed in the cloud, with no need for download or upload.</td>
</tr>
<tr>
<td>Operation</td>
<td>You need to have some knowledge of image editing to be able to use image editing software.</td>
<td>You can edit images in real time simply by specifying URL parameters.</td>
</tr>
<tr>
<td>Speed</td>
<td>It can be slow to access and download images stored in the cloud via URLs, hurting the user experience.</td>
<td>CDNs are used for acceleration, allowing you to get the result immediately.</td>
</tr>
</tbody>
</Table>

The real-time image processing feature of VOD supports scaling and cropping operations.

<Table>
<tbody>
<tr>
<th>Type</th>
<th>Operation</th>
</tr>
<tr>
<td rowspan=5>Scaling</td>
<td>Width: Specified; height: Auto-scaled</td>
</tr>
<tr>
<td>Height: Specified; width: Auto-scaled</td>
</tr>
<tr>
<td>Long side: Specified; short side: Auto-scaled</td>
</tr>
<tr>
<td>Short side: Specified; long side: Auto-scaled</td>
</tr>
<tr>
<td>Width: Specified; height: Specified</td>
</tr>
<tr>
<td rowspan="2">Cropping</td>
<td>Cropping to circle, with the radius specified</td>
</tr>
<tr>
<td>Cropping to rectangle, with height and width specified</td>
</tr>
</tbody>
</Table>

For detailed directions on how to process images with VOD, see [Real-Time Image Processing](https://intl.cloud.tencent.com/document/product/266/42094).
