Video composing is an offline task that performs a series of complicated operations on a video in VOD such as clipping, splicing, overlaying, and flipping. It can achieve the following effects:

* **Rotation**: rotates videos or images by certain degrees or in a certain direction.
* **Audio control**: turns up/down volume in videos/audios or mutes videos.
* **Overlaying**: overlays videos/images in sequence to achieve effects such as picture-in-picture.
* **Audio mixing**: mixes the sound in videos/audios.
* **Audio extraction**: extracts sound from videos (without retaining the image).
* **Clipping**: clips segments within the specified period of time out of videos/audios.
* **Splicing**: splices videos/audios/images in chronological order.
* **Transition**: adds transition effects between segments during video or image splicing.

The container format of the media file after composing is MP4 (video) or MP3 (audio).

## Task Initiation

You can initiate a video composing task by calling a [server API](#https://intl.cloud.tencent.com/document/product/266/35286). The return result of the API contains the task ID, which is used to associate with the corresponding task result when [getting result](#.E7.BB.93.E6.9E.9C.E8.8E.B7.E5.8F.96).

## Getting Result

After initiating a composing task, you can wait for [result notification](https://intl.cloud.tencent.com/document/product/266/33931#ResultNotification) asynchronously or perform [task query](https://intl.cloud.tencent.com/document/product/266/33931#TaskQuery) synchronously to get the task execution result. Below is an example of getting the result notification in normal callback mode after the video composing task is initiated (the fields with null value are omitted):

```json
{
	"EventType": "ComposeMediaComplete",
	"ComposeMediaCompleteEvent": {
		"TaskId": "ComposeMedia-f5ac8127b3b6b85cdc13f237c6005d8",
		"Status": "FINISH",
		"ErrCode": 0,
		"Message": "SUCCESS",
		"Input": {
			"Tracks": [{
					"Type": "Video",
					"TrackItems": [{
						"Type": "Video",
						"SourceMedia": "5285485487985271487",
						"AudioOperations": [{
							"Type": "Volume",
							"VolumeParam": {
								"Mute": 1
							}
						}]
					}]
				},
				{
					"Type": "Audio",
					"TrackItems": [{
							"Type": "Empty",
							"EmptyItem": {
								"Duration": 5
							}
						},
						{
							"Type": "Audio",
							"AudioItem": {
								"SourceMedia": "5285485487985271488",
								"Duration": 15
							}
						},
						{
							"Type": "Audio",
							"AudioItem": {
								"SourceMedia": "5285485487985271489",
								"SourceMediaStartTime": 2,
								"Duration": 14
							}
						}
					]
				}
			],
			"Output": {
				"FileName": "Video composing effect test",
				"Container": "mp4"
			}
		},
		"Output": {
			"FileType": "mp4",
			"FileId": 5285485487985271490,
			"FileUrl": "http://125676836723.vod2.myqcloud.com/xxx/xxx/xxx.mp4"
		}
	}
}
```

In the callback result, `Input.Tracks` contains two elements in `Type` of `Video` and `Audio`, indicating the composed video contains a video track and an audio track.
- Video track: the ID of the source video is `5285485487985271487`, and the video is muted.
- Audio track: it includes 5 seconds of silence and two voiceover bits lasting 15s and 14s, respectively.

`Output.FileId` is the `FileId` of the new video generated after video composing, and the playback URL is the value in `FileUrl`.
