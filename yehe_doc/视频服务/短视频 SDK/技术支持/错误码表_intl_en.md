## Shooting

| Code | Corresponding Constant in `TXRecordCommon`                    | Description                   |
| ---- | -------------------------------------------- | -------------------------- |
-1 | START_RECORD_ERR_IS_IN_RECORDING | There was an uncompleted task when user tried to start shooting. |
-2 | START_RECORD_ERR_VIDEO_PATH_IS_EMPTY | Empty value for video path when user tried to start shooting. |
| -3   | START_RECORD_ERR_API_IS_LOWER_THAN_18        | API version is below 18.                  |
| -4   | START_RECORD_ERR_NOT_INIT                    | Initialization was not finished when user tried to start shooting.   |
| -5   | START_RECORD_ERR_LICENCE_VERIFICATION_FAILED | License verification failed.           |
| -1   | RECORD_RESULT_FAILED                         | Shooting failed.                   |

## Editing

| Code    | Corresponding Constant in `TXVideoEditConstants`  | Description                                                     |
| ------- | ------------------------------- | ------------------------------------------------------------ |
| -100001 | ERR_SOURCE_NO_FOUND             | Source video file passed in via `setVideoPath` not found.                     |
| -100002 | ERR_SOURCE_DAMAGED              | Source video file passed in via `setVideoPath` is damaged.                   |
-100003 | ERR_SOURCE_NO_TRACK | Unsupported video format for demuxing (extracting audio/video files of different formats from composed videos).|

## Uploading

### SDK Error Codes

The UGSV SDK listens for publishing-related events through the `TXRecordCommon.ITXVideoPublishListener` API. Therefore, you can check the publishing status of videos from `retCode` in `TXRecordCommon.TXPublishResult`.

| Code | Event Definition                       | Description                                   |
| ---- | ------------------------------ | ------------------------------------------ |
| 0    | NO_ERROR                       | Published successfully.                                   |
| 1001 | ERR_UGC_REQUEST_FAILED         | Uploading request failed.                               |
| 1002 | ERR_UGC_PARSE_FAILED           | Parsing request failed.               |
| 1003 | ERR_UPLOAD_VIDEO_FAILED        | Failed to upload video.                 |
| 1004 | ERR_UPLOAD_COVER_FAILED        | Failed to upload thumbnail.                 |
| 1005  |  ERR_UGC_FINISH_REQUEST_FAILED  | Request to finish uploading failed.                |
| 1006 | ERR_UGC_FINISH_RESPONSE_FAILED | Response error for finishing uploading.               |
| 1007 | ERR_USER_CANCEL                | Publishing canceled by user.                           |
| 1007 | ERR_CLIENT_BUSY | Client is busy (Object cannot handle more requests.) |
| 1008 | ERR_FILE_NOEXIT | File to be uploaded does not exist.                |
| 1009 | ERR_UGC_PUBLISHING                | Video is being uploaded.                |
| 1010 | ERR_UGC_INVALID_PARAM          | Incorrect uploading parameters.                           |
1011  |  ERR_UGC_INVALID_SECRETID |  Incorrect `secretID` for uploading. This error code has been disused and will not be thrown. |
| 1012 | ERR_UGC_INVALID_SIGNATURE      | Incorrect signature for uploading. |
| 1013 | ERR_UGC_INVALID_VIDOPATH | Incorrect video file path.     |
| 1014  |  ERR_UGC_INVALID_VIDEO_FILE     |  Video file does not exist under current path.           |
| 1015 | ERR_UGC_FILE_NAME | Video file name is too long or contains special characters. |
| 1016 | ERR_UGC_INVALID_COVER_PATH     | Incorrect thumbnail path. File does not exist.       |

>? If error codes 1003 and 1004 are returned, troubleshoot the problems according to the error messages (`errMsg`) returned. To handle COS errors, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31517).

### Server Error Codes  

If you are unable to determine the result of video publishing using the SDK error codes, check for the following error codes returned by the server, which can be found in the log.

| Error Code | Description                                                         |
| :----: | :----------------------------------------------------------- |
|   0    | Published successfully.                                                     |
| -20001 | Instant upload successful.                                                     |
| -20002 | Task cancelled.                                                     |
| -20003 | Task paused.                                                     |
| -20004 | File does not exist.                                                   |
| -20007 | Server returned empty packets.                                               |
| -20008 | Request timeout.                                                     |
| -20009 | Empty value for `appid`.                                                   |
| -20010 | Empty value for `bucket`.                                                  |
| -20011 | Empty value for COS remote path.                                             |
| -20012 | Reserved characters in COS directory.                                       |
| -20013 | Empty value for `dest_fileId`.                                             |
| -20014 | Empty value for `bucket_authority`.                                        |
| -21001 | Out of memory.                                                |
| -22000 | IO exception.                                                      |
| -25000 | Other errors. If you need help handling such errors, contact Tencent Cloud sales at 4009100100 or [submit a ticket](https://console.cloud.tencent.com/workorder/category). |

