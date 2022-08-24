## Overview
Media deletion involves deleting media resources stored in VOD to reduce the storage costs. VOD provides a rich-featured and easy-to-use media deletion service.

<table>
    <tr>
        <th style="width:150px">
           Strengths              
        </th>
				<th>
           Description
        </th>
    </tr>
		 <tr>
        <td>
            Comprehensive features
        </td>
				<td>
				Two deletion modes are supported:
				<li>Complete deletion: The source file uploaded to VOD and all the files generated after processing such as transcoded files and screenshots are deleted.</li>
				<li>Partial deletion: Only a part of files such as the source file and the transcoded file of the specified definition are deleted.</li>
        </td>
 </tr>
 <tr>
        <td>
           Ease of use
        </td>
				<td>
				Automatic deletion and manual deletion are supported.</br>
				Automatic deletion:
				<ul>
				<li>You can specify the expiration time when uploading a media file. Upon expiration, the media file and its related resources (such as transcoding results and image sprites) will be permanently deleted.
				<ul><li>You can specify the expiration time when using a server API for upload application.</li>
				</ul></li>
				<li>You can specify the expiration time for an uploaded media file. Upon expiration, the media file and its related resources (such as transcoding results and image sprites) will be permanently deleted.
				<ul><li>You can set this through the console or an API.</li></ul></li>
				</ul>
				Manual deletion:
				<li>You can delete files in the console.</li>
				<li>You can call an API to delete files.</li>
        </td>
	</tr>
</table>

## Use Cases
Media deletion is generally used to reduce the storage costs or remove non-compliant media.

<table>
    <tr>
        <th style="width:150px">
            Use Case              
        </th>
				<th>
           Description
        </th>
    </tr>
		 <tr>
        <td>
            Ecommerce platform
        </td>
				<td>
				After an item is removed, the images and videos of the item are also removed to reduce the storage costs.
        </td>
 </tr>
 <tr>
        <td>
           Video website
        </td>
				<td>
				Copyright-infringing and non-compliant media resources can be deleted. For old and unpopular videos, you can delete the source HD videos while retaining only the transcoded LD videos to reduce the costs.
        </td>
	</tr>
	<tr>
        <td>
            Game/Sports event recording
        </td>
				<td>
				Old game and sports media files that are confirmed to be no longer needed can be deleted.
        </td>
	</tr>
	<tr>
        <td>
            Enterprise event
        </td>
				<td>
				Photos taken and media resources generated during enterprise team building activities generally don't need to be retained permanently. You can set a validity period for enterprise employees to view, watch, and download them. You can specify an expiration time when uploading the media files to automatically delete them upon expiration.
        </td>
	</tr>
	<tr>
        <td>
            Burn-after-reading application
        </td>
				<td>
				In burn-after-reading applications, resources uploaded by end users will become unavailable after a certain period of time (such as 24 hours). For such applications, the media expiration time can be specified during upload, and VOD will automatically delete relevant media resources upon expiration.
        </td>
	</tr>
</table>

## Directions
For detailed directions on how to delete media files in the console, see:
- [Deleting Video](https://intl.cloud.tencent.com/document/product/266/33891).
- [Deleting Image](https://intl.cloud.tencent.com/document/product/266/37901).

For media deletion server APIs, see:
- [ApplyUpload](https://intl.cloud.tencent.com/document/product/266/34120). Enter the `ExpireTime` parameter to specify the expiration time of the uploaded file in VOD.
- [ModifyMediaInfo](https://intl.cloud.tencent.com/document/product/266/37570). Enter the `ExpireTime` parameter to modify the expiration time of the media file.
- [DeleteMedia](https://intl.cloud.tencent.com/document/product/266/37571).
