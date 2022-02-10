## Use Cases

### Cases

#### Online education

In one-to-one or one-to-many small classes, you can record streams in multiple dimensions for different students:


- For one single student, you can record the student's separate data stream to compose relevant data. In this way, you can record the highlights of each student and push them to their parents.
- You can directly record the data in the room and generate videos that students can play back and watch repeatedly for learning.
- In order to facilitate repeated watches, redundant data can be removed during recording.


#### Customer service center


- In smart customer service scenarios, you can record the separate data streams of users and combine the data with recognition APIs to implement information verification during card application and smart account opening.
- You can record the speeches of the customer service representatives and users separately and automatically recognize keywords, so as to evaluate the service quality and iteratively train the smart customer service.
- You can save and archive the data generated in the course of service.

#### Social networking

- You can record only the desired video streams in the room for data retention, which helps reduce the costs of storage and stream mix.
- You can record the specified data in the room, call moderation APIs for content moderation, and set different moderation standards for different users.
- You can directly generate segment files based on live streams.

### Business process

This document describes how to [use API Gateway and SCF](https://cloud.tencent.com/product/serverless-catalog) to record a single anchor's audio/video stream in a TRTC room and upload the recording file to COS for storage. This solution provides out-of-the-box, flexible, convenient, and programmable live recording capabilities. SCF offers 512 MB of memory by default for recording file storage. If you need more storage space, you can choose to use [the mount capability of CFS](https://intl.cloud.tencent.com/document/product/583/37497). The workflow is as shown below: 
![](https://main.qcloudimg.com/raw/8375a6728642bfedc4a46796c75b583f.png)




The parameters for calling APIs are as follows:

| Parameter | Type | Required | Description |
| --------- | --------- | ---- | ------------------------------------------------------------ |
| SdkAppId | Int | Yes | Application ID, which is used to distinguish different TRTC applications. |
| RoomId | Int | Yes | Room ID in integer type, which is used to uniquely identify a room in a TRTC application. |
| StrRoomId | String | No | Room ID in string type. Either `RoomId` or `StrRoomId` must be configured. If both are configured, `RoomId` will be used. |
| UserId | String | Yes | Recorded user ID, which is used to uniquely identify a user in a TRTC application. |
| UserSig | String | Yes | Recorded user signature, which is used to authenticate the user login. |
| CosConfig | cosConfig | Yes | COS storage configuration for recording file storage. |
| Callback | String | No | Callback address after recording. The POST method is used for callback. |
| Mode | String | No | <li>00: single audio stream output in MP3 format (default mode).<br><li>01: single video stream output in MP4 format.<br><li>02: single audio/video stream output in MP4 format. |

// The parameters involved in `CosConfig` are as follows:

| Parameter | Type | Required | Description |
| --------- | ------ | ---- | ------------------------------------------------------------ |
| SecretId | String | No | `SecretId` of Tencent Cloud account. For more information, please see [Root Account Access Key Management](https://intl.cloud.tencent.com/document/product/598/34228). |
| SecretKey | String | No | `SecretKey` of Tencent Cloud account. For more information, please see [Root Account Access Key Management](https://intl.cloud.tencent.com/document/product/598/34228). |
| Region | String | Yes | COS region, such as `ap-guangzhou`. |
| Bucket | String | Yes | Bucket name, such as `susu-123456789`. |
| Path | String | Yes | Path in the bucket. For example, for `/test`, the root directory is `/`. |

>? 
>-  `UserId` is the specified user ID. Idempotency is not guaranteed for multiple requests to API Gateway. 
>- If `SecretId` and `SecretKey` are not configured in `CosConfig`, the function will use the permission of the execution role `SCF_ExecuteRole` when accessing COS.

Trigger conditions for stopping recording:

- The TRTC room is terminated. When there is no anchor in the TRTC room for more than 300s, the room will be automatically terminated.
- The user removal API is actively called to kick the recorded user out of the room.
- To stop recording for users with `RoomId`, you need to call the [RemoveUser](https://cloud.tencent.com/document/api/647/40496) API.
- To stop recording for users with `StrRoomId`, you need to call the [RemoveUserByStrRoomId](https://cloud.tencent.com/document/product/647/50426) API.

After recording is stopped, the data returned by the function is as follows:

| Parameter | Type | Required | Description |
| :-------- | :----- | :--- | :------------ |
| SdkAppId | String | Yes | Application ID. |
| RoomId | String | Yes | Room ID in integer type. |
| UserId | String | Yes | Recorded user ID. |
| StrRoomId | String | Yes | Room ID in string type. |
| Files | Array  | Yes | [{},{},{},{}] |

> ? If callback is configured, after the stop, SCF will pass the returned data to the callback address in POST method.

Each item in the `Files` array is a JSON object as follows:

| Parameter | Type | Required | Description |
| :--------- | :----- | :--- | :---------------------------------------------------- |
| UserId | String | Yes | Recorded user ID. |
| RecordFile | String | Yes | URL of the recording file uploaded to COS. |
| Status | Int | Yes | <li>0: failure.<br><li>1: success. |
| Message | String | Yes | Execution result of the recording task, such as recording failed, transcoding failed, and write to COS failed. |

## Directions

### Creating function[](id:step01)

1. Log in to the SCF console and select **[Function Service](https://console.cloud.tencent.com/scf/list)** on the left sidebar.
2. At the top of the **Function Service** page, select the **Guangzhou** region and click **Create** to enter the function creating page and configure the function as shown below:
   ![](https://main.qcloudimg.com/raw/6a91112239c4883e552a5e58066d52c6.png)
   - **Creation method**: select **Template**.
   - **Fuzzy search**: enter "TRTC", search, and select the **Single audio/video stream recording** template.
     Click **Learn More** in the template to view relevant information in the **Template Details** pop-up window, which can be downloaded.
3. Click **Next** and configure the related information as shown below:
![](https://main.qcloudimg.com/raw/3ad55bb34d51ff6f2089a35afd625c62.png)
 - **Function Name**: the function name is automatically generated by default.
 - **Async Execution**: select the checkbox to enable the async execution. When it's enabled, the function will respond to the event in async execution mode. The event goes to async execution status after being invoked without waiting for the processing result.
 - **Status Trace**: select the checkbox to enable the status trace. When it's enabled, it will keep the logs of real-time status of response for async function events. You can query and stop the event and check the related statistics. Data of event status will be retained for three days.
 - **Execution Timeout Period**: it can be modified as needed.
 - **Execution Role**: **SCF_ExecuteRole** is used as the execution role by default, which grants the access permissions of **QcloudCOSFullAccess** and **QcloudCFSFullAccess**.
4. Configure an API Gateway trigger. An API service is created by default and the integration response is disabled. You can customize the trigger, but please ensure that the integration response is disabled as shown below:
![](https://main.qcloudimg.com/raw/c6070898ad0dd3c57b7db8b35bfabf6b.png)
5. Click **Complete**.
6. If you need to use the [mount capability of CFS](https://intl.cloud.tencent.com/document/product/583/37497), as CFS can only be accessed in VPC, you should use the VPC of CFS as the VPC of the function as shown below:
![](https://main.qcloudimg.com/raw/e625a2a4e80082b4c82a570862e8b7dc.png)
>? To enable CFS, you need to set the environment variable `CFS_PATH` to a local directory, such as `/mnt/audio/`.



### Creating TRTC application[](id:step02)

1. Log in to the TRTC console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)** on the left sidebar.
2. Enter the demo name and click **Create**. You can choose a template for test run according to your client, such as the [demo for desktop browser](https://intl.cloud.tencent.com/document/product/647/35607).
    ![](https://main.qcloudimg.com/raw/983bc88596478c0c6396bb8b3cda2c34.png)




### Testing function[](id:step03)

1. [Create a TRTC application](#step02) and enter the application.
2. Use Postman to construct an HTTP request, where `roomId` is the room ID of the created TRTC application, and `userId` is the ID of another random user (which must be unique). Below is the sample code:
```
{
      "SdkAppId": 1400000000, 
      "RoomId": 43474, 
      "UserId": "user_55952145", 
      "Mode": "02", 
      "UserSig": "eJwtzNEKgkAUBNB-2efQ3e3eUqG3tMCKJJEIIxxxxxxxxxxxxxxxhvmweLWzGlUxj0mLs1GXKVf3mgrq*GFUdUR0UQrAYWDyW6Y15cwTwDm4UkxF36iXpkq1joiSc9xxxxxxxxxxxxx-S*CZeOk9sHfnEhCwlUW*fE4oWusw3dULlJ7HoSJ2e6d9fM8Y98fxUAzWA__", 
      "CosConfig": {
          "Region": "ap-shanghai", 
          "Bucket": "test-123456789", 
          "Path": "/trtc"
		  }
}
```
See the figure below:
![](https://main.qcloudimg.com/raw/62beb93a0b40b037df60fe4dfa87cc8f.png)

3. After the request is sent, an async function response "Async run task submitted" will be received. The `RequestId` of this function will be returned through `x-scf-reqid` in the HTTP header as shown below:
    ![](https://main.qcloudimg.com/raw/2659951b64f7bd81fe29bdd700fa6590.png)
4. On the **[Function Service](https://console.cloud.tencent.com/scf/list)** page in the SCF console, click the name of the function created in the [Creating function](#step01) step above to enter the function details page.
5. Select the **Log Query** tab on the function details page to view the printed recording log information as shown below:
    ![](https://qcloudimg.tencent-cloud.cn/raw/66ef3fc1e76fa635720b76cdaa5fffd7.png)
6. Log in to the [TRTC console](https://console.cloud.tencent.com/trtc/monitor) and click the room ID on the **Monitoring Dashboard** page to view all users in the room, one of whom is the recorded user .
7. To stop recording, you can call the [RemoveUser](https://cloud.tencent.com/document/api/647/40496) or [RemoveUserByStrRoomId](https://cloud.tencent.com/document/product/647/50426) API to move the user out of the room.



