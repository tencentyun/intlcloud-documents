Thanks for using Tencent Cloud Game Multimedia Engine (GME) SDK. This document describes error codes to help developers debug and access GME APIs.

## General Errors
|Error Name|Value|Cause and Solution|
|--------|-------|------------|
| AV_ERR_NET_REQUEST_FALLED |7004|Network request fails, which is usually caused by unstable network status. It is recommended to check the network status.|
| AV_ERR_CHARGE_OVERDUE   |7005|Failure is caused by account arrears, check whether the account is in arrears on Tencent Cloud Console.|
| AV_ERR_AUTH_FIALD     |7006|Authentication failure is caused by the following reasons: 1. Appid does not exist or is incorrect; 2. authbuff authentication error; 3. Authentication expired|
| AV_ERR_IN_OTHER_ROOM   |7007|Already in other rooms|
| AV_ERR_DISSOLVED_OVERUSER |7008|Billed by DAU, the room is dismissed after more than 90 minutes|
| AV_ERR_NO_PERMISSION   |7009|No permission to operate |
| AV_ERR_FILE_CANNOT_ACCESS |7010|Unable to access file|
| AV_ERR_FILE_DAMAGED    |7011|File is damaged|
| AV_ERR_3DVOICE_ERR_FILE_DAMAGED    |7002|Failed to load 3D sound file|
| AV_ERR_3DVOICE_ERR_NOT_INITED    |7003|The InitSpatializer API must be called first|


## Client Errors
| Error Name | Value | Description | Cause | Solution |
|--------|----|-------|--------------------|-------------------|
| AV_ERR_REPEATED_OPERATION | 1001 | Repeated operation | "An operation is performed when the same operation is in progress. Operation types include AVContext, room, device, and member. AVContext-related operations: StartContext/StopContext. Room-related operations: EnterRoom/ExitRoom. Device-related operations: start/shut down a device. Member-related operations: video image request/cancellation." | Perform next operation after the last operation is completed. |
| AV_ERR_EXCLUSIVE_OPERATION | 1002 | Exclusive operation | An operation is performed when another operation of the same type is in progress. | Perform next operation after the last operation is completed. |
| AV_ERR_HAS_IN_THE_STATE | 1003 | Repeated operation | An operation is performed to enable an object to enter a state when the object is already in the state. For example, when a client is already in a room, it performs an operation to enter the room again. | Regard the current operation result as successful because the object is already in the required state. |
| AV_ERR_INVALID_ARGUMENT | 1004 | Invalid parameter | One or more incorrect parameters are passed when an SDK API is called. For example, when a client is trying to enter a room, the input room type is not AVRoom::ROOM_TYPE_PAIR or AVRoom::ROOM_TYPE_MULTI. | Read the relevant API document carefully to get the valid value range for each parameter of each API. Take preventive measures to ensure the correctness of input parameters. |
| AV_ERR_TIMEOUT | 1005 | Timeout | The result of an operation is not returned within the specified time. This error occurs mostly when signaling is transmitted and the network is exceptional. For example, after a client performs an operation to enter a room, the result of the operation is not returned within 30 seconds. | Check whether the network is normal and whether the external network can be connected, and then try again. |
| AV_ERR_NOT_IMPLEMENTED | 1006 | Not implement | The relevant feature has not been implemented when an SDK API is called. | Find other alternative methods. |
| AV_ERR_NOT_IN_MAIN_THREAD | 1007 | Not in the main thread | External SDK APIs must be called in the main thread, but a client does not call an SDK API in the main thread. | Modify the service logic to ensure that SDK APIs are called in the main thread. |
| AV_ERR_RESOURCE_IS_OCCUPIED | 1008 | Occupied resources | A required resource, such as the camera or screen, has already been occupied. | Identify the specific resources to be used and confirm the reason why these resources are occupied to ensure that SDK features are used at the right time without resource conflict. |
| AV_ERR_CONTEXT_NOT_EXIST | 1101 | Invalid AVContext status | When an AVContext object is not in the CONTEXT_STATE_STARTED status, a client calls an API that can be called only when the AVContext object is in the CONTEXT_STATE_STARTED status. | Modify the service logic to ensure that SDK APIs are called at the right time. |
| AV_ERR_CONTEXT_NOT_STOPPED | 1102 | Invalid AVContext status | When an AVContext object is not in the CONTEXT_STATE_STOPPED status, a client calls an API that can be called only when the AVContext object is in the CONTEXT_STATE_STOPPED status. For example, a client calls AVContext::DestroyContext when an AVContext object is not in the CONTEXT_STATE_STOPPED status. | Modify the service logic to ensure that SDK APIs are called at the right time. |
| AV_ERR_ROOM_NOT_EXIST | 1201 | Invalid AVRoom status | When an AVRoom object is not in the ROOM_STATE_ENTERED status, a client calls an API that can be called only when the AVRoom object is in the ROOM_STATE_ENTERED status. | Modify the service logic to ensure that SDK APIs are called at the right time. |
| AV_ERR_ROOM_NOT_EXITED | 1202 | Invalid AVRoom status | When an AVRoom object is not in the ROOM_STATE_EXITED status, a client calls an API that can be called only when the AVRoom object is in the ROOM_STATE_EXITED status. For example, a client calls AVContext::StopContext when an AVRoom object is not in the ROOM_STATE_EXITED status. | Modify the service logic to ensure that SDK APIs are called at the right time. |
| AV_ERR_DEVICE_NOT_EXIST | 1301 | The device does not exist. | A client uses a device that does not exist or has not been initialized. | Verify that the device exists, ensure that the device ID is entered correctly, and use the device after it is successfully initialized. |
| AV_ERR_ENDPOINT_NOT_EXIST | 1401 | The AVEndpoint object does not exist. | When a member has not initiated a voice chat or video chat, a client obtains the AVEndpoint object of the member. | Modify the service logic to ensure that SDK APIs are called at the right time. |
| AV_ERR_ENDPOINT_HAS_NOT_VIDEO | 1402 | The member does not initiate a video chat. | When a member has not initiated a video chat, a client performs an operation that can be completed only after a video chat is initiated. For example, when a member has not initiated a video chat, a client requests the video image of the member. | Modify the service logic to ensure that SDK APIs are called at the right time. |
| AV_ERR_TINYID_TO_OPENID_FAILED | 1501 | Failed to convert a tinyid into an identifier. | After receiving the signaling indicating a member's information update, a client needs to convert the relevant tinyid into an identifier. However, the conversion fails because the relevant logic of the IMSDK library or the network is exceptional. | Check whether the network is normal and check logs to confirm whether the relevant logic of the IMSDK library is normal. |
| AV_ERR_OPENID_TO_TINYID_FAILED | 1502 | Failed to convert an identifier into a tinyid. | When calling the StartContext API, a client needs to convert the relevant identifier into a tinyid. However, the conversion fails because the relevant logic of the IMSDK library or the network is exceptional, or the client is not in the login status. | Check whether the network is normal, check logs to confirm whether the relevant logic of the IMSDK library is normal and verify that the IMSDK login API has been successfully called. |
| AV_ERR_DEVICE_TEST_NOT_EXIST | 1601 | Invalid AVDeviceTest status | When an AVDeviceTest object is not in the DEVICE_TEST_STATE_STARTED status, a client calls an API that can be called only when the AVDeviceTest object is in the DEVICE_TEST_STATE_STARTED status. | Modify the service logic to ensure that SDK APIs are called at the right time. |
| AV_ERR_DEVICE_TEST_NOT_STOPPED | 1602 | Invalid AVDeviceTest status | When an AVDeviceTest object is not in the DEVICE_TEST_STATE_STOPPED status, a client calls an API that can be called only when the AVDeviceTest object is in the DEVICE_TEST_STATE_STOPPED status. For example, a client calls AVContext::StopContext when an AVDeviceTest object is not in the DEVICE_TEST_STATE_STOPPED status. | Modify the service logic to ensure that SDK APIs are called at the right time. |
| AV_ERR_INVITE_FAILED | 1801 | Failed to send an invitation. | A failure occurs when a client tries to send an invitation. | The invitation module is used only for demonstration, and the invitation feature is not supported externally. So this error code can be ignored. |
| AV_ERR_ACCEPT_FAILED | 1802 | Failed to accept an invitation. | A failure occurs when a client tries to accept an invitation. | The invitation module is used only for demonstration, and the invitation feature is not supported externally. So this error code can be ignored. |
| AV_ERR_REFUSE_FAILED | 1803 | Failed to refuse an invitation. | A failure occurs when a client tries to reject an invitation. | The invitation module is used only for demonstration, and the invitation feature is not supported externally. So this error code can be ignored. |
| QAV_ERR_NOT_TRY_NEW_ROOM | 2001 | A client fails to enter a new room and remains in the original room. | A client fails to switch to a new room and remains in the current room. | Remain in the current room. |
| QAV_ERR_TRY_NEW_ROOM_FAILED | 2002 | A client attempts to enter a new room but fails, and exits the original room. | A client fails to switch to a new room and has exited the original room. | Enter a room again. |


## Server Errors

| Error Code Name | Error Code Value | Description | Cause | Suggested Solution |
|-----------------------------------|-----|-----|----------------------------------------------------------------------------------------------|---------------------------------------------------------|
| AV_ERR_SERVER_FAILED | 10001 | Common error | Locate the specific cause based on the real error code (in logs) returned from the backend to a client. | View and confirm the validity of the parameters in the API for room entering, such as Appid, UIN and AuthBuffer (see the documentation). Check whether the relevant parameters in the console match the local ones. Check whether the console is in arrears. Check whether the network environment of the developer's testing devices is a private network or a public network. |
| AV_ERR_SERVER_INVALID_ARGUMENT | 10002 | Invalid parameter | One or more incorrect parameters are passed when an SDK API is called or when internal SDK signaling is sent to the backend. | Ensure the correctness of parameters passed in SDK API calls. Analyze logs, obtain the real error code returned from the backend to the client, and ask backend personnel for help. |
| AV_ERR_SERVER_NO_PERMISSION | 10003 | No permission | A client has no permission to use a feature. For example, a client carries an incorrect or expired signature when it tries to enter a room. | Be sure to use a feature after the permission parameters are correctly set. Check whether the appid and permission key are correct. |
| AV_ERR_SERVER_TIMEOUT | 10004 | Timeout | The result of an operation is not returned within the specified time. | Analyze logs, obtain the real error code returned from the backend to the client, and ask backend personnel for help. |
| AV_ERR_SERVER_ALLOC_RESOURCE_FAILED | 10005 | Network error | Network error occurred when a client performs an operation. | View and confirm the validity of the parameters in the API for room entering, such as Appid, UIN, and AuthBuffer (see the documentation). If they are valid, check whether the network environment of the developer's testing devices is a private network or a public network. If it is a private network, ask the developer to check whether the following URL can be connected to: openmsf.3g.qq.com:15000. If yes, check whether the following URL can be connected to: cloud.tim.qq.com:15000. |
| AV_ERR_SERVER_ID_NOT_IN_ROOM | 10006 | Not in a room | A client performs some operations when it is not in a room. | Ensure that SDK features are used at the right time. |
| AV_ERR_SERVER_NOT_IMPLEMENT | 10007 | Not implement | The relevant feature has not been implemented when an SDK API is called. | Find other alternative methods. |
| AV_ERR_SERVER_REPEATED_OPERATION | 10008 | Repeated operation | An operation is performed when another operation of the same type is in progress. | Perform next operation after the last operation is completed. |
| AV_ERR_SERVER_ROOM_NOT_EXIST | 10009 | The room does not exist. | A client performs some operations when it is not in a room. | Ensure that SDK features are used at the right time. |
| AV_ERR_SERVER_ENDPOINT_NOT_EXIST | 10010 | The member does not exist. | Some operations related to a nonexistent member are performed. | Analyze logs, obtain the real error code returned from the backend to the client, and ask backend personnel for help. |
| AV_ERR_SERVER_INVALID_ABILITY | 10011 | Invalid capability | Locate the specific cause based on the real error code (in logs) returned from the backend to a client. | Analyze logs, obtain the real error code returned from the backend to the client, and ask backend personnel for help. |

## Voice Message Errors

| Error Code Name | Error Code Value | Description | Cause | Suggested Solution |
|------|-----|-----|------|------|
| QAVPTTERROR_RECORDER_PARAM_NULL | 4097 | Recording error | Empty parameters |Check if the API parameters in the codes are correct. |
| QAVPTTERROR_RECORDER_INIT_ERROR | 4098 | Recording error | Initialization error | Check if the device is occupied, the permission is normal, and the initialization is normal. |
| QAVPTTERROR_RECORDER_RECORDING_ERR | 4099 | Recording error | Recording is in progress | Ensure that the SDK recording feature is used at the right time. |
| QAVPTTERROR_RECORDER_NODATA_ERR | 4100 | Recording error | Audio data is not collected | Check if the microphone works properly. |
| QAVPTTERROR_RECORDER_OPENFILE_ERR | 4101 | Recording error | File access error while recording | Ensure that the file exists and its path is valid. |
| QAVPTTERROR_RECORDER_PERMISSION_MIC_ERR | 4102 | Recording error | The microphone is not authorized | Microphone permission is required for using SDK. To add the permission, see SDK project configuration document for the applicable engine or platform. |
| QAVPTTERROR_RECORDER_AUDIO_TOO_SHORT | 4103 | Recording error | The recording time is too short. | The recording time should be in millisecond and longer than 1 second. |
| QAVPTTERROR_RECORDER_RECORD_NOT_START | 4104 | Recording error | No recording start operation | Check if the start recording API is called. |
| QAVPTTERROR_UPLOAD_FILE_ACCESSERROR | 8193 | Upload error | File access error while uploading the file | Ensure that the file exists and its path is valid. |
| QAVPTTERROR_UPLOAD_SIGN_CHECK_FAIL | 8194 | Upload error | Failed to verify signature | Check if the authentication key is correct, and if the offline voice is initialized. |
| QAVPTTERROR_UPLOAD_COS_INTERNAL_FAIL | 8195 | Upload error | Network error | Check if the device can be accessed via a public network. |
| QAVPTTERROR_UPLOAD_GET_TOKEN_NETWORK_FAIL | 8196 | Upload error | The network connection failed while getting upload parameters | Check if the authentication is correct, and the device can be accessed via a public network. |
| QAVPTTERROR_UPLOAD_SYSTEM_INNER_ERROR | 8197 | Upload error | The response packet is empty while getting upload parameters | Check if the authentication is correct, and the device can be accessed via a public network. |
| QAVPTTERROR_UPLOAD_RSP_DATA_DECODE_FAIL | 8198 | Upload error | Failed to parse the response packet while getting upload parameters | Check if the authentication is correct, and the device can be accessed via a public network. |
| QAVPTTERROR_UPLOAD_APPINFO_UNSET | 8200 | Upload error | The appinfo is not set | Check if the applied API is called, or the input parameter is empty. |
| QAVPTTERROR_DOWNLOAD_FILE_ACCESSERROR | 12289 | Download error | File access error while downloading the file | Check if the file path is valid. |
| QAVPTTERROR_DOWNLOAD_SIGN_CHECK_FAIL | 12290 | Download error | The signature verification failed | Check if the authentication key is correct and if the offline voice is initialized. |
| QAVPTTERROR_DOWNLOAD_COS_INTERNAL_FAIL | 12291 | Download error | Network error | The server failed to get voice file. Check if the field is correct and network status is normal. |
| QAVPTTERROR_DOWNLOAD_REMOTEFILE_ACCESSERROR | 12292 | Download error | An error occurs in the file system of the server | Check if the device can be accessed via a public network, and if the server has this file. |
| QAVPTTERROR_DOWNLOAD_GET_SIGN_NETWORK_FAIL | 12293 | Download error | An HTTP network error occurs while getting download parameters | Check if the device can be accessed via a public network. |
| QAVPTTERROR_DOWNLOAD_SYSTEM_INNER_ERROR | 12294 | Download error | The response packet is empty while getting download parameters | Check if the device can be accessed via a public network. |
| QAVPTTERROR_DOWNLOAD_GET_SIGN_RSP_DATA_DECODE_FAIL | 12295 | Download error | Failed to parse the response packet while getting download parameters | Check if the device can be accessed via a public network. |
| QAVPTTERROR_DOWNLOAD_APPINFO_UNSET | 12297 | Download error | The appinfo is not set | Check if the authentication key is correct and if the offline voice is initialized. |
| QAVPTTERROR_PLAYER_INIT_ERR | 20481 | Download error | Initialization error | Check if the device is occupied, the permission is normal, and the initialization is normal. |
| QAVPTTERROR_PLAYER_PLAYING_ERR | 20482 | Playback error | A client fails to stop a video that is being played and play the next one (this can be done normally) | Check if the code logic is correct. |
| QAVPTTERROR_PLAYER_PARAM_NULL | 20483 | Playback error | Empty parameter | Check if the API parameter in the code is correct. |
| QAVPTTERROR_PLAYER_OPENFILE_ERR | 20484 | Playback error | File access error during the playback | Ensure that the file exists and its path is valid. |
| QAVPTTERROR_PLAYER_PLAYER_NOT_START_ERR | 20485 | Playback error | Playback does not start | Ensure that the file exists and its path is valid. |
| QAVPTTERROR_S2T_INTERNAL_ERROR | 32769 | Voice-to-text converting error | Internal error | Analyze logs, obtain the real error code returned from the backend to the client, and ask backend personnel for help. |
| QAVPTTERROR_S2T_NETWORK_FAIL | 32770 | Voice-to-text converting error | Network error | Check if the device can be accessed via a public network. |
| QAVPTTERROR_S2T_RSP_DATA_DECODE_FAIL | 32772 | Voice-to-text converting error | Failed to parse the response packet | Analyze logs, obtain the real error code returned from the backend to the client, and ask backend personnel for help. |
| QAVPTTERROR_S2T_APPINFO_UNSET | 32774 | Voice-to-text converting error | The appinfo is not set | Check if the authentication key is correct, and if the offline voice is initialized. |
| QAVPTTERROR_STREAMIN_RECORD_SUC_REC_FAIL | 32775 | Voice-to-text converting error | Streaming voice-to-text converting fails, but recording is successful | Check if the network is connected correctly, and permission key is correct. |
| QAVPTTERROR_S2T_SIGN_CHECK_FAIL | 32776 | authbuffer verification failed | Failed to verify authbuffer | Check if the authbuffer is correct. |
| QAVPTTERROR_STREAMIN_UPLOADANDRECORD_SUC_REC_FAIL | 32777 | Streaming voice-to-text converting error | Streaming voice-to-text converting failed, but recording is successful. | Check if there is an error in the codes. |
| QAVPTTERROR_S2T_PARAM_NULL | 32784 | Voice-to-text converting error | Voice-to-text converting parameter error | Check if the field parameter is empty in the codes. |
| QAVPTTERROR_S2T_AUTO_SPEECH_REC_ERROR | 32785 | Voice-to-text converting error | Error returned for voice-to-text conversion | There is an offline voice error in the backend. Analyze logs, obtain the real error code returned from the backend to the client, and ask backend personnel for help. |
|QAVPTTERROR_ERR_VOICE_STREAMIN_RUNING_ERROR  |32786 |Streaming voice-to-text converting error   |Streaming voice-to-text converting failed|Streaming recording is in process, please wait for the streaming recording API to return execution result.|