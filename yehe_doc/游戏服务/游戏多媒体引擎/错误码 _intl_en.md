This document provides error codes that may be reported during Tencent Cloud Game Multimedia Engine (GME) development so that developers can easily debug and access GME APIs.

## General Errors

| Error Code Name                    | Error Code Value | Cause and Suggested Solution                                               |
| ----------------------------- | -------- | ------------------------------------------------------------ |
| AV_ERR_3DVOICE_ERR_NOT_INITED | 7003     | The `InitSpatializer` API needs to be called first.                              |
|AV_ERR_NET_REQUEST_FALLED |7004| Network request failed mainly due to an unstable network connection. To troubleshoot, see [FAQ > Voice Chat Room](https://intl.cloud.tencent.com/document/product/607/35611). |
|AV_ERR_CHARGE_OVERDUE     |7005| Operation failed due to account arrears. You need to check whether your account is in arrears in the Tencent Cloud Console. |
|AV_ERR_AUTH_FIALD         |7006| Authentication failed. Possible causes: 1. The `AppID` does not exist or is incorrect; 2. An error occurred while authenticating the `authbuff`; 3. Authentication expired. |
| AV_ERR_IN_OTHER_ROOM          | 7007     | Already in another room.                                               |
| AV_ERR_NO_PERMISSION          | 7009     | No permission to perform the operation.                               |
| AV_ERR_FILE_CANNOT_ACCESS     | 7010     | Unable to access the file.                                                 |
| AV_ERR_FILE_DAMAGED           | 7011     | File is corrupted.                                                   |
| AV_ERR_SERVICE_NOT_OPENED     | 7012     | Please enable this feature in the console before using it.                     |
|AV_ERR_USER_CANCELED       |7013| The user canceled an operation before it succeeds, such as entering a room. |
|AV_ERR_LOAD_LIB_FAILED       |7014| The library file is not loaded properly, please check if it is missing. |
|AV_ERR_SDK_NOT_FULL_UPDATE       |7015|When upgrading the SDK, not all files were upgraded, which caused some module mismatches. Please fully upgrade the SDK. |
|AV_ERR_3DVOICE_ERR_FILE_DAMAGED       |7002| Failed to load the 3D sound effect file. |

## Client Errors for Voice Chat

<table>
<thead>
<tr>
<th>Error Code Name</th>
<th>Error Code Value</th>
<th>Description</th>
<th>Cause</th>
<th>Suggested Solution&nbsp;&nbsp;&nbsp;&nbsp;</th>
</tr>
</thead>
<tbody><tr>
<td>AV_ERR_REPEATED<br>_OPERATION</td>
<td>1001</td>
<td>Repeated operation</td>
<td>An operation is performed when the same operation is in progress. Operation types include AVContext, room, device, and member. AVContext operations: StartContext/StopContext. Room operations: EnterRoom/ExitRoom. Device operations: enabling/disabling a device.</td>
<td>Perform the next operation after the ongoing operation is completed.</td>
</tr>
<tr>
<td>AV_ERR_EXCLUSIVE<br>_OPERATION</td>
<td>1002</td>
<td>Exclusive operation</td>
<td>An operation is performed when another operation of the same type is in progress.</td>
<td>Perform the next operation after the ongoing operation is completed.</td>
</tr>
<tr>
<td>AV_ERR_HAS_IN<br>_THE_STATE</td>
<td>1003</td>
<td>Repeated operation</td>
<td>An operation is performed to make an object enter a state which it is already in, for example, making a client enter a room again which it is already in.</td>
<td>Regard the current operation as successful since the object is already in the desired state.</td>
</tr>
<tr>
<td>AV_ERR_INVALID<br>_ARGUMENT</td>
<td>1004</td>
<td>Invalid parameter</td>
<td>One or more incorrect parameters are passed in when an SDK API is called; for example, when the client is trying to enter a room, the input room type is not `AVRoom::ROOM_TYPE_PAIR` or `AVRoom::ROOM_TYPE_MULTI`.</td>
<td>Read the API document carefully to get the valid value range for each parameter of each API, and take preventive measures to ensure the correctness of input parameters.</td>
</tr>
<tr>
<td>AV_ERR_TIMEOUT</td>
<td>1005</td>
<td>Timeout</td>
<td>The result of an operation is not returned within the specified time. This error occurs mostly when signaling transmission is involved and network problem occurs. For example, after a client performs an operation to enter a room, the result of the operation is not returned within 30 seconds.</td>
<td>Check whether the network is normal and whether the public network can be connected, and then try again.</td>
</tr>
<tr>
<td>AV_ERR_NOT<br>_IMPLEMENTED</td>
<td>1006</td>
<td>Not implemented</td>
<td>The feature is not available yet when an SDK API is called.</td>
<td>Find other alternative methods.</td>
</tr>
<tr>
<td>AV_ERR_NOT_IN<br>_MAIN_THREAD</td>
<td>1007</td>
<td>Not in the main thread</td>
<td>External SDK APIs must be called in the main thread, but a client failed to do so.</td>
<td>Modify the service logic to ensure that SDK APIs are called in the main thread.</td>
</tr>
<tr>
<td>AV_ERR_RESOURCE<br>_IS_OCCUPIED</td>
<td>1008</td>
<td>Occupied resource</td>
<td>A required resource, such as the camera or screen, has already been occupied.</td>
<td>Identify the specific resources to be used and confirm the reason why these resources are occupied to ensure that SDK features are used at the right time without resource conflict.</td>
</tr>
<tr>
<td>AV_ERR_CONTEXT<br>_NOT_EXIST</td>
<td>1101</td>
<td>Invalid AVContext status</td>
<td>When an AVContext object is not in the CONTEXT_STATE_STARTED status, a client calls an API that can be called only when the AVContext object is in this status.</td>
<td>Modify the service logic to ensure that SDK APIs are called at the right time.</td>
</tr>
<tr>
<td>AV_ERR_CONTEXT<br>_NOT_STOPPED</td>
<td>1102</td>
<td>Invalid AVContext status</td>
<td>When an AVContext object is not in the CONTEXT_STATE_STOPPED status, a client calls an API that can be called only when the AVContext object is in this status, such as the API AVContext::DestroyContext.</td>
<td>Modify the service logic to ensure that SDK APIs are called at the right time.</td>
</tr>
<tr>
<td>AV_ERR_ROOM<br>_NOT_EXIST</td>
<td>1201</td>
<td>Invalid AVRoom status</td>
<td>When an AVRoom object is not in the ROOM_STATE_ENTERED status, a client calls an API that can be called only when the AVRoom object is in this status.</td>
<td>Modify the service logic to ensure that SDK APIs are called at the right time.</td>
</tr>
<tr>
<td>AV_ERR_ROOM<br>_NOT_EXITED</td>
<td>1202</td>
<td>Invalid AVRoom status</td>
<td>When an AVRoom object is not in the ROOM_STATE_EXITED status, a client calls an API that can be called only when the AVRoom object is in this status, such as the API AVContext::StopContext.</td>
<td>Modify the service logic to ensure that SDK APIs are called at the right time.</td>
</tr>
<tr>
<td>AV_ERR_DEVICE<br>_NOT_EXIST</td>
<td>1301</td>
<td>The device does not exist</td>
<td>A client uses a device that does not exist or has not been initialized.</td>
<td>Verify that the device exists, ensure that the device ID is entered correctly, and use the device after it is successfully initialized.</td>
</tr>
<tr>
<td>AV_ERR_ENDPOINT<br>_NOT_EXIST</td>
<td>1401</td>
<td>The AVEndpoint object does not exist.</td>
<td>When a member has not initiated a voice chat or video chat, a client tries to obtain the AVEndpoint object of the member.</td>
<td>Modify the service logic to ensure that SDK APIs are called at the right time.</td>
</tr>
<tr>
<td>AV_ERR_ENDPOINT<br>_HAS_NOT_VIDEO</td>
<td>1402</td>
<td>The member does not initiate a video chat.</td>
<td>When a member has not initiated a video chat, a client performs an operation that can be completed only after a video is initiated. For example, when a member has not initiated a video chat, a client requests the video image of the member.</td>
<td>Modify the service logic to ensure that SDK APIs are called at the right time.</td>
</tr>
<tr>
<td>AV_ERR_TINYID_TO<br>_OPENID_FAILED</td>
<td>1501</td>
<td>Failed to convert a tinyid into an identifier</td>
<td>After receiving the signaling indicating a member's information update, a client needs to convert the tinyid into an identifier. However, the conversion failed due to issues with the logic of the IMSDK library or the network.</td>
<td>Confirm that the network works well, and check logs for any problem with the logic of the IMSDK library.</td>
</tr>
<tr>
<td>AV_ERR_OPENID_TO<br>_TINYID_FAILED</td>
<td>1502</td>
<td>Failed to convert an identifier into a tinyid</td>
<td>When calling the StartContext API, a client needs to convert the identifier into a tinyid. However, the conversion failed due to issues with the logic of the IMSDK library, the network, or no login status.</td>
<td>Confirm that the network works well, check logs for any problem with the logic of the IMSDK library, and confirm that the IMSDK login API has been successfully called.</td>
</tr>
<tr>
<td>AV_ERR_DEVICE<br>_TEST_NOT_EXIST</td>
<td>1601</td>
<td>Invalid AVDeviceTest status</td>
<td>When an AVDeviceTest object is not in the DEVICE_TEST_STATE_STARTED status, a client calls an API that can be called only when the AVDeviceTest object is in this status.</td>
<td>Modify the service logic to ensure that SDK APIs are called at the right time.</td>
</tr>
<tr>
<td>AV_ERR_DEVICE<br>_TEST_NOT_STOPPED</td>
<td>1602</td>
<td>Invalid AVDeviceTest status</td>
<td>When an AVDeviceTest object is not in the DEVICE_TEST_STATE_STOPPED status, a client calls an API that can be called only when the AVDeviceTest object is in this status, such as the API AVContext::StopContext.</td>
<td>Modify the service logic to ensure that SDK APIs are called at the right time.</td>
</tr>
<tr>
<td>AV_ERR_INVITET<br>_FAILED</td>
<td>1801</td>
<td>Failed to send an invitation.</td>
<td>A failure occurs when a client tries to send an invitation.</td>
<td>The invitation module is used only for demo, and the invitation feature is not available yet. So this error code can be ignored.</td>
</tr>
<tr>
<td>AV_ERR_ACCEPTT<br>_FAILED</td>
<td>1802</td>
<td>Failed to accept an invitation.</td>
<td>A failure occurs when a client tries to accept an invitation.</td>
<td>The invitation module is used only for demo, and the invitation feature is not available yet. So this error code can be ignored.</td>
</tr>
<tr>
<td>AV_ERR_REFUSE<br>_FAILED</td>
<td>1803</td>
<td>Failed to refuse an invitation.</td>
<td>A failure occurs when a client tries to reject an invitation.</td>
<td>The invitation module is used only for demo, and the invitation feature is not available yet. So this error code can be ignored.</td>
</tr>
<tr>
<td>QAV_ERR_NOT_TRY<br>_NEW_ROOM</td>
<td>2001</td>
<td>A client fails to enter a new room and remains in the original room.</td>
<td>A client fails to switch to a new room and remains in the current room.</td>
<td>Remain in the current room.</td>
</tr>
<tr>
<td>QAV_ERR_TRY_NEW<br>_ROOM_FAILED</td>
<td>2002</td>
<td>A client attempts to enter a new room but fails, and exits the original room.</td>
<td>A client fails to switch to a new room and has exited the original room.</td>
<td>Exit a room and enter again.</td>
</tr>
</tbody></table>

## Server Errors for Voice Chat

<table>
<thead>
<tr>
<th width="30%">Error Code Name</th>
<th width="11%">Error Code Value</th>
<th width="20%">Description</th>
<th width="22%">Cause</th>
<th width="22%">Suggested Solution</th>
</tr>
</thead>
<tbody><tr>
<td>AV_ERR_SERVER_FAILED</td>
<td>10001</td>
<td>General error</td>
<td>Locate the specific cause based on the real error code (in logs) returned from the backend to a client.</td>
<td>View and confirm the validity of the parameters in the API for room entry, such as AppID, UIN and AuthBuffer (see the documentation). In the console, check whether the relevant parameters match the local ones, and whether there is any account arrears. Check whether the developer's testing devices are running over a private or public network.</td>
</tr>
<tr>
<td>AV_ERR_SERVER<br>_INVALID_ARGUMENT</td>
<td>10002</td>
<td>Invalid parameter</td>
<td>One or more incorrect parameters are passed when an SDK API is called or when internal SDK signaling is sent to the backend.</td>
<td>Ensure the correctness of parameters passed in SDK API calls. Analyze logs, obtain the real error code returned from the backend to the client, and ask backend personnel for help.</td>
</tr>
<tr>
<td>AV_ERR_SERVER<br>_NO_PERMISSION</td>
<td>10003</td>
<td>No permission</td>
<td>A client has no permission to use a feature. For example, a client provides an incorrect or expired signature when it tries to enter a room.</td>
<td>Be sure to use a feature only after providing correct permission parameters. Check whether the AppID and permission key are correct.</td>
</tr>
<tr>
<td>AV_ERR_SERVER_TIMEOUT</td>
<td>10004</td>
<td>Hour</td>
<td>The result of an operation is not returned within the specified time.</td>
<td>Analyze logs, obtain the real error code returned from the backend to the client, and ask backend personnel for help.</td>
</tr>
<tr>
<td>AV_ERR_SERVER_ALLOC<br>_RESOURCE_FAILED</td>
<td>10005</td>
<td>Network error</td>
<td>Network error occurs when a client performs an operation.</td>
<td>View and confirm the validity of the parameters in the API for room entry, such as AppID, UIN and AuthBuffer (see the documentation). If they are valid, check whether the developer's testing devices are running over a private or public network. If it is a private network, ask the developer to check whether the following URL can be connected to: openmsf.3g.qq.com:15000. If yes, check whether the following URL can be connected to: cloud.tim.qq.com:15000.</td>
</tr>
<tr>
<td>AV_ERR_SERVER<br>_ID_NOT_IN_ROOM</td>
<td>10006</td>
<td>Not in a room</td>
<td>A client performs some operations when it is not in a room.</td>
<td>Ensure that SDK features are used at the right time.</td>
</tr>
<tr>
<td>AV_ERR_SERVER<br>_NOT_IMPLEMENT</td>
<td>10007</td>
<td>Not implemented</td>
<td>The feature is not available yet when an SDK API is called.</td>
<td>Find other alternative methods.</td>
</tr>
<tr>
<td>AV_ERR_SERVER<br>_REPEATED_OPERATION</td>
<td>10008</td>
<td>Repeated operation</td>
<td>An operation is performed when another operation of the same type is in progress.</td>
<td>Perform the next operation after the ongoing operation is completed.</td>
</tr>
<tr>
<td>AV_ERR_SERVER<br>_ROOM_NOT_EXIST</td>
<td>10009</td>
<td>Room does not exist</td>
<td>A client is performing an operation related to a room that does not exist.</td>
<td>Ensure that SDK features are used at the right time.</td>
</tr>
<tr>
<td>AV_ERR_SERVER<br>_ENDPOINT_NOT_EXIST</td>
<td>10010</td>
<td>The member does not exist.</td>
<td>Some operations related to a nonexistent member are performed.</td>
<td>Analyze logs, obtain the real error code returned from the backend to the client, and ask backend personnel for help.</td>
</tr>
<tr>
<td>AV_ERR_SERVER<br>_INVALID_ABILITY</td>
<td>10011</td>
<td>Invalid capability</td>
<td>Locate the specific cause based on the real error code (in logs) returned from the backend to a client.</td>
<td>Analyze logs, obtain the real error code returned from the backend to the client, and ask backend personnel for help.</td>
</tr>
</tbody></table>

## Speech-to-Text Errors

| Error Code Name | Error Code Value | Description | Cause | Suggested Solution |
| -------------------------------------------------- | -------- | ------------------ | ---------------------------------------------------------- | ------------------------------------------------------------ |
| QAVPTTERROR_RECORDER<br>\_PARAM_NULL                    | 4097     | Recording error           | Parameter is empty.                                                    | Check whether the API parameters in the code are correct.                                 |
| QAVPTTERROR_RECORDER<br>\_INIT_ERROR                    | 4098     | Recording error           | Initialization error |                                                  | Confirm that the device is not occupied, the permissions are granted, and the initialization process goes well.      |
| QAVPTTERROR_RECORDER<br>\_RECORDING_ERR                 | 4099     | Recording error           | Recording is in progress. | Ensure that the SDK recording feature is used at the right time. |
| QAVPTTERROR_RECORDER<br>\_NODATA_ERR                    | 4100   | Recording error | Audio data is not collected. | Check if the microphone is working properly. |
| QAVPTTERROR_RECORDER<br>\_OPENFILE_ERR                  | 4101     | Recording error | An error occurs during access to a recording file. | Ensure the existence of the file and the validity of the file path. |
| QAVPTTERROR_RECORDER<br>\_PERMISSION_MIC_ERR            | 4102     | Recording error | No microphone permission. | Microphone permission is required for using SDK. To add the permission, see SDK project configuration document for the specific engine or platform. |
| QAVPTTERROR_RECORDER<br>\_AUDIO_TOO_SHORT               | 4103     | Recording error | The recording time is too short. | The recording time should be in ms and longer than 1,000 milliseconds. |
| QAVPTTERROR_RECORDER<br>\_RECORD_NOT_START              | 4104     |  Recording error | No recording operation is started. | Check whether the API for starting recording has been called. |
| QAVPTTERROR_UPLOAD<br>\_FILE_ACCESSERROR                | 8193     | Upload error | An error occurs during file access. | Ensure the existence of the file and the validity of the file path. |
| QAVPTTERROR_UPLOAD<br>\_SIGN_CHECK_FAIL                 | 8194     | Upload error | The signature verification failed. | Check whether the authentication key is correct, and the voice messaging and speech-to-text feature has been initialized. |
| QAVPTTERROR_UPLOAD<br>\_COS_INTERNAL_FAIL               | 8195     | Upload error | A network error occurs. | Check if the device can access the Internet. See [How do I troubleshoot network problems](https://intl.cloud.tencent.com/document/product/607/35611#.E5.87.BA.E7.8E.B0.E7.BD.91.E7.BB.9C.E9.97.AE.E9.A2.98.EF.BC.8C.E8.AF.A5.E5.A6.82.E4.BD.95.E6.8E.92.E6.9F.A5.EF.BC.9F).|
| QAVPTTERROR_UPLOAD<br>\_COS_INTERNAL_FAIL               | 8195     | Upload error | A network failure occurs when getting upload parameters. | Check if the device can access the Internet. See [How do I troubleshoot network problems](https://intl.cloud.tencent.com/document/product/607/35611#.E5.87.BA.E7.8E.B0.E7.BD.91.E7.BB.9C.E9.97.AE.E9.A2.98.EF.BC.8C.E8.AF.A5.E5.A6.82.E4.BD.95.E6.8E.92.E6.9F.A5.EF.BC.9F).|
| QAVPTTERROR_UPLOAD<br>\_SYSTEM_INNER_ERROR              | 8197  |  Upload error | The packet returned is empty when getting upload parameters. | Check whether the authentication is correct and whether the device can access the Internet. See [How do I troubleshoot network problems](https://intl.cloud.tencent.com/document/product/607/35611#.E5.87.BA.E7.8E.B0.E7.BD.91.E7.BB.9C.E9.97.AE.E9.A2.98.EF.BC.8C.E8.AF.A5.E5.A6.82.E4.BD.95.E6.8E.92.E6.9F.A5.EF.BC.9F).|
| QAVPTTERROR_UPLOAD<br>\_RSP_DATA_DECODE_FAIL            | 8198     | Upload error           | The packet returned fails to be parsed when getting upload parameters. | Check whether the authentication is correct and whether the device can access the Internet. See [How do I troubleshoot network problems](https://intl.cloud.tencent.com/document/product/607/35611#.E5.87.BA.E7.8E.B0.E7.BD.91.E7.BB.9C.E9.97.AE.E9.A2.98.EF.BC.8C.E8.AF.A5.E5.A6.82.E4.BD.95.E6.8E.92.E6.9F.A5.EF.BC.9F). |
| QAVPTTERROR_UPLOAD<br>\_APPINFO_UNSET                   | 8200     | Upload error           | `appinfo` is not specified.                                          | Check whether the `apply` API is called or the input parameter is empty.                |
| QAVPTTERROR_DOWNLOAD<br>\_FILE_ACCESSERROR              | 12289    | Download error | A file access error occurs when downloading a file. | Check if the file path is valid. |                                       |
| QAVPTTERROR_DOWNLOAD<br>\_SIGN_CHECK_FAIL               | 12290    | Download error | The signature verification failed. | Check whether the authentication key is correct, and the voice messaging and speech-to-text feature has been initialized. |
| QAVPTTERROR_DOWNLOAD<br>\_COS_INTERNAL_FAIL             | 12291    | Download error | Network error. | The server failed to get the audio file. Check whether the API parameter `fileid` is correct and whether the network is normal. |
| QAVPTTERROR_DOWNLOAD<br>\_REMOTEFILE_ACCESSERROR        | 12292    | Download error  | Server file system error. | Check whether the device can access the Internet and whether the file exists on the server. |
| QAVPTTERROR_DOWNLOAD<br>\_GET_SIGN_NETWORK_FAIL         | 12293    | Download error          | HTTP network failure occurs when getting download parameters.  | Check if the device can access the Internet. See [How do I troubleshoot network problems](https://intl.cloud.tencent.com/document/product/607/35611#.E5.87.BA.E7.8E.B0.E7.BD.91.E7.BB.9C.E9.97.AE.E9.A2.98.EF.BC.8C.E8.AF.A5.E5.A6.82.E4.BD.95.E6.8E.92.E6.9F.A5.EF.BC.9F).|
| QAVPTTERROR_DOWNLOAD<br>\_SYSTEM_INNER_ERROR            | 12294    | Download error           | The packet returned is empty when getting upload parameters. | Check whether the device can access the Internet. See [How do I troubleshoot network problems](https://intl.cloud.tencent.com/document/product/607/35611#.E5.87.BA.E7.8E.B0.E7.BD.91.E7.BB.9C.E9.97.AE.E9.A2.98.EF.BC.8C.E8.AF.A5.E5.A6.82.E4.BD.95.E6.8E.92.E6.9F.A5.EF.BC.9F).|
| QAVPTTERROR_DOWNLOAD_GET<br>\_SIGN_RSP_DATA_DECODE_FAIL | 12295    |  Download error           | The packet returned fails to be parsed when getting upload parameters. | Check whether the device can access the Internet. See [How do I troubleshoot network problems](https://intl.cloud.tencent.com/document/product/607/35611#.E5.87.BA.E7.8E.B0.E7.BD.91.E7.BB.9C.E9.97.AE.E9.A2.98.EF.BC.8C.E8.AF.A5.E5.A6.82.E4.BD.95.E6.8E.92.E6.9F.A5.EF.BC.9F). |
| QAVPTTERROR_DOWNLOAD<br>\_APPINFO_UNSET                 | 12297    | Download error | `appinfo` is not specified. | Check whether the authentication key is correct, and the voice messaging and speech-to-text feature has been initialized.  |
| QAVPTTERROR_PLAYER_INIT_ERR                        | 20481    | Playback error           |  Initialization error. |                                                  | Confirm that the device is not occupied, the permissions are granted, and the initialization process goes well.      |       |
| QAVPTTERROR_PLAYER<br>\_PLAYING_ERR                     | 20482    | Playback error | During playback, the client tried to interrupt and play back the next one but failed (which should succeed normally). | Check whether the code logic is correct. |                                       |
| QAVPTTERROR_PLAYER<br>\_PARAM_NULL                      | 20483    | Playback error           | Parameter is empty.                                                    | Check whether the API parameters in the code are correct.                                 |
| QAVPTTERROR_PLAYER<br>\_OPENFILE_ERR                    | 20484    |Playback error | A playback error occurs during file access. | Ensure the existence of the file and the validity of the file path. |
| QAVPTTERROR_PLAYER<br>\_PLAYER_NOT_START_ERR            | 20485    | Playback error           | Playback is not started. | Ensure the existence of the file and the validity of the file path. |                             |
| QAVPTTERROR_S2T<br>\_INTERNAL_ERROR                     | 32769    | Speech-to-text error     | Internal error.                                                   | Contact Tencent Cloud technical support for assistance, and provide your logs as instructed in [FAQ > Download and Use](https://intl.cloud.tencent.com/document/product/607/30256). |
| QAVPTTERROR_S2T<br>\_NETWORK_FAIL                       | 32770    | Speech-to-text error         | Network failure.   | Check if the device can access the Internet. See [How do I troubleshoot network problems](https://intl.cloud.tencent.com/document/product/607/35611#.E5.87.BA.E7.8E.B0.E7.BD.91.E7.BB.9C.E9.97.AE.E9.A2.98.EF.BC.8C.E8.AF.A5.E5.A6.82.E4.BD.95.E6.8E.92.E6.9F.A5.EF.BC.9F).|
| QAVPTTERROR_S2T<br>\_RSP_DATA_DECODE_FAIL               | 32772    | Speech-to-text error     | The packet returned failed to be parsed.                                                   | Contact Tencent Cloud technical support for assistance, and provide your logs as instructed in [FAQ > Download and Use](https://intl.cloud.tencent.com/document/product/607/30256). |
| QAVPTTERROR_S2T<br>\_APPINFO_UNSET                      | 32774    | Speech-to-text error     | `appinfo` is not specified.                                           | Check whether the authentication key is correct, and whether the voice messaging and speech-to-text feature has been initialized.         |
| QAVPTTERROR_STREAMIN<br>\_RECORD_SUC_REC_FAIL           | 32775    | Streaming speech-to-text converting error | Streaming speech-to-text converting fails, but recording is successful. | Check if the network is connected correctly, and if the permission key is correct. |
| QAVPTTERROR_S2T<br>\_SIGN_CHECK_FAIL                    | 32776    | authbuffer check failure | authbuffer check failed. | Check if authbuffer is correct. |                                   |
| QAVPTTERROR_STREAMIN<br>\_RECORD_SUC_REC_FAIL           | 32775    | Streaming speech-to-text converting error | Streaming speech-to-text converting fails, but recording and upload are successful. | Check if there are any errors in the code. |
| QAVPTTERROR_S2T_PARAM_NULL                         | 32784    | Speech-to-text error     | Invalid speech-to-text parameter                                      | Check whether the API parameter `fileid` is empty in the code.                |
| QAVPTTERROR_S2T<br>\_AUTO_SPEECH_REC_ERROR              | 32785    | Speech-to-text error     | An error occurred when getting the text from speech-to-text conversion.                                            | Contact Tencent Cloud technical support for assistance, and provide your logs as instructed in [FAQ > Download and Use](https://intl.cloud.tencent.com/document/product/607/30256). |
| QAVPTTERROR_ERR<br>\_VOICE_STREAMIN_RUNING_ERROR        | 32786    | Streaming speech-to-text converting error | Streaming speech-to-text converting failed.                                         | Stream recording is in progress. Wait for the stream recording API to return a response.        |
| QAVPTTERROR_ERR_VOICE<br>\_STREAMING_ASR_ERROR          | 50012    | Streaming speech-to-text converting error | ASR request error.                                                | Upload the recorded file again using the UploadRecordedFile API, and then call the SpeechToText API. Meanwhile, contact Tencent Cloud technical support for assistance, and provide your logs as instructed in [FAQ > Download and Use](https://intl.cloud.tencent.com/document/product/607/30256).  |
