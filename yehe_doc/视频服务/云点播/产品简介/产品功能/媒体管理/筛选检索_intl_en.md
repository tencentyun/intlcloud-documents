## Overview
VOD allows you to use media attributes as search criteria for exact, prefix, and fuzzy match to get the list of target media files.
The list of found files can be exported as local files (currently, files can be exported in CSV and JSON Lines formats).
You can use multiple filter fields for combined search. The supported fields can be divided into the following media attribute categories:

<table>
    <tr>
        <th style="width:100px">
            Media Attribute Category             
        </th>
				<th>
           Description
        </th>
    </tr>
		<tr>
        <td>
            Basic attributes
        </td>
				<td>
				Mainly includes:
				<li>`FileId`: The unique ID of the VOD media file.</li>
				<li>Media source: The source of the media file, such as recording, upload, and video processing.</li>
				<li>Media upload time: The upload time of the media.</li>
				<li>Stream ID: The stream ID if the media source is **Record**.</li>
        </td>
		</tr>
		<tr>
        <td>
            Custom attribute
        </td>
				<td>
				Mainly includes:
				<li>Media name: The name of the media file.</li>
				<li>Media description: The description of the media file.</li>
				<li>Media category: The category of the media file.</li>
				<li>Media tag: The tag of the media file.</li>
				<li>Expiration time: The expiration time of the media file. Once the file expires, it will be deleted automatically.</li>
				<li>Storage class: The storage class of the media file, such as STANDARD, STANDARD_IA, ARCHIVE, and DEEP ARCHIVE.</li>
        </td>
		</tr>
</table>


## Use Cases
<table>
    <tr>
        <th style="width:100px">
            Use Case              
        </th>
				<th>
           Description
        </th>
    </tr>
		<tr>
        <td>
            Online education
        </td>
				<td>
				A student can directly enter any information such as the subject name, chapter title, and description into the search box and can combine other multidimensional information such as the video category and tag to quickly find teaching videos that match the search criteria.
        </td>
		</tr>
		<tr>
        <td>
            Video portal
        </td>
				<td>
				An operator can use various search criteria, including video category, tag, and storage class, to find a list of target media files so he or she can remove files, change the file category, modify tags, or adjust the storage class. An end user can search for videos by search criteria like video title keyword, category, and tag.
        </td>
		</tr>
		<tr>
        <td>
            Live streaming platform
        </td>
				<td>
				An operator can search for VOD recording files by stream ID. For example, if a live stream is interrupted, multiple VOD files may be generated for the same stream ID, and searching by stream ID makes it easier for the operator to find and splice the files together.
        </td>
		</tr>
		<tr>
        <td>
            UGSV on social media platforms
        </td>
				<td>
				End users can use a keyword like “street dance” or “concert” to fuzzy search a list of videos.
        </td>
		</tr>
</table>

## Directions
Relevant console guides:
- [Filtering Video](https://intl.cloud.tencent.com/document/product/266/33894)
- [Exporting Videos](https://intl.cloud.tencent.com/document/product/266/38534)
- [Managing Image](https://intl.cloud.tencent.com/document/product/266/37903)

Relevant server APIs:
- [SearchMedia](https://intl.cloud.tencent.com/document/product/266/34179)
