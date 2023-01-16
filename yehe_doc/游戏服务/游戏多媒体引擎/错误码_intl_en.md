
This document provides error codes that may be reported during Tencent Cloud Game Multimedia Engine (GME) development so that developers can easily debug and integrate GME APIs.



## Common Error Codes


| Error Message | Error Code | Cause and Suggested Solution |
| ----------------------------- | --------  | ------------------------------------------------------------ |
| AV_ERR_NET_REQUEST_FALLED         | 7004      | Network request failed mainly due to unstable network connection. To troubleshoot, see [FAQ > Voice Chat Room](https://intl.cloud.tencent.com/document/product/607/39523). |
| AV_ERR_CHARGE_OVERDUE             | 7005      | Operation failed due to overdue payments. You need to check whether your account has any overdue payment in the Tencent Cloud console. |
| AV_ERR_AUTH_FIALD                 | 7006      | Authentication failed. Possible causes: <br>1. The `AppID` does not exist or is incorrect. <br>2 An error occurred while authenticating the `authbuff`. <br>3 Authentication expired. |
|AV_ERR_REPEATED_OPERATION|1001| An operation is performed when the same operation is in progress. Operation types include AVContext, room, device, and member. AVContext operations: StartContext/StopContext. Room operations: EnterRoom/ExitRoom. Device operations: start/shut down a device. Perform an operation after the last one is completed. |
|AV_ERR_EXCLUSIVE_OPERATION         |1002       | An operation is performed when another operation of the same type is in progress. Perform an operation after the last one is completed. |
|AV_ERR_HAS_IN_THE_STATE            |1003       | An operation is performed to bring an object into a state which it is already in. For example, perform a room entry operation on a client that is already in the room. Regard the current operation result as successful because the object is already in the required state. |
|AV_ERR_INVALID_ARGUMENT            |1004       | One or more incorrect parameters are passed when an SDK API is called. For example, when a client is trying to enter a room, the input room type is not AVRoom::ROOM_TYPE_PAIR or AVRoom::ROOM_TYPE_MULTI. Read the relevant API document carefully to get the valid value range for each parameter of each API. Take preventive measures to ensure the correctness of input parameters. |
|AV_ERR_TIMEOUT                     |1005       | The result of an operation is not returned within the specified time. This error occurs mostly when signaling transmission is involved and network problem occurs. For example, after a client performs an operation to enter a room, the result of the operation is not returned within 30 seconds. Check whether the network is normal and whether the external network can be connected, and then try again. |
|AV_ERR_NOT_IMPLEMENTED             |1006       | The feature has not been available when an SDK API is called. |
|AV_ERR_NOT_IN_MAIN_THREAD          |1007       | External SDK APIs must be called in the main thread, but a client fails to do so. Modify the service logic to ensure that SDK APIs are called in the main thread. |
|AV_ERR_CONTEXT_NOT_EXIST           |1101       | When an AVContext object is not in the CONTEXT_STATE_STARTED status, a client calls an API that can be called only when the AVContext object is in this status. Modify the service logic to ensure that SDK APIs are called at the right time. |
|AV_ERR_CONTEXT_NOT_STOPPED         |1102       | When an AVContext object is not in the CONTEXT_STATE_STOPPED status, a client calls an API that can be called only when the AVContext object is in this status, such as the API AVContext::DestroyContext. Modify the service logic to ensure that SDK APIs are called at the right time. |


## Voice Chat Error Codes

| Error Message | Error Code | Cause and Suggested Solution |
| ----------------------------- | --------  | ------------------------------------------------------------ |
|AV_ERR_IN_OTHER_ROOM              |7007       | The user is already in another room. Perform operations after the user exits the room first. |
|AV_ERR_ROOM_NOT_EXIST              |1201       | When the user hasn't entered the room, a client calls an API that can be called only when the user has entered the room. Ensure that SDK APIs are called at the right time. |
|AV_ERR_ROOM_NOT_EXITED             |1202       | When the user hasn't exited the room, a client calls an API that can be called only when the user has exited the room, such as the AVContext::StopContext API. Ensure that SDK APIs are called at the right time. |
|AV_ERR_DEVICE_NOT_EXIST            |1301       | A client uses a device that does not exist or has not been initialized. Verify that the device exists, ensure that the device ID is entered correctly, and use the device after it is successfully initialized. |
|AV_ERR_SERVER_FAILED               |10001       | An unknown error occurred during room entry. <br>1. View and confirm the validity of the parameters in the room entering API, such as `AppID`, `UIN`, and `AuthBuffer` (see the documentation). <br>2. Check whether the relevant parameters in the console match the local ones. <br>3. Check whether your account is in arrears. <br>4. Check whether the network environment of your testing devices is in the private network or public network. |
|AV_ERR_SERVER_NO_PERMISSION        |10003       | The user was removed from the voice chat room. |
|AV_ERR_SERVER_REQUEST_ROOM_ADDRESS_FAIL|10004  | Failed to enter the voice chat room. Collect logs as instructed in [Troubleshooting Guide](https://www.tencentcloud.com/document/product/607/51562) and submit them to the GME team for troubleshooting. |
|AV_ERR_SERVER_CONNECT_ROOM_FAIL    |10005       | Failed to enter the voice chat room. Collect logs as instructed in [Troubleshooting Guide](https://www.tencentcloud.com/document/product/607/51562) and submit them to the GME team for troubleshooting. |


## Voice Message Error Codes

### Audio recording error codes

| Error Message | Error Code | Cause and Suggested Solution |
| -------------------- | -------- | ------------------ |
|VOICE_RECORDER_PARAM_NULL      |4097| The parameter is empty. Check whether the API parameters in the code are correct. |
|VOICE_RECORDER_INIT_ERROR      |4098| Initialization error. <br>1. Check whether the device is being used. <br>2. Check whether the permissions are normal. <br>3. Check whether the initialization is normal. |
|VOICE_RECORDER_RECORDING_ERROR |4099| Recording is in progress when the recording API is called. Ensure that the SDK recording feature is used at the right time. |
|VOICE_RECORDER_NO_AUDIO_DATA_WARN|4100| No audio data is captured. Check whether the mic is working properly. |
|VOICE_RECORDER_OPENFILE_ERROR  |4101| An error occurred while accessing the file during recording. <br>1. Ensure the existence of the file. <br>2. Check the validity of the file path. |
|VOICE_RECORDER_MIC_PERMISSION_ERROR|4102| The mic is not authorized. Mic permission is required for using the SDK. To add the permission, see the SDK project configuration document for the corresponding engine or platform. |
|VOICE_RECORD_AUDIO_TOO_SHORT   |4103| The recording duration is too short. <br>1. Check whether the recording duration is in ms. <br>2. Ensure that the recording is longer than 1,000 ms. |
|VOICE_RECORD_NOT_START         |4104| No recording operation is started. Check whether the recording starting API has been called. |


### Audio upload error codes

| Error Message | Error Code | Cause and Suggested Solution |
| -------------------- | -------- | ------------------ |
|VOICE_UPLOAD_FILE_ACCESSERROR       |8193| An error occurred while accessing the file during upload. 1. Ensure the existence of the file. 2. Check the validity of the file path. |
|VOICE_UPLOAD_SIGN_CHECK_FAIL        |8194| Signature verification failed. <br>1. Check whether the authentication key is correct. <br>2. Check whether the voice message and speech-to-text feature is initialized. |
|VOICE_UPLOAD_COS_INTERNAL_FAIL      |8195| Failed to upload to COS due to a network error. Check whether the device can access the internet. For more information, see [Network](https://intl.cloud.tencent.com/document/product/607/39519). |
|VOICE_UPLOAD_GET_TOKEN_NETWORK_FAIL |8196| File upload failed. <br>1. Check whether the authentication is correct. <br>2. Check whether the device can access the internet. For more information, see [Network](https://intl.cloud.tencent.com/document/product/607/39519). |
|VOICE_UPLOAD_SYSTEM_INNER_ERROR     |8197| File upload failed. <br>1. Check whether the authentication is correct. <br>2. Check whether the device can access the internet. For more information, see [Network](https://intl.cloud.tencent.com/document/product/607/39519). |
|VOICE_UPLOAD_RSP_DATA_DECODE_FAIL   |8198| File upload failed. <br>1. Check whether the authentication is correct. <br>2. Check whether the device can access the internet. For more information, see [Network](https://intl.cloud.tencent.com/document/product/607/39519). |
|VOICE_UPLOAD_APPINFO_UNSET          |8200| Authentication is not configured. <br>1. Check whether the applyAuthBuffer API is called. <br>2. Check whether the input parameters of the applyAuthBuffer API are empty. |


### Audio download error codes

| Error Message | Error Code | Cause and Suggested Solution |
| -------------------- | -------- | ------------------ |
|VOICE_DOWNLOAD_FILE_ACCESS_ERROR            | 12289  	| An error occurred while accessing the path during download. Check whether the file path is valid. |
|VOICE_DOWNLOAD_SIGN_CHECK_FAIL              | 12290  	| Signature verification failed. <br>1. Check whether the authentication key is correct. <br>2. Check whether the voice message and speech-to-text feature is initialized. |
|VOICE_DOWNLOAD_COS_INTERNAL_FAIL            | 12291  	| Failed to obtain the audio file. <br>1. Check whether the API parameter `fileid` is correct. <br>2. Check whether the network is normal. |
|VOICE_DOWNLOAD_REMOTEFILE_ACCESS_ERROR      | 12292  	| Failed to obtain the audio file. <br>1. Check whether the API parameter `fileid` is correct. <br>2. Check whether the network is normal. |
|VOICE_DOWNLOAD_GET_SIGN_NETWORK_FAIL        | 12293  	| Failed to obtain the audio file due to a network error. Check whether the device can access the internet. For more information, see [Network](https://intl.cloud.tencent.com/document/product/607/39519). |
|VOICE_DOWNLOAD_SYSTEM_INNER_ERROR           | 12294	| Failed to obtain the audio file due to a network error. Check whether the device can access the internet. For more information, see [Network](https://intl.cloud.tencent.com/document/product/607/39519). |
|VOICE_DOWNLOAD_GET_SIGN_RSP_DATA_DECODE_FAIL| 12295	| Failed to obtain the audio file due to a network error. Check whether the device can access the internet. For more information, see [Network](https://intl.cloud.tencent.com/document/product/607/39519). |
|VOICE_DOWNLOAD_APPINFO_UNSET                | 12297	| Authentication is not configured. <br>1. Check whether the applyAuthBuffer API is called. <br>2. Check whether the input parameters of the applyAuthBuffer API are empty. |

### Audio playback error codes
| Error Message | Error Code | Cause and Suggested Solution |
| -------------------- | -------- | ------------------ |
|VOICE_PLAY_INIT_ERROR      		|20481			| Initialization error. <br>1. Check whether the device is being used. <br>2. Check whether the permissions are normal. <br>3. Check whether the initialization is normal. |
|VOICE_PLAY_PLAYING_ERROR   		|20482			| During playback, the client tried to interrupt and play back the next one but failed. Pause the audio and resume it. |
|VOICE_PLAY_PARAM_NULL      		|20483			| An error occurred due to empty parameters. Check whether the API parameters in the code are correct. |
|VOICE_PLAY_OPEN_FILE_ERROR 		|20484			| Failed to open the audio file. <br>1. Ensure the existence of the file. <br>2. Check the validity of the file path. |
|VOICE_PLAY_NOT_START 	   			|20485			| Failed to play back the audio file. <br>1. Ensure the existence of the file. <br>2. Check the validity of the file path. |
|VOICE_PLAYER_SILKFILE_NULL 		|20486			| The audio file is empty. Ensure that the file has content. |
|VOICE_PLAYER_SILKFILE_READ_ERROR 	|20487			| Failed to read the audio file. Ensure that the file format is correct. |
|VOICE_PLAYER_INIT_DEVICE_ERROR 	|20488			| Device initialization failed. Check whether the speaker device is normal. |
|VOICE_PLAYER_ERROR 				|20489			| Playback failed due to an internal system error, such as thread creation or memory application release error. Restart the audio file. |

## Speech-to-Text Error Codes

| Error Message | Error Code | Cause and Suggested Solution |
| -------------------- | -------- | ------------------ |
|VOICE_ERR_VOICE_S2T_SYSTEM_INTERNAL_ERROR       			 |32769        | Speech-to-text conversion failed due to a system error. Collect logs as instructed in [Troubleshooting Guide](https://www.tencentcloud.com/document/product/607/51562) and submit them to the GME team for troubleshooting. |
|VOICE_ERR_VOICE_S2T_NETWORK_FAIL						     |32770        | Speech-to-text conversion failed due to a network error. Check whether the device can access the internet. For more information, see [Network](https://intl.cloud.tencent.com/document/product/607/39519). |
|VOICE_ERR_VOICE_S2T_RSP_DATA_DECODE_FAIL  					 |32772	       | Speech-to-text conversion failed due to a network error. Check whether the device can access the internet. For more information, see [Network](https://intl.cloud.tencent.com/document/product/607/39519). |
|VOICE_ERR_VOICE_S2T_APPINFO_UNSET         					 |32774	       | Authentication is not configured. <br>1. Check whether the applyAuthBuffer API is called. <br>2. Check whether the input parameters of the applyAuthBuffer API are empty. |
|VOICE_ERR_VOICE_STREAMIN_RECORD_SUC_REC_FAIL			     |32775    | Streaming speech-to-text conversion failed, but recording succeeded. Check whether the authentication key is correct. |
|VOICE_ERR_VOICE_S2T_SIGN_CHECK_FAIL					     |32776        | Signature verification failed. <br>1. Check whether the authentication key is correct. <br>2. Check whether the voice message and speech-to-text feature is initialized. |
|VOICE_ERR_VOICE_STREAMIN_UPLOADANDRECORD_SUC_REC_FAIL       |32777        | Streaming speech-to-text conversion failed, but recording and upload succeeded. Check whether the network is correct and call the API again to convert the file to text. |
|VOICE_ERR_VOICE_S2T_PARAM_NULL                              |32784        | Incorrect speech-to-text conversion parameter.  Check whether the API parameter `fileid` in the code is empty. |
|VOICE_ERR_VOICE_S2T_AUTO_SPEECH_REC_ERROR                   |32785        | An error is returned for speech-to-text conversion. Collect logs as instructed in [Troubleshooting Guide](https://www.tencentcloud.com/document/product/607/51562) and submit them to the GME team for troubleshooting. |
|VOICE_ERR_VOICE_STREAMIN_RUNING_ERROR                       |32786        | Streaming speech-to-text conversion was in progress when the API was called. Wait for the API to return the execution result. |
|VOICE_ERR_VOICE_S2T_TRNSLATE_SERVICE_NOT_AVALIABLE          |32787        | The translation feature is not supported. Collect logs as instructed in [Troubleshooting Guide](https://www.tencentcloud.com/document/product/607/51562) and submit them to the GME team for troubleshooting. |
|VOICE_ERR_VOICE_S2T_TRNSLATE_LANGUAGE_NOT_SUPPORTED         |32788        | The language parameter in the translation API call is not supported. Check the input parameters of the API. |
|VOICE_ERR_VOICE_STREAMING_ASR_ERROR                         |327698       | An error occurred while requesting the streaming speech-to-text service. Upload the recording file (UploadRecordedFile) and call the speech-to-text API (SpeechToText) again. |



## Accompaniment Error Codes

| Error Message | Error Code | Cause and Suggested Solution |
| ----------------------------- | --------  | ------------------------------------------------------------ |
|AV_ERR_ACC_OPENFILE_FAILED                 |4001| Failed to open the file. Check whether the file exists. |
|AV_ERR_ACC_FILE_FORAMT_NOTSUPPORT          |4002| Unsupported file format. Check whether the file format is supported. |
|AV_ERR_ACC_DECODER_FAILED                  |4003| Decoding failed. Check whether the file format is supported. |
|AV_ERR_ACC_BAD_PARAM                       |4004| Incorrect parameter. Check the parameter. |
|AV_ERR_ACC_MEMORY_ALLOC_FAILED             |4005| Memory allocation failed due to insufficient memory. Clean up the device memory. |
|AV_ERR_ACC_CREATE_THREAD_FAILED            |4006| Thread creation failed. Clean up the device memory. |
|AV_ERR_ACC_STATE_ILLIGAL                   |4007| Invalid status. Clean up the device memory. |
|AV_ERR_START_ACC_FIRST                     |4008| Device capturing and playback were delayed. Accompaniment must be enabled before recording begins. |
|AV_ERR_START_ACC_IS_STARTED                |4009| Device capturing and playback were delayed. Accompaniment must be stopped before preview begins. |
|AV_ERR_HARDWARE_TEST_RECORD_IS_STARTED     |4010| Device capturing and playback were delayed. Recording must be stopped before preview begins. |
|AV_ERR_HARDWARE_TEST_PREVIEW_IS_STARTED    |4011| Device capturing and playback were delayed. Preview must be stopped before recording begins. |
|AV_ERR_HARDWARE_TEST_PREVIEW_DATA_IS_EMPTY |4012| Device capturing and playback were delayed. Preview must be stopped before recording begins. |



## Sound Effect Error Codes

| Error Message | Error Code | Cause and Suggested Solution |
| ----------------------------- | --------  | ------------------------------------------------------------ |
|AV_ERR_EFFECT_OPENFILE_FAILED         |4051| Failed to open the file. Check whether the file exists and whether the file path is correct. |
|AV_ERR_EFFECT_FILE_FORAMT_NOTSUPPORT  |4052| Unsupported file format. Check whether the file format is correct. |
|AV_ERR_EFFECT_DECODER_FAILED          |4053| Decoding failed. Check the file format. |
|AV_ERR_EFFECT_BAD_PARAM               |4054| Incorrect parameter. Check whether the input parameters of the API are correct. |
|AV_ERR_EFFECT_MEMORY_ALLOC_FAILED     |4055| Memory allocation failed due to insufficient memory. Clean up the device memory. |
|AV_ERR_EFFECT_CREATE_THREAD_FAILED    |4056| Thread creation failed. Clean up the device memory. |
|AV_ERR_EFFECT_STATE_ILLIGAL           |4057| Invalid status. Clean up the device memory. |


## Voice Chat Recording Error Codes

| Error Message | Error Code | Cause and Suggested Solution |
| ----------------------------- | --------  | ------------------------------------------------------------ |
|AV_ERR_RECORD_OPENFILE_FAILED 			|5001| Failed to open the file. Check whether the file exists and whether the file path is correct. |
|AV_ERR_RECORD_FILE_FORAMT_NOTSUPPORT 	|5002| Unsupported file format. Check whether the file format is correct. |
|AV_ERR_RECORD_DECODER_FAILED 			|5003| Decoding failed. Check the file format. |
|AV_ERR_RECORD_BAD_PARAM 				|5004| Incorrect parameter. Check whether the input parameters of the API are correct. |
|AV_ERR_RECORD_MEMORY_ALLOC_FAILED 		|5005| Memory allocation failed due to insufficient memory. Clean up the device memory. |
|AV_ERR_RECORD_CREATE_THREAD_FAILED 	|5006| Thread creation failed. Clean up the device memory. |
|AV_ERR_RECORD_STATE_ILLIGAL 			|5007| Invalid status. Clean up the device memory. |

## Other Error Codes

| Error Message | Error Code | Cause and Suggested Solution |
| ----------------------------- | --------  | ------------------------------------------------------------ |
| AV_ERR_3DVOICE_ERR_FILE_DAMAGED   | 7002      | Failed to load the 3D sound effect file. |
| AV_ERR_3DVOICE_ERR_NOT_INITED     | 7003      | To use the 3D sound effect feature, the `InitSpatializer` API needs to be called first. |
| AV_ERR_NO_PERMISSION              | 7009      | No permission to perform the operation. Check whether the permission has been applied for. |
| AV_ERR_FILE_CANNOT_ACCESS         | 7010      | Unable to access the file. Check whether the file exists and whether the file path is correct. |
| AV_ERR_FILE_DAMAGED               | 7011      | The file is corrupted. Check whether the file is available. |
| AV_ERR_SERVICE_NOT_OPENED         | 7012      | The voice chat feature is not enabled in the console. Enable it in the console as instructed in [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782). |
| AV_ERR_USER_CANCELED              | 7013      | The user canceled an operation before it succeeds, such as entering a room. |
| AV_ERR_LOAD_LIB_FAILED            | 7014      | The library file is not loaded normally. Check whether the library file is missing and whether there is a corresponding library file for the feature used. For more information, see [SDK Version Upgrade Guide](https://intl.cloud.tencent.com/document/product/607/32363). |
| AV_ERR_SDK_NOT_FULL_UPDATE        | 7015      | Not all files were upgraded during the SDK upgrade, causing some modules to mismatch. Upgrade the entire SDK. For more information, see [SDK Version Upgrade Guide](https://intl.cloud.tencent.com/document/product/607/32363). |
|AV_ERR_MUTESWITCH_DECTECT_ERR 	    |7018       | An error occurred while detecting the iOS mute switch status. Check whether the API is called on an iOS device. |
| AV_ERR_SERVICE_NOT_OPENED         |7022      | The voice message and speech-to-text feature is not enabled in the console. Enable it in the console as instructed in [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782). |
