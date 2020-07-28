This document provides error codes that may be reported during Tencent Cloud Game Multimedia Engine (GME) development so that developers can easily debug and access GME APIs.

## General Errors

| Error Code Name | Error Code Value | Cause and Suggested Solution |
|--------|-------|------------|
|AV_ERR_3DVOICE_ERR_NOT_INITED       |7003| The `InitSpatializer` API needs to be called first. |
|AV_ERR_NET_REQUEST_FALLED |7004| Network request failed mainly due to an unstable network connection. To troubleshoot, see [FAQ > Voice Chat Room](https://intl.cloud.tencent.com/document/product/607/35611). |
|AV_ERR_CHARGE_OVERDUE     |7005| Operation failed due to account arrears. You need to check whether your account is in arrears in the Tencent Cloud Console. |
|AV_ERR_AUTH_FIALD         |7006| Authentication failed. Possible causes: 1. The `AppID` does not exist or is incorrect; 2. An error occurred while authenticating the `authbuff`; 3. Authentication expired. |
|AV_ERR_IN_OTHER_ROOM      |7007| Already in another room. |
|AV_ERR_NO_PERMISSION      |7009| No permission to perform the operation. |
|AV_ERR_FILE_CANNOT_ACCESS |7010| Unable to access the file. |
|AV_ERR_FILE_DAMAGED       |7011| File is corrupted. |
|AV_ERR_SERVICE_NOT_OPENED       |7012| Please enable this feature in the console before using it. |
|AV_ERR_USER_CANCELED       |7013| The user canceled an operation before it succeeds, such as entering a room. |
|AV_ERR_LOAD_LIB_FAILED       |7014| The library file is not loaded properly, please check if it is missing. |
|AV_ERR_SDK_NOT_FULL_UPDATE       |7015|When upgrading the SDK, not all files were upgraded, which caused some module mismatches. Please fully upgrade the SDK. |
|AV_ERR_3DVOICE_ERR_FILE_DAMAGED       |7002| Failed to load the 3D sound effect file. |

## Client Errors

| Error Code Name | Error Code Value | Description | Cause | Suggested Solution |
|--------|----|-------|--------------------|-------------------|
| AV_ERR_REPEATED_OPERATION | 1001 | Repeated operation | An operation is performed when the same operation is in progress. Operation types include AVContext, room, device, and member. AVContext operations: StartContext/StopContext. Room operations: EnterRoom/ExitRoom. Device operations: start/shut down a device. | Perform an operation after the last one is completed. |
| AV_ERR_EXCLUSIVE_OPERATION | 1002 | Exclusive operation | An operation is performed when another operation of the same type is in progress. | Perform an operation after the last one is completed. |
| AV_ERR_HAS_IN_THE_STATE | 1003 | Repeated operation | An operation is performed to bring an object into a state which it is already in. For example, perform a room entry operation on a client that is already in the room. | Regard the current operation result as successful because the object is already in the required state. |
| AV_ERR_INVALID_ARGUMENT | 1004 | Invalid parameter | One or more incorrect parameters are passed when an SDK API is called. For example, when a client is trying to enter a room, the input room type is not AVRoom::ROOM_TYPE_PAIR or AVRoom::ROOM_TYPE_MULTI. | Read the relevant API document carefully to get the valid value range for each parameter of each API. Take preventive measures to ensure the correctness of input parameters. |
| AV_ERR_TIMEOUT | 1005 | Timeout | The result of an operation is not returned within the specified time. This error occurs mostly when signaling transmission is involved and network problem occurs. For example, after a client performs an operation to enter a room, the result of the operation is not returned within 30 seconds. | Check whether the network is normal and whether the external network can be connected, and then try again. |
| AV_ERR_NOT_IMPLEMENTED | 1006 | Not implemented | The feature has not been available when an SDK API is called. | Find other alternative methods. |
| AV_ERR_NOT_IN_MAIN_THREAD | 1007 | Not in the main thread | External SDK APIs must be called in the main thread, but a client fails to do so. | Modify the service logic to ensure that SDK APIs are called in the main thread. |
| AV_ERR_RESOURCE_IS_OCCUPIED | 1008 | Occupied resource | A required resource, such as the camera or screen, has already been occupied. | Identify the specific resources to be used and confirm the reason why these resources are occupied to ensure that SDK features are used at the right time without resource conflict. |
| AV_ERR_CONTEXT_NOT_EXIST | 1101 | Invalid AVContext status | When an AVContext object is not in the CONTEXT_STATE_STARTED status, a client calls an API that can be called only when the AVContext object is in this status. | Modify the service logic to ensure that SDK APIs are called at the right time. |
| AV_ERR_CONTEXT_NOT_STOPPED | 1102 | Invalid AVContext status | When an AVContext object is not in the CONTEXT_STATE_STOPPED status, a client calls an API that can be called only when the AVContext object is in this status, such as the API AVContext::DestroyContext. | Modify the service logic to ensure that SDK APIs are called at the right time. |
| AV_ERR_ROOM_NOT_EXIST | 1201 | Invalid AVRoom status | When an AVRoom object is not in the ROOM_STATE_ENTERED status, a client calls an API that can be called only when the AVRoom object is in this status. | Modify the service logic to ensure that SDK APIs are called at the right time. |
| AV_ERR_ROOM_NOT_EXITED | 1202 | Invalid AVRoom status | When an AVRoom object is not in the ROOM_STATE_EXITED status, a client calls an API that can be called only when the AVRoom object is in this status, such as the API AVContext::StopContext. | Modify the service logic to ensure that SDK APIs are called at the right time. |
| AV_ERR_DEVICE_NOT_EXIST | 1301 | The device does not exist. | A client uses a device that does not exist or has not been initialized. | Verify that the device exists, ensure that the device ID is entered correctly, and use the device after it is successfully initialized. |
| AV_ERR_ENDPOINT_NOT_EXIST | 1401 | The AVEndpoint object does not exist. | When a member has not initiated a voice chat or video chat, a client tries to obtain the AVEndpoint object of the member. | Modify the service logic to ensure that SDK APIs are called at the right time. |
| AV_ERR_ENDPOINT_HAS_NOT_VIDEO | 1402 | The member does not initiate a video chat. | When a member has not initiated a video chat, a client performs an operation that can be completed only after a video is initiated. For example, when a member has not initiated a video chat, a client requests the video image of the member. | Modify the service logic to ensure that SDK APIs are called at the right time. |
| AV_ERR_TINYID_TO_OPENID_FAILED | 1501 | Failed to convert a tinyid into an identifier. | After receiving the signaling indicating a member's information update, a client needs to convert the tinyid into an identifier. However, the conversion fails due to issues with the logic of the IMSDK library or the network. | Confirm that the network works well, and check logs for any problem with the logic of the IMSDK library. |
| AV_ERR_OPENID_TO_TINYID_FAILED | 1502 | Failed to convert an identifier into a tinyid. | When calling the StartContext API, a client needs to convert the identifier into a tinyid. However, the conversion fails due to issues with the logic of the IMSDK library, the network, or no login status. | Confirm that the network works well, check logs for any problem with the logic of the IMSDK library, and confirm that the IMSDK login API has been successfully called. |
| AV_ERR_DEVICE_TEST_NOT_EXIST | 1601 | Invalid AVDeviceTest status | When an AVDeviceTest object is not in the DEVICE_TEST_STATE_STARTED status, a client calls an API that can be called only when the AVDeviceTest object is in this status. | Modify the service logic to ensure that SDK APIs are called at the right time. |
| AV_ERR_DEVICE_TEST_NOT_STOPPED | 1602 | Invalid AVDeviceTest status | When an AVDeviceTest object is not in the DEVICE_TEST_STATE_STOPPED status, a client calls an API that can be called only when the AVDeviceTest object is in this status, such as the API AVContext::StopContext. | Modify the service logic to ensure that SDK APIs are called at the right time. |
| AV_ERR_INVITE_FAILED | 1801 | Failed to send an invitation. | A failure occurs when a client tries to send an invitation. | The invitation module is used only for Demo, and the invitation feature is not available yet. So this error code can be ignored. |
| AV_ERR_ACCEPT_FAILED | 1802 | Failed to accept an invitation. | A failure occurs when a client tries to accept an invitation. | The invitation module is used only for Demo, and the invitation feature is not available yet. So this error code can be ignored. |
| AV_ERR_REFUSE_FAILED | 1803 | Failed to refuse an invitation. | A failure occurs when a client tries to reject an invitation. | The invitation module is used only for demo, and the invitation feature is not available yet. So this error code can be ignored. |
| QAV_ERR_NOT_TRY_NEW_ROOM | 2001 | A client fails to enter a new room and remains in the original room. | A client fails to switch to a new room and remains in the current room. | Remain in the current room. |
| QAV_ERR_TRY_NEW_ROOM_FAILED | 2002 | A client attempts to enter a new room but fails, and exits the original room. | A client fails to switch to a new room and has exited the original room. | Enter a room again. |


## Server Errors

| Error Code Name | Error Code Value | Description | Cause | Suggested Solution |
|-----------------------------------|-----|-----|----------------------------------------------------------------------------------------------|---------------------------------------------------------|
| AV_ERR_SERVER_FAILED | 10001 | Common error | Locate the specific cause based on the real error code (in logs) returned from the backend to a client. | View and confirm the validity of the parameters in the API for room entry, such as AppID, UIN and AuthBuffer (see the documentation). In the console, check whether the relevant parameters match the local ones, and whether there is any account arrears. Check whether the developer's testing devices are running over a private or public network. |
| AV_ERR_SERVER_INVALID_ARGUMENT | 10002 | Invalid parameter | One or more incorrect parameters are passed when an SDK API is called or when internal SDK signaling is sent to the backend. | Ensure the correctness of parameters passed in SDK API calls. Analyze logs, obtain the real error code returned from the backend to the client, and ask backend personnel for help. |
| AV_ERR_SERVER_NO_PERMISSION | 10003 | No permission | A client has no permission to use a feature. For example, a client provides an incorrect or expired signature when it tries to enter a room. | Be sure to use a feature only after providing correct permission parameters. Check whether the AppID and permission key are correct. |
| AV_ERR_SERVER_TIMEOUT | 10004 | Timeout | The result of an operation is not returned within the specified time. | Analyze logs, obtain the real error code returned from the backend to the client, and ask backend personnel for help. |
| AV_ERR_SERVER_ALLOC_RESOURCE_FAILED | 10005 | Network error | Network error occurs when a client performs an operation. | View and confirm the validity of the parameters in the API for room entry, such as AppID, UIN and AuthBuffer (see the documentation). If they are valid, check whether the developer's testing devices are running over a private or public network. If it is a private network, ask the developer to check whether the following URL can be connected to: openmsf.3g.qq.com:15000. If yes, check whether the following URL can be connected to: cloud.tim.qq.com:15000. |
| AV_ERR_SERVER_ID_NOT_IN_ROOM | 10006 | Not in a room | A client performs some operations when it is not in a room. | Ensure that SDK features are used at the right time. |
| AV_ERR_SERVER_NOT_IMPLEMENT | 10007 | Not implemented | The feature has not been available when an SDK API is called. | Find other alternative methods. |
| AV_ERR_SERVER_REPEATED_OPERATION | 10008 | Repeated operation | An operation is performed when another operation of the same type is in progress. | Perform an operation only after the last operation is completed. |
| AV_ERR_SERVER_ID_NOT_IN_ROOM | 10009 | The room does not exist. | A client performs an operation on a room that does not exist. | Ensure that SDK features are used at the right time. |
| AV_ERR_SERVER_ENDPOINT_NOT_EXIST | 10010 | The member does not exist. | Some operations related to a nonexistent member are performed. | Analyze logs, obtain the real error code returned from the backend to the client, and ask backend personnel for help. |
| AV_ERR_SERVER_INVALID_ABILITY | 10011 | Invalid capability | Locate the specific cause based on the real error code (in logs) returned from the backend to a client. | Analyze logs, obtain the real error code returned from the backend to the client, and ask backend personnel for help. |

## Voice Message Errors

| Error Code Name | Error Code Value | Description | Cause | Suggested Solution |
|------|-----|-----|------|------|
| QAVPTTERROR_RECORDER_PARAM_NULL | 4097 | Recording error | Empty parameter. | Check whether the API parameters in the code are correct. |
| QAVPTTERROR_RECORDER_INIT_ERROR | 4098 | Recording error | Initialization error. | Check whether the device is occupied, whether the permissions are normal, and whether the initialization is normal. |
| QAVPTTERROR_RECORDER_RECORDING_ERR | 4099 | Recording error | Recording is in progress. | Ensure that the SDK recording feature is used at the right time. |
| QAVPTTERROR_RECORDER_NODATA_ERR | 4100 | Recording error | Audio data is not collected. | Check if the microphone is working properly. |
| QAVPTTERROR_RECORDER_OPENFILE_ERR | 4101 | Recording error | An error occurs during access to a recording file. | Ensure the existence of the file and the validity of the file path. |
| QAVPTTERROR_RECORDER_PERMISSION_MIC_ERR | 4102 | Recording error | The microphone is not authorized. | Microphone permission is required for using SDK. To add the permission, see SDK project configuration document for the specific engine or platform. |
| QAVPTTERROR_RECORDER_AUDIO_TOO_SHORT | 4103 | Recording error | The recording time is too short. | The recording time should be in ms and longer than 1,000 milliseconds. |
| QAVPTTERROR_RECORDER_RECORD_NOT_START | 4104 | Recording error | No recording operation is started. | Check whether the API for starting recording has been called. |
| QAVPTTERROR_UPLOAD_FILE_ACCESSERROR | 8193 | Upload error | An error occurs during file access. | Ensure the existence of the file and the validity of the file path. |
| QAVPTTERROR_UPLOAD_SIGN_CHECK_FAIL | 8194 | Upload error | The signature verification fails. | Check if the authentication key is correct, and if the voice message is initialized. |
| QAVPTTERROR_UPLOAD_COS_INTERNAL_FAIL | 8195 | Upload error | A network error occurs. | Check if the device can access the internet. |
| QAVPTTERROR_UPLOAD_GET_TOKEN_NETWORK_FAIL | 8196 | Upload error | The network failed while getting the upload parameters. | Check whether the authentication is correct and whether the device can access the internet. |
| QAVPTTERROR_UPLOAD_SYSTEM_INNER_ERROR | 8197 | Upload error | The packet returned during the process of getting the upload parameters is empty. | Check whether the authentication is correct and whether the device network can normally access the external network environment. |
| QAVPTTERROR_UPLOAD_RSP_DATA_DECODE_FAIL | 8198 | Upload error | Failed to decode the packet returned during the process of getting the upload parameters. | Check whether the authentication is correct and whether the device can access the internet. |
| QAVPTTERROR_UPLOAD_APPINFO_UNSET | 8200 | Upload error | No `appinfo` is set. | Check whether the `apply` API is called or whether the input parameters are empty. |
| QAVPTTERROR_DOWNLOAD_FILE_ACCESSERROR | 12289 | Download error | An error occurs during file access. | Check if the file path is valid. |
| QAVPTTERROR_DOWNLOAD_SIGN_CHECK_FAIL | 12290 | Download error | The signature verification fails. | Check if the authentication key is correct, and if the voice message is initialized. |
| QAVPTTERROR_DOWNLOAD_COS_INTERNAL_FAIL | 12291 | Download error | Network error. | The server failed to get the audio file. Check whether the API parameter `fileid` is correct and whether the network is normal. |
| AVPTTERROR_DOWNLOAD_REMOTEFILE_ACCESSERROR | 12292 | Download error | Server file system error. | Check whether the device can access the internet and whether the file exists on the server. |
| QAVPTTERROR_DOWNLOAD_GET_SIGN_NETWORK_FAIL | 12293 | Download error | The HTTP network failed during the process of getting the download parameters. | Check whether the device can access the internet. |
| QAVPTTERROR_DOWNLOAD_SYSTEM_INNER_ERROR | 12294 | Download error | The packet returned during the process of getting the download parameters is empty. | Check whether the device can access the internet. |
| QAVPTTERROR_DOWNLOAD_GET_SIGN_RSP_DATA_DECODE_FAIL | 12295 | Download error | Failed to decode the packet returned during the process of getting the download parameters. | Check whether the device can access the internet. |
| QAVPTTERROR_DOWNLOAD_APPINFO_UNSET | 12297 | Download error | The appinfo is not set. | Check if the authentication key is correct, and if the voice message is initialized. |
| QAVPTTERROR_PLAYER_INIT_ERR | 20481 | Playback error | Initialization error. | Check whether the device is being used, whether the permissions are normal, and whether the initialization is normal. |
| QAVPTTERROR_PLAYER_PLAYING_ERR | 20482 | Playback error | During playback, the client tried to interrupt and play back the next one but failed (which should succeed normally). | Check whether the code logic is correct. |
| QAVPTTERROR_PLAYER_PARAM_NULL | 20483 | Playback error | Parameter is empty. | Check whether the API parameters in the code are correct. |
| QAVPTTERROR_PLAYER_OPENFILE_ERR | 20484 | Playback error | A playback error occurs during file access. | Ensure the existence of the file and the validity of the file path. |
| QAVPTTERROR_PLAYER_PLAYER_NOT_START_ERR | 20485 | Playback error | Playback is not started. | Ensure the existence of the file and the validity of the file path. |
| QAVPTTERROR_S2T_INTERNAL_ERROR | 32769 | Speech-to-text converting error | An internal error occurs. | Analyze logs, obtain the real error code returned from the backend to the client, and ask backend personnel for help. |
| QAVPTTERROR_S2T_NETWORK_FAIL | 32770 | Speech-to-text conversion error | Network failed. | Check whether the device can access the internet. |
| QAVPTTERROR_S2T_RSP_DATA_DECODE_FAIL | 32772 | Speech-to-text converting error | The response packet fails to be parsed. | Analyze logs, obtain the real error code returned from the backend to the client, and ask backend personnel for help. |
| QAVPTTERROR_S2T_APPINFO_UNSET | 32774 | Speech-to-text converting error | The appinfo is not set. | Check if the authentication key is correct, and if the voice message is initialized. |
| QAVPTTERROR_STREAMIN_RECORD_SUC_REC_FAIL | 32775 | Streaming speech-to-text converting error | Streaming speech-to-text converting fails, but recording is successful. | Check if the network is connected correctly, and if the permission key is correct. |
| QAVPTTERROR_S2T_SIGN_CHECK_FAIL | 32776 | authbuffer check failure | authbuffer check fails. | Check if authbuffer is correct. |
| QAVPTTERROR_STREAMIN_UPLOADANDRECORD_SUC_REC_FAIL | 32777 | Streaming speech-to-text converting error | Streaming speech-to-text converting fails, but recording and upload are successful. | Check if there are any errors in the code. |
| QAVPTTERROR_S2T_PARAM_NULL | 32784 | Speech-to-text conversion error | Incorrect speech-to-text conversion parameter. | Check whether the API parameter `fileid` in the code is empty. |
| QAVPTTERROR_S2T_AUTO_SPEECH_REC_ERROR | 32785 | Speech-to-text conversion error | Speech-to-text translation returned an error. | Error with the backend of voice messaging and speech-to-text feature. Analyze logs, get the actual error code returned from the backend to the client, and ask backend personnel for assistance. |
| QAVPTTERROR_ERR_VOICE_STREAMIN_RUNING_ERROR | 32786 | Streaming speech-to-text conversion error | Streaming speech-to-text conversion failed. | During streaming recording, wait for the execution result of the streaming recording API to return. |


