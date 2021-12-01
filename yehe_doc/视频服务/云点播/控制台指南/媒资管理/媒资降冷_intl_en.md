## Overview
You can perform cold storage operations on VOD resources in the VOD console. VOD supports cold storage based on policy and batch cold storage based on `FileId`.
>!When you perform cold storage for media assets, it will take effect for all files under the `FileId`, including files related to transcoding, adaptive bitrate streaming, and screencapturing.


## Custom Rule-based Cold Storage Policy
1. Log in to the VOD console and select **Media Assets** > [**Cold Storage**](https://console.cloud.tencent.com/vod/pics) to enter the **Custom Rule-based** tab page.
![](https://qcloudimg.tencent-cloud.cn/raw/489e80b1035adb73926db9b6d46b0725.png)


| Attribute | Description | 
|---------|---------|
| Policy ID/Name | Unique identifier of a media asset cold storage policy in VOD. You can set cold storage rules by adding or editing a cold storage policy. | 
| Storage Type| Storage class of a media asset after cold storage based on the policy, including STANDARD_IA, ARCHIVE, and DEEP_ARCHIVE. | 
| Creation Time | Time when the policy is created. | 
| Enabled/Disabled | Whether the policy is enabled. | 
| Operation | Policies can be disabled and deleted. | 
>?
>- You can create up to 10 custom rule-based cold storage policies under an account.
>- Enabled cold storage policies will be executed at 00:00 every day for all storage data under the current application.
>- If multiple cold storage policies hit a media asset at the same time, the media asset will be stored in the following priority order: DEEP_ARCHIVE > ARCHIVE > STANDARD_IA.


 
## FileId-based Cold Storage
1. Log in to the VOD console, select **Media Assets** > [**Cold Storage**](https://console.cloud.tencent.com/vod/pics), and click the **FileId-based** tab. You can trigger cold storage by `FileId`.
![](https://qcloudimg.tencent-cloud.cn/raw/0eb7eb77ed62962fd26f353ae79a434a.png)
>?FileId-based cold storage supports up to 100 `FileId` values at a time.


## Creating Custom Rule-based Cold Storage Policy
1. Click **Create Policy** and enter the policy name, which can contain up to 20 letters, digits, spaces, underscores, hyphens, and dots.
![](https://qcloudimg.tencent-cloud.cn/raw/3ef4fa3afca1eac8a4fac27a186efdb1.png)
2. Cold storage policy: the final storage class of a media asset file based on the cold storage policy, which supports only one storage class.
![](https://qcloudimg.tencent-cloud.cn/raw/8d8d508d682f1adc9ace2b0c78ae0fbe.png)
3. Policy configuration: you can configure different policies to implement the cold storage logic.
 - Time: you can specify the upload time and storage time.
		- Specify upload time: you can configure a cold storage policy by specifying a time point/period.
			 - Specify time point/period: if no start time point is specified, the oldest stored video file will be cold stored by default. If no end time point is specified, all video files after the start time point will be cold stored. If neither is specified, all video files in VOD will be cold stored.
			 - Specify storage time: a media asset will be cold stored after the entered time elapses.
 - Category: cold storage by category ID is supported. You can set multiple category IDs/names.
 - Source: cold storage is supported for different media sources. You can set multiple media sources.
 - Access policy: it can be set by setting the number of times to play back the video during a period of time. A cold storage policy supports only one access policy.
 - Media type: whether to perform the cold storage logic will be determined based on the media type. A cold storage policy supports only one media type.
4. After the policy is created, you need to enable it manually.

