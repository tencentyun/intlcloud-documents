## Overview
The labeling and categorization feature performs structured analysis on various dimensions, including people, behavior, speech, text, objects, and scenes in audios/videos to generate high-accuracy audio/video labels, frame-specific labels, and audio/video categories automatically.
<table>
    <tr>
        <th style="width:130px">
            Feature               
        </th>
				<th>
           Description
        </th>
    </tr>
 <tr>
        <td>
            Audio/Video labeling
        </td>
				<td>
            Audio/Video labeling gives suggestions on the labels that can be added to an audio/video. Currently, it supports over 3,000 labels such as game, vehicle, musician, race car, pet, drum, bike, World of Warcraft, computer, and school, and it supports categories like people, event, scene, objects, landscape, food, animals.
        </td>
 </tr>
 <tr>
        <td>
            Frame-specific labeling
        </td>
				<td>
            Frame-specific labeling automatically recognizes labels in the video frames captured at the custom frame capturing interval, and locates the labels in the video. Frame labels are divided into nine categories, such as people, landscape, artificial object, building, plant, animal, and food, covering various aspects of daily life.
        </td>
 </tr>
 <tr>
        <td>
            Audio/Video categorization
        </td>
				<td>
            Audio/Video categorization gives suggestions for which category an audio/video should belong to. There are currently over twenty categories, such as car, parenting, fashion and entertainment, game, military, technology, politics, animal, food, sports, travel, animation, dance, music, television, variety show, host, political news, international news, and social news.
        </td>
 </tr>
</table>
The labeling and categorization feature helps you efficiently manage media resources and can be used to give personalized audio/video recommendations.

## Use cases
<table>
    <tr>
        <th style="width:130px">
            Scenario               
        </th>
				<th>
           Description
        </th>
    </tr>
 <tr>
        <td>
            Media resource management
        </td>
				<td>
            Users can search for media resources on audio/video platforms by category and label, greatly improving the search efficiency.
        </td>
 </tr>
  <tr>
        <td>
            Audio/Video creation
        </td>
				<td>
           Audio/Video creators can quickly search for materials by category or by label, helping them create content more efficiently.
        </td>
 </tr>
 <tr>
        <td>
            Personalized audio/video recommendations
        </td>
				<td>
            Businesses such as UGSV platforms, ecommerce platforms, and social media applications can push media content that precisely matches users' needs. This not only helps increase the clicks of the media content on platforms but also helps users save time when filtering content.
        </td>
 </tr>
 <tr>
        <td>
            Radio and TV cataloging
        </td>
				<td>
            The radio and TV industry can use the labeling and categorization feature of VOD to efficiently manage massive amounts of video content. Based on the recognized label and category information, videos can be quickly archived, labeled, and searched for.
        </td>
 </tr>
</table>

## Directions
You can implement audio/video labeling, frame-specific labeling, and audio/video categorization through the **intelligent labeling**, **intelligent labeling by frame**, and **intelligent categorization** features as described in [Video Content Analysis](https://intl.cloud.tencent.com/document/product/266/33945) as follows:
1. [Create an audio/video content analysis template](https://intl.cloud.tencent.com/document/product/266/34170) and configure intelligent labeling (`TagConfigure`), intelligent labeling by frame (`FrameTagConfigure`), and intelligent categorization (`ClassificationConfigure`) as needed. For example, the following API requests indicate to enable all labeling and categorization features and set the interval for frame-specific labeling to three seconds:
```
{
	"TagConfigure": {
		"Switch": "ON"
	},
	"FrameTagConfigure": {
		"Switch": "ON",
		"ScreenshotInterval": 3
	},
	"ClassificationConfigure": {
		"Switch": "ON"
	}
}
```
Get the template ID from the response.
To use all labeling and categorization features, you can directly use template ID 20 in [List of Preset Parameter Templates](https://intl.cloud.tencent.com/document/product/266/33932).
2. Initiate a labeling and categorization task with the template ID obtained in step 1 as instructed in [Video Content Analysis](https://intl.cloud.tencent.com/document/product/266/33945#.E4.BB.BB.E5.8A.A1.E5.8F.91.E8.B5.B7).
3. Get the task result as instructed in [Video Content Analysis](https://intl.cloud.tencent.com/document/product/266/33945#.E7.BB.93.E6.9E.9C.E8.8E.B7.E5.8F.96).
