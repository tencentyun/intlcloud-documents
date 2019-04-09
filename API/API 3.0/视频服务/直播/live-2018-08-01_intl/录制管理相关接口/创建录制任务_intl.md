## 1. API Description

API request domain name: live.tencentcloudapi.com.

- Prerequisites
  1. Recording files are stored on the VOD platform, so if you need to use the recording feature, you must first activate the VOD service.
  2. After the recording files are stored, applicable fees (including storage fees and downstream playback traffic fees) are charged according to the VOD billing method. For details, see the [corresponding document](https://cloud.tencent.com/document/product/266/2838).

- Mode description
  This API supports two recording modes:
  1. Scheduled recording mode **(default mode)**.
    The start time and end time need to be passed in, and the recording task automatically starts and ends based on the time parameters.
  2. Real-time video recording mode.
    The start time passed in is ignored, and recording is started immediately after the recording task is created. The recording duration can be up to 30 minutes. If the end time passed in is more than 30 minutes after the current time, it will be counted as 30 minutes. Real-time video recording is mainly used for recording highlight scenes, and it is recommended to keep the duration within 5 minutes.

- Precautions
  1. The API call timeout should be set to more than 3 seconds; otherwise, retries and frequent calls may result in repeated recording tasks.

Default API request frequency limit: 100 times/second.

## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/267/20459).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: CreateLiveRecord |
| Version | Yes | String | Common parameter; the value for this API: 2018-08-01 |
| Region | No | String | Common parameter; not passed in for this API |
| StreamName | Yes | String | Stream name |
| AppName | No | String | Push app name |
| DomainName | No | String | Push domain name. This parameter has to be set for multi-domain push. |
| StartTime | No | String | Recording start time. This is China standard time, and URL-encoding is required. For example, 2017-01-01 10:10:01 is encoded as 2017-01-01+10%3a10%3a01. <br/>In scheduled recording mode, this field must be set; in real-time video recording mode, this field is ignored. |
| EndTime | No | String | Recording end time. This is China standard time, and URL-encoding is required. For example, 2017-01-01 10:30:01 is encoded as 2017-01-01+10%3a30%3a01. <br/>In scheduled recording mode, this field must be set; in real-time video recording mode, this field is optional. If the recording is set to real-time video recording mode through the Highlight parameter, the end time set should not be more than 30 minutes after the current time. If the set end time is more than 30 minutes after the current time, older than the current time or left blank, the actual end time will be 30 minutes after the current time. |
| RecordType | No | String | Recording type. <br/>"video": audio-video recording **(default)**. <br/>"audio": audio recording. <br/>In both scheduled and real-time video recording modes, this parameter is valid and is not case sensitive. |
| FileFormat | No | String | Recording file format. Value range: <br/>"flv", "hls", "mp4", "aac", "mp3"; "flv" by default. <br/>In both scheduled and real-time video recording modes, this parameter is valid and is not case sensitive. |
| Highlight | No | Integer | This is the mark for enabling real-time video recording mode. 0: real-time video recording mode is disabled, i.e., scheduled recording mode is used **(default)**; 1: real-time video recording mode is enabled. |
| MixStream | No | Integer | This is the mark for enabling A+B=C mixed stream recording. 0: A+B=C mixed stream recording is disabled **(default)**; 1: A+B=C mixed stream recording is enabled. <br/>In both scheduled and real-time video recording modes, this parameter is valid. |
| StreamParam | No | String | Recording stream parameter. The following parameters are currently supported: <br/>record_interval: recording interval in seconds, value range: 1800-7200 <br/>storage_time: recording file storage period in seconds <br/>E.g., record_interval=3600&storage_time=2592000 <br/>Note: The parameters needs to be URL-encoded. <br/>In both scheduled and real-time video recording modes, this parameter is valid. |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TaskId | Integer | The task ID which uniquely identifies the recording task globally |
| RequestId | String | The unique request ID which is returned for each request The RequestId for the current request needs to be provided when troubleshooting |

## 4. Sample

### Request Sample

#### Input Sample Code

```
https://live.tencentcloudapi.com/?Action=CreateLiveRecord
&AppName=live
&DomainName=5000.live.push.com
&StreamName=livetest
&StartTime=2018-09-11+12%3a04%3a01
&EndTime=2018-09-11+12%3a08%3a01
&RecordType=video
&FileFormat=flv
&Highlight=0
&MixStream=0
&<Common request parameter>
```

#### Output Sample Code

```
{
    "Response": {
        "RequestId": "eac6b301-a322-493a-8e36-83b295459397",
        "TaskId": 1234
    }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=live&Version=2018-08-01&Action=CreateLiveRecord)

### SDK

Cloud API 3.0 comes with a set of complementary development toolkits (SDKs) that support multiple programming languages and make it easier to call the API.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

Only the error codes related to the API business logic are listed below. For other error codes, see [Common Error Codes](/document/api/267/20461#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error |
| InvalidParameter | Parameter error |
| InvalidParameterValue | Incorrect parameter value |

