## 이벤트 이름
ReduceMediaBitrateComplete

## 이벤트 설명
App에 이벤트 알림이 설정된 경우 동영상 합성 완료 후 App 백엔드는 ‘일반 콜백’ 또는 ‘신뢰할 수 있는 콜백’을 통해 이벤트 알림을 받을 수 있습니다. 이벤트 알림의 내용은 [ReduceMediaBitrateTask 구조](https://intl.cloud.tencent.com/document/product/266/34187#ReduceMediaBitrateTask)입니다.

## 예시
### 일반 콜백
일반 콜백 모드를 선택하면 콜백 URL은 아래와 같이 BODY에 내용이 있는 VOD로부터 HTTP POST 요청을 수신합니다(null 값이 있는 필드는 생략됨).

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


### 신뢰할 수 있는 콜백
신뢰할 수 있는 콜백 모드를 선택하면 [PullEvents](https://intl.cloud.tencent.com/document/product/266/34183) API가 호출된 후 다음 형식의 HTTP 응답이 수신됩니다(null 값이 있는 필드는 생략됨).

```json
{
  "Response":{
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