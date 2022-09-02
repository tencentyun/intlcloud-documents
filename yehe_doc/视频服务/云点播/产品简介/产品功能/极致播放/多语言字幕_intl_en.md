## Overview
VOD’s multilingual subtitling feature allows you to associate/unassociate standard multilingual subtitle files with an output file of adaptive bitrate streaming. During playback, users can switch between subtitles in different languages. This feature helps increase cross-border viewer rates, and allows more viewers in target regions to understand and enjoy video content.
Multilingual subtitle sets support various languages, including English, Simplified Chinese, Traditional Chinese, French, German, Spanish, Portuguese, Russian, Japanese, Korean, Thai, Vietnamese, and Indonesian. For all the supported languages and their corresponding code, see [RFC 5646](https://datatracker.ietf.org/doc/html/rfc5646).

## Use cases
<table>
    <tr>
        <th>
            Scenario              
        </th>
				<th>
           Description
        </th>
    </tr>
		<tr>
        <td>
            International enterprise meetings
        </td>
				<td>
				International enterprises often hold internal meetings that involve attendees speaking different languages. You can add multilingual subtitles to recorded meetings so that employees in different countries or regions can watch and share the videos with coworkers.
        </td>
		</tr>
		<tr>
        <td>
            International conference/sporting events
        </td>
				<td>
				For recordings of international video conferences and world-wide esports and sporting events, multilingual subtitles can be added to allow viewers from different countries and regions to understand what is said by speakers and sports announcers. 
        </td>
		</tr>
		<tr>
        <td>
            Video websites
        </td>
				<td>
				Multiple languages can be added to foreign movies/TV series so that viewers of different languages can watch their favorite shows and share with their friends.
        </td>
		</tr>
		<tr>
        <td>
            Online education platforms
        </td>
				<td>
				If the teaching content involves a foreign language, such as a foreign language course, or involves communication with foreign experts and scholars, multilingual subtitles can be added to help viewers learn and understand the video content.
        </td>
		</tr>
		<tr>
        <td>
            Cross-border ecommerce platforms
        </td>
				<td>
				Multilingual subtitles can be added to product presentation videos so that shoppers from different countries/regions can become more familiar with the products the want to buy.
        </td>
		</tr>
		<tr>
        <td>
            Network ads
        </td>
				<td>
				Network ads can be shown with multilingual subtitles, so that ads can be delivered to users from different countries/regions around the world.
        </td>
		</tr>
</table>

## Directions
Multilingual subtitling support the HLS format for output adaptive bitstreams. Before using this feature, you need to add a subtitle set to the media file and call the [ModifyMediaInfo](https://intl.cloud.tencent.com/document/product/266/37570) API to add a subtitle set (enter the `AddSubtitles.N` parameter) or delete a subtitle set (enter the `DeleteSubtitleIds.N` parameter). The list of new subtitle sets (`AddedSubtitleSet`, which contains the ID of each subtitle set) will be returned by the API.

After a subtitle set is added to a media file, you can associate/unassociate the subtitle set with the output file of adaptive bitrate streaming by calling the [AttachMediaSubtitles](https://intl.cloud.tencent.com/document/product/266/40004) API. You can also initiate an [adaptive bitrate streaming](https://intl.cloud.tencent.com/document/product/266/33942) task again. Note that you need to specify the subtitle set ID list in the input parameter of the adaptive bitrate streaming task ([MediaProcessTask](https://intl.cloud.tencent.com/document/product/266/34187#MediaProcessTaskInput) > [AdaptiveDynamicStreamingTaskSet](https://intl.cloud.tencent.com/document/product/266/34187#AdaptiveDynamicStreamingTaskInput) > `SubtitleSet`).
