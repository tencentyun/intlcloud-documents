## Use Cases

#### Quick playback file generation

   Live stream playback can increase the value and reduce the production costs of high-quality resources to boost the profits. The panoramic recording feature can record the class content from user's perspective in real time, quickly transcode the content based on the massive serverless computing power pool after a class ends, and generate the recording file for playback instantly.

#### Highlight collection

   Parents seldom have time to watch entire class videos of their children. The highlight collection feature renders the moments of children's excellent performance during the class to parents to improve their perception and recognition of the class. You can clip highlights from class recording files on the HTML5 platform, use panoramic recording to generate MP4 files, create a collection of highlight moments of children in class, and quickly distribute them through CDN.

#### File composition

   General file composition requires transcoding, which consumes a lot of computing power. With SCF + TRTC, you can compose videos, audios, images, etc. on the same frontend page, adjust the layout, perform panoramic recording, decode multiple streams, and encode all of them into one stream to quickly generate video files, giving full play to computing power resources.


## How It Works

Tencent Cloud's proprietary panoramic recording feature allows you to record videos in a WYSIWYG way. You only need to provide an accessible public network URL, and the feature can use Chrome for page rendering and recording, perform FFmpeg transcoding, and directly upload videos to COS to generate recording files in real time. Together with other Tencent Cloud products such as CSS, VOD, and TRTC, this offers a one-stop solution for education, gaming, and interactive entertainment scenarios.


![](https://qcloudimg.tencent-cloud.cn/raw/334a0fe70caf0fe2c27e11591a91294f.png)

## Application Strengths

- **Lower costs**
Panoramic recording uses Chrome for multi-stream decoding and one-stream encoding, which reduces computing power consumption and lowers the cost by over 60% compared with traditional recording solutions.
- **High fidelity**
Panoramic recording can capture all external information such as special effects in class on the client, fully retaining the in-person class experience.  
- **Free switch**
During panoramic recording, you can flexibly adjust the browser layout and switch between teacher and student views.
- **Ultra high concurrency**
SCF computing instances can be quickly started to stably sustain high concurrency and handle business traffic spikes with ease.
- **Instant output**
Panoramic recording allows you to directly get the recording file for playback once the live stream ends, with no need to perform complex composition, which is time-saving and efficient.

## Application Resources




After panoramic recording is deployed, the following resources will be created:

- **SCF function**: it gets the external link data and uses panoramic recording to record videos in real time.
- **CLS log**: it stores video processing logs and may incur fees. For more information, see [CLS Billing Rules](https://intl.cloud.tencent.com/document/product/614/37889).
- **API Gateway**: you can use an API Gateway trigger to trigger events.

## Prerequisites

1. Configure and deploy account permissions as detailed in [Account and Permission Configuration](https://intl.cloud.tencent.com/document/product/1040/36793).
2. Configure [execution role](https://intl.cloud.tencent.com/document/product/1040/36819) permissions.
3. Panoramic recording needs to be used together with other services, so you must add the following policies: QcloudRedisFullAccess, QcloudVPCFullAccess, QcloudCFSFullAcces, QcloudSCFFullAccess, QcloudCOSFullAccess, and QcloudAccessForScfRole. For more information, see [Policy](https://intl.cloud.tencent.com/document/product/598/10601).

## Directions



### Creating dependency resources


The following components are required as dependencies during function creation and must be created in advance: VPC, CFS file system or COS bucket, and TencentDB for Redis instance. For detailed directions on how to create them, see [Building up an IPv4 VPC](https://intl.cloud.tencent.com/document/product/215/31891), [Creating File Systems and Mount Targets](https://intl.cloud.tencent.com/document/product/582/9132), [Getting Started with the Console](https://intl.cloud.tencent.com/document/product/436/32955), and [Creating TencentDB for Redis Instances](https://intl.cloud.tencent.com/document/product/239/37712) respectively.






### Creating panoramic recording application

1. Log in to the Serverless console and select **[Serverless Application](https://console.cloud.tencent.com/sls)** on the left sidebar.
2. On the **Serverless Application** page, click **Create Application**.
3. On the **Create Application** page, configure as prompted.
   - **Creation method**: select **Template**.
   - **Fuzzy search**: enter "panoramic", search, and select **Panoramic recording** .
    Click **Learn More** in the template to view relevant information in the **Template Details** pop-up window, which can be downloaded.
4. Click **Next** and configure the related information .   
   - **Application Name**: enter a name such as "record-app".
   - **Region**: select a region such as "Shanghai".
   - **Intermediate Result Storage**: select the storage position of temporary files during recording. You can select COS or CFS as needed.
   - **Target Storage**: select the final storage position of recording results. You can select VOD or COS as needed.
   - **File System**: select as needed.
   - **Redis**: select as needed.
5. Click **Complete**.
    If you want to modify function configuration based on your business scenario, do so in **Serverless Application** > **Resource List** > **Function Details** as shown below:
    ![](https://qcloudimg.tencent-cloud.cn/raw/c1299a492435f7d8ffe59cbfd9526ed0.png)
    <dx-alert infotype="explain" title="">
- If the recording application needs to rely on the prolonged function execution capability, configure as instructed in [Async Execution](https://intl.cloud.tencent.com/document/product/583/39466).
- To avoid request timeout, we recommend you set the backend timeout period of the API Gateway trigger to a large value or use the default value. For more information, see [Provisioned Concurrency](https://intl.cloud.tencent.com/document/product/583/37704).
</dx-alert>



### API use instructions



#### Prerequisites

- Prepare a webpage that can be visited through a URL and is compatible with Chrome as the recording content source.
- You should handle the possible login status or authentication on the page to be recorded by yourself.
- If multimedia needs to be played back on the page to be recorded, you should handle multimedia operations such as playback, redirect, and stop by yourself.
- The page to be recorded must display the complete content within the specified width and height with no scrollbars, as web panoramic recording can record only the visible area of the browser window but cannot record the content outside this area.

#### API request path
<dx-tabs>
::: Request URL
1. Log in to the Serverless console and select **[Serverless Application](https://console.cloud.tencent.com/sls)** on the left sidebar.
2. On the serverless application list page, click the target application name.
3. On the application details page, get the trigger access entry as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/e26540e716f73fa5af1ea4a10b87c91b.png)
:::
::: Request method
POST 
Content-Type: application/json
:::
::: API authentication method
The panoramic recording service API is implemented through SCF and uses an API Gateway trigger to provide service. The application verification method (`ApiAppKey` and `ApiAppSecret`) is used for authentication. For more information, see [Application-Enabled Authentication](https://intl.cloud.tencent.com/document/product/628/40304).
:::
</dx-tabs>


#### Recording start API

This API is used to start panoramic recording. Parameters such as recording URL, resolution, and result callback address need to be specified in API parameters.
<dx-tabs>
::: Request body parameter description
| Parameter | Type | Required | Description |
| --------------- | ------ | ---- | ------------------------------------------------------------ |
| Action          | string | Yes   | Requested operation type. To start recording, set it to `Start`.                             |
| Data            | object | Yes   | Request protocol parameter.                                                 |
| RecordURL       | string | Yes   | Access URL of the webpage to be recorded. It must be accessible in Chrome.       |
| ManualStart      | bool | Yes   | Whether the recording task to be created can start after the page actively calls the `window.startRecord` method to trigger recording. The default value is `false`, indicating that the recording task will start automatically. If the value is set to `true`, after the recording function loads the page, it will not automatically start recording but will trigger recording after the page actively calls the `window.startRecord` method. |
| Width           | number | No   | Recording image width, which is 1280 by default. Value range: 0–2560.            |
| Height          | number | No   | Recording image height, which is 720 by default. Value range: 0–2560.             |
| CallbackURL     | string | No   | Callback address for recording result notification                                         |
| MaxDurationLimit | int    | No   | Maximum recording duration in seconds. Value range: 0–36000s. Default value: 21600s (6 hours). You need to configure a permanent key if this value exceeds 6 hours. |
| StorageType | string   | No   | Storage position of the intermediate state `webm` file during recording. Valid values: `cos` and `cfs`. Default value: `cfs`. (If the `COS_BUCKET_RAW` parameter is configured in the environment variables, data will be written into the bucket; otherwise, data will be written to the `raw` path in the target bucket.) |
 | Output         | object | No   | Request protocol parameter.          
| Cos             | object | No   | Request protocol parameter.                                                 |
| Domain          | string | No   | Recording file playback domain name. If it is not set, it will be the origin server domain name by default.                       |
| Bucket          | string | No   | Recording file storage bucket. If it is not set, it will be the storage bucket set during function creation by default.       |
| Region          | string | No   | Recording file storage region. If it is not set, it will be the region of the storage bucket by default.                  |
| TargetDir       | string | No   | Recording file storage path. If it is not set, it will be `Taskid` by default.                      |
| TargetName      | string | No   | Recording filename. If it is not set, it will be the stop timestamp by default.                             |
| Vod     | object | No   | VOD configuration parameter.                            |
| MediaInfo| object | No   | VOD media asset information.                         |
| MediaName    | string | No   | Media asset name.                           |
| ExpireTime      | Timestamp ISO8601 | No   | Expiration time of media asset file in ISO 8601 format. For more information, see [ISO date format](https://intl.cloud.tencent.com/document/product/266/11732). |
| StorageRegion     | string | No   | Upload region. This is only applicable to users who have special requirements for the upload region.                            |
| ClassId| Integer | No   | Category ID, which is used to categorize the media asset for management. A category can be created and its ID can be obtained by using the [CreateClass](https://intl.cloud.tencent.com/document/product/266/35325) API.                           |
| SourceContext| string | No   | Source context of up to 250 characters, which is used to pass through the user request information and will be returned by the VOD upload completion callback.         |
|ProcedureInfo    | object| No   | Task flow information                             |
| Procedure| string | No   | Subsequent task operation on a media asset file, i.e., after a media asset file is uploaded, task flow operations will be initiated automatically. This parameter value is a task flow template name. VOD supports [creating templates](https://intl.cloud.tencent.com/document/product/266/14059) and naming them. |
|SessionContext   | string | No   | Session context of up to 1,000 characters, which is used to pass through the user request information. If the `procedure` parameter is specified, the task flow status change callback API will return the value of this field.                           |
| SubAppId| string | No   | ID of a [subapplication](https://intl.cloud.tencent.com/document/product/266/33987) in VOD. If you need to access a resource in a subapplication, enter the subapplication ID in this field; otherwise, leave it empty.         |
| Video      | object | No   | Request protocol parameter.                           |
|  Muxer     | string | No   | Recording file format. Valid values: `hls` and `mp4`. If it is not set, it will be `mp4` by default.                              |
|    EncryptKey   | string | No   | HLS encryption public key. If it is not set, no encryption will be performed by default.                            |
|    AuthUrl   | string | No   | Decryption private key address, which is required if the public key is set.                            |


:::
::: Sample request body
<dx-codeblock>
::: json
{
    "Action": "Start",
    "Data": {
        "RecordURL": "https://web-record-12596******.cos.ap-chengdu.myqcloud.com/test/ponyo.mp4", 
        "Width": 1280,
        "Height": 720,
        "CallbackURL": "http://xxx/webrecord/callback",
        "MaxDurationLimit": 21600,
        "Output":{
            "Cos":{
                "Domain":"abc.xxx.com", 
                "Bucket":"webrecord-xxx", 
                 "Region":"ap-shanghai", 
                "TargetDir":"11234/", 
                "TargetName":"record-file-name.mp4"  
        },
	     "Vod": {
		  "MediaInfo": {
				"MediaName": "test",
				"ExpireTime": "2023-10-01T10:00:00Z",
				"StorageRegion": "ap-shanghai",
				"ClassId": 1
				},
		"ProcedureInfo": {
				"Procedure": "",
				"SessionContext": ""
				},
		"SubAppId": 1500007120
			},
	 "Video": {
		"Muxer": "hls",
	        "EncryptKey": "21834cca41778803e1afba3f41e70c90",
	        "AuthUrl": "https://hls-web-record-1253970226.cos.ap-shanghai.myqcloud.com/m3u8-encrypt/enc.key"
			}
         }
        }
}
:::
</dx-codeblock>
:::
::: Response parameter description

| Parameter | Type | Required | Description |
| ------------ | ------ | ---- | ------------------------------------------------ |
| ErrorCode    | string | No   | Error code, which will be returned only when a request error occurs.       |
| ErrorMessage | string | No   | Error message, which will be returned only when a request error occurs.       |
| TaskID       | string | No   | Recording task ID, which will be returned only when recording successfully starts. |
| RequestID    | string | No   | Request ID.                                           |
:::
::: Sample response parameters
<dx-codeblock>
::: json
// Response upon request success
{
    "TaskID": "d1806f20-25b8-4c30-8176-c0832b******",
    "RequestID": "95941e2c85898384a95b81c2a5******"
}

// Response upon request failure
{
    "ErrorCode": "InvalidParam",
    "ErrorMessage": "RecordURL missing",
    "RequestID": "95941e2c85898384a95b81c2a5******"
}
:::
</dx-codeblock>
:::
</dx-tabs>

#### Recording pause API

This API is used to pause a running recording task. 
<dx-tabs>
::: Request body parameter description
| Parameter | Type | Required | Description |
| ----------- | ------ | ---- | ------------------------------------------------------------ |
| Action      | string | Yes   | Requested operation type. To pause recording, set it to `Pause`.                             |
| Data        | object | Yes   | Request protocol parameter.                                                 |
| Data.TaskID | string | Yes   | ID of the recording task to be paused, which can be obtained in the response parameters of the recording start API. |
:::
::: Sample request body
<dx-codeblock>
::: json
{
    "Action": "Pause", 
    "Data": {
        "TaskID": "0f7d9522-a1a3-4517-b5ad-7a6eca******" 
    }
}
:::
</dx-codeblock>
:::
::: Response parameter description

| Parameter | Type | Required | Description |
| ------------ | ------ | ---- | ------------------------------------------------ |
| ErrorCode    | string | No   | Error code, which will be returned only when a request error occurs.       |
| ErrorMessage | string | No   | Error message, which will be returned only when a request error occurs.       |
| TaskID       | string | No   | Recording task ID, which will be returned only when recording successfully starts. |
| RequestID    | string | No   | Request ID.                                           |
:::
::: Sample response parameters
<dx-codeblock>
::: json
// Response upon request success
{
    "TaskID": "d1806f20-25b8-4c30-8176-c0832b******",
    "RequestID": "95941e2c85898384a95b81c2a5******"
}

// Response upon request failure
{
    "ErrorCode": "InvalidParam",
    "ErrorMessage": "TaskID missing",
    "RequestID": "95941e2c85898384a95b81c2a5******"
}
:::
</dx-codeblock>
:::
</dx-tabs>

#### Recording resumption API

This API is used to resume a paused recording task. The video content after resumption will be directly added to the content before pause without generating new video segments.

<dx-tabs>
::: Request body parameter description

| Parameter | Type | Required | Description |
| ----------- | ------ | ---- | ------------------------------------------------------------ |
| Action      | string | Yes   | Requested operation type. To resume recording, set it to `Resume`.                             |
| Data        | object | Yes   | Request protocol parameter.                                                 |
| Data.TaskID | string | Yes   | ID of the recording task to be resumed, which can be obtained in the response parameters of the recording start API. |
:::
::: Sample request body
<dx-codeblock>
::: json
{
    "Action": "Resume", 
    "Data": {
        "TaskID": "0f7d9522-a1a3-4517-b5ad-7a6eca******" 
    }
}
:::
</dx-codeblock>
:::
::: Response parameter description
| Parameter | Type | Required | Description |
| ------------ | ------ | ---- | ------------------------------------------------ |
| ErrorCode    | string | No   | Error code, which will be returned only when a request error occurs.       |
| ErrorMessage | string | No   | Error message, which will be returned only when a request error occurs.       |
| TaskID       | string | No   | Recording task ID, which will be returned only when recording successfully starts. |
| RequestID    | string | No   | Request ID.                                           |
:::
::: Sample response parameters
<dx-codeblock>
::: json
// Response upon request success
{
    "TaskID": "d1806f20-25b8-4c30-8176-c0832b******",
    "RequestID": "95941e2c85898384a95b81c2a5******"
}

// Response upon request failure
{
    "ErrorCode": "InvalidParam",
    "ErrorMessage": "TaskID missing",
    "RequestID": "95941e2c85898384a95b81c2a5******"
}
:::
</dx-codeblock>
:::
</dx-tabs>

#### Recording page refresh API

This API is used to initiate a request to refresh the page to be recorded. 
<dx-tabs>
::: Request body parameter description

| Parameter | Type | Required | Description |
| ----------- | ------ | ---- | ------------------------------------------------------------ |
| Action      | string | Yes   | Requested operation type. To refresh recording, set it to `Refresh`.                              |
| Data        | object | Yes   | Request protocol parameter.                                                 |
| Data.TaskID | string | Yes   |  ID of the recording task to be refreshed, which can be obtained in the response parameters of the recording start API. |
:::
::: Sample request body
<dx-codeblock>
::: json
{
    "Action": "Refresh", 
    "Data": {
        "TaskID": "0f7d9522-a1a3-4517-b5ad-7a6eca******" 
    }
}
:::
</dx-codeblock>
:::
::: Response parameter description
| Parameter | Type | Required | Description |
| ------------ | ------ | ---- | ------------------------------------------------ |
| ErrorCode    | string | No   | Error code, which will be returned only when a request error occurs.       |
| ErrorMessage | string | No   | Error message, which will be returned only when a request error occurs.       |
| TaskID       | string | No   | Recording task ID, which will be returned only when recording successfully starts. |
| RequestID    | string | No   | Request ID.                                           |

:::
::: Sample response parameters
<dx-codeblock>
::: json
// Response upon request success
{
    "TaskID": "d1806f20-25b8-4c30-8176-c0832b******",
    "RequestID": "95941e2c85898384a95b81c2a5******"
}

// Response upon request failure
{
    "ErrorCode": "InvalidParam",
    "ErrorMessage": "TaskID missing",
    "RequestID": "95941e2c85898384a95b81c2a5******"
}
:::
</dx-codeblock>
:::
</dx-tabs>

#### Recording stop API

This API is used to initiate a recording stop request. 
<dx-tabs>
::: Request body parameter description

| Parameter | Type | Required | Description |
| ----------- | ------ | ---- | ------------------------------------------------------------ |
| Action      | string | Yes   | Requested operation type. To stop recording, set it to `Stop`.                             |
| Data        | object | Yes   | Request protocol parameter.                                                 |
| Data.TaskID | string | Yes   | ID of the recording task to be stopped, which can be obtained in the response parameters of the recording start API. |
:::
::: Sample request body
<dx-codeblock>
::: json
{
    "Action": "Stop", 
    "Data": {
        "TaskID": "0f7d9522-a1a3-4517-b5ad-7a6eca******" 
    }
}
:::
</dx-codeblock>
:::
::: Response parameter description
| Parameter | Type | Required | Description |
| ------------ | ------ | ---- | ------------------------------------------------ |
| ErrorCode    | string | No   | Error code, which will be returned only when a request error occurs.       |
| ErrorMessage | string | No   | Error message, which will be returned only when a request error occurs.       |
| TaskID       | string | No   | Recording task ID, which will be returned only when recording successfully starts. |
| RequestID    | string | No   | Request ID.                                           |

:::
::: Sample response parameters
<dx-codeblock>
::: json
// Response upon request success
{
    "TaskID": "d1806f20-25b8-4c30-8176-c0832b******",
    "RequestID": "95941e2c85898384a95b81c2a5******"
}

// Response upon request failure
{
    "ErrorCode": "InvalidParam",
    "ErrorMessage": "TaskID missing",
    "RequestID": "95941e2c85898384a95b81c2a5******"
}
:::
</dx-codeblock>
:::
</dx-tabs>



#### Recording task information query API

This API is used to initiate a request to query the recording task information.
<dx-tabs>
::: Request body parameter description
| Parameter | Type | Required | Description |
| ----------- | ------ | ---- | ------------------------------------------------------------ |
| Action      | string | Yes   | Requested operation type. To query a recording task, set it to `Describe`.                  |
| Data        | object | Yes   | Request protocol parameter.                                                 |
| Data.TaskID | string | Yes   | ID of the recording task to be queried, which can be obtained in the response parameters of the recording start API. |
:::
::: Sample request body
<dx-codeblock>
::: json
{
    "Action": "Describe", 
    "Data": {
        "TaskID": "0f7d9522-a1a3-4517-b5ad-7a6ec******"
    }
}
:::
</dx-codeblock>
:::
::: Response parameter description
| Parameter | Type | Required | Description |
| ---------------------- | -------- | ---- | ------------------------------------------------------------ |
| ErrorCode    | string | No   | Error code, which will be returned only when a request error occurs.       |
| ErrorMessage | string | No   | Error message, which will be returned only when a request error occurs.       |
| TaskID       | string | No   | Recording task ID, which will be returned only when recording successfully starts. |
| RequestID    | string | No   | Request ID.                                           |
| Status                 | string   | No   | Current recording task status. Valid values: <br> normal: the recording task is successfully created but has not been started yet.<br> recording: the recording task is running.<br> paused: the recording task is paused.<br> canceled: the recording task is canceled.<br> transcode: the recording task is performing an operation on the recorded video such as splicing and transcoding.<br> upload: the recording task is uploading the recorded video to a Tencent Cloud storage service.<br> callback: the recording task is notifying the recording result at the callback address configured during recording initiation.<br> finished: all operations of the recording task have been completed. |
| CreateTime             | int      | No   | Recording task creation timestamp in seconds.                                |
| StartTime              | int      | No   | Recording task start timestamp in secpnds, which will be returned only after recording is successfully started.  |
| CancelTime             | int      | No   | Recording task cancellation timestamp in seconds, which will be returned only after the recording cancellation request is initiated. |
| StopTime               | int      | No   | Recording task stop timestamp in seconds, which will be returned only after the recording task is stopped. |
| FinishTime             | int      | No   | Recording task completion timestamp in seconds, which will be returned only after all operations in the recording task are completed. |
| Result                 | object   | No   | Recording task result.                                                 |
| Result.ErrorCode       | string   | No   | Recording task error code, which will be returned only if an error occurs during recording task execution. |
| Result.ErrorMessage    | string   | No   | Recording task error message, which will be returned only if an error occurs during recording task execution. |
| Result.Videos          | []object | No   | List of recorded video files.                                             |
| Result.Videos.Filename | string   | No   | Video filename.                                                 |
| Result.Videos.FileSize | int      | No   | Video file size.                                                 |
| Result.Videos.FileDuration | string    | No   | Video file duration.                                                |
| Result.Videos.FileId |string   | No   | If the target is VOD, this parameter is the unique ID of the media asset file in VOD.                                              |	
| Result.Videos.FileURL  | string   | No   | Video file URL.                                                 |
:::
::: Sample response parameters
<dx-codeblock>
::: json
// Response upon request success
{
    "TaskID": "7a035551-d9d6-494e-b604-fa787b******",
    "RequestID": "95941e2c85898384a95b81c2a5******",
    "CreateTime": 1620982173,
    "Status": "finished",
    "StartTime": 1620982177,
    "CancelTime": 1620982203,
    "StopTime": 1620982203,
    "FinishTime": 1620982210,
    "Result": {
        "Videos": [
            {
                "Filename": "1621406865789.mp4",
                "FileSize": 169780,
           "FileDuration": 9,
            "FileId": 31235664578998,
                "FileURL": "http://web-record-125******.cos.ap-chengdu.myqcloud.com/4d0f336d-4de4-4fc8-b505-d1f790974909/162140******.mp4"
            }
        ]
    }
}

// Response upon request error
{
    "ErrorCode": "InvalidParam",
    "ErrorMessage": "TaskID missing",
    "RequestID": "95941e2c85898384a95b81c2a5******"
}

// Response upon recording task error
{
    "TaskID": "7a035551-d9d6-494e-b604-fa787b******",
    "RequestID": "95941e2c85898384a95b81c2a5******",
    "CreateTime": 1620982173,
    "Status": "finished",
    "StartTime": 1620982177,
    "CancelTime": 1620982203,
    "StopTime": 1620982203,
    "FinishTime": 1620982210,
    "Result": {
        "ErrorCode": "CallbackFailed",
        "ErrorMessage": "Callback failed even all tries. last error message:ECONNABORTED:timeout of 2000ms exceeded"
    }
}
:::
</dx-codeblock>
:::
</dx-tabs>

