## Overview

VOD allows you to set a rich variety of attributes for media files, including media name, description, category, tag, thumbnail, timestamp information, subtitle information, expiration time, storage class, and block status.
* The media name, description, category, and tags add additional information to media files to help you manage them more efficiently.
* Media thumbnails, timestamps, and subtitle information can be displayed during media playback to improve the viewing experience.
* Expiration time and block status enable you to automatically delete files and block non-compliant media files more easily.


<table>
    <tr>
        <th style="width:100px">
            Media Attribute              
        </th>
				<th>
           Description
        </th>
    </tr>
		<tr>
        <td>
            Media name
        </td>
				<td>
				The media name can be the title of a movie or TV series episode (e.g., Empresses in the Palace episode 6), course title (e.g., lesson 1 of grade 12 math), product video name (e.g, Coca-Cola new package in 2022). Its use cases include:
				<li>Playlist: The media name is displayed in a user's playlist.</li>
				<li>Media search: A user can enter a media name for prefix match or fuzzy search.</li>
        </td>
		</tr>
		<tr>
        <td>
            Media description
        </td>
				<td>
				The description of the media file. Its use cases include:
				<li>Media search: A user can fuzzy search for a media file by its description.</li>
        </td>
		</tr>
		<tr>
        <td>
            Media category
        </td>
				<td>
				The category of the media file, such as movie, TV series, or variety show. Its use cases include:
				<li>Media search: A user can search for files based on the specified category.</li>
				<li>Smart cold storage: Files in the specified category can be transitioned to a colder storage class.</li>
        </td>
		</tr>
		<tr>
        <td>
            Media tag
        </td>
				<td>
				The tag of the media file, such as ACG, action, or imperial drama. Its use cases include:
				<li>Media search: A user can search for files with the specified tag.</li>
        </td>
		</tr>
		<tr>
        <td>
            Media thumbnail
        </td>
				<td>
				The thumbnail URL of the media file. Its use cases include:
				<li>Media asset console: Thumbnails can be displayed in the media file list.</li>
        </td>
		</tr>
		<tr>
        <td>
            Timestamp
        </td>
				<td>
				Media timestamps are a set of playback time points and the content (including text, images, and links) displayed at those points. When you hover over a timestamp on the progress bar, the content at that time point will be displayed. Use cases for timestamps include:
				<li>Highlights: Viewers can go directly to the important time points in a movie or the goals in a sports match, allowing them to save time during playback.</li>
				<li>Ad: When a viewer drags the progress bar to a timestamp, the relevant ad information will be displayed.</li>
        </td>
		</tr>
		<tr>
        <td>
            Subtitles information
        </td>
				<td>
				The subtitle information of the media file. It is used to display subtitles during media playback.
        </td>
		</tr>
		<tr>
        <td>
            Expiration time
        </td>
				<td>
				The expiration time of the media file. Once expired, the file will be automatically deleted by VOD.
        </td>
		</tr>
		<tr>
        <td>
            Storage class
        </td>
				<td>
				The storage class of the media file. VOD offers the following storage classes (in descending order by storage fees and file read speed): STANDARD, STANDARD_IA, ARCHIVE, and DEEP ARCHIVE. You can select an appropriate storage class based on your needs to help control your media storage costs.
        </td>
		</tr>
		<tr>
        <td>
            Block status
        </td>
				<td>
				The block status of the media file. You can block non-compliant media content to prevent it from being further spread.
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
				Online education platforms can manage teaching videos by assigning categories and tags based on the subject content, so that students can quickly find the videos they want. The platform can also recommend relevant videos based on the category and tag information.
        </td>
		</tr>
		<tr>
        <td>
            Video portal
        </td>
				<td>
				Users can specify multiple query conditions, such as category, tag, and video name, to quickly find the video they want among massive numbers of media resources. VOD files can also be associated with multilingual subtitles, so viewers who speak different languages can select the appropriate subtitles, and media content can be enjoyed and shared by users across the world. 
        </td>
		</tr>
		<tr>
        <td>
            Live streaming platform
        </td>
				<td>
				To meet regulatory and moderation requirements, live videos need to be recorded and retained for a certain period of time and can be deleted upon expiration. For those live videos, you can set an expiration time, and VOD will automatically delete them upon expiration to reduce storage costs.
        </td>
		</tr>
		<tr>
        <td>
            UGSV on social media platforms
        </td>
				<td>
				Video communities can set multiple channels by scenario and manage scenarios by category and tag. Timestamps can be set for popular content to display the item purchase links. Non-compliant UGSVs can be blocked to stop them from being further spread.
        </td>
		</tr>
</table>


## Directions
Relevant console guides:
- [Quick Edit](https://intl.cloud.tencent.com/document/product/266/33893)
- [Filtering Video](https://intl.cloud.tencent.com/document/product/266/33894)
- [Managing Video](https://intl.cloud.tencent.com/document/product/266/33896)
- [Associating Subtitles](https://intl.cloud.tencent.com/document/product/266/47180)
- [Modifying Image Category](https://intl.cloud.tencent.com/document/product/266/37902)
- [Managing Image](https://intl.cloud.tencent.com/document/product/266/37903)

Relevant server APIs:
- [ModifyMediaInfo](https://intl.cloud.tencent.com/document/product/266/37570)
- [SearchMedia](https://intl.cloud.tencent.com/document/product/266/34179)
- [DescribeMediaInfos](https://intl.cloud.tencent.com/document/product/266/34181)
- [ForbidMediaDistribution](https://intl.cloud.tencent.com/document/product/266/34180)
