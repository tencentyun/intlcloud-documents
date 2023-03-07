Audio/Video content moderation is an offline task that intelligently moderates audio/video content with the aid of AI. The task execution results include confidence score, moderation suggestion, and suspected audio/video segments. According to the suggestion, you can decide whether to allow an audio/video to be published, effectively avoiding potential legal risks and damage to your brand’s reputation.

VOD can perform content moderation on images, text in images, speech, and sounds. Supported moderation labels include “porn”, “terror”, and “moan”.

<table>
    <tr>
        <th style="width:20%">
            Object
        </th>
        <th style="width:20%">
            Moderation Label
        </th>
        <th>
            Description
        </th>
    </tr>
    <tr>
        <td rowspan=3>
            Images
        </td>
    </tr>
    <tr>
        <td>
            Pornographic (`Porn`)
        </td>
        <td>
				    Pornographic and erotic content.
        </td>
    </tr>
    <tr>
        <td>
            Terrorist (`Terror`)
        </td>
        <td>
				    Violence, bloodiness, and terrorist content.
        </td>
    </tr>
		<tr>
        <td rowspan=1>
           Sounds
        </td>
        <td>
				    Moaning (`moan`)
        </td>
        <td>
            Sexually suggestive sounds.
        </td>
    </tr>
    <tr>
        <td rowspan=3>
            Speech in audio (ASR)
        </td>
        <tr>
        <td>
            Pornographic (`Porn`)
        </td>
        <td>
				    Pornographic and erotic content.
        </td>
    </tr>
    <tr>
        <td>
            Terrorist (`Terror`)
        </td>
        <td>
				    Violence, bloodiness, and terrorist content.
        </td>
    </tr>
        <td rowspan=3>
            Text in images (OCR)
        </td>
        <tr>
        <td>
            Pornographic (`Porn`)
        </td>
        <td>
				    Pornographic and erotic content.
        </td>
    </tr>
    <tr>
        <td>
            Terrorist (`Terror`)
        </td>
        <td>
				    Violence, bloodiness, and terrorist content.
        </td>
    </tr>
</table>

The table below lists some of the fields in moderation results:

| Field | Type | Description |
| ---------- | ------ | ------------------------------------------------------------ |
| Confidence | Float | The confidence score (0–100). The higher the score, the greater the suspicion. |
| Suggestion | String | There are three types of moderation suggestions: <ul><li>`pass`: There is not a high suspicion of inappropriate content, and it is recommended to allow the content to pass.</li><li>`review`: There is a high suspicion of inappropriate content, and manual review is recommended.</li><li>`block`: There is a very high suspicion of inappropriate content, and blocking is recommended.</li></ul> |
| Form   | String  | The format of the content moderated. Valid values: <ul><li>`Image`</li><li>`Voice`</li><li>`OCR`</li><li>`ASR`</li></ul> |
| Label   | String  | The moderation label. Valid values:<ul><li>`Porn`</li><li>`Terror`</li><li>`Moan`</li></ul> |

## [](id:sh)Audio/Video Moderation Template

An audio/video moderation template represents a set of moderation parameters. You can use a template to specify which of the following moderation labels to use:
- Porn
- Terror
- Moan

VOD provides [preset audio/video moderation templates](https://intl.cloud.tencent.com/document/product/266/33932) for common parameter combinations. You can also use a [server API](https://www.tencentcloud.com/document/product/266/37566) to create and manage custom templates.

## Initiating a Task

You can initiate an audio/video moderation task by calling a server API, via the console, or by specifying the task when uploading videos. For details, see [Task Initiation](https://intl.cloud.tencent.com/document/product/266/33931).

You can initiate an audio/video moderation task in these ways:

* Call the server-side API [ReviewAudioVideo](https://www.tencentcloud.com/document/product/266/50634).
* Initiate a task in the console. For detailed directions, see [Audio/Video Moderation](https://intl.cloud.tencent.com/document/product/266/33897).
* Call the server-side API [CreateProcedureTemplate](https://www.tencentcloud.com/document/product/266/34167) to create a task flow with audio/video moderation enabled (`ReviewAudioVideoTask`) and, when calling [ApplyUpload](https://www.tencentcloud.com/document/product/266/34120#2.-.E8.BE.93.E5.85.A5.E5.8F.82.E6.95.B0) to upload a video, set `procedure` to the name of the task flow created.
* Call the server-side API [CreateProcedureTemplate](https://www.tencentcloud.com/document/product/266/34167) to create a task flow with audio/video moderation enabled (`ReviewAudioVideoTask`) and, in the [signature for upload from client](https://intl.cloud.tencent.com/document/product/266/33922), set `procedure` to the name of the task flow created.
* Call the server-side API [CreateProcedureTemplate](https://www.tencentcloud.com/document/product/266/34167) to create a task flow with audio/video moderation enabled (`ReviewAudioVideoTask`) and, when uploading videos via the console, select [Auto-processing after upload](https://intl.cloud.tencent.com/document/product/266/33890) and select the task flow created.

## Getting the Result

After initiating a moderation task, you can either wait for the [ReviewAudioVideoComplete](https://www.tencentcloud.com/document/product/266/50677) notification asynchronously or perform a [task query](https://intl.cloud.tencent.com/document/product/266/33931) synchronously to get the task execution result. Below is an example of the notification in normal callback mode (the fields with null value are omitted):
```json
{
    "EventType": "ReviewAudioVideoComplete",
    "ReviewAudioVideoCompleteEvent": {
        "TaskId": "125xxxx-ReviewAudioVideo-07edbc78ba20563cdf2362cffbf4aa0ct",
        "Status": "FINISH",
        "ErrCodeExt": "",
        "Message": "SUCCESS",
        "Input":{
            "FileId": "387702130626135215"
        },
        "Output": {
            "Suggestion": "block",
            "Label": "Porn",
            "Form": "Image",
            "SegmentSet": [
                {
                    "StartTimeOffset": 0,
                    "EndTimeOffset": 1,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "SexyBehavior",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": [],
                    "Url": "https://251000800.vod2.myqcloud.com/1a168d62vodcq251000800/result/vod/w-video-Y7uETQ0Oqj4SY3Fh/screenshot_0_1638163480.jpg",
                    "PicUrlExpireTime": "2023-01-16T03:06:16.039Z"
                },
                {
                    "StartTimeOffset": 1,
                    "EndTimeOffset": 2,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "SexyBehavior",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": [],
                    "Url": "https://251000800.vod2.myqcloud.com/1a168d62vodcq251000800/result/vod/w-video-Y7uETQ0Oqj4SY3Fh/screenshot_0_1638163481.jpg",
                    "PicUrlExpireTime": "2023-01-16T03:06:17.039Z"
                },
                {
                    "StartTimeOffset": 2,
                    "EndTimeOffset": 3,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "SexyBehavior",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": [],
                    "Url": "https://251000800.vod2.myqcloud.com/1a168d62vodcq251000800/result/vod/w-video-Y7uETQ0Oqj4SY3Fh/screenshot_0_1638163482.jpg",
                    "PicUrlExpireTime": "2023-01-16T03:06:18.039Z"
                },
                {
                    "StartTimeOffset": 3,
                    "EndTimeOffset": 4,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "SexyBehavior",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": [],
                    "Url": "https://251000800.vod2.myqcloud.com/1a168d62vodcq251000800/result/vod/w-video-Y7uETQ0Oqj4SY3Fh/screenshot_0_1638163483.jpg",
                    "PicUrlExpireTime": "2023-01-16T03:06:19.039Z"
                },
                {
                    "StartTimeOffset": 4,
                    "EndTimeOffset": 5,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "SexyBehavior",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": [],
                    "Url": "https://251000800.vod2.myqcloud.com/1a168d62vodcq251000800/result/vod/w-video-Y7uETQ0Oqj4SY3Fh/screenshot_0_1638163484.jpg",
                    "PicUrlExpireTime": "2023-01-16T03:06:20.039Z"
                },
                {
                    "StartTimeOffset": 5,
                    "EndTimeOffset": 6,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "SexyBehavior",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": [],
                    "Url": "https://251000800.vod2.myqcloud.com/1a168d62vodcq251000800/result/vod/w-video-Y7uETQ0Oqj4SY3Fh/screenshot_0_1638163485.jpg",
                    "PicUrlExpireTime": "2023-01-16T03:06:21.039Z"
                },
                {
                    "StartTimeOffset": 6,
                    "EndTimeOffset": 7,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "SexyBehavior",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": [],
                    "Url": "https://251000800.vod2.myqcloud.com/1a168d62vodcq251000800/result/vod/w-video-Y7uETQ0Oqj4SY3Fh/screenshot_0_1638163486.jpg",
                    "PicUrlExpireTime": "2023-01-16T03:06:22.039Z"
                },
                {
                    "StartTimeOffset": 7,
                    "EndTimeOffset": 8,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "SexyBehavior",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": [],
                    "Url": "https://251000800.vod2.myqcloud.com/1a168d62vodcq251000800/result/vod/w-video-Y7uETQ0Oqj4SY3Fh/screenshot_0_1638163487.jpg",
                    "PicUrlExpireTime": "2023-01-16T03:06:23.039Z"
                },
                {
                    "StartTimeOffset": 8,
                    "EndTimeOffset": 9,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "SexyBehavior",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": [],
                    "Url": "https://251000800.vod2.myqcloud.com/1a168d62vodcq251000800/result/vod/w-video-Y7uETQ0Oqj4SY3Fh/screenshot_0_1638163488.jpg",
                    "PicUrlExpireTime": "2023-01-16T03:06:24.039Z"
                },
                {
                    "StartTimeOffset": 9,
                    "EndTimeOffset": 10,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "SexyBehavior",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": [],
                    "Url": "https://251000800.vod2.myqcloud.com/1a168d62vodcq251000800/result/vod/w-video-Y7uETQ0Oqj4SY3Fh/screenshot_0_1638163489.jpg",
                    "PicUrlExpireTime": "2023-01-16T03:06:25.039Z"
                }
            ],
            "SegmentSetFileUrl": "http://251000800.vod2.myqcloud.com/a8800b40vodtranssgp251000800/0f9bd2b0-34a8-4642-f481-001894d93019.txt",
            "SegmentSetFileUrlExpireTime": "2022-10-12T07:01:07.695Z"
        },
        "SessionContext": "",
        "SessionId": ""
    }
}
```

In the above callback, `ReviewAudioVideoCompleteEvent.Output` is the audio/video moderation result; `Output.Suggestion=block` indicates that VOD suggests you block the content; `Output.Label=Porn` and `Output.Form=Image` indicate that the mostly likely violation is pornographic content in images.

An audio/video clip may include multiple suspicious segments. `Output.SegmentSet` lists only the first 10. You can view the information of all suspicious segments by visiting `Output.SegmentSetFileUrl` within the validity period.

`StartTimeOffset` and `EndTimeOffset` are the start and end time of a suspicious segment, and `SubLabel` indicate the type of violation.

If text in images or speech is moderated:
* `Text` is the full text recognized.
* `KeywordSet` is the list of keywords hit.

If images (people and objects) or text in images are moderated:
* `AreaCoordSet` is the coordinates of the suspicious object.
* `Url` is the URL of the suspicious image.
* `PicUrlExpireTime` is the expiration time of `Url`.
