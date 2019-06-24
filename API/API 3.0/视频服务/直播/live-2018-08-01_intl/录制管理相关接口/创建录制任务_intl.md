## 1. API Description

API request domain name: live.tencentcloudapi.com.

- Prerequisites
  1. Recording files are stored on the VOD platform, so if you need to use the recording feature, you must first activate the VOD service.
  2. After the recording files are stored, applicable fees (including storage fees and downstream playback traffic fees) are charged according to the VOD billing method. For details, see the [corresponding document](https://cloud.tencent.com/document/product/266/2838).

- Mode description
  This API supports two recording modes:
  1. Scheduled recording mode **(default mode)**.
    You need to set the start time and end time; the recording task automatically starts and ends based on the timeframe you set.
  2. Real-time video recording mode.
    You don't need to set the start time as the recording starts as soon as the task is created. You can record up to 30 minutes. If you set an end time 30 minutes later than the current time, the time difference will be counted as 30 minutes. This feature is for recording highlights in the video, so we recommend you keep the length of each record no longer than 5 minutes.

- Notes

    ! The API call timeout should be set to more than 3 seconds; otherwise, retries and frequent calls may result in repeated recording tasks.

Default API request rate limit: 100 requests/second.

## 2. Request Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all  requests, see [Common Request Parameters](/document/api/267/20459).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: CreateLiveRecord |
| Version | Yes | String | Common parameter; the version of this API: 2018-08-01 |
| Region | No | String | Common parameter; optional for this API |
| StreamName | Yes | String | Stream name |
| AppName | No | String | Upstream app name |
| DomainName | No | String | Upstream domain name. This parameter has to be set for multi-domain push. |
| StartTime | No | String | Recording start time. This is China standard time, and URL-encoding is required. For example, 2017-01-01 10:10:01 is encoded as 2017-01-01+10%3a10%3a01. <br/>Required for the scheduled recording mode; ignore it when using the real-time video recording mode. |
| EndTime | No | String | Recording end time. This is China standard time, and URL-encoding is required. For example, 2017-01-01 10:30:01 is encoded as 2017-01-01+10%3a30%3a01. <br/>Required for the scheduled recording mode; optional for the real-time video recording mode. When you set real-time video recording mode through the Highlight parameter, you must set an end time no later than 30 minutes after the current time. If the difference between the end time and the current time is larger than 30 minutes, or you leave this parameter blank, the actual end time will be 30 minutes after the current time. |
| RecordType | No | String | Recording type. <br/>"video": audio-video recording **(default)**. <br/>"audio": audio recording. <br/>In both scheduled and real-time video recording modes, this parameter is valid and is not case sensitive. |
| FileFormat | No | String | Recording file format. Valid values: <br/>"flv", "hls", "mp4", "aac", "mp3"; "flv" by default. <br/>In both scheduled and real-time video recording modes, this parameter is valid and is not case sensitive. |
| Highlight | No | Integer | This is the mark for enabling real-time video recording mode. 0: real-time video recording mode is disabled, i.e., scheduled recording mode is used **(default)**; 1: real-time video recording mode is enabled. |
| MixStream | No | Integer | This is the mark for enabling A+B=C mixed stream recording. 0: A+B=C mixed stream recording is disabled **(default)**; 1: A+B=C mixed stream recording is enabled. <br/>In both scheduled and real-time video recording modes, this parameter is valid. |
| StreamParam | No | String | Recording stream parameter. The following parameters are currently supported: <br/>record_interval: recording interval in seconds, value range: 1800-7200 <br/>storage_time: recording file storage period in seconds <br/>E.g., record_interval=3600&storage_time=2592000 <br/>Note: The parameters needs to be URL-encoded. <br/>In both scheduled and real-time video recording modes, this parameter is valid. |

## 3. Return Parameters
| Parameter name | Type | Description |
|---------|---------|---------|
| TaskId | Integer | The task ID which uniquely identifies the recording task globally |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

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

**API Explorer is a tool that provides ease of use in requesting APIs, authenticating identities, generating SDK and exploring APIs in Tencent Cloud environment. **

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

The following error codes are API business logic-related. For other error codes, see [Common Error Codes](/document/api/267/20461#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error |
| InvalidParameter | Parameter error |
| InvalidParameterValue | Incorrect parameter value |

