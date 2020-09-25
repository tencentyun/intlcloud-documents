
## Short Video Shooting

Code | Constant in TXRecordCommon | Description
---|--- | ---
-1 | START_RECORD_ERR_IS_IN_RECORDING | There is an uncompleted task when shooting starts
-2 | START_RECORD_ERR_VIDEO_PATH_IS_EMPTY | The video file path is empty when shooting starts
-3 | START_RECORD_ERR_API_IS_LOWER_THAN_18 | The version is earlier than 18
-4 | START_RECORD_ERR_NOT_INIT | Initialization has not been completed when shooting starts
-5 | START_RECORD_ERR_LICENCE_VERIFICATION_FAILED | License verification failed
-1 | RECORD_RESULT_FAILED | Shooting failed
 
## Short Video Editing
Code | Constant in TXVideoEditConstants | Description
---|--- | ---
-100001 | ERR_SOURCE_NO_FOUND | The source video file passed in through `setVideoPath` cannot be found
-100002 | ERR_SOURCE_DAMAGED | The source video file passed in through `setVideoPath` is corrupted
-100003 | ERR_SOURCE_NO_TRACK | The video format is currently not supported for demux (extracting audio and video files into different formats from the composed video) (OPPO R9s currently does not support .mp3 audio files)

## Short Video Uploading
### SDK error codes
The short video upload SDK listens on the short video upload status through the `TXRecordCommon.ITXVideoPublishListener` API. Therefore, you can check the video release status with the `retCode` in `TXRecordCommon.TXPublishResult`

Code | Event Definition | Description
---|--- | ---
 0  |  NO_ERROR | Published successfully   
1001  |  ERR_UGC_REQUEST_FAILED | The upload request failed   
 1002  |  ERR_UGC_PARSE_FAILED | Failed to parse the request information   
 1003  |  ERR_UPLOAD_VIDEO_FAILED |   Failed to upload the video   
 1004  |  ERR_UPLOAD_COVER_FAILED  |  Failed to upload the cover   
 1005  |  ERR_UGC_FINISH_REQUEST_FAILED |  The request to end the upload failed   
1006  |  ERR_UGC_FINISH_RESPONSE_FAILED |  An error occurred with the response to ending the upload   
 1007  |  ERR_USER_CANCEL |  Upload canceled by the user  
 1007  |  ERR_CLIENT_BUSY |  The client is busy (the object cannot process more requests)   
 1008  |  ERR_FILE_NOEXIT |  The file to be uploaded does not exist   
 1009  |  ERR_UGC_PUBLISHING  |  The video is being uploaded   
1010  |  ERR_UGC_INVALID_PARAM |  The upload parameter is incorrect   
 1011  |  ERR_UGC_INVALID_SECRETID |  The `secretID` for video upload is incorrect. This error code has been disused and will not be thrown   
 1012  |  ERR_UGC_INVALID_SIGNATURE |  The signature for video upload is incorrect   
 1013  |  ERR_UGC_INVALID_VIDOPATH |  The path of the video file is incorrect   
 1014  |  ERR_UGC_INVALID_VIDEO_FILE |  The video file does not exist under the current path   
 1015  |  ERR_UGC_FILE_NAME |  The file name of the video to be uploaded is too long or contains special symbols   
 1016  |  ERR_UGC_INVALID_COVER_PATH |  Invalid path of the cover of the video file. The file does not exist 

### Server error codes  
If you cannot determine the video release result based on the SDK error code, you can query the error code returned by the server, which can be found in the logs.

| Error Code | Description |
| :--------: | :--------| 
|   0  |  Published successfully | 
| -20001  | Completed instant transfer successfully | 
| -20002  | The task is canceled | 
| -20003  | The task is paused | 
| -20004  | The file does not exist | 
| -20007  | The packet returned by the server is empty | 
| -20008  |  The request timed out | 
| -20009  |  `appid` is empty | 
| -20010  |  `bucket` is empty | 
| -20011  |  The remote path of COS is empty | 
| -20012  |  The COS directory contains reserved characters | 
| -20013  |  `dest_fileId` is empty | 
| -20014  |  `bucket_authority` is empty | 
| -21001  |  Out of memory | 
| -22000  |  I/O exception | 
| -25000  |  Other errors. If you need help, contact your Tencent Cloud rep or [submit a ticket](https://console.cloud.tencent.com/workorder/category) | 
