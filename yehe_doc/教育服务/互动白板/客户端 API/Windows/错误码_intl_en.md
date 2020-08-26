
## TEduBoardErrorCode
Whiteboard error codes (critical) 


| Enumerated Value | Description |
| --- | --- |
| TEDU_BOARD_ERROR_INIT | Failed to initialize the whiteboard |
| TEDU_BOARD_ERROR_AUTH | Service authentication failed. This error occurs because you have not purchased the service or the service has expired |
| TEDU_BOARD_ERROR_LOAD | Failed to load files |
| TEDU_BOARD_ERROR_TIM_INVALID | Tencent Cloud IMSDK is unavailable |
| TEDU_BOARD_ERROR_HISTORYDATA | Failed to sync historical data |
| TEDU_BOARD_ERROR_RUNTIME | The whiteboard encountered an error during runtime. Confirm the error type based on the error information |
| TEDU_BOARD_ERROR_AUTH_TIMEOUT | Service authentication timed out. This problem may result from a network problem. To correct it, try again |
| TEDU_BOARD_ERROR_DATA_TOO_LARGE | The data to be transmitted is too large. For example, there may be too many URLs when the image files are added. Please split the data into two or more parts and then transmit them |
| TEDU_BOARD_ERROR_PATH_INVALID | The path is invalid |
| TEDU_BOARD_ERROR_WRITE_ERROR | A file write error occurred |
| TEDU_BOARD_ERROR_OOM | The memory is exhausted |



## TEduBoardWarningCode
Whiteboard error codes (warning) 


| Enumerated Value | Description |
| --- | --- |
| TEDU_BOARD_WARNING_SYNC_DATA_PARSE_FAILED | Failed to parse the synchronization data from the other end |
| TEDU_BOARD_WARNING_TIM_SEND_MSG_FAILED | Tencent IMSDK failed to send the message |
| TEDU_BOARD_WARNING_H5PPT_ALREADY_EXISTS | The H5PPT to be added already exists |
| TEDU_BOARD_WARNING_AUTO_RELOAD | The whiteboard is automatically reloaded due to an exception |
| TEDU_BOARD_WARNING_ILLEGAL_OPERATION | No operation is allowed until the whiteboard historical data is successfully loaded |
| TEDU_BOARD_WARNING_H5FILE_ALREADY_EXISTS | This warning occurs when the H5File to be added already exists |
| TEDU_BOARD_WARNING_VIDEO_ALREADY_EXISTS | This warning occurs when the video file to be added already exists |
| TEDU_BOARD_WARNING_IMAGESFILE_ALREADY_EXISTS | This warning occurs when the image file to be added already exists |




