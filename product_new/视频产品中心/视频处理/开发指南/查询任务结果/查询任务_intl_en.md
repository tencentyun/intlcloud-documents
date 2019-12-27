MPS not only can receive notifications of file transcoding results through the [event notification mechanism](https://intl.cloud.tencent.com/document/product/1041/33499), but also supports querying details of a specified transcoding task through the DescribeTaskDetail API. This API is generally used to query the progress and result of a transcoding task that is manually initiated by the ProcessMedia API. In the query result, the task status may be `WAITING`, `PROCESSING`, or `FINISH`.
- **WAITING**: The task has been initiated and is waiting to be processed.
- **PROCESSING**: The task is being processed.
- **FINISH**: The task has been completed processed.

Below are some samples of task status:

**`PROCESSING` sample**
```
{
    "Response":{
        "TaskType":"WorkflowTask",
        "Status":"PROCESSING",
        "CreateTime":"2019-08-08T07:47:08Z",
        "BeginProcessTime":"2019-08-08T07:47:09Z",
        "FinishTime":"0000-00-00T00:00:00Z",
        "WorkflowTask":{
            "TaskId":"2451******-WorkflowTask-fc2172f5******a2e507cece0cb06fbet0",
            "Status":"PROCESSING",
            "ErrCode":0,
            "Message":"",
            "InputInfo":{
                "Type":"COS",
                "CosInputInfo":{
                    "Bucket":"macvc-1251132654",
                    "Region":"ap-chengdu",
                    "Object":"/abvc/111/2222/15692847.mp4"
                }
            },
            "MetaData":{
                "AudioDuration":204.2779998779297,
                "AudioStreamSet":[
                    {
                        "Bitrate":127999,
                        "Codec":"mp3",
                        "SamplingRate":44100
                    }
                ],
                "Bitrate":1232376,
                "Container":"mov,mp4,m4a,3gp,3g2,mj2",
                "Duration":204.2919921875,
                "Height":720,
                "Rotate":0,
                "Size":31647438,
                "VideoDuration":204.2919921875,
                "VideoStreamSet":[
                    {
                        "Bitrate":1104377,
                        "Codec":"h264",
                        "Fps":24,
                        "Height":720,
                        "Width":1280
                    }
                ],
                "Width":1280
            },
            "MediaProcessResultSet":[
                {
                    "Type":"Transcode",
                    "TranscodeTask":{
                        "Status":"PROCESSING",
                        "ErrCode":0,
                        "Message":"SUCCESS",
                        "Input":{
                            "Definition":10,
                            "WatermarkSet":[

                            ],
                            "OutputStorage":{
                                "Type":"COS",
                                "CosOutputStorage":{
                                    "Bucket":"macyin**-12511*****",
                                    "Region":"ap-beijing"
                                }
                            },
                            "OutputObjectPath":"/15692847_transcode_10",
                            "SegmentObjectName":"/15692847_transcode_10_{number}",
                            "ObjectNumberFormat":{
                                "InitialValue":0,
                                "Increment":1,
                                "MinLength":1,
                                "PlaceHolder":"0"
                            }
                        },
                        "Output":null
                    },
                    "AnimatedGraphicTask":null,
                    "SnapshotByTimeOffsetTask":null,
                    "SampleSnapshotTask":null,
                    "ImageSpriteTask":null
                }
            ]
        },
        "TaskNotifyConfig":{
            "CmqModel":"Queue",
            "CmqRegion":"gz",
            "QueueName":"macvtstest",
            "TopicName":"",
            "NotifyMode":"Change"
        },
        "TasksPriority":10,
        "SessionId":"100",
        "SessionContext":"100",
        "RequestId":"13499555-145a-47f5-b6f6-64e829ed3b20"
    }
}
```

**`FINISH` example**
```
{
  "Response": {
    "TaskType": "WorkflowTask",
    "Status": "FINISH",
    "CreateTime": "2019-07-16T06:21:27Z",
    "BeginProcessTime": "2019-07-16T06:21:28Z",
    "FinishTime": "2019-07-16T06:21:46Z",
    "WorkflowTask": {
      "TaskId": "235303****-WorkflowTask-80108cc3380155d98b2e3573a48a******",
      "Status": "FINISH",
      "ErrCode": 0,
      "Message": "",
      "InputInfo": {
        "Type": "COS",
        "CosInputInfo": {
          "Bucket": "vodtestbj-235303****",
          "Region": "ap-beijing",
          "Object": "/input/videoplayback.mp4"
        }
      },
      "MetaData": {
        "AudioDuration": 380.9465637207031,
        "AudioStreamSet": [
          {
            "Bitrate": 95999,
            "Codec": "aac",
            "SamplingRate": 44100
          }
        ],
        "Bitrate": 409657,
        "Container": "mov,mp4,m4a,3gp,3g2,mj2",
        "Duration": 380.9465637207031,
        "Height": 360,
        "Rotate": 0,
        "Size": 19626862,
        "VideoDuration": 380.8804931640625,
        "VideoStreamSet": [
          {
            "Bitrate": 313658,
            "Codec": "h264",
            "Fps": 29,
            "Height": 360,
            "Width": 480
          }
        ],
        "Width": 480
      },
      "MediaProcessResultSet": [
        {
          "Type": "Transcode",
          "TranscodeTask": {
            "Status": "SUCCESS",
            "ErrCode": 0,
            "Message": "SUCCESS",
            "Input": {
              "Definition": 210,
              "WatermarkSet": [],
              "OutputStorage": {
                "Type": "COS",
                "CosOutputStorage": {
                  "Bucket": "vodtestgz-235303****",
                  "Region": "ap-guangzhou"
                }
              },
              "OutputObjectPath": "/output/{inputName}_transcode_{definition}.{format}",
              "SegmentObjectName": "/output/{inputName}_transcode_{definition}_{number}",
              "ObjectNumberFormat": {
                "InitialValue": 0,
                "Increment": 1,
                "MinLength": 1,
                "PlaceHolder": ""
              }
            },
            "Output": {
              "OutputStorage": {
                "Type": "COS",
                "CosOutputStorage": {
                  "Bucket": "vodtestgz-235303****",
                  "Region": "ap-guangzhou"
                }
              },
              "Path": "/output/videoplayback_transcode_210.m3u8",
              "Definition": 210,
              "Bitrate": 353297,
              "Height": 240,
              "Width": 320,
              "Size": 5692,
              "Duration": 380.9580078125,
              "Container": "hls,applehttp",
              "Md5": "ae0dfe7c7336291d6243463b7bb14fea",
              "VideoStreamSet": [
                {
                  "Bitrate": 302307,
                  "Codec": "h264",
                  "Fps": 24,
                  "Height": 240,
                  "Width": 320
                }
              ],
              "AudioStreamSet": [
                {
                  "Bitrate": 50990,
                  "Codec": "aac",
                  "SamplingRate": 44100
                }
              ]
            }
          },
          "AnimatedGraphicTask": null,
          "SnapshotByTimeOffsetTask": null,
          "SampleSnapshotTask": null,
          "ImageSpriteTask": null
        }
      ]
    },
    "TaskNotifyConfig": null,
    "TasksPriority": 0,
    "SessionId": "",
    "SessionContext": "",
    "RequestId": "requestId"
  }
}
```
<!--For more information on relevant structures and fields, please see [DescribeTaskDetail API Document]().-->
