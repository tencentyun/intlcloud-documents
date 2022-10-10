This document shows you how to implement content moderation for a specific room. This requires you to manually start and end a moderation task.



## Implementation
### Workflow
![](https://qcloudimg.tencent-cloud.cn/raw/af96d1a900603c441fce5cde5c972ec9.jpg)

### Directions
1. Create a room with the TRTC SDK, after which you will get the application ID (`sdk_app_id`) and room ID (`room_id`). Generate a user ID (`user_id`), which will allow the moderation system to enter the room and pull live content for moderation. We recommend you generate a different user ID for content moderation for each room. In addition to the user ID, you will also get the signature (`user_sig`) for the moderation system.
2. Use the `sdk_app_id`, `room_id`, `user_id``, and user_sig` obtained in the previous step to splice a moderation URL in the following format:[](id:step2)
```
trtc://trtc.tencentcloudapi.com/moderation?sdk_app_id=xxxx&room_id=xxxx&user_id=xxxx&user_sig=xxxx
```
>! 
>- To avoid parsing failure due to special characters, escape the parameter values before splicing the URL, especially `user_sig`.
>- The parameters `sdk_app_id`, `user_id`, `user_sig`, and `room_id` mentioned in this document correspond to `SDKAppID`, `UserID`, `UserSig`, and `RoomID` you use with the TRTC SDK.
<table>
<thead><tr><th>Parameter</th><th>Required</th><th>Description</th></tr></thead>
<tbody><tr>
<td>sdk_app_id</td>
<td>Yes</td>
<td>The ID assigned when an application is created in the TRTC console.</td>
</tr><tr>
<td>room_id</td>
<td>Yes</td>
<td>The ID assigned when a room is created. The data type of this parameter may be string or numeric (default). To use string-type room IDs, set `room_id_type` to `string`.</td>
</tr><tr>
<td>user_id</td>
<td>Yes</td>
<td>The user ID used by the moderation system to enter a room and pull data. We recommend you generate a different user ID for each room.</td>
</tr><tr>
<td>user_sig</td>
<td>Yes</td>
<td>The security signature generated based on `sdk_app_id` and `user_id`.</td>
</tr><tr>
<td>mix</td>
<td>No</td>
<td>If this is set to `true`, the streams in a room will be mixed first before moderation. If it is `false`, the streams in a room will be reviewed separately.<br>With single-stream moderation, you can get from the moderation callback the specific users (user_id) whose streams contain non-compliant content. This is not possible with mixed-stream moderation.</td>
</tr><tr>
<td>room_id_type</td>
<td>No</td>
<td>The data type of the room ID parameter. Valid values: string, number.</td>
</tr></tbody></table>

3. Call the [CreateAudioModerationTask](https://intl.cloud.tencent.com/document/product/1139/46101) API to start a content moderation task for the room.
<table>
<thead><tr><th>Parameter</th><th>Required</th><th>Type</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Action</td>
<td>Yes</td>
<td>String</td>
<td>A common parameter. For this API, its value is `CreateAudioModerationTask`.</td>
</tr><tr>
<td>Version</td>
<td>Yes</td>
<td>String</td>
<td>A common parameter. For this API, its value is `2020-12-29`.</td>
</tr><tr>
<td>Region</td>
<td>No</td>
<td>String</td>
<td>A common parameter. It’s used to specify a region outside the Chinese mainland. Currently, only Singapore (`ap-singapore`) is supported.</td>
</tr><tr>
<td>Tasks.N</td>
<td>Yes</td>
<td>Array of <a href="https://intl.cloud.tencent.com/document/product/1139/46098">TaskInput</a></td>
<td>The information of audio moderation tasks. For details, see the description of `TaskInput`.<br>Note: You can create up to <strong>10 tasks</strong>.</td>
</tr><tr>
<td>BizType</td>
<td>No</td>
<td>String</td>
<td>The ID of the moderation policy, which is configured in the CMS console. Specify this parameter to use a specific moderation policy. If you do not pass in this parameter, the default moderation policy will be used.<br>Note: Biztype can be 3-32 characters long and can contain numbers, letters, and underscores. Different Biztype values are associated with different business scenarios. Make sure you use the right Biztype.</td>
</tr><tr>
<td>Type</td>
<td>No</td>
<td>String</td>
<td>The type of audio to moderate. Valid values: <b>AUDIO</b>(VOD audio), <b>LIVE_AUDIO</b>(live audio). The default is `AUDIO`.</td>
</tr><tr>
<td>Seed</td>
<td>No</td>
<td>String</td>
<td>The callback signature key, which helps ensure data security. Add the field `X-Signature` to the HTTP response header. The value of the field is a SHA256 hash of `seed + body` represented in hexadecimal. After receiving the callback, use <b>sha256(seed + body)</b> to calculate the <code>X-Signature</code> for verification. For details, see <a href="https://intl.cloud.tencent.com/document/product/1139/46091">Signature v3</a>.</td></tr>
<tr>
<td>CallbackUrl</td>
<td>No</td>
<td>String</td>
<td>The address to receive moderation results. The default format is a URL. After configuration, the information of non-compliant audio segments detected will be sent to this address. For the callback format, see <a href="https://intl.cloud.tencent.com/document/product/1139/46101#.E7.A4.BA.E4.BE.8B2-.E5.9B.9E.E8.B0.83.E7.AD.BE.E5.90.8D.E7.A4.BA.E4.BE.8B">Sample Callback Signature</a>.</td></tr>
</tbody></table>


In the step above, the `CreateAudioModerationTask` API is called to create an audio moderation task. To start a video moderation task, call [CreateVideoModerationTask]](#appendix).
	Pay attention to the following:

   - **BizType**
      You can create different moderation policies in [Policy Management](https://console.intl.cloud.tencent.com/cms/video/strategy) of the CMS console. When you activate CMS, a policy whose BizType is `default` is created automatically. You can pass in this value for testing.
      ![](https://qcloudimg.tencent-cloud.cn/raw/46e0ce41f8f49998e93b2ff0d5f79849.png)
   - **Type**
      Set this parameter according to the scenario of your TRTC application. For example, for audio chat room, the API of AMS (Audio Moderation System) is used, and you should set this parameter to `LIVE_AUDIO`; for video chat, the API of VMS (Video Moderation System) is used, and you should set this parameter to `LIVE_VIDEO`.
   - **CallbackUrl**
      This address is used to receive callbacks of moderation results during or after a live stream. You can configure this address in the console or pass it to the API. For the callback format, refer to the response parameters of [DescribeTaskDetail](https://intl.cloud.tencent.com/document/product/1139/46100).
   - **Tasks.N.Input.Url**
      Pass in the moderation URL spliced in [step 2](#step2).
      ![](https://qcloudimg.tencent-cloud.cn/raw/64bc723804a0d30610870bb034701084.png)
4. After a moderation task is created successfully, a unique task ID (`TaskId`) will be returned.
5. During the moderation process, the moderation system will review the audio segments and video screenshots of each user in the room and continuously send the results to your callback server. Based on the results, you can decide whether to block the room or send a warning.
6. After a live stream ends, you need to call an API (pass in the `TaskId`) to end the moderation task.
7. After receiving the request to end moderation, the moderation system will stop pulling data from the room, generate the final moderation result, and send you a callback indicating the end of moderation. The non-compliant audio/video segments identified will be saved to COS and named as follows:
```
trtc/{{sdk_app_id}}/screenshot_{{room_id}}_{{user_id}}{{timestamp}}.jpg (image format)
trtc/{{sdk_app_id}}/audio{{room_id}}_{{user_id}}_{{timestamp}}.mp3 (audio format)
```
>!
>- **In the mixed-stream moderation mode, `user_id` is `mixer`.**
>- During the moderation process, in case of stream interruption or failure to pull data from the room, the moderation system will retry. If it still fails to pull any data after a certain period of time (which varies depending on the error code), the live stream will be considered ended, and the moderation system will send you a callback indicating that moderation has stopped. After receiving this callback, if you want to continue to moderate the streams in the room, you can start another moderation task.

## FAQs

### 1. Is the moderation system user ID visible to other users in the room?
No. To pull data for moderation, the moderation system enters the TRTC room as an audience member. The moderation system is not visible to other users in the room.

### 2. Does pulling data from TRTC incur a fee?

The moderation system enters the TRTC room as an audience member and pulls data, so TRTC’s billing rules apply. The fee is based on the duration of audio/video subscribed (pulled). For details, see [Billing of TRTC Basic Services](https://intl.cloud.tencent.com/document/product/647/42734).
>!
>- The `user_ID` of the moderation system cannot be identical to another user in the room.
>- `room_id` is a UNIT and its value range is 1-4294967295. You will be responsible for assigning and maintaining room IDs.

### 3. The moderation system enters a TRTC room as an audience member to pull data for moderation. Do I need to create a user for it the same way as I create other users?
Yes. When the moderation system enters the TRTC room to pull data, it is considered the same as other users in the room.

### 4. How long do audio and video moderation usually take respectively?
Non-compliant audio/video segments are returned immediately. The real time factor of audio moderation is 0.2, and the results of image recognition are returned within one second of data arrival.

### 5. What is `user_sig`?
See [UserSig](https://intl.cloud.tencent.com/document/product/647/35166).

### 6. How does TRTC verify `user_sig`? How do I troubleshoot the “-3319” or “-3320” error during room entry?

To verify `user_sig`, log in to the TRTC console and go to **Development Assistance** > [UserSig Generation & Verification](https://console.cloud.tencent.com/trtc/usersigtool).

### 7. In an audio chat room where there are multiple streams, how do I know which stream contains non-compliant content?

Non-compliant audio/video segments are saved to COS and named `trtc_[room_id]_[user_id]_timestamp`. You can tell which user a segment belongs to from the segment’s COS address.

### 8. Is there anything I need to pay attention to when splicing the moderation URL?
Because `user_sig` may contain special characters, you should escape it first before including it in the URL.

>? For more questions, see [FAQs](https://intl.cloud.tencent.com/document/product/647/36057).

[](id:appendix)

## Appendix
- You may need to use the following four APIs for **audio moderation**:
     - [CreateAudioModerationTask](https://intl.cloud.tencent.com/document/product/1139/46101)
     - [CancelTask](https://intl.cloud.tencent.com/document/product/1139/46097)
     - [DescribeTasks](https://intl.cloud.tencent.com/document/product/1139/46096) 
     - [DescribeTaskDetail](https://intl.cloud.tencent.com/document/product/1139/46100)
- You may need to use the following four APIs for **video moderation**:
     - [CreateVideoModerationTask](https://intl.cloud.tencent.com/document/product/1140/46113)
     - [CancelTask](https://intl.cloud.tencent.com/document/product/1140/46114)
     - [DescribeTasks](https://intl.cloud.tencent.com/document/product/1140/46111)
     - [DescribeTaskDetail](https://intl.cloud.tencent.com/document/product/1140/46112)
