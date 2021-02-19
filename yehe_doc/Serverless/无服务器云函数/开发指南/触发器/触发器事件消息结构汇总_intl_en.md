This document summarizes the message structures of all trigger events that are connected to SCF. For more information on trigger configuration and restrictions, please see [Trigger Management](https://intl.cloud.tencent.com/document/product/583/9705).
>!The event structure of the input parameter passed in by a trigger has been partially defined and can be used directly. You can get and use the Java library through the [Java Cloud Event Definition](https://github.com/tencentyun/scf-java-libs) or the Go library through the [Go Cloud Event Definition](https://github.com/tencentyun/scf-go-lib/tree/master/events).
>

## Event Message Structure of Integration Request for API Gateway Trigger

When an API Gateway trigger receives a request, event data will be sent to the bound function in JSON format as shown below.
```
{
  "requestContext": {
    "serviceId": "service-f94sy04v",
    "path": "/test/{path}",
    "httpMethod": "POST",
    "requestId": "c6af9ac6-****-****-9a41-93e8deadbeef",
    "identity": {
      "secretId": "abdcdxxxxxxxsdfs"
    },
    "sourceIp": "10.0.2.14",
    "stage": "release"
  },
  "headers": {
    "Accept-Language": "en-US,en,cn",
    "Accept": "text/html,application/xml,application/json",
    "Host": "service-3ei3tii4-251000691.ap-guangzhou.apigateway.myqloud.com",
    "User-Agent": "User Agent String"
  },
  "body": "{\"test\":\"body\"}",
  "pathParameters": {
    "path": "value"
  },
  "queryStringParameters": {
    "foo": "bar"
  },
  "headerParameters":{
    "Refer": "10.0.2.14"
  },
  "stageVariables": {
    "stage": "release"
  },
  "path": "/test/value",
  "queryString": {
    "foo" : "bar",
    "bob" : "alice"
  },
  "httpMethod": "POST"
}
```

## Event Message Structure for Timer Trigger

When a function is invoked at a scheduled time, event data will be sent to the bound function in JSON format as shown below.

```
{
    "Type":"Timer",
    "TriggerName":"EveryDay",
    "Time":"2019-02-21T11:49:00Z",
    "Message":"user define msg body"
}
```



## Event Message Structure for COS Trigger

When an object creation or deletion event occurs in the specified COS bucket, event data will be sent to the bound function in JSON format as shown below.
```
{
    "Records": [{
        "cos": {
            "cosSchemaVersion": "1.0",
            "cosObject": {
                "url": "http://testpic-1253970026.cos.ap-chengdu.myqcloud.com/testfile",
                "meta": {
                    "x-cos-request-id": "NWMxOWY4MGFfMjViMjU4NjRfMTUy********ZjM=",
                    "Content-Type": ""
                },
                "vid": "",
                "key": "/1253970026/testpic/testfile",
                "size": 1029
            },
            "cosBucket": {
                "region": "cd",
                "name": "testpic",
                "appid": "1253970026"
            },
            "cosNotificationId": "unkown"
        },
        "event": {
            "eventName": "cos:ObjectCreated:*",
            "eventVersion": "1.0",
            "eventTime": 1545205770,
            "eventSource": "qcs::cos",
            "requestParameters": {
                "requestSourceIP": "192.168.15.101",
                "requestHeaders": {
                    "Authorization": "q-sign-algorithm=sha1&q-ak=AKIDQm6iUh2NJ6jL41tVUis9KpY5Rgv49zyC&q-sign-time=1545205709;1545215769&q-key-time=1545205709;1545215769&q-header-list=host;x-cos-storage-class&q-url-param-list=&q-signature=098ac7dfe9cf21116f946c4b4c29001c2b449b14"
                }
            },
            "eventQueue": "qcs:0:lambda:cd:appid/1253970026:default.printevent.$LATEST",
            "reservedInfo": "",
            "reqid": 179398952
        }
    }]
}
```

## Event Message Structure for CKafka Trigger

When a specified CKafka topic receives a message, the backend consumption module of SCF will consume the message and encapsulate it into an event in JSON format like the one below, which will trigger the bound function and pass the data content as input parameters to the function.
```
{
  "Records": [
    {
      "Ckafka": {
        "topic": "test-topic",
        "partition":1,
        "offset":36,
        "msgKey": "None",
        "msgBody": "Hello from Ckafka!"
      }
    },
    {
      "Ckafka": {
        "topic": "test-topic",
        "partition":1,
        "offset":37,
        "msgKey": "None",
        "msgBody": "Hello from Ckafka again!"
      }
    }
  ]
}
```

## Event Message Structure for CMQ Topic Trigger

When a specified CMQ topic receives a message, event data will be sent to the bound function in JSON format as shown below.
```
{
  "Records": [
    {
      "CMQ": {
        "type": "topic",
        "topicOwner":"120xxxxx",
        "topicName": "testtopic",
        "subscriptionName":"xxxxxx",
        "publishTime": "1970-01-01T00:00:00.000Z",
        "msgId": "123345346",
        "requestId":"123345346",
        "msgBody": "Hello from CMQ!",
        "msgTag": "tag1,tag2"
      }
    }
  ]
}
```


## Event Message Structure for CLS Trigger

When the specified CLS trigger receives a message, the CLS backend consumption module will consume the message and encapsulate it to asynchronously invoke your function. In order to ensure the efficiency of data transfer in a single triggering action, the value of the data field is a Base64-encoded ZIP document.

```
{
  "clslogs": {
    "data": "ewogICAgIm1lc3NhZ2VUeXBlIjogIkRBVEFfTUVTU0FHRSIsCiAgICAib3duZXIiOiAiMTIzNDU2Nzg5MDEyIiwKICAgICJsb2dHcm91cCI6I..."
  }
} 
```

After being decoded and decompressed, the log data will look like the following JSON body (with decoded CLS Logs message data as an example):

```
{
	"topic_id": "xxxx-xx-xx-xx-yyyyyyyy",
	"topic_name": "testname",
	"records": [{
		"timestamp": "1605578090000000",
		"content": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
	}, {
		"timestamp": "1605578090000003",
		"content": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
	}]
}
```

## Event Message Structure for MPS Trigger

When a specified MPS trigger receives a message, the event structures and fields will be as shown below (with the `WorkflowTask` task as an example):

```
{
    "EventType":"WorkflowTask",
    "WorkflowTaskEvent":{
        "TaskId":"245****654-WorkflowTask-f46dac7fe2436c47******d71946986t0",
        "Status":"FINISH",
        "ErrCode":0,
        "Message":"",
        "InputInfo":{
            "Type":"COS",
            "CosInputInfo":{
                "Bucket":"macgzptest-125****654",
                "Region":"ap-guangzhou",
                "Object":"/dianping2.mp4"
            }
        },
        "MetaData":{
            "AudioDuration":11.261677742004395,
            "AudioStreamSet":[
                {
                    "Bitrate":127771,
                    "Codec":"aac",
                    "SamplingRate":44100
                }
            ],
            "Bitrate":2681468,
            "Container":"mov,mp4,m4a,3gp,3g2,mj2",
            "Duration":11.261677742004395,
            "Height":720,
            "Rotate":90,
            "Size":3539987,
            "VideoDuration":10.510889053344727,
            "VideoStreamSet":[
                {
                    "Bitrate":2553697,
                    "Codec":"h264",
                    "Fps":29,
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
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"SUCCESS",
                    "Input":{
                        "Definition":10,
                        "WatermarkSet":[
                            {
                                "Definition":515247,
                                "TextContent":"",
                                "SvgContent":""
                            }
                        ],
                        "OutputStorage":{
                            "Type":"COS",
                            "CosOutputStorage":{
                                "Bucket":"gztest-125****654",
                                "Region":"ap-guangzhou"
                            }
                        },
                        "OutputObjectPath":"/dasda/dianping2_transcode_10",
                        "SegmentObjectName":"/dasda/dianping2_transcode_10_{number}",
                        "ObjectNumberFormat":{
                            "InitialValue":0,
                            "Increment":1,
                            "MinLength":1,
                            "PlaceHolder":"0"
                        }
                    },
                    "Output":{
                        "OutputStorage":{
                            "Type":"COS",
                            "CosOutputStorage":{
                                "Bucket":"gztest-125****654",
                                "Region":"ap-guangzhou"
                            }
                        },
                        "Path":"/dasda/dianping2_transcode_10.mp4",
                        "Definition":10,
                        "Bitrate":293022,
                        "Height":320,
                        "Width":180,
                        "Size":401637,
                        "Duration":11.26200008392334,
                        "Container":"mov,mp4,m4a,3gp,3g2,mj2",
                        "Md5":"31dcf904c03d0cd78346a12c25c0acc9",
                        "VideoStreamSet":[
                            {
                                "Bitrate":244608,
                                "Codec":"h264",
                                "Fps":24,
                                "Height":320,
                                "Width":180
                            }
                        ],
                        "AudioStreamSet":[
                            {
                                "Bitrate":48414,
                                "Codec":"aac",
                                "SamplingRate":44100
                            }
                        ]
                    }
                },
                "AnimatedGraphicTask":null,
                "SnapshotByTimeOffsetTask":null,
                "SampleSnapshotTask":null,
                "ImageSpriteTask":null
            },
            {
                "Type":"AnimatedGraphics",
                "TranscodeTask":null,
                "AnimatedGraphicTask":{
                    "Status":"FAIL",
                    "ErrCode":30010,
                    "Message":"TencentVodPlatErr Or Unkown",
                    "Input":{
                        "Definition":20000,
                        "StartTimeOffset":0,
                        "EndTimeOffset":600,
                        "OutputStorage":{
                            "Type":"COS",
                            "CosOutputStorage":{
                                "Bucket":"gztest-125****654",
                                "Region":"ap-guangzhou"
                            }
                        },
                        "OutputObjectPath":"/dasda/dianping2_animatedGraphic_20000"
                    },
                    "Output":null
                },
                "SnapshotByTimeOffsetTask":null,
                "SampleSnapshotTask":null,
                "ImageSpriteTask":null
            },
            {
                "Type":"SnapshotByTimeOffset",
                "TranscodeTask":null,
                "AnimatedGraphicTask":null,
                "SnapshotByTimeOffsetTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"SUCCESS",
                    "Input":{
                        "Definition":10,
                        "TimeOffsetSet":[

                        ],
                        "WatermarkSet":[
                            {
                                "Definition":515247,
                                "TextContent":"",
                                "SvgContent":""
                            }
                        ],
                        "OutputStorage":{
                            "Type":"COS",
                            "CosOutputStorage":{
                                "Bucket":"gztest-125****654",
                                "Region":"ap-guangzhou"
                            }
                        },
                        "OutputObjectPath":"/dasda/dianping2_snapshotByOffset_10_{number}",
                        "ObjectNumberFormat":{
                            "InitialValue":0,
                            "Increment":1,
                            "MinLength":1,
                            "PlaceHolder":"0"
                        }
                    },
                    "Output":{
                        "Storage":{
                            "Type":"COS",
                            "CosOutputStorage":{
                                "Bucket":"gztest-125****654",
                                "Region":"ap-guangzhou"
                            }
                        },
                        "Definition":0,
                        "PicInfoSet":[
                            {
                                "TimeOffset":0,
                                "Path":"/dasda/dianping2_snapshotByOffset_10_0.jpg",
                                "WaterMarkDefinition":[
                                    515247
                                ]
                            }
                        ]
                    }
                },
                "SampleSnapshotTask":null,
                "ImageSpriteTask":null
            },
            {
                "Type":"ImageSprites",
                "TranscodeTask":null,
                "AnimatedGraphicTask":null,
                "SnapshotByTimeOffsetTask":null,
                "SampleSnapshotTask":null,
                "ImageSpriteTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"SUCCESS",
                    "Input":{
                        "Definition":10,
                        "OutputStorage":{
                            "Type":"COS",
                            "CosOutputStorage":{
                                "Bucket":"gztest-125****654",
                                "Region":"ap-guangzhou"
                            }
                        },
                        "OutputObjectPath":"/dasda/dianping2_imageSprite_10_{number}",
                        "WebVttObjectName":"/dasda/dianping2_imageSprite_10",
                        "ObjectNumberFormat":{
                            "InitialValue":0,
                            "Increment":1,
                            "MinLength":1,
                            "PlaceHolder":"0"
                        }
                    },
                    "Output":{
                        "Storage":{
                            "Type":"COS",
                            "CosOutputStorage":{
                                "Bucket":"gztest-125****654",
                                "Region":"ap-guangzhou"
                            }
                        },
                        "Definition":10,
                        "Height":80,
                        "Width":142,
                        "TotalCount":2,
                        "ImagePathSet":[
                            "/dasda/imageSprite/dianping2_imageSprite_10_0.jpg"
                        ],
                        "WebVttPath":"/dasda/imageSprite/dianping2_imageSprite_10.vtt"
                    }
                }
            }
        ]
    }
}
```

## Event Message Structure for CLB Trigger

When a CLB Gateway trigger receives a request, event data will be sent to the bound function in JSON format as shown below.
```
{  
  "headers": { 
    "Content-type": "application/json",  
    "Host": "test.clb-scf.com",  
    "User-Agent": "Chrome",  

    "X-Stgw-Time": "1591692977.774",  
    "X-Client-Proto": "http",  
    "X-Forwarded-Proto": "http",  
    "X-Client-Proto-Ver": "HTTP/1.1",  
    "X-Real-IP": "9.43.175.219",
    "X-Forwarded-For": "9.43.175.xx"  
 
    "X-Vip": "121.23.21.xx",  
    "X-Vport": "xx",  
    "X-Uri": "/scf_location",  
    "X-Method": "POST"    
    "X-Real-Port": "44347",  
  },  
  "payload": {  
    "key1": "123",  
    "key2": "abc"  
  },
  "isBase64Encoded": "false"
}  
```
