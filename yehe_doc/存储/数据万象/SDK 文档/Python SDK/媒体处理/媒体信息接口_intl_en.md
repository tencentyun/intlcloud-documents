## Overview

This document provides an overview of APIs and SDK code samples for media information.

>! The COS Python SDK version must be at least v5.1.9.11.

| API | Operation |  Description |
| ------------------------------------------------------------ | --------------------------|---------------------------- |
|  [GetMediaInfo](https://intl.cloud.tencent.com/document/product/436/46915)    |   Querying file information | Queries media file information      |

>! Before using this API, make sure that the media processing feature has been enabled in the data processing section in the console; otherwise, the error `media bucket unbinded, bucket's host is unavailable` will be reported. For more information, see [Enabling Media Processing](https://intl.cloud.tencent.com/document/product/436/46275).

## Querying File Information

#### Feature description

This API is used to query the information of a media file.

#### Method prototype

```py
def get_media_info(Bucket, Key, **kwargs)
```

#### Sample request
```py
response = client.get_media_info(
    Bucket=bucket_name,
    Key='demo.mp4'
)
print(response)
```

#### Parameter description

| Parameter | Description | Required | Type |
| :------- | :----------------------------------------------------------- | :----- | :------- |
| Bucket        | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | Yes | String     |
| Key     | Object key, which is the unique identifier of the object in the bucket. | Yes       | String   |

#### Response description

```py
{
	'MediaInfo': [{
		'Format': {
			'Bitrate': '16869.432000',
			'Duration': '129.200000',
			'FormatLongName': 'QuickTime / MOV',
			'FormatName': 'mov,mp4,m4a,3gp,3g2,mj2',
			'NumProgram': '0',
			'NumStream': '2',
			'Size': '272441346',
			'StartTime': '0.000000'
		},
		'Stream': {
			'Audio': {
				'Bitrate': '125.712000',
				'Channel': '2',
				'ChannelLayout': 'stereo',
				'CodecLongName': 'AAC (Advanced Audio Coding)',
				'CodecName': 'aac',
				'CodecTag': '0x6134706d',
				'CodecTagString': 'mp4a',
				'CodecTimeBase': '1/44100',
				'Duration': '129.160998',
				'Index': '0',
				'Language': 'und',
				'SampleFmt': 'fltp',
				'SampleRate': '44100',
				'StartTime': '0.000000',
				'Timebase': '1/44100'
			},
			'Subtitle': None,
			'Video': {
				'AvgFps': '30/1',
				'Bitrate': '16738.543000',
				'CodecLongName': 'H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10',
				'CodecName': 'h264',
				'CodecTag': '0x31637661',
				'CodecTagString': 'avc1',
				'CodecTimeBase': '1/600',
				'Duration': '129.200000',
				'Fps': '30.500000',
				'HasBFrame': '1',
				'Height': '1920',
				'Index': '1',
				'Language': 'und',
				'Level': '40',
				'NumFrames': '3876',
				'PixFormat': 'yuvj420p',
				'Profile': 'High',
				'RefFrames': '1',
				'Rotation': '0.000000',
				'StartTime': '0.000000',
				'Timebase': '1/600',
				'Width': '1080'
			}
		}
	}]
}

```

The nodes are as described below:

 `MediaInfo` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------- | :------- | :-------- |
| Stream             | MediaInfo | Stream information.   | dict |
| Format             | MediaInfo | Format information. | dict |

`Stream` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------- | :------- | :-------- |
| Video              | MediaInfo.Stream | Video information. | dict |
| Audio              | MediaInfo.Stream | Audio information. | dict |
| Subtitle           | MediaInfo.Stream | Subtitles information. | dict |

`Format` has the following sub-nodes (certain nodes may not be returned during video information query):

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------- | :------------------------------------------ | :----- |
| NumStream          | MediaInfo.Format | Number of streams (including videos, audios, and subtitles). | String    |
| NumProgram         | MediaInfo.Format | Number of programs.                                  | String    |
| FormatName         | MediaInfo.Format | Container format name.                                | String |
| FormatLongName     | MediaInfo.Format | Detailed name of the container format.                          | String |
| StartTime          | MediaInfo.Format | Start time in seconds.                          | String  |
| Duration           | MediaInfo.Format | Duration in seconds.                          | String  |
| Bitrate            | MediaInfo.Format | Bitrate in Kbps.                         | String    |
| Size               | MediaInfo.Format | Size in bytes.                           | String    |

`Video` has the following sub-nodes (certain nodes may not be returned during video information query):

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------------- | :-------------------------- | :----- |
| Index              | MediaInfo.Stream.Video | Stream number.                  | String    |
| CodecName          | MediaInfo.Stream.Video | Codec format name.              | String |
| CodecLongName      | MediaInfo.Stream.Video | Detailed name of the codec format.        | String |
| CodecTimeBase      | MediaInfo.Stream.Video | Codec timebase.                     | String |
| CodecTagString     | MediaInfo.Stream.Video | Codec tag name.                   | String |
| CodecTag           | MediaInfo.Stream.Video | Codec tag.                    | String |
| Profile            | MediaInfo.Stream.Video | Video codec profile.                | String |
| Height             | MediaInfo.Stream.Video | Video height in px.             | String    |
| Width              | MediaInfo.Stream.Video | Video width in px.             | String    |
| HasBFrame          | MediaInfo.Stream.Video | Whether B-frames exist. 1: yes; 0: no. | String    |
| RefFrames          | MediaInfo.Stream.Video | Number of reference frames for video codec.        | String    |
| Sar                | MediaInfo.Stream.Video | Sample aspect ratio.                  | String |
| Dar                | MediaInfo.Stream.Video | Display aspect ratio.                  | String |
| PixFormat          | MediaInfo.Stream.Video | Pixel format.                     | String |
| FieldOrder         | MediaInfo.Stream.Video | Field order.                     | String |
| Level              | MediaInfo.Stream.Video | Video codec level.                | String    |
| Fps                | MediaInfo.Stream.Video | Video frame rate.                     | String    |
| AvgFps             | MediaInfo.Stream.Video | Average frame rate.                    | String |
| Timebase           | MediaInfo.Stream.Video | Timebase.                     | String |
| StartTime          | MediaInfo.Stream.Video | Video start time in seconds.      | String  |
| Duration           | MediaInfo.Stream.Video | Video duration in seconds.          | String  |
| Bitrate            | MediaInfo.Stream.Video | Bitrate in Kbps.         | String  |
| NumFrames          | MediaInfo.Stream.Video | Total number of frames.                      | String    |
| Language           | MediaInfo.Stream.Video | Language.                      | String |

`Audio` has the following sub-nodes (certain nodes may not be returned during video information query):

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------------- | :------------------- | :----- |
| Index              | MediaInfo.Stream.Audio | Stream number.           | String    |
| CodecName          | MediaInfo.Stream.Audio | Codec format name.       | String |
| CodecLongName      | MediaInfo.Stream.Audio | Detailed name of the codec format. | String |
| CodecTimeBase      | MediaInfo.Stream.Audio | Codec timebase.              | String |
| CodecTagString     | MediaInfo.Stream.Audio | Codec tag name.           | String |
| CodecTag           | MediaInfo.Stream.Audio | Codec tag.             | String |
| SampleFmt          | MediaInfo.Stream.Audio | Sample format.            | String |
| SampleRate         | MediaInfo.Stream.Audio | Sample rate.               | String    |
| Channel            | MediaInfo.Stream.Audio | Number of channels.             | String    |
| ChannelLayout      | MediaInfo.Stream.Audio | Channel layout.             | String |
| Timebase           | MediaInfo.Stream.Audio | Timebase.                 | String |
| StartTime          | MediaInfo.Stream.Audio | Audio start time in seconds. | String  |
| Duration           | MediaInfo.Stream.Audio | Audio duration in seconds.     | String  |
| Bitrate            | MediaInfo.Stream.Audio | Bitrate in Kbps.    | String  |
| Language           | MediaInfo.Stream.Audio | Language.                 | String |

`Subtitle` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :---------------------------------- | :----------------------- | :----- |
| Index              | MediaInfo.Stream.Subtitle | Stream number.               | String    |
| Language           | MediaInfo.Stream.Subtitle | Language. `und` indicates no query result. | String |
