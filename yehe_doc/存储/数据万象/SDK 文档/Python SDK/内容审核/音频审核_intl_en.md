## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for audio moderation.

>! COS Python SDK v5.1.9.10 or later is required. Earlier versions may contain bugs and need to be upgraded to the [latest version](https://github.com/tencentyun/cos-python-sdk-v5/releases) when being used.
>

| API | Description    |
| :----------------------------------------------------------- | :------------------------- |
|[Submitting audio moderation job](https://intl.cloud.tencent.com/document/product/436/48262) | Submits an audio moderation job.   |
|[Querying audio moderation job result](https://intl.cloud.tencent.com/document/product/436/48263)  | Queries the result of a specified audio moderation job. |


## Submitting an Audio Moderation Job

#### Feature description

This API is used to submit an audio moderation job. The audio moderation feature is async. You can submit a job to moderate your audio files, and then use the API for querying audio moderation job result to query the moderation results.

#### Sample code

```shell
    """Test the CI's API for moderating audio file content"""
    # Create a COS client
    # Recognize an audio in COS
	response= client.ci_auditing_audio_submit(
		Bucket='bucket',
		DetectType=CiDetectType.PORN | CiDetectType.ADS,
		Key='test.mp3'
	)
	print response
```

#### Parameter description

The `ci_auditing_audio_submit` function is called. Specific request parameters are as follows:

| Parameter | Description | Type | Required |
| --------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket | Bucket name.                                 | String  | Yes       |
| Key | Object name, such as `picture.jpg`.                                 | String  | Yes      |
| BizType | Unique identifier of the moderation policy. You can configure the scenes you want to moderate on the moderation policy page in the console, such as pornographic, adverting, and illegal information. For configuration guidelines, see [Setting Public Moderation Policy](https://intl.cloud.tencent.com/document/product/436/52095). You can get `BizType` in the console. If `BizType` is specified, the moderation request will perform moderation based on the scenes configured in the moderation policy. If `BizType` is not specified, the default moderation policy will be used automatically. | String | No |
| DetectType      | Moderation type. Valid values: `CiDetectType.PORN` (pornography), `CiDetectType.ADS` (advertising). You can select multiple types. For example, `CiDetectType.PORN \| CiDetectType.ADS` indicates to moderate the audio for pornographic and advertising information. If you need more moderation scenes, use the `BizType` parameter.  | enum | No  
| Url | An audio URL that is not in COS can be directly used for moderation.                                 | String  | No       |
| Callback | Callback address, which must start with `http://` or `https://`.              | String    | No       |
| CallbackVersion | Structure of the callback content. Valid values: `Simple` (the callback content contains basic information), `Detail` (the callback content contains detailed information). Default value: `Simple`. | String | No |
| UserInfo | Business field. For details on parameters that can be passed in, see the `UserInfo` field in [Submitting Audio Moderation Job](https://intl.cloud.tencent.com/document/product/436/48262).                            | Dict  | No       |
| DataId | This field will return the original content in the moderation result, which can contain up to 512 bytes. You can use this field to uniquely identify the data to be moderated in your business. | String | No |

#### Response parameters

Calling the `ci_auditing_audio_submit` function will convert the XML returned in the API into a `dict` value. For specific response parameters, see [Submitting Audio Moderation Job](https://intl.cloud.tencent.com/document/product/436/48262).

## Querying Audio Moderation Job Result

#### Feature description

This API is used to query the result of a specified audio moderation job. The audio moderation feature is async. You can submit a job to moderate your audio files, and then use the API for querying audio moderation job result to query the moderation results.

#### Sample code

```shell
    """Test the CI's API for querying moderation job result"""
    # Create a COS client
    # Query the moderation result
	response = client.ci_auditing_audio_query(
		Bucket='bucket',
		JobID='v11122zxxxazzz'
	)
	print response
```

#### Parameter description

The `ci_auditing_audio_query` function is called. Specific request parameters are as follows:

| Parameter | Description | Type | Required |
| --------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket | Bucket name.                                 | String  | Yes       |
| JobID | Moderation job ID.                                | String  | Yes       |

#### Response parameters

Calling the `ci_auditing_audio_query` function will convert the XML returned in the API into a `dict` value. For specific response parameters, see [Querying Audio Moderation Job Result](https://intl.cloud.tencent.com/document/product/436/48263).

