## Overview
The smart media asset cold storage feature of VOD is based on custom cold storage policies. It automatically transitions cold files to a storage class at lower costs based on the file creation time, file type, and access frequency. VOD has the following storage classes: STANDARD, STANDARD_IA, ARCHIVE, and DEEP ARCHIVE. Below is the comparison of the costs and access performance of the storage classes:

<table>
    <tr>
        <th style="width:150px">
            Metric              
        </th>
				<th>
           Ranking (highest to lowest)
        </th>
    </tr>
		 <tr>
        <td>
            Storage cost
        </td>
				<td>
				STANDARD > STANDARD_IA > ARCHIVE > DEEP_ARCHIVE
        </td>
		</tr>
		<tr>
        <td>
            Access performance
        </td>
				<td>
				STANDARD > STANDARD_IA. ARCHIVE and DEEP_ARCHIVE storage classes don't support direct access. You need to <a href="https://intl.cloud.tencent.com/document/product/266/43051#.E6.95.B0.E6.8D.AE.E5.8F.96.E5.9B.9E.E5.8F.8A.E5.8F.96.E5.9B.9E.E6.A8.A1.E5.BC.8F.3Ca-id.3D.22retake.22.3E.3C.2Fa.3E" title="retrieve the data" target="_blank">retrieve the data</a> first before you can access it.
        </td>
		</tr>
</table>

You can change the storage class of VOD files from STANDARD to STANDARD_IA, ARCHIVE, or DEEP_ARCHIVE according to certain <a href="https://intl.cloud.tencent.com/document/product/266/43051#.E7.AD.96.E7.95.A5.E7.AE.A1.E7.90.86.3Ca-id.3D.22strategy.22.3E.3C.2Fa.3E" title="cold storage policies">cold storage policies</a> based on your business characteristics so as to effectively reduce your storage costs.

### Smart cold storage policy
VOD supports flexible smart cold storage polices and various cold storage dimensions, including creation time, file category, and playback count.

<table>
    <tr>
        <th style="width:150px">
            Dimension              
        </th>
				<th>
           Description
        </th>
    </tr>
		 <tr>
        <td>
            File creation time
        </td>
				<td>
				You can specify the upload time and storage time.
				<ul>
					<li>Specify the upload time: You can configure a cold storage policy by specifying a time point or time period.
						<ul>
						<li>Specify the time period: If no start time point is specified, the oldest stored video file will be transitioned to the cold storage class by default. If no end time point is specified, all video files after the start time point will be transitioned. If neither is specified, all video files in VOD will be transitioned. </li>
							</ul>
					</li>
					<li>Specify the storage time: A media asset will be automatically transitioned to the cold storage class after the entered time elapses.</li>
				</ul>
        </td>
		</tr>
		<tr>
        <td>
            File category
        </td>
				<td>
				Cold storage by category ID is supported. You can set multiple category IDs/names.
        </td>
		</tr>
		<tr>
        <td>
            File source
        </td>
				<td>
				Cold storage is supported for different media sources. You can set multiple media sources.
        </td>
		</tr>
		<tr>
        <td>
            Playback count
        </td>
				<td>
				The cold storage policy depends on the number of times a video is played by during a specified period of time. A cold storage policy supports only one access policy.
        </td>
		</tr>
		<tr>
        <td>
            Media type
        </td>
				<td>
				Whether to perform the cold storage logic will be determined based on the media type. A cold storage policy supports only one media type.
        </td>
		</tr>
</table>

In addition to configuring cold storage policies, VOD also allows you to manually transition multiple files at a time. You can do this directly in the console as instructed in [Cold Storage](https://intl.cloud.tencent.com/document/product/266/42092) or by calling the [ModifyMediaStorageClass](https://intl.cloud.tencent.com/document/product/266/46008) API.

## Use Cases
<table>
    <tr>
        <th style="width:160px">
            Use Case              
        </th>
				<th>
           Description
        </th>
    </tr>
		 <tr>
        <td>
            Ecommerce live streaming
        </td>
				<td>
				As required by <a href="https://gkml.samr.gov.cn/nsjg/fgs/202103/t20210315_326936.html" title="Measures for the Supervision and Administration of Online Trading" target="_blank">Measures for the Supervision and Administration of Online Trading</a> issued by the State Administration for Market Regulation of China, live streaming service providers must retain live videos of online transactions for at least three years after the live streaming ends. Such videos are generally stored in VOD in STANDARD storage class, some of which will seldom or never be played back and are only used for review by applicable authorities. The smart cold storage feature can effectively help you reduce the storage costs of these media assets.
        </td>
		</tr>
		<tr>
        <td>
            Cold storage of infrequently accessed media
        </td>
				<td>
				For video portals, streaming media platforms, and UGC management platforms, media assets that are infrequently accessed or watched by users cannot be directly removed from the platform for various reasons and often incur unnecessarily high storage costs. The smart cold storage feature of VOD can store media files in a cold storage class according to their access frequency, which effectively reduces the storage costs of media assets while still allowing infrequent views.
        </td>
		</tr>
		<tr>
        <td>
            Media asset archive
        </td>
				<td>
				In the news, media, radio, and TV industries, some media files are only relevant for a short period of time but are generally archived for long periods of time so they can be available for occasional playback in the future. Such playback usually does not have high requirements for time to first frame. You can save these assets in ARCHIVE or DEEP_ARCHIVE storage of VOD to reduce storage costs.
        </td>
		</tr>
</table>

## Directions
Refer to:
- [Smart Cold Storage of VOD Media Asset Files](https://intl.cloud.tencent.com/document/product/266/43051)
- [Cold Storage](https://intl.cloud.tencent.com/document/product/266/42092)
- [ModifyMediaStorageClass](https://intl.cloud.tencent.com/document/product/266/46008) (server API)
- [RestoreMedia](https://intl.cloud.tencent.com/document/product/266/48378) (server API). This API can be used to generate a media file that can be accessed temporarily for files stored in ARCHIVE or DEEP ARCHIVE storage class.
