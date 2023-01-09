
## Overview

This document describes how to use CI's speech recognition template SDK.

| API | Operation |  Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [Creating automatic speech recognition template](https://intl.cloud.tencent.com/document/product/436/50157) | Creates a template | Creating a template |
| Deleting automatic speech recognition template | Deletes a template | Deleting a template |
| [DescribeTemplates](https://intl.cloud.tencent.com/document/product/436/50159) | Queries templates | Querying the list of templates. |
| [Updating automatic speech recognition template](https://intl.cloud.tencent.com/document/product/436/50160) | Modifies a template | Modifying a template |

## Basic Operations

### Creating template

#### Feature description

This API is used to create a template.

#### Method prototype

```py
def ci_create_asr_template(self, Bucket, Name, EngineModelType, ChannelNum,
                           ResTextFormat, FilterDirty=0, FilterModal=0, ConvertNumMode=0, SpeakerDiarization=0,
                           SpeakerNumber=0, FilterPunc=0, OutputFileType='txt', **kwargs)
```

#### Parameter description

`Request` has the following sub-nodes:

| Node Name (Keyword) | Description | Type | Required |
| ------------------ | -------------------------------------------------------- | --------- | ---- |
| Bucket | Bucket name | String | Yes |
| Name               | Template name, which can contain letters, digits, underscores (_), hyphens (-), and asterisks (*).                    | String    | Yes   |
| EngineModelType    | Engine model type, divided into phone call and non-phone call scenarios. <br>Phone call scenarios: <br><li>`8k_zh`: 8 kHz, for Mandarin in general scenarios (available for dual-channel audio). <br><li>`8k_zh_s`: 8 kHz, for Mandarin with speaker separation (available for mono-channel audio only). <br><li>`8k_en`: 8 kHz, for English. <br>Non-phone call scenarios: <br><li>`16k_zh`: 16 kHz, for Mandarin in general scenarios. <br><li>`16k_zh_video`: 16 kHz, for audio/video scenarios. <br><li>`16k_en`: 16 kHz, for English. <br><li>`16k_ca`: 16 kHz, for Cantonese. <br><li>`16k_ja`: 16 kHz, for Japanese. <br><li>`16k_zh_edu`: For Mandarin in education scenarios. <br><li>`16k_en_edu`: For English in education scenarios. <br><li>`16k_zh_medical`: For healthcare scenarios. <br><li>`16k_th`: For Thai. <br><li>`16k_zh_dialect`: Multi-dialect, for up to 23 dialects.                                               | String | Yes   |
| ChannelNum         | Number of sound channels: <br><li>`1`: Mono. If `EngineModelType` is not the phone call scenario, only mono channel is supported. <br><li>`2`: Dual (for the 8k_zh engine only, where the two channels correspond to the caller and callee respectively).                                           | int | No   |
| ResTextFormat      | Format of the returned recognition result. <br><li>`0`: Recognition result text, including the list of segment timestamps. <br><li>`1`: Detailed word-level recognition result, excluding punctuation marks but including the speech speed value (the list of word timestamps, generally used to generate subtitles). <br><li>`2`: Detailed word-level recognition result, including punctuation marks and the speech speed value.  | int | Yes       |
| FilterDirty        | Whether to filter restricted words (for the Mandarin engine only). <br><li>`0`: Does not filter. <br><li>`1`: Filters. <br><li>`2`: Replaces restricted words with `*`. <br><li>Default value: `0`. | int | No       |
| FilterModal        | Whether to filter modal particles (for the Mandarin engine only). <br><li>`0`: Does not filter. <br><li>`1`: Filters partially. <br><li>`2`: Filters strictly. <br><li>Default value: `0`. | int | No       |
| ConvertNumMode     | Whether to intelligently convert Chinese numbers to Arabic numerals (for the Mandarin engine only): <br><li>`0`: Directly outputs Chinese numbers. <br><li>`1`: Intelligently converts based on the scenario. <br><li>`3`: Enables mathematic number conversion. <br><li>Default value: `0`.| int | No       |
| SpeakerDiarization | Whether to enable speaker separation: <br><li>`0`: No. <br><li>`1`: Yes (for mono-channel audios with the 8k_zh, 16k_zh, or 16k_zh_video engine only). <br><li>Default value: `0`. <br><li>Note: In the 8 kHz phone call scenario, we recommend you use dual channels to distinguish between the caller and callee by setting `ChannelNum=2`, so you don't need to enable speaker separation. | int | No       |
| SpeakerNumber      | Number of speakers to be separated (with speaker separation enabled). Value range: 0–10. <br><li>`0`: Automatic separation (currently only for six or fewer people only). 1–10: Specified number of speakers to be separated. Default value: `0`. | int | No       |
| FilterPunc         | Whether to filter punctuation marks (currently for the Mandarin engine only): <br><li>`0`: Does not filter. <br><li>`1`: Filters the punctuation mark at the end of the sentence. <br><li>`2`: Filters all punctuation marks. <br><li>Default value: `0`. | int | No       |
| OutputFileType     | Output file type. Valid values: `txt` (default), `srt`. | String | No       |

#### Sample request

```py
def ci_create_asr_template():
    # Create a speech recognition template
    response = client.ci_create_asr_template(
        Bucket=bucket_name,
        Name='templateName',
        EngineModelType='16k_zh',
        ChannelNum=1,
        ResTextFormat=2,
    )
    print(response)
    return response
```
#### Response description

```py
{
    'RequestId': 'NjMyMjliMWZfZWM0YTYyNjRfNWNmNF8xMDBh', 
    'Template': {
        'TemplateId': 't1c1287c04c147443da0b2cc7b8fbabf32', 
        'Name': 'templateName', 
        'State': 'Normal', 
        'Tag': 'SpeechRecognition', 
        'CreateTime': '2022-09-15T11:25:19+0800', 
        'UpdateTime': '2022-09-15T11:25:19+0800', 
        'BucketId': 'testpic-1253960454', 
        'Category': 'Custom', 
        'SpeechRecognition': {
            'EngineModelType': '16k_zh', 
            'ChannelNum': '1', 
            'ResTextFormat': '2', 
            'FilterDirty': '0', 
            'FilterModal': '0', 
            'ConvertNumMode': '0', 
            'SpeakerDiarization': '0', 
            'SpeakerNumber': '0', 
            'FilterPunc': '0', 
            'OutputFileType': 'txt'
        }
    }
}
```
For more information on response fields, see the response in [Creating Speech Recognition Template](https://intl.cloud.tencent.com/document/product/1045/50303).

### Deleting template

#### Feature description
This API is used to delete a template.
#### Method prototype

```py
def ci_delete_asr_template(self, Bucket, TemplateId, **kwargs)
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---------- | ------------------------------------------------------------ | ------ |-----|
| Bucket | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| TemplateId | ID of the template to be canceled | String | Yes |

#### Sample request

```py
def ci_delete_asr_template():
    # Delete the specified speech recognition template
    response = client.ci_delete_asr_template(
        Bucket=bucket_name,
        TemplateId='t1bdxxxxxxxxxxxxxxxxx94a9',
    )
    print(response)
    return response
```

#### Response description

```py
{
    'RequestId': 'NjMyMjlkZmRfZWM0YTYyNjRfNWNmNF8xMDBi', 
    'TemplateId': 't1c1287c04c147443da0b2cc7b8fbabf32'
}
```
For more information on response fields, see the response in DeleteTemplate.

### Querying template list

#### Feature description
This API is used to query the template list.
#### Method prototype

```py
def ci_get_asr_template(self, Bucket, Category='Custom', Ids='', Name='', PageNumber=1, PageSize=10, **kwargs)
```

#### Parameter description

| Parameter | Description | Type | Required |
|:---           |:--                    |   :--     |   :--    |
| Bucket | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| Category  | Template category: `Custom` or `Official`. Default value: `Custom`. | String  | No |
| Ids       | Template ID. If you enter multiple IDs, separate them by comma.  | String     |No|
| Name      | Template name prefix              | String     |No|
| PageNumber| Page number                   | Integer     |No|
| PageSize  | Number of entries per page                 | Integer     |No|

#### Sample request

```py
def ci_get_asr_template():
    # Get the information of speech recognition templates
    response = client.ci_get_asr_template(
        Bucket=bucket_name,
    )
    print(response)
    return response
```

#### Response description

```py
{
    'TotalCount': '1', 
    'RequestId': 'NjMyMjljNTlfMTIwNjUzMDlfMmUzYV8xMWNh', 
    'PageNumber': '1', 
    'PageSize': '10', 
    'TemplateList': [
        {
            'TemplateId': 't1c1287c04c147443da0b2cc7b8fbabf32', 
            'Name': 'templateName', 
            'State': 'Normal', 
            'Tag': 'SpeechRecognition', 
            'CreateTime': '2022-09-15T11:25:19+0800', 
            'UpdateTime': '2022-09-15T11:25:19+0800', 
            'BucketId': 'testpic-1253960454', 
            'Category': 'Custom', 
            'SpeechRecognition': {
                'EngineModelType': '16k_zh', 
                'ChannelNum': '1', 
                'ResTextFormat': '2', 
                'FilterDirty': '0', 
                'FilterModal': '0', 
                'ConvertNumMode': '0', 
                'SpeakerDiarization': '0', 
                'SpeakerNumber': '0', 
                'FilterPunc': '0', 
                'OutputFileType': 'txt'
            }
        }
    ]
}
```
For more information on response fields, see the response in [DescribeTemplates](https://www.tencentcloud.com/document/product/1045/51271).

### Modifying template

#### Feature description
This API is used to modify a template.
#### Method prototype

```py
def ci_update_asr_template(self, Bucket, TemplateId, Name, EngineModelType, ChannelNum,
                           ResTextFormat, FilterDirty=0, FilterModal=0, ConvertNumMode=0, SpeakerDiarization=0,
                           SpeakerNumber=0, FilterPunc=0, OutputFileType='txt', **kwargs)  
```

#### Parameter description

| Node Name (Keyword) | Description | Type | Required |
|:---|:--|:--|:--|
| bucketName| Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| templateId| ID of the template to be modified |String|Yes|

>? Other parameters are the same as those of the template creation API as described in [Creating Speech Recognition Template](https://intl.cloud.tencent.com/document/product/1045/50303).

#### Sample request

```py
def ci_update_asr_template():
    # Modify a speech recognition template
    response = client.ci_update_asr_template(
        Bucket=bucket_name,
        TemplateId='t1bdxxxxxxxxxxxxxxxxx94a9',
        Name='QueueId1',
        EngineModelType='16k_zh',
        ChannelNum=1,
        ResTextFormat=1,
    )
    print(response)
    return response
```

#### Response description

```py
{
    'RequestId': 'NjMyMjlkNzhfMTIwNjUzMDlfMmUxZF8xMGM4', 
    'Template': {
        'TemplateId': 't1c1287c04c147443da0b2cc7b8fbabf32', 
        'Name': 'QueueId1', 
        'State': 'Normal', 
        'Tag': 'SpeechRecognition', 
        'CreateTime': '2022-09-15T11:25:19+0800', 
        'UpdateTime': '2022-09-15T11:35:20+0800', 
        'BucketId': 'testpic-1253960454', 
        'Category': 'Custom', 
        'SpeechRecognition': {
            'EngineModelType': '16k_zh', 
            'ChannelNum': '1', 
            'ResTextFormat': '1', 
            'FilterDirty': '0', 
            'FilterModal': '0', 
            'ConvertNumMode': '0', 
            'SpeakerDiarization': '0', 
            'SpeakerNumber': '0', 
            'FilterPunc': '0', 
            'OutputFileType': 'txt'
        }
    }
}
```
For more information on response fields, see the response in [Updating Speech Recognition Template](https://intl.cloud.tencent.com/document/product/1045/50317).
