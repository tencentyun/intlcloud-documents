## Event Name
ReduceMediaBitrateComplete

## Event Description
If you have configured event notifications for your application, after a smart bitrate reduction task is completed, your application backend will be notified either by a “normal callback” or a “reliable callback”. For the content of the callback, see [ReduceMediaBitrateTask](https://intl.cloud.tencent.com/document/product/266/34187#ReduceMediaBitrateTask).

## Examples
### Normal callback
In the normal callback mode, your callback URL will receive an HTTP POST request from VOD. The content of the callback is included in the request body, as shown below (fields with null values are omitted):

```json
{
  "EventType": "ReduceMediaBitrateComplete",
  "ReduceMediaBitrateCompleteEvent": {
    "TaskId": "1500013xxx-ReduceMediaBitrate-0c64611d529f2656c4133128ee053063txxx",
    "Status": "FINISH",
    "FileId": "5287852109848150xxx",
    "FileName": "xxx",
    "FileUrl": "http://1500013xxx.vod2.myqcloud.com/xxx/xxx/playlist.f9.mp4",
    "MetaData":{
      "AudioDuration": 359.306,
      "AudioStreamSet":[
        {
          "Bitrate": 130720,
          "Codec": "aac",
          "SamplingRate": 44100
        }
      ],
      "Bitrate": 475103,
      "Container": "mov,mp4,m4a,3gp,3g2,mj2",
      "Duration": 359.362,
      "Height": 224,
      "Rotate": 0,
      "Size": 21341780,
      "VideoDuration": 359.362,
      "VideoStreamSet":[
        {
          "Bitrate": 337666,
          "Codec": "h264",
          "Fps": 24,
          "Height": 224,
          "Width": 440
        }
      ],
      "Width": 440
    },
    "MediaProcessResultSet":[
      {
        "Type": "Transcode",
        "TranscodeTask":{
          "Status": "SUCCESS",
          "ErrCodeExt": "",
          "Message": "SUCCESS",
          "Progress": 100,
          "BeginProcessTime": "2022-09-15T10:19:46Z",
          "FinishTime": "2022-09-15T10:22:14Z",
          "Input":{
            "Definition": 220,
            "TraceWatermark": {
              "Definition": 0,
              "DefinitionForBStream": 0,
              "Switch": ""
            },
            "WatermarkSet": [
              {
                "Definition": 103660,
                "TextContent": "xxx",
                "SvgContent": "",
                "StartTimeOffset": 0,
                "EndTimeOffset": 0
              }
            ],
            "HeadTailSet": [],
            "MosaicSet": [
              {
                "CoordinateOrigin": "TopLeft",
                "XPos": "",
                "YPos": "",
                "Width": "50%",
                "Height": "50%",
                "StartTimeOffset": 0,
                "EndTimeOffset": 0
              }
            ],
            "StartTimeOffset": 1,
            "EndTimeOffset": 10
          },
          "Output":{
            "Url": "http://1500013xxx.vod2.myqcloud.com/xxx/xxx/v.f220.m3u8",
            "Size": 634592,
            "Container": "hls",
            "Height": 324,
            "Width": 640,
            "Bitrate": 561461,
            "Md5": "7ea93ecbcfbff49285cf5be484d4d1d6",
            "Duration": 9.042,
            "VideoStreamSet":[
              {
                "Bitrate": 506583,
                "Codec": "h264",
                "Fps": 24,
                "Height": 324,
                "Width": 640
              }
            ],
            "AudioStreamSet":[
              {
                "Bitrate": 49293,
                "Codec": "aac",
                "SamplingRate": 44100
              }
            ],
            "Definition": 220,
            "DigitalWatermarkType": "None"
          }
        },
        "AdaptiveDynamicStreamingTask": null
      },
      {
        "Type": "AdaptiveDynamicStreaming",
        "TranscodeTask": null,
        "AdaptiveDynamicStreamingTask":{
          "Status": "SUCCESS",
          "ErrCodeExt": "",
          "Message": "SUCCESS",
          "Input":{
            "Definition": 161978,
            "WatermarkSet": [],
            "SubtitleSet": [],
            "TraceWatermark": {
              "Definition": 0,
              "DefinitionForBStream": 0,
              "Switch": ""
            }
          },
          "Output":{
            "Definition": 161978,
            "Package": "HLS",
            "DrmType": "",
            "Url": "http://1500013xxx.vod2.myqcloud.com/xxx/xxx/adp.161978.m3u8",
            "Size": 45552495,
            "DigitalWatermarkType": "None"
          }
        }
      }
    ],
    "SessionContext": "",
    "SessionId": "",
    "TasksPriority": 0,
    "TasksNotifyMode": "Finish"
  }
}
```


### Reliable callback
In the reliable callback mode, after calling the [PullEvents](https://intl.cloud.tencent.com/document/product/266/34183) API, you will receive an HTTP response in the following format (fields with null values are omitted):

```json
{
  "Response": {
    "EventSet":[
      {
        "EventHandle": "830895250939762237",
        "EventType": "ReduceMediaBitrateComplete",
        "ReduceMediaBitrateCompleteEvent": {
          "TaskId": "1500013xxx-ReduceMediaBitrate-10ac18cb58aaf2012475e33991dc59betxxxxx",
          "Status": "FINISH",
          "FileId": "5287852109848150xxx",
          "FileName": "xxx",
          "FileUrl": "http://1500013xxx.vod2.myqcloud.com/xxx/xxx/playlist.f9.mp4",
          "MetaData":{
            "AudioDuration": 359.306,
            "AudioStreamSet":[
              {
                "Bitrate": 130720,
                "Codec": "aac",
                "SamplingRate": 44100
              }
            ],
            "Bitrate": 475103,
            "Container": "mov,mp4,m4a,3gp,3g2,mj2",
            "Duration": 359.362,
            "Height": 224,
            "Rotate": 0,
            "Size": 21341780,
            "VideoDuration": 359.362,
            "VideoStreamSet":[
              {
                "Bitrate": 337666,
                "Codec": "h264",
                "Fps": 24,
                "Height": 224,
                "Width": 440
              }
            ],
            "Width": 440
          },
          "MediaProcessResultSet":[
            {
              "Type": "Transcode",
              "TranscodeTask":{
                "Status": "SUCCESS",
                "ErrCodeExt": "",
                "Message": "SUCCESS",
                "Progress": 100,
                "BeginProcessTime": "2022-09-15T09:54:03Z",
                "FinishTime": "2022-09-15T09:56:22Z",
                "Input":{
                  "Definition": 220,
                  "TraceWatermark": {
                    "Definition": 0,
                    "DefinitionForBStream": 0,
                    "Switch": ""
                  },
                  "WatermarkSet": [
                    {
                      "Definition": 103660,
                      "TextContent": "xxx",
                      "SvgContent": "",
                      "StartTimeOffset": 0,
                      "EndTimeOffset": 0
                    }
                  ],
                  "HeadTailSet": [],
                  "MosaicSet": [
                    {
                      "CoordinateOrigin": "TopLeft",
                      "XPos": "",
                      "YPos": "",
                      "Width": "50%",
                      "Height": "50%",
                      "StartTimeOffset": 0,
                      "EndTimeOffset": 0
                    }
                  ],
                  "StartTimeOffset": 1,
                  "EndTimeOffset": 10
                },
                "Output":{
                  "Url": "http://1500013xxx.vod2.myqcloud.com/xxx/xxx/v.f220.m3u8",
                  "Size": 634592,
                  "Container": "hls",
                  "Height": 324,
                  "Width": 640,
                  "Bitrate": 561461,
                  "Md5": "7ea93ecbcfbff49285cf5be484d4d1d6",
                  "Duration": 9.042,
                  "VideoStreamSet":[
                    {
                      "Bitrate": 506583,
                      "Codec": "h264",
                      "Fps": 24,
                      "Height": 324,
                      "Width": 640
                    }
                  ],
                  "AudioStreamSet":[
                    {
                      "Bitrate": 49293,
                      "Codec": "aac",
                      "SamplingRate": 44100
                    }
                  ],
                  "Definition": 220,
                  "DigitalWatermarkType": "None"
                }
              },
              "AdaptiveDynamicStreamingTask": null
            },
            {
              "Type": "AdaptiveDynamicStreaming",
              "TranscodeTask": null,
              "AdaptiveDynamicStreamingTask":{
                "Status": "SUCCESS",
                "ErrCodeExt": "",
                "Message": "SUCCESS",
                "Input":{
                  "Definition": 161978,
                  "WatermarkSet": [],
                  "SubtitleSet": [],
                  "TraceWatermark": {
                    "Definition": 0,
                    "DefinitionForBStream": 0,
                    "Switch": ""
                  }
                },
                "Output":{
                  "Definition": 161978,
                  "Package": "HLS",
                  "DrmType": "",
                  "Url": "http://1500013xxx.vod2.myqcloud.com/xxx/xxx/adp.161978.m3u8",
                  "Size": 45554187,
                  "DigitalWatermarkType": "None"
                }
              }
            }
          ],
          "SessionContext": "",
          "SessionId": "",
          "TasksPriority": 0,
          "TasksNotifyMode": "Finish"
        }
      }
    ],
    "RequestId": "baa9058f-8c91-4b9c-b519-db7f9a6cd41d"
  }
}
```