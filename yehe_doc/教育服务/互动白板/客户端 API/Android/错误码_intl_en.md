## TEduBoardErrorCode
Whiteboard error codes (critical) 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| TEDU_BOARD_ERROR_INIT | int | Initialization failed (this does not occur on Android) |
| TEDU_BOARD_ERROR_AUTH | int | Authentication failed. Please purchase the service first |
| TEDU_BOARD_ERROR_LOAD | int | Failed to load the whiteboard |
| TEDU_BOARD_ERROR_TIM_INVALID | int | Tencent Cloud IMSDK is unavailable |
| TEDU_BOARD_ERROR_HISTORYDATA | int | Failed to sync historical data |
| TEDU_BOARD_ERROR_RUNTIME | int | Whiteboard runtime error |
| TEDU_BOARD_ERROR_AUTH_TIMEOUT | int | Service authentication timed out. This problem may result from a network problem. Please try again |
| TEDU_BOARD_ERROR_DATA_TOO_LARGE | int | The data to be transmitted is too large. For example, there are too many URLs when the image files are added. Please split the data into two or more smaller parts for transmission |
| TEDU_BOARD_ERROR_PATH_INVALID | int | The path is invalid |
| TEDU_BOARD_ERROR_WRITE_ERROR | int | A file write error occurred |


## TEduBoardWarningCode
Whiteboard error codes (warning) 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| TEDU_BOARD_WARNING_SYNC_DATA_PARSE_FAILED | int | Failed to parse the synchronization data from the other end |
| TEDU_BOARD_WARNING_TIM_SEND_MSG_FAILED | int | Tencent Cloud IMSDK failed to send the message |
| TEDU_BOARD_WARNING_H5PPT_ALREADY_EXISTS | int | This warning occurs when the H5PPT to be added already exists |
| TEDU_BOARD_WARNING_ILLEGAL_OPERATION | int | No operation is allowed until whiteboard historical data is successfully loaded |
| TEDU_BOARD_WARNING_H5FILE_ALREADY_EXISTS | int | This warning occurs when the H5File to be added already exists |
| TEDU_BOARD_WARNING_VIDEO_ALREADY_EXISTS | int | This warning occurs when the video to be added already exists |
| TEDU_BOARD_WARNING_IMAGESFILE_ALREADY_EXISTS | int | This warning occurs when the image files to be added in batches already exist |


