## TEduBoardCallback
Whiteboard event callback APIs 

## Common Event Callbacks

### onTEBError
Whiteboard error callback 
``` Java
void onTEBError(int code, String msg)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| code | int | Error code. For more information, see the definitions of TEduBoardErrorCode. |
| msg | String | Error information, which is UTF8-coded |


### onTEBWarning
Whiteboard alarm callback 
``` Java
void onTEBWarning(int code, String msg)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| code | int | Error code. For more information, see the definitions of TEduBoardWarningCode. |
| msg | String | Error information, which is UTF8-coded |



## Basic Process Callbacks

### onTEBInit
Whiteboard initialization completion callback 
``` Java
void onTEBInit()
```
#### Description
If this callback is returned, the whiteboard is running normally (in this case, the whiteboard is blank and no historical data has been pulled.) 


### onTEBHistroyDataSyncCompleted
Callback for the completion of whiteboard historical data synchronization 
``` Java
void onTEBHistroyDataSyncCompleted()
```

### onTEBSyncData
Whiteboard synchronization data callback 
``` Java
void onTEBSyncData(String data)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| data | String | Whiteboard synchronization data (a JSON string) |

#### Description
When this callback is returned, you need to send the callback data to other members in the room through signaling channels. After the recipients receive the callback data, call the addSyncData API to add the data to the whiteboard to sync the data. This callback is used to sync data between multiple whiteboards. This callback is not returned during real-time data synchronization by using Tencent Cloud IMSDK. 


### onTEBUndoStatusChanged
Callback for the whiteboard undo status change 
``` Java
void onTEBUndoStatusChanged(boolean canUndo)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| canUndo | boolean | Whether the whiteboard allows undo operations or not |


### onTEBRedoStatusChanged
Callback for the whiteboard redo status change 
``` Java
void onTEBRedoStatusChanged(boolean canRedo)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| canRedo | boolean | Whether the whiteboard allows redo operations or not |



## Doodle Feature Callbacks

### onTEBImageStatusChanged
Callback for the whiteboard image status change 
``` Java
void onTEBImageStatusChanged(final String boardId, final String url, int status)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| boardId | final String | Whiteboard ID |
| url | final String | Whiteboard image URL |
| status | int | New whiteboard image status |


### onTEBSetBackgroundImage
Callback for setting the whiteboard background image 
``` Java
void onTEBSetBackgroundImage(final String url)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| url | final String | URL that you passed in when calling setBackgroundImage |

#### Description
This callback is returned only when SetBackgroundImage is called locally. When this callback is returned, the background image has been uploaded or downloaded successfully and is displayed. 


### onTEBAddImageElement
Callback for adding image elements 
``` Java
void onTEBAddImageElement(final String url)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| url | final String | URL that you passed in when calling setBackgroundImage |

#### Description
This callback is returned only when addImageElement is called locally. When this callback is returned, the background image has been uploaded or downloaded successfully and is displayed. 


### onTEBBackgroundH5StatusChanged
Callback for the whiteboard background H5 status change 
``` Java
void onTEBBackgroundH5StatusChanged(final String boardId, final String url, final int status)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| boardId | final String | Whiteboard ID |
| url | final String | Whiteboard image URL |
| status | final int | New whiteboard image status |



## Whiteboard Page Operation Callbacks

### onTEBAddBoard
Callback for adding a whiteboard page 
``` Java
void onTEBAddBoard(final List< String > boardList, final String fileId)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| boardList | final List< String > | List of IDs of added whiteboard pages. After using this parameter, you do not need to call the Release method to release it as the SDK will automatically release it internally. |
| fileId | final String | ID of the file to which the added whiteboard pages belong.The value must be ::DEFAULT in the current version. |


### onTEBDeleteBoard
Callback for deleting a whiteboard page 
``` Java
void onTEBDeleteBoard(final List< String > boardList, final String fileId)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| boardList | final List< String > | List of IDs of deleted whiteboard pages. After using this parameter, you do not need to call the Release method to release it as the SDK will automatically release it internally. |
| fileId | final String | ID of the file to which the deleted whiteboard pages belong. The value must be ::DEFAULT in the current version. |


### onTEBGotoBoard
Callback for redirecting to a whiteboard page 
``` Java
void onTEBGotoBoard(final String boardId, final String fileId)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| boardId | final String | ID of the whiteboard page to redirect to |
| fileId | final String | ID of the file to which the whiteboard page to redirect to belongs |


### onTEBGotoStep
Callback for whiteboard page animation steps 
``` Java
void onTEBGotoStep(int currentStep, int totalStep)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| currentStep | int | Current step of the current whiteboard page animation. Value range: [0, totalStep) |
| totalStep | int | Total steps of the current whiteboard page animation |


### onTEBRectSelected
Callback for the selection made by the selection tool 
``` Java
void onTEBRectSelected()
```
#### Warning
This callback is triggered only after the rectangle selection tool selects a doodle or image element. 


### onTEBRefresh
Callback for refreshing a whiteboard 
``` Java
void onTEBRefresh()
```


## File Operation Callbacks

### onTEBAddTranscodeFile
Callback for adding a file for transcoding 
``` Java
void onTEBAddTranscodeFile(String fileId)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | String | ID of the file for transcoding |

#### Description
This callback is triggered only after the file is loaded successfully. 


### onTEBDeleteFile
Callback for deleting a file 
``` Java
void onTEBDeleteFile(String fileId)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | String | ID of the file to delete |


### onTEBSwitchFile
Callback for switching to another file 
``` Java
void onTEBSwitchFile(String fileId)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | String | ID of the file to switch to |


### onTEBFileUploadProgress
File upload progress callback 
``` Java
void onTEBFileUploadProgress(final String path, int currentBytes, int totalBytes, int uploadSpeed, float percent)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| path | final String | Path of the file being uploaded |
| currentBytes | int | Size already uploaded in bytes |
| totalBytes | int | Total file size in bytes |
| uploadSpeed | int | File upload speed in bytes |
| percent | float | File upload progress. Value range: [0, 1] |


### onTEBFileUploadStatus
File upload status callback 
``` Java
void onTEBFileUploadStatus(final String path, int status, int errorCode, final String errorMsg)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| path | final String | Path of the file being uploaded |
| status | int | File upload status |
| errorCode | int | File upload error code |
| errorMsg | final String | File upload error information |


### onTEBFileTranscodeProgress
File transcoding progress callback 
``` Java
void onTEBFileTranscodeProgress(final String file, final String errorCode, final String errorMsg, final TEduBoardTranscodeFileResult result)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| file | final String | Path of the local file being transcoded |
| errorCode | final String | File transcoding error code. If no error occurs, the value is the null string (""). |
| errorMsg | final String | File transcoding error information. If no error occurs, the value is the null string (""). |
| result | final TEduBoardTranscodeFileResult | File transcoding result |


### onTEBH5FileStatusChanged
H5 file status callback 
``` Java
void onTEBH5FileStatusChanged(String fileId, int status)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | String | File ID |
| status | int | File status |


### onTEBAddImagesFile
Callback for adding a batch of image files 
``` Java
void onTEBAddImagesFile(String fileId)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | String | ID of the added file |

#### Description
This callback is triggered only after the file is loaded successfully. 


### onTEBVideoStatusChanged
Video file status callback 
``` Java
void onTEBVideoStatusChanged(String fileId, int status, float progress, float duration)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | String | File ID |
| status | int | File status |
| progress | float | Current progress in seconds (only for mp4 files) |
| duration | float | Total duration in seconds (only for mp4 files) |


### onTEBSnapshot
Creates a whiteboard snapshot. 
``` Java
void onTEBSnapshot(final String path, int code, final String msg)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| path | final String | Local snapshot path |
| code | int | Error code. If 0 is returned, the snapshot is obtained successfully. |
| msg | final String | Error information |



