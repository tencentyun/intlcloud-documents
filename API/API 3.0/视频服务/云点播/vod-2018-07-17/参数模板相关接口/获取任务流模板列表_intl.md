## 1. API Description
API domain name: vod.tencentcloudapi.com.  
This API gets the list of task flow template details by task flow template name.  
Default API request rate limit: 100 requests/sec.

## 2. Input Parameters
The following parameters are required for requesting this API, including action-specific parameters and common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/266/31756). 

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: DescribeProcedureTemplates |
| Version | Yes | String | Common parameter; the version of this API: 2018-07-17 |
| Region | No | String | Common parameter; optional for this API |
| Names.N | No | Array of String | Name filter of the task flow template; array length limit: 100. |
| Offset | No | Integer | Paged offset; 0 by default. |
| Limit | No | Integer | Number of returned entries; 10 by default, up to 100. |
| SubAppId | No | Integer | ID of the VOD [sub-application](/document/product/266/14574). Input the ID of the sub-application that has the desired resources; otherwise, leave it blank. |
## 3. Output Parameters
| Parameter name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Number of eligible entries. |
| ProcedureTemplateSet | Array of [ProcedureTemplate](/document/api/266/31773#ProcedureTemplate) | List of task flow template details. |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |
## 4. Sample
### Sample 1. Querying a Specified Task Flow Template
Query the details of the task flow template named "My Task Flow A"
#### Input Sample Code
```
https://vod.tencentcloudapi.com/?Action=DescribeProcedureTemplates
&Names.0=My Task Flow A
&<Common request parameter>
```
#### Output Sample Code
```
{
  "Response": {
    "TotalCount": 1,
    "ProcedureTemplateSet": [
      {
        "Name": "My Task Flow A",
        "MediaPrcoessTask": {
          "TranscodeTaskSet": [
            {
              "Definition": 20,
              "WatermarkSet": null
            },
            {
              "Definition": 30,
              "WatermarkSet": null
            },
            {
              "Definition": 40,
              "WatermarkSet": null
            }
          ],
          "AnimatedGraphicTaskSet": null,
          "SnapshotByTimeOffsetTaskSet": null,
          "SampleSnapshotTaskSet": null,
          "ImageSpriteTaskSet": null,
          "CoverBySnapshotTaskSet": null
        },
        "AiContentReviewTask": null,
        "AiAnalysisTask": null,
        "AiRecognitionTask": null
      }
    ],
    "RequestId": "6ca31e3a-6b8e-4b4e-9256-fdc700064ef3"
  }
}
```
### Sample 2. Querying All Task Flow Templates
Query the details of all task flow templates (3 templates are queried)
#### Input Sample Code
```
https://vod.tencentcloudapi.com/?Action=DescribeProcedureTemplates
&<Common request parameter>
```
#### Output Sample Code
```
{
  "Response": {
    "TotalCount": 3,
    "ProcedureTemplateSet": [
      {
        "Name": "My Task Flow A",
        "MediaPrcoessTask": {
          "TranscodeTaskSet": [
            {
              "Definition": 20,
              "WatermarkSet": null
            },
            {
              "Definition": 30,
              "WatermarkSet": null
            },
            {
              "Definition": 40,
              "WatermarkSet": null
            }
          ],
          "AnimatedGraphicTaskSet": null,
          "SnapshotByTimeOffsetTaskSet": null,
          "SampleSnapshotTaskSet": null,
          "ImageSpriteTaskSet": null,
          "CoverBySnapshotTaskSet": null
        },
        "AiContentReviewTask": null,
        "AiAnalysisTask": null,
        "AiRecognitionTask": null
      },
      {
        "Name": "My Task Flow Template B",
        "MediaPrcoessTask": {
          "TranscodeTaskSet": [
            {
              "Definition": 20,
              "WatermarkSet": [
                {
                  "Definition": 15780,
                  "TextContent": null
                }
              ]
            },
            {
              "Definition": 30,
              "WatermarkSet": [
                {
                  "Definition": 15780,
                  "TextContent": null
                }
              ]
            },
            {
              "Definition": 40,
              "WatermarkSet": [
                {
                  "Definition": 15780,
                  "TextContent": null
                }
              ]
            }
          ],
          "AnimatedGraphicTaskSet": null,
          "SnapshotByTimeOffsetTaskSet": null,
          "SampleSnapshotTaskSet": null,
          "ImageSpriteTaskSet": null,
          "CoverBySnapshotTaskSet": null
        },
        "AiContentReviewTask": null,
        "AiAnalysisTask": null,
        "AiRecognitionTask": null
      },
      {
        "Name": "My Task Flow Template C",
        "MediaPrcoessTask": null,
        "AiContentReviewTask": {
          "Definition": 10
        },
        "AiAnalysisTask": null,
        "AiRecognitionTask": null
      }
    ],
    "RequestId": "6ca31e3a-6b8e-4b4e-9256-fdc700064ef3"
  }
}
```
## 5. Developer Resources
### API Explorer
**API Explorer is a tool that provides ease of use in requesting APIs, authenticating identities, generating SDK and exploring APIs in Tencent Cloud environment.**
* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=vod&Version=2018-07-17&Action=DescribeProcedureTemplates)

### SDK
TencentCloud API 3.0 integrates software development toolkits (SDKs) that support various programming languages to make it easier for you to call the APIs.
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
| InvalidParameterValue.Limit | The value of *Limit* is invalid. |
| InvalidParameterValue.Names | The number of elements allowed in array *Names* is exceeded. |


