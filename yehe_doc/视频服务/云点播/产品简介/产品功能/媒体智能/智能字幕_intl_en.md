## Overview
Smart subtitling can help users automatically generate a subtitle set file for the audio in a media file. This feature is useful for online course recordings, audio/video meeting minutes, and speech quality assurance. Based on advanced speech recognition algorithms and massive amounts of training data, VOD’s smart subtitling feature utilizes industry-leading speech recognition capabilities to offer high recognition accuracy, even under various interferences such as ambient and background noise.

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
            Online classes
        </td>
				<td>
            Smart subtitling can automatically generate subtitles for online course recordings to make it easier for viewers to learn the content of the course.
        </td>
 </tr>
 <tr>
        <td>
            Social media platforms
        </td>
				<td>
            General users can add subtitles to their vlogs and share them with others.
        </td>
 </tr>
 <tr>
        <td>
            Movie/TV series
        </td>
				<td>
            Older videos such as movies and TV series often lack subtitles, which makes it difficult for some viewers to enjoy them. You can use smart subtitling to generate subtitles automatically, which greatly improves efficiency compared with the long process of manual subtitling.
        </td>
 </tr>
 <tr>
        <td>
            Audio/Video meetings
        </td>
				<td>
            Subtitles can be automatically generated for recordings of key meetings to help generate meeting minutes. In addition, the added subtitles make it easier for viewers to play through meetings more quickly.
        </td>
 </tr>
 <tr>
        <td>
            Speech quality control
        </td>
				<td>
            Subtitles can be generated for speech in recorded call files, which helps you evaluate the quality of customer service calls more quickly and improves the efficiency of speech quality control.
        </td>
 </tr>
</table>


## Directions
You can implement smart subtitling through the **full speech-to-text recognition** feature as described in [Video Content Recognition](https://intl.cloud.tencent.com/document/product/266/33946) as follows:
1. [Create an audio/video content recognition template](https://intl.cloud.tencent.com/document/product/266/37568), enable **full speech-to-text recognition** (`AsrFullTextConfigure`), and specify to generate a subtitle set:
```
{
	"AsrFullTextConfigure": {
		"Switch": "ON",
                "SubtitleFormats": ["vtt", "srt"]
	}
}
```
Get the template ID from the response.
2. With the template ID obtained in step 1, initiate a smart subtitling task as instructed in [Video Content Recognition](https://intl.cloud.tencent.com/document/product/266/33946#.E4.BB.BB.E5.8A.A1.E5.8F.91.E8.B5.B7).
3. Get the task result as instructed in [Video Content Recognition](https://intl.cloud.tencent.com/document/product/266/33946#.E7.BB.93.E6.9E.9C.E8.8E.B7.E5.8F.96).
