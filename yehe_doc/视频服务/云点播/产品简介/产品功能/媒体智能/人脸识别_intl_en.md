## Overview
Based on Tencent's industry-leading AI technology, face recognition helps you quickly recognize faces in a video, including the frames a person appears in and the coordinates of the areas of the face. You can directly use VOD’s public person libraries or use and manage your own custom person libraries. The public person libraries contain celebrities in various fields, such as movies, music, sports, and academics.
## Use cases
Face recognition in media content has been widely used for video creation, media search, and generation of personalized recommendations.

<table>
    <tr>
        <th style="width:150px">
            Scenario               
        </th>
				<th>
           Description
        </th>
    </tr>
 <tr>
        <td>
            Video creation
        </td>
				<td>
            With the face recognition feature, users can find quickly find the time points, <br/>image areas, and duration at which a target person's face appears throughout a large number of historical videos. This makes finding relevant materials and creating content much more efficient.
        </td>
 </tr>
 <tr>
        <td>
            Event replays and highlights
        </td>
				<td>
				You can add timestamps for when a certain player appears during a sports and esports event, so users can quickly locate the relevant time points. You can also find the time points and capture the video frames in which a certain celebrity appears in a video, so as to make it easier to create a highlight reel or generate an animated image as the thumbnail to attract more viewers.
        </td>
 </tr>
  <tr>
        <td>
            Video websites
        </td>
				<td>
            Users can search for relevant videos by the name of a person. The website can also automatically recommend relevant videos based on the list of persons followed by the user.
        </td>
 </tr>
</table>



## Directions
You can implement face recognition through the **face recognition** feature as described in [Video Content Recognition](https://intl.cloud.tencent.com/document/product/266/33946) as follows:
1. Prepare an [audio/video content recognition template](https://intl.cloud.tencent.com/document/product/266/33946#.E9.9F.B3.E8.A7.86.E9.A2.91.E5.86.85.E5.AE.B9.E8.AF.86.E5.88.AB.E6.A8.A1.E6.9D.BF).
You can directly use a [preset audio/video content recognition template](https://intl.cloud.tencent.com/document/product/266/33932) to recognize the people in all the public person libraries.
You can also specify certain labels of public and custom person libraries to recognize certain types of people by using the face recognition configuration item (`FaceConfigure`) of the API for creating an audio/video content recognition template. For example, the following code sample indicates to recognize only sports celebrities in the public person libraries:
```
{
	"FaceConfigure": {
		"Switch": "ON",
		"DefaultLibraryLabelSet": ["sport"]
	}
}
```
Get the template ID from the response.
\* Custom person libraries are managed through the **material sample creation/modification/deletion/acquisition** APIs as described in [API Category](https://intl.cloud.tencent.com/document/product/266/34110).

2. Initiate a face recognition task with the template ID obtained in step 1 as instructed in [Video Content Recognition](https://intl.cloud.tencent.com/document/product/266/33946#.E4.BB.BB.E5.8A.A1.E5.8F.91.E8.B5.B7).
3. Get the task result as instructed in [Video Content Recognition](https://intl.cloud.tencent.com/document/product/266/33946#.E7.BB.93.E6.9E.9C.E8.8E.B7.E5.8F.96).
