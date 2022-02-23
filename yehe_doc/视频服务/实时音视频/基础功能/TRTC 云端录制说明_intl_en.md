In applications such as online education, live showroom, video conferencing, online medical consultation, and remote banking, it is often necessary to record entire video calls or live streaming sessions for purposes including content moderation, archiving, and playback. The on-cloud recording feature of TRTC can help meet these demands.

## Overview
The on-cloud recording feature of TRTC allows you to record an audio/video stream in real time using a RESTful API. It is flexible, light, and easy-to-use, saving you the trouble of deploying servers and recording modules.

- Recording mode: Single-stream recording records the audio and video of each user in a room separately, while mixed-stream recording records all audios and videos in a room into one result.

* Stream subscription: You can determine whose streams you receive or do not receive using an allowlist/blocklist.
* Transcoding parameters: In the mixed-stream recording mode, you can determine the output video quality by specifying transcoding parameters.
* Stream-mixing parameters: For mixed-stream recording, we offer multiple auto-arranged layout templates. You can also customize a layout template.
* File storage: Currently, you can save recording files only in COS or VOD of Tencent Cloud.
  (We plan to add support for storage and video-on-demand services of third-party cloud vendors in the future. To save files to third-party platforms, you will need to provide your cloud service account and the storage parameters.)
* Callback notification: By configuring a callback domain in the console, you can receive notifications about on-cloud recording events via your callback server.

### Single-stream recording

![Single-stream recording](https://qcloudimg.tencent-cloud.cn/raw/cd843d26b27ed6f4179ebbff401ae6e3.png)

The diagram above shows the workflow of single-stream recording. In room 1234, anchor 1 and anchor 2 are publishing streams. If you subscribe to their streams and enable single-stream recording, the TRTC backend will record the audio and video data of anchor 1 and anchor 2 separately. The recording results will include:

1. An M3U8 index file of anchor 1’s video
2. Multiple TS segment files of anchor 1’s video
3. An M3U8 index file of anchor 1’s audio
4. Multiple TS segment files of anchor 1’s audio
5. An M3U8 index file of anchor 2’s video
6. Multiple TS segment files of anchor 2’s video
7. An M3U8 index file of anchor 2’s audio
8. Multiple TS segment files of anchor 2’s audio

The backend will then upload the files to the cloud storage server you specify. You need to download the files and merge/transcode them. We offer a [script for merging audio and video streams](https://intl.cloud.tencent.com/zh/document/product/647/45169#.E5.8D.95.E6.B5.81.E6.96.87.E4.BB.B6.E5.90.88.E5.B9.B6.E8.84.9A.E6.9C.AC).

### Mixed-stream recording

![Mixed-stream recording](https://qcloudimg.tencent-cloud.cn/raw/3a29f4527601abe3ac981759bf44ad07.png)

The above shows the workflow of mixed-stream recording. In room 1234, anchor 1 and anchor 2 are publishing streams. If you subscribe to their streams and enable mixed-stream recording, the TRTC backend will mix the streams of anchor 1 and anchor 2 according to the layout template you specify and then record them into one result, which will include:

1. An M3U8 index file of the mixed video
2. Multiple TS segment files of the mixed video

The backend will then upload the files to the cloud storage server you specify. You need to download the files and merge/transcode them. We offer a [script for merging audio and video streams](https://intl.cloud.tencent.com/zh/document/product/647/45169#.E5.8D.95.E6.B5.81.E6.96.87.E4.BB.B6.E5.90.88.E5.B9.B6.E8.84.9A.E6.9C.AC).

> !
>- The rate limit for the recording API is 20 queries per second.
>- The timeout period for a query is 6 seconds.
>- We allow up to 100 ongoing recording tasks at the same time. If you need to record more, please [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category?step=0&source=14).
>- In the single-stream recording mode, you can record up to 25 streams in a room at the same time.

## Directions
### 1. Start recording

Call the RESTful API `CreateCloudRecording` from your server to start on-cloud recording. Pay attention to the following parameters:

#### TaskId

This parameter uniquely identifies a recording task. Note it as you will need to provide it for other actions on the same task later.

#### RecordMode
- Single-stream recording separately records the audios and videos of individual anchors whose streams you receive before uploading the results (including M3U8 and TS segment files) to the cloud.
- Mixed-stream recording records all the audios and videos of anchors whose streams you receive into one result (including M3U8 and TS segment files) before uploading it to the cloud.

#### SubscribeStreamUserIds
By default, on-cloud recording records all the streams (max 25) you receive in a room. You can use this parameter to specify whose streams you want to record and can change its value during recording.

#### StorageParams
You can use this parameter to specify the cloud storage/video-on-demand service you want to save recording files to. Make sure you use a valid value and that the cloud storage/video-on-demand service you use is available. Below are the naming conventions of recording files:

##### Naming of recording files

* M3U8 file in the single-stream recording mode:
\<Prefix>/\<TaskId>/\<SdkAppId>\_\<RoomId>\_\_UserId\_s\_\<UserId>\_\_UserId\_e\_\<MediaId>\_\<Type>.m3u8

* TS segment file in the single-stream recording mode:
\<Prefix>/\<TaskId>/\<SdkAppId>\_\<RoomId>\_\_UserId\_s\_\<UserId>\_\_UserId\_e\_\<MediaId>\_\<Type>\_\<UTC>.ts

* MP4 file in the single-stream recording mode:
\<Prefix>/\<TaskId>/\<SdkAppId>\_\<RoomId>\_\_UserId\_s\_\<UserId>\_\_UserId\_e\_\<MediaId>\_\<Index>.mp4

* M3U8 file in the mixed-stream recording mode:
\<Prefix>/\<TaskId>/\<SdkAppId>\_\<RoomId>.m3u8

* TS segment file in the mixed-stream recording mode:
\<Prefix>/\<TaskId>/\<SdkAppId>\_\<RoomId>\_\<UTC>.ts

* MP4 file in the mixed-stream recording mode:
\<Prefix>/\<TaskId>/\<SdkAppId>\_\<RoomId>\_\<Index>.mp4

* Naming of recovered files
The on-cloud recording feature has a high availability scheme that can recover recording files if the server fails. To prevent the recovered files from replacing the original files, we add a prefix `ha<1/2/3>` to the names of recovered files. The numbers indicate the times (max 3) the high availability scheme is used.

* M3U8 file in the single-stream recording mode:
\<Prefix>/\<TaskId>/ha\<1/2/3>\_\<SdkAppId>\_\<RoomId>\_\_UserId\_s\_\<UserId>\_\_UserId\_e\_\<MediaId>\_\<Type>.m3u8

* TS segment file in the single-stream recording mode:
\<Prefix>/\<TaskId>/ha\<1/2/3>\_\<SdkAppId>\_\<RoomId>\_\_UserId\_s\_\<UserId>\_\_UserId\_e\_\<MediaId>\_\<Type>\_\<UTC>.ts

* M3U8 file in the mixed-stream recording mode:
\<Prefix>/\<TaskId>/ha\<1/2/3>\_\<SdkAppId>\_\<RoomId>.m3u8

* TS segment file in the mixed-stream recording mode:
\<Prefix>/\<TaskId>/ha\<1/2/3>\_\<SdkAppId>\_\<RoomId>\_\<UTC>.ts

###### Field description
\<Prefix>: filename prefix, which is not used if not specified
\<TaskId>: task ID, which is unique and is returned by the start recording API
\<SdkAppId>: application ID
\<RoomId>: room ID
\<UserId>: Base64-encoded ID of a user whose stream is recorded
\<MediaId>: indicates whether the primary stream (`main`) or substream (`aux`) is recorded
\<Type>: the type of stream that is recorded (audio or video)
\<UTC>: recording start time (UTC+0) (year, month, day, hour, minute, second, millisecond)
\<Index>: index of a segment, which starts from 1. This field is used only if the size of an MP4 file reaches 2 GB or its length reaches 24 hours and needs to be segmented.
ha\<1/2/3>: prefix for a file recovered by the high availability scheme. For example, if the scheme is used for the first time, the recovered file is named \<Prefix>/\<TaskId>/ha1\_\<SdkAppId>\_\<RoomId>.m3u8.
>! If \<RoomId> is a string, it will be encoded into Base64. In the result, "/" is replaced with "-" and "=" is replaced with "."
\<UserId> is encoded into Base64. In the result, "/" is replaced with "-" and "=" is replaced with "."

#### Recording start time
Recording starts when you start receiving data from an anchor. Recording start time is the Unix time on the server when recording starts.
You can query the start time of a recording task in three ways:

* Using the `DescribeCloudRecording` API. `BeginTimeStamp` in the response parameters indicates the recording start time (ms).

Below is a response of the `DescribeCloudRecording` API, in which `BeginTimeStamp` is `1622186279144`.

```json
{
  "Response": {
    "Status": "xx",
    "StorageFileList": [
      {
        "TrackType": "xx",
        "BeginTimeStamp": 1622186279144,
        "UserId": "xx",
        "FileName": "xx"
      }
    ],
    "RequestId": "xx",
    "TaskId": "xx"
  }
}
```

* Viewing the M3U8 file (the \#EXT-X-TRTC-START-REC-TIME directive)

According to the M3U8 file below, the Unix time (ms) when recording started was 1622425551884.

```m3u8
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-ALLOW-CACHE:NO
#EXT-X-MEDIA-SEQUENCE:0
#EXT-X-TARGETDURATION:70
#EXT-X-TRTC-START-REC-TIME:1622425551884
#EXT-X-TRTC-VIDEO-METADATA:WIDTH:1920 HEIGHT:1080
#EXTINF:12.074
1400123456_12345__UserId_s_MTY4NjExOQ..__UserId_e_main_video_20330531094551825.ts
#EXTINF:11.901
1400123456_12345__UserId_s_MTY4NjExOQ..__UserId_e_main_video_20330531094603825.ts
#EXTINF:12.076
1400123456_12345__UserId_s_MTY4NjExOQ..__UserId_e_main_video_20330531094615764.ts
#EXT-X-ENDLIST
```

* Via a recording callback

If you have registered recording callbacks, you will receive a callback for the generation of recording files (event type 307), in which `BeginTimeStamp` indicates the recording start time.
According to the callback below, the Unix time (ms) when recording started was 1622186279144.

```json
{
        "EventGroupId": 3,
        "EventType":    307,
        "CallbackTs":   1622186289148,
        "EventInfo":    {
                "RoomId":       "xx",
                "EventTs":      "1622186289",
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "FileName":     "xx.m3u8",
                        "UserId":       "xx",
                        "TrackType":    "audio",
                        "BeginTimeStamp":       1622186279144
                }
        }
}
```

#### MixWatermark
TRTC allows you to watermark videos during mixed-stream recording. You can add up to 25 marks to a video in your desired positions.

|Field|Description|
|---|---|
|Top|Vertical offset of the watermark from the top-left corner of the video|
|Left|Horizontal offset of the watermark from the top-left of the video|
|Width|Watermark width|
|Height|Watermark height|
|url|URL of the watermark file|

#### MixLayoutMode
TRTC supports the grid layout (default), floating layout, screen sharing layout, and custom layout.

##### Grid layout

The videos of anchors are scaled and positioned automatically according to the total number of anchors in a room. Each video has the same size. Up to 25 videos can be displayed.

* When there is only one video:
The video is scaled to fill the canvas.

* When there are two videos:
The width of each video is half of the canvas width.
The height of each video is the same as the canvas height.

* When there are three or four videos:
The canvas is split evenly into four windows and each video is displayed in one window.

* When the number of videos is between four and nine:
The canvas is split evenly into nine windows and each video is displayed in one window.

* When the number of videos is between 10 and 16:
The canvas is split evenly into 16 windows and each video is displayed in one window.

* When there are more than 16 videos:
The canvas is split evenly into 25 windows and each video is displayed in one window.

 As shown below:

![Grid 1](https://qcloudimg.tencent-cloud.cn/raw/9d989363167bd9231a1ebf3097b8fb5c.jpg)
![Grid 2](https://qcloudimg.tencent-cloud.cn/raw/cd5437606f3a5dceb723d6e63eb283ee.jpg)
![Grid 3](https://qcloudimg.tencent-cloud.cn/raw/98295756807b1aba1457f668f85d7fd9.jpeg)
![Grid 4](https://qcloudimg.tencent-cloud.cn/raw/87b3d8d21d3e22704c379a534faf37b8.jpeg)
![Grid 5](https://qcloudimg.tencent-cloud.cn/raw/3418887536457bfa607ecdfb34a71b7f.jpeg)
![Grid 6](https://qcloudimg.tencent-cloud.cn/raw/ae3aa97ee2cbe5678f1672b34a610d20.jpeg)

##### Floating layout
By default, the video of the first anchor (you can also specify an anchor) who enters the room is scaled to fill the screen. When other anchors enter the room, their videos appear smaller and are superimposed over the large video from left to right starting from the bottom of the canvas according to their room entry sequence. If the total number of videos is 17 or less, there will be four windows in each row (4 × 4); if it is greater than 17, there will be five windows in each row (5 × 5). Up to 25 videos can be displayed. A user who publishes only audio will still be displayed in one window.

* When there are 17 or fewer videos:
       The width and height of each video are 23.5% of the canvas width and height.
       The horizontal space and vertical space between two neighboring videos are 1.2% of the canvas width and height.
       The right/left and top/bottom margin are 1.2% of the canvas width and height.

* When there are more than 17 videos:
       The width and height of each video are 18.8% of the canvas width and height.
       The horizontal space and vertical space between two neighboring videos are 1% of the canvas width and height.
       The right/left and top/bottom margin are 1% of the canvas width and height.

  As shown below:
   ![Floating 1](https://qcloudimg.tencent-cloud.cn/raw/96a531ba9f6a69297ea4f1a5a365794a.jpg)
   ![Floating 2](https://qcloudimg.tencent-cloud.cn/raw/be91b17b6b557fcd7d1d76c589e15917.jpg)


##### Screen sharing layout
The video of a specified anchor occupies a larger part of the canvas on the left side (if you do not specify an anchor, the left window will display the canvas background). The videos of other anchors are smaller and are positioned on the right side. If the total number of videos is 17 or less, the small videos are positioned from top to bottom in up to two columns on the right side, with eight videos per column at most. If there are more than 17 videos, the additional videos are positioned at the bottom of the canvas from left to right. Up to 24 videos can be displayed. A user who publishes only audio will still is displayed in one window.

* When there are five or fewer videos:
The size of each small video on the right is 1/5 the canvas width and 1/4 the canvas height.
The width of the large video on the left is 4/5 the canvas width, and its height is the same as the canvas height.

* When the number of videos is between 5 and 7:
The size of each small video on the right are 1/7 the canvas width and 1/6 the canvas height.
The width of the large video on the left is 6/7 the canvas width, and its height is the same as the canvas height.
* When there are eight or nine videos:
The size of each small video on the right is 1/9 the canvas width and 1/8 the canvas height.
The width of the large video on the left is 8/9 the canvas width, and its height is the same as the canvas height.

* When the number of videos is between 10 and 17:
The size of each small video on the right side is 1/10 the canvas width and 1/8 the canvas height.
The width of the large video on the left side is 4/5 the canvas width, and its height is the same as the canvas height.

* When there are more than 17 videos:
The size of each small video on the right and bottom is 1/10 the canvas width and 1/8 the canvas height.
The width of the large video on the left is 4/5 the canvas width, and its height is 7/8 the canvas height.

As shown below:
   ![Screen sharing 1](https://qcloudimg.tencent-cloud.cn/raw/d64e7e705060d21ec24d7392f8d43728.png)
   ![Screen sharing 2](https://qcloudimg.tencent-cloud.cn/raw/695683aecb62c29976f16124d6e9b29b.png)
   ![Screen sharing 3](https://qcloudimg.tencent-cloud.cn/raw/8423e777eb1a5bfb80e384e7b97db49d.png)
   ![Screen sharing 4](https://qcloudimg.tencent-cloud.cn/raw/538faeb7d2f993427b7ab1db548cb633.png)
   ![Screen sharing 4](https://qcloudimg.tencent-cloud.cn/raw/f911eb5a849da0aa22ed9b69ebe2f63a.png)

##### Custom layout
You can also use `MixLayoutList` to customize a layout for anchor videos.

### 2. Query the recording task
You can use the `DescribeCloudRecording` API to query the status of an ongoing recording task. If the queried task has already ended, an error will be returned.
The file list (`StorageFile`) that is returned will include all the M3U8 files of the recording as well as the Unix time when recording started. If the task queried is a recording to VOD task, the `StorageFile` returned will be empty.

### 3. Modify recording parameters
You can use the `ModifyCloudRecording` API to modify recording parameters, including `SubscribeStreamUserIds` and `MixLayoutParams` (valid only for mixed-stream recording). Note that to modify parameters, you need to respecify all the parameters, including `MixLayoutParams` and `SubscribeStreamUserIds`, and not just the one you want to modify. As a result, we recommend you note all the values before modifying a parameter, or you will need to calculate them again.

### 4. Stop recording
You can call the `DeleteCloudRecording` API to stop recording. A recording task will also end automatically if there are no anchors in a room for longer than the specified time period (`MaxIdleTime`). We recommend that you call the API to stop recording when you no longer need the service.

## Advanced Features

### Recording in MP4 format

To record in MP4 format, set `OutputFormat` to `hls+mp4` when calling the `CreateCloudRecording` API. TRTC will still record in HLS format, but once recording ends, it will download the HLS file from its COS bucket, convert it into MP4 format, and upload the MP4 file to the COS bucket.
Please note that COS download access is required for the above to work.
An MP4 file will be segmented if one of the following conditions is met.

1. The recording lasts for 24 hours or longer.
2. The MP4 file is 2 GB or larger.
   <br>The figure below shows the workflow of recording in MP4 format.
   <br>![Record in MP4 format](https://qcloudimg.tencent-cloud.cn/raw/d3a3f5121e9832cc8a39b8d9ec6f7b1a.png)

### Recording to VOD

To record to VOD, specify the `CloudVod` parameter in `StorageParams` when calling the `CreateCloudRecording` API. After recording ends, the backend will save the file in MP4 format to VOD using the method you specify and send you a playback URL via a callback. In the single-stream recording mode, there will be a playback URL for each anchor whose stream is recorded; in the mixed-stream recording mode, there will be only one playback URL. When you record to VOD, pay attention to the following:

1. `CloudVod` and `CloudStorage` are mutually exclusive. If you specify both, the recording task will fail to start.
2. If you use `DescribeCloudRecording` to query a recording to VOD task, the `StorageFile` returned will be empty.
   <br>The figure below shows the workflow of recording to VOD, in which "cloud storage" refers to the internal storage of the recording backend. You don’t need to specify a COS bucket for it.
   <br>![Record to VOD](https://qcloudimg.tencent-cloud.cn/raw/28da00ba87fc1b9be2030f96d2dfd820.png)



### Script for merging single-stream recording files

We offer a [script]() for merging single-stream audio and video files into MP4 files.

>? If two segment files are more than 15 seconds apart, during which no audio or video data is recorded (if the substream is disabled, its data will be ignored), the two segments will be considered to belong to different sections, one being the ending segment of the previous section, and the other the starting segment of the next section.

 - Section-based merge (`-m 0`)
In this mode, the recording files of each user (`UserId`) are merged by section. An MP4 file is generated for each section.
 - User-based merge (`-m 1`)
In this mode, the recording files of each user (`UserId`) are merged into one MP4 file. You can use the `-s` option to specify whether to fill in the blanks between sections.

#### Environment requirements

Python 3

-   Centos: sudo yum install python3
-   Ubuntu: sudo apt-get install python3

Python 3 dependency

-sortedcontainers：pip3 install sortedcontainers

#### Directions

 1. Run the merge script: python3 TRTC_Merge.py [option]
 2. An MP4 file will be generated in the directory of the recording files.
E.g.: python3 TRTC_Merge.py -f /xxx/file -m 0

Below is a list of the options:

|Option| Description |
|---|---|
|-f | Directory of the recording files. If there are multiple users (`UserId`), their recording files will be merged separately.|
|-m   | `0`: section-based marge (default). In this mode, the recording files of each user (`UserId`) are merged by section. Multiple MP4 files may be generated for each user. <br>`1`: user-based merge. In this mode, the recording files of each user (`UserId`) are merged into one MP4 file.|
|-s| Indicates whether to delete the blanks between sections in the user-based merge mode, in which case the files generated will be shorter than the recording duration.|
|-a|`0`: primary stream merge (default). The audio of a user (`UserId`) is merged with the user’s primary stream, not the substream. <br>`1`: automatic merge. If a user (`UserId`) has a primary stream, the user’s audio is merged with the primary stream; if not, it is merged with the substream. <br>`2`: substream merge. The audio of a user (`UserId`) is merged with the user’s substream, not the primary stream. |
|-p|Frame rate (fps) of the output video, which is `15` by default. Value range: 5-120. If you enter a value smaller than `5`, `5` will be used; if you enter a value greater than `120`, `120` will be used.|
|-r|Resolution of the output video. For example, `-r 640 360` indicates that the resolution of the output video is 640 × 360. |

**File Naming**

- Audio-video file: UserId\_timestamp\_av.mp4
- Audio-only file: UserId\_timestamp.m4a

>? `UserId` is the Base64-encoded ID of a user whose stream is recorded. For details, see the naming of recording files. `timestamp` is the starting time of the first TS segment of a section.



## Callback APIs

You can register callbacks by providing an HTTP/HTTPS gateway to receive callbacks. When an on-cloud recording event occurs, the system will send a callback notification to your callback server.

### Callback format

Callbacks are sent to your server in the form of HTTP/HTTPS POST requests, which consist of the following parts:
Character encoding: UTF-8
Request: The request body is in JSON format.
Response: HTTP STATUS CODE = 200. The server ignores the content of the response packet. For protocol-friendliness, we recommend adding `JSON: `{"code":0}`` to the response.

### Field description

The header of a callback contains the following fields.


| Field       | Description                 |
| ------------ | ------------------ |
| Content-Type | application/json   |
| Sign         | Signature value             |
| SdkAppId     | SDK application ID |

The body of a callback contains the following fields.

| Field       | Type        | Description                                                         |
| ------------ | ----------- | ------------------------------------------------------------ |
| EventGroupId | Number      | Event group ID, which is `3` for on-cloud recording                                  |
| EventType    | Number      | Event type                                           |
| CallbackTs   | Number      | Unix time (ms) when the callback was sent to your server |
| EventInfo    | JSON Object | Event information                                                     |

Event types

| Field                                                | Type | Description                                                    |
| ----------------------------------------------------- | ---- | ------------------------------------------------------- |
| EVENT\_TYPE\_CLOUD\_RECORDING\_RECORDER\_START        | 301  | On-cloud recording - The recording module was started.                                   |
| EVENT\_TYPE\_CLOUD\_RECORDING\_RECORDER\_STOP         | 302  | On-cloud recording - The recording module was stopped.                                   |
| EVENT\_TYPE\_CLOUD\_RECORDING\_UPLOAD\_START          | 303  | On-cloud recording - The upload module was started.                                   |
| EVENT\_TYPE\_CLOUD\_RECORDING\_FILE\_INFO             | 304  | On-cloud recording - The first M3U8 file was generated and uploaded successfully. |
| EVENT\_TYPE\_CLOUD\_RECORDING\_UPLOAD\_STOP           | 305  | On-cloud recording - The upload finished.                                       |
| EVENT\_TYPE\_CLOUD\_RECORDING\_FAILOVER               | 306  | On-cloud recording - The recording task was migrated.  |
| EVENT\_TYPE\_CLOUD\_RECORDING\_FILE\_SLICE            | 307  | On-cloud recording - The first TS segment was available and an M3U8 file was generated.       |
| EVENT\_TYPE\_CLOUD\_RECORDING\_UPLOAD\_ERROR          | 308  | On-cloud recording - The upload module encountered an error.                               |
| EVENT\_TYPE\_CLOUD\_RECORDING\_DOWNLOAD\_IMAGE\_ERROR | 309  | On-cloud recording - An error occurred during the download of the image decoding file.                       |
| EVENT\_TYPE\_CLOUD\_RECORDING\_MP4\_STOP              | 310  | On-cloud recording - The task of recording in MP4 format ended and the name of the MP4 file generated was returned.       |
| EVENT\_TYPE\_CLOUD\_RECORDING\_VOD\_COMMIT            | 311  | On-cloud recording - Upload was completed for the recording to VOD task.                    |
| EVENT\_TYPE\_CLOUD\_RECORDING\_VOD\_STOP              | 312  | On-cloud recording - The recording to VOD task ended.                                |

Event information

| Field  | Type          | Description                                |
| ------- | ------------- | ------------------------------------ |
RoomId      |     String/Number       |     Room ID (same type as Room ID on the client)   |
| EventTs | Number | Unix timestamp (s) when the event occurred    |
| UserId  | String        | User ID of the recording robot          |
| TaskId  | String        | Recording ID, which uniquely identifies a recording task     |
| Payload | JsonObject    | The content of this field varies with event type.             |

If the event type is `301` (EVENT\_TYPE\_CLOUD\_RECORDING\_RECORDER\_START):

| Field | Type | Description |
| ------ | ------ | -------------------------------------------------- |
| Status | Number | `0`: The recording module was started successfully. `1`: The recording module failed to be started. |

```json
{
        "EventGroupId": 3,
        "EventType":    301,
        "CallbackTs":   1622186275913,
        "EventInfo":    {
                "RoomId":       "xx",
                "EventTs":      "1622186275",
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Status":       0
                }
        }
}
```

If the event type is `302` (EVENT\_TYPE\_CLOUD\_RECORDING\_RECORDER\_STOP):

| Field | Type | Description |
| --------- | ------ | ------------------------------------------------------------ |
| LeaveCode | Number | `0`: The recording module ended the recording normally.<br>`1`: The recording robot was removed from the room.<br>`2`: The room was closed.<br>`3`: The server removed the recording robot from the room.<br>`4`: The server closed the room.<br>`99`: There were no anchors in the room except the recording robot, which quit after the specified time period elapsed. <br>`100`: The recording robot quit after timeout.<br>`101`: The recording robot was removed due to repeat entry by the same user. |

```json
{
        "EventGroupId": 3,
        "EventType":    302,
        "CallbackTs":   1622186354806,
        "EventInfo":    {
                "RoomId":       "xx",
                "EventTs":      "1622186354",
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "LeaveCode":    0
                }
        }
}
```

If the event type is `303` (EVENT\_TYPE\_CLOUD\_RECORDING\_UPLOAD\_START):

| Field | Type | Description |
| ------ | ------ | ------------------------------------------------------ |
| Status | Number | `0`: The upload module was started successfully.<br>`1`: The upload module failed to be started. |

```json
{
        "EventGroupId": 3,
        "EventType":    303,
        "CallbackTs":   1622191965320,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191965,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Status":       0
                }
        }
}
```

If the event type is `304` (EVENT\_TYPE\_CLOUD\_RECORDING\_FILE\_INFO):

| Field   | Type   | Description             |
| -------- | ------ | ---------------- |
| FileList | String | Name of the M3U8 file generated |

```json
{
        "EventGroupId": 3,
        "EventType":    304,
        "CallbackTs":   1622191965350,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191965,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "FileList":     "xx.m3u8"
                }
        }
}
```


If the event type is `305` (EVENT\_TYPE\_CLOUD\_RECORDING\_UPLOAD\_STOP):

| Field | Type | Description |
| ------ | ------ | ------------------------------------------------------------ |
| Status | Number | `0`: The recording task ended and all the files were uploaded to the specified third-party cloud storage service.<br>`1`: The recording task ended, but at least one file on the server or in backup storage failed to be uploaded. <br>`2`: The files that failed to be uploaded earlier were uploaded to the specified third-party cloud storage service. |

```json
{
        "EventGroupId": 3,
        "EventType":    305,
        "CallbackTs":   1622191989674,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191989,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Status":       0
                }
        }
}
```

If the event type is `306` (EVENT\_TYPE\_CLOUD\_RECORDING\_FAILOVER):

| Field  | Type   | Description                              |
| ------ | ------ | ----------------------- |
| Status | Number | `0`: The migration was completed. |

```json
{
        "EventGroupId": 3,
        "EventType":    306,
        "CallbackTs":   1622191989674,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191989,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Status":       0
                }
        }
}
```

If the event type is `307` (EVENT\_TYPE\_CLOUD\_RECORDING\_FILE\_SLICE):

| Field | Type | Description |
| -------------- | ------ | ----------------------------------- |
| FileName       | String | Name of the M3U8 file generated                          |
| UserId         | String | ID of the user whose stream was recorded in the file              |
| TrackType      | String | Valid values: audio/video/audio_video             |
| BeginTimeStamp | Number | Unix timestamp on the server when recording started |


```json
{
        "EventGroupId": 3,
        "EventType":    307,
        "CallbackTs":   1622186289148,
        "EventInfo":    {
                "RoomId":       "xx",
                "EventTs":      "1622186289",
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "FileName":     "xx.m3u8",
                        "UserId":       "xx",
                        "TrackType":    "audio",
                        "BeginTimeStamp":       1622186279144
                }
        }
}
```

If the event type is `308` (EVENT\_TYPE\_CLOUD\_RECORDING\_UPLOAD\_ERROR):

| Field  | Type   | Description                              |
| ------- | ------ | -------------------------- |
| Code    | String | Error code returned by the third-party cloud storage service     |
| Message | String | Error message returned by the third-party cloud storage service |


```json
{
  "Code": "InvalidParameter",
  "Message": "AccessKey invalid"
}

{
        "EventGroupId": 3,
        "EventType":    308,
        "CallbackTs":   1622191989674,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191989,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Code":       "xx",
                        "Message":    "xx"
                }
        }
}
```

If the event type is `309` (EVENT\_TYPE\_CLOUD\_RECORDING\_DOWNLOAD\_IMAGE\_ERROR):

| Field  | Type   | Description                              |
| ------ | ------ | ------------- |
| Url    | String | The URL from which the file failed to be downloaded  |


```json
{
        "EventGroupId": 3,
        "EventType":    309,
        "CallbackTs":   1622191989674,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191989,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Url":       "http://xx",
                }
        }
}
```

If the event type is `310` (EVENT\_TYPE\_CLOUD\_RECORDING\_MP4\_STOP):

| Field | Type | Description |
| -------- | ------ | ------------------------------------------------------------ |
| Status   | Number | `0`: The task ended and all the files were uploaded to the specified third-party cloud storage service.<br>`1`: The task ended, but at least one file on the server or in backup storage failed to be uploaded.<br>`2`: The task stopped due to an error, for example, failure to download HLS files from COS. |
| FileList | String | Name of the MP4 file generated                                              |


```json
{
        "EventGroupId": 3,
        "EventType":    310,
        "CallbackTs":   1622191989674,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191989,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Status":       0,
                        "FileList": ["xxxx1.mp4", "xxxx2.mp4"]
                }
        }
}
```

If the event type is `311` (EVENT\_TYPE\_CLOUD\_RECORDING\_VOD\_COMMIT):

| Field | Type | Description |
| --------- | ------ | ------------------------------------------------------------ |
| Status    | Number | `0`: The recording file was successfully uploaded to VOD.<br>`1`: The recording file failed to be uploaded.<br>`2`: An error occurred. |
| UserId    | String | ID of the user whose stream is recorded. In the mixed-stream recording mode, this field is empty. |
| TrackType | String | Valid values: audio/video/audio_video                                      |
| MediaId   | String | Valid values: main/aux                                                     |
| FileId    | String | Unique ID of the recording file in VOD                                 |
| VideoUrl  | String | Playback URL of the recording file in VOD                               |
| CacheFile | String | Name of the MP4 file converted from the recording file (before it was uploaded to VOD)                  |
| Errmsg    | String | Error message when `Status` is not `0`                                |


Callback for successful upload:

```json
{
        "EventGroupId": 3,
        "EventType":    311,
        "CallbackTs":   1622191965320,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191965,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Status":       0,
                        "TencentVod":   {
                            "UserId":       "xx",
                            "TrackType":    "audio_video",
                            "MediaId":      "main",
                            "FileId":       "xxxx",
                            "VideoUrl":     "http://xxxx"
                        }
                }
        }
}
```

Callback for failed upload:

```json
{
        "EventGroupId": 3,
        "EventType":    311,
        "CallbackTs":   1622191965320,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191965,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Status":       1,
                        "Errmsg":       "xxx",
                        "TencentVod":   {
                            "UserId":       "123",
                            "TrackType":    "audio_video",
                            "CacheFile":    "xxx.mp4"
                        }
                }
        }
}
```

If the event type is `312` (EVENT\_TYPE\_CLOUD\_RECORDING\_VOD\_STOP):

| Field | Type | Description |
| ------ | ------ | ------------------------------------------------------------ |
| Status | Number | `0`: The task ended after upload was completed.<br>`1`: The task ended due to an error. |


```json
{
        "EventGroupId": 3,
        "EventType":    312,
        "CallbackTs":   1622191965320,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191965,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Status":       0
                }
        }
}
```



## Best Practices

To ensure the high availability of the recording service, we recommend the following practices when you use the RESTful APIs:

1. Pay attention to the HTTP response after you call `CreateCloudRecording`. If your request fails, fix the problem according to the status code and try again.

   The status code consists of two parts, for example `InvalidParameter.SdkAppId`.

   - `InValidParameter.xxxxx` indicates that a parameter value entered was invalid. Please check the parameter.
   - `InternalError.xxxxx` indicates that a server error occurred. You can retry until the request succeeds and `TaskId` is returned. We recommend you use the exponential backup algorithm for retry. For example, you can wait for three seconds for the first retry, six seconds for the second, 12 seconds for the third, and so on.
   - `FailedOperation.RestrictedConcurrency` indicates that you reached the maximum number (100 by default) of ongoing recording tasks allowed. To raise the limit, please contact technical support.

2. The `UserId` and `UserSig` you pass in when calling `CreateCloudRecording` are for the recording robot. Please make sure that they are different from those of other users in the room. In addition, the room users join from the TRTC client must be of the same type as the room you specify when calling the API. For example, if the room created in the TRTC SDK is a string, the room specified for on-cloud recording must also be a string.

3. You can obtain the information of a recording file in the following ways.

   - Call `DescribeCloudRecording` 15 seconds after a `CreateCloudRecording` request succeeds. If the status returned is `idle`, it indicates that no audio or video data is available for recording. Please check whether there are anchors publishing data in the room.
   - After a `CreateCloudRecording` request succeeds, if there are anchors publishing data in the room, you can splice the name of the recording file according to the naming conventions.
   - If you have registered on-cloud recording callbacks, the information of recording files will be sent to your server via callbacks.
   - You can specify a COS bucket to save recording files when calling the `CreateCloudRecording` API, so after a recording task ends, you can find the recording file in the COS bucket.

