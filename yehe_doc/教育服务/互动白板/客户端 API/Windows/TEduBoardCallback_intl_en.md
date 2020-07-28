## TEduBoardCallback
Whiteboard event callback delegate 

## Common Event Callbacks

### onTEBError
Whiteboard error callback 
``` C++
virtual void onTEBError(TEduBoardErrorCode code, const char *msg)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| code | TEduBoardErrorCode | Error code. See the definitions of TEduBoardErrorCode. |
| msg | const char * | Error information, which is UTF8-coded |


### onTEBWarning
Whiteboard warning callback 
``` C++
virtual void onTEBWarning(TEduBoardWarningCode code, const char *msg)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| code | TEduBoardWarningCode | Error code. For more information, see the definitions of TEduBoardWarningCode. |
| msg | const char * | Error information, which is UTF8-coded |



## Basic Process Callbacks

### onTEBInit
Whiteboard initialization completion callback 
``` C++
virtual void onTEBInit()=0
```
#### Description
If this callback is returned, the whiteboard is running normally (in this case, the whiteboard is blank and no historical data has been pulled.) 


### onTEBHistroyDataSyncCompleted
Callback for the completion of whiteboard historical data synchronization 
``` C++
virtual void onTEBHistroyDataSyncCompleted()
```

### onTEBSyncData
Whiteboard synchronization data callback 
``` C++
virtual void onTEBSyncData(const char *data)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| data | const char * | Whiteboard synchronization data (a JSON string) |

#### Description
When this callback is returned, you need to send the callback data to other members in the room through signaling channels. After the recipients receive the callback data, call the AddSyncData API to add the data to the whiteboard to sync the data. This callback is used to sync data between multiple whiteboards. This callback is not returned during real-time data synchronization by using Tencent Cloud IMSDK. 


### onTEBUndoStatusChanged
Callback for the whiteboard undo status change 
``` C++
virtual void onTEBUndoStatusChanged(bool canUndo)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| canUndo | bool | Whether the whiteboard allows undo operations or not |


### onTEBRedoStatusChanged
Callback for the whiteboard redo status change 
``` C++
virtual void onTEBRedoStatusChanged(bool canRedo)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| canRedo | bool | Whether the whiteboard allows redo operations or not |


### onTEBRectSelected
Callback for selecting certain content by the rectangle tool. This callback is triggered only after the tool selects a doodle or an image element. 
``` C++
virtual void onTEBRectSelected()
```

### onTEBRefresh
Callback for refreshing a whiteboard 
``` C++
virtual void onTEBRefresh()
```

### onTEBOffscreenPaint
Whiteboard off-screen rendering callback 
``` C++
virtual void onTEBOffscreenPaint(const void *buffer, uint32_t width, uint32_t height, const TEduBoardRect *dirtyRects, uint32_t dirtyRectCount)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| buffer | const void * | Whiteboard data |
| width | uint32_t | Whiteboard pixel data width |
| height | uint32_t | Whiteboard pixel data height |
| dirtyRects | const TEduBoardRect * | Rectangle area arrays that need to be re-drawn |
| dirtyRectCount | uint32_t | Number of rectangle area arrays that need to be re-drawn |

#### Warning
This callback is not triggered from the unified callback thread. It may be triggered by calls from different threads.

#### Description
This callback can be triggered only when off-screen rendering is enabled. When width != 0 || height != 0, buffer points to the whiteboard pixel data with the size of width x height x 4. The pixels are sorted by BGRA from left to right and from top to bottom, with the upper-left corner of the whiteboard as the origin. 


### onTEBAudioCallbackStarted
Callback for starting whiteboard audio 
``` C++
virtual void onTEBAudioCallbackStarted(uint32_t channels, uint32_t channelSize, uint32_t sampleRate)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| channels | uint32_t | Number of sound channels of the callback |
| channelSize | uint32_t | Number of sampling points per sound channel of the callback |
| sampleRate | uint32_t | Audio sampling rate of the callback |

#### Warning
This callback is not triggered from the unified callback thread. It may be triggered by calls from different threads. 


### onTEBAudioCallbackPacket
Whiteboard audio packet callback 
``` C++
virtual void onTEBAudioCallbackPacket(const float **buffer, int64_t pts)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| buffer | const float ** | Audio data array in the format of buffer[channels][channelSize] |
| pts | int64_t | Audio packet timestamp |

#### Warning
This callback is not triggered from the unified callback thread. It may be triggered by calls from different threads. 


### onTEBAudioCallbackStopped
Whiteboard audio stop callback 
``` C++
virtual void onTEBAudioCallbackStopped()
```
#### Warning
This callback is not triggered from the unified callback thread. It may be triggered by calls from different threads. 



## Doodle Feature Callbacks

### onTEBImageStatusChanged
Callback for the whiteboard image status change 
``` C++
virtual void onTEBImageStatusChanged(const char *boardId, const char *url, TEduBoardImageStatus status)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| boardId | const char * | Whiteboard ID |
| url | const char * | Whiteboard image URL |
| status | TEduBoardImageStatus | New whiteboard image status |


### onTEBSetBackgroundImage
Callback for setting the whiteboard background image 
``` C++
virtual void onTEBSetBackgroundImage(const char *url)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| url | const char * | URL that you passed in when calling SetBackgroundImage |

#### Description
This callback is returned only when SetBackgroundImage is called locally. When this callback is returned, the background image has been uploaded or downloaded successfully and is displayed. 


### onTEBAddImageElement
Callback for adding whiteboard image elements 
``` C++
virtual void onTEBAddImageElement(const char *url)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| url | const char * | URL that you passed in when calling AddImageElement |

#### Description
This callback is returned only when AddImageElement is called locally. When this callback is returned, the image has been uploaded or downloaded successfully and is displayed. 


### onTEBAddElement
Callback for adding whiteboard elements 
``` C++
virtual void onTEBAddElement(const char *elementId, const char *url)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| elementId | const char * | Element ID that is returned when you call AddElement |
| url | const char * | URL that you passed in when calling AddElement |

#### Description
This callback is received only when AddElement is called locally. Receiving this callback indicates that the element has been displayed. 


### onTEBBackgroundH5StatusChanged
Callback for the whiteboard background H5 status change 
``` C++
virtual void onTEBBackgroundH5StatusChanged(const char *boardId, const char *url, TEduBoardBackgroundH5Status status)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| boardId | const char * | Whiteboard ID |
| url | const char * | Whiteboard image URL |
| status | TEduBoardBackgroundH5Status | New whiteboard image status|



## Whiteboard Page Operation Callbacks

### onTEBAddBoard
Callback for adding a whiteboard page 
``` C++
virtual void onTEBAddBoard(const TEduBoardStringList *boardList, const char *fileId)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| boardList | const TEduBoardStringList * | List of IDs of added whiteboard pages. After using this parameter, you do not need to call the Release method to release it as the SDK will automatically release it internally. |
| fileId | const char * | ID of the file to which the added whiteboard pages belong. The value must be ::DEFAULT in the current version. |


### onTEBDeleteBoard
Callback for deleting a whiteboard page 
``` C++
virtual void onTEBDeleteBoard(const TEduBoardStringList *boardList, const char *fileId)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| boardList | const TEduBoardStringList * | List of IDs of deleted whiteboard pages. After using this parameter, you do not need to call the Release method to release it as the SDK will automatically release it internally. |
| fileId | const char * | ID of the file to which the deleted whiteboard pages belong. The value must be ::DEFAULT in the current version. |


### onTEBGotoBoard
Callback for redirecting to a whiteboard page 
``` C++
virtual void onTEBGotoBoard(const char *boardId, const char *fileId)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| boardId | const char * | ID of the whiteboard page to redirect to |
| fileId | const char * | ID of the file to which the whiteboard page to redirect to belongs |


### onTEBGotoStep
Callback for whiteboard page animation steps 
``` C++
virtual void onTEBGotoStep(uint32_t currentStep, uint32_t totalStep)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| currentStep | uint32_t | Current step of the current whiteboard page animation. Value range: [0, totalStep) |
| totalStep | uint32_t | Total steps of the current whiteboard page animation |


### onTEBSnapshot
Creates a whiteboard snapshot. 
``` C++
virtual void onTEBSnapshot(const char *path)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| path | const char * | Local path for storing snapshots, which is UTF8-coded |



## File Operation Callbacks

### onTEBFileTranscodeProgress
File transcoding progress callback 
``` C++
virtual void onTEBFileTranscodeProgress(const char *path, const char *errorCode, const char *errorMsg, const TEduBoardTranscodeFileResult &result)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| path | const char * | Path of the local file being transcoded |
| errorCode | const char * | File transcoding error code. If no exception occurs, the value is the null string (""). |
| errorMsg | const char * | File transcoding error message. If no exception occurs, the value is the null string (""). |
| result | const TEduBoardTranscodeFileResult & | File transcoding result |


### onTEBAddTranscodeFile
Callback for adding a file for transcoding 
``` C++
virtual void onTEBAddTranscodeFile(const char *fileId)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | const char * | ID of the file to add |

#### Description
This callback is triggered only after the file is loaded successfully. 


### onTEBAddImagesFile
Callback for adding a batch of image files 
``` C++
virtual void onTEBAddImagesFile(const char *fileId)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | const char * | ID of the file to add |

#### Description
This callback is triggered only after the file is loaded successfully. 


### onTEBVideoStatusChanged
Video file status callback 
``` C++
virtual void onTEBVideoStatusChanged(const char *fileId, TEduBoardVideoStatus status, double progress, double duration)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | const char * | File ID |
| status | TEduBoardVideoStatus | File status |
| progress | double | Current progress in seconds (only for mp4 files) |
| duration | double | Total duration in seconds (only for mp4 files) |


### onTEBH5FileStatusChanged
H5 file status callback 
``` C++
virtual void onTEBH5FileStatusChanged(const char *fileId, TEduBoardH5FileStatus status)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | const char * | File ID |
| status | TEduBoardH5FileStatus | File status |


### onTEBDeleteFile
Callback for deleting a file 
``` C++
virtual void onTEBDeleteFile(const char *fileId)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | const char * | ID of the file to delete |


### onTEBSwitchFile
Callback for switching to another file 
``` C++
virtual void onTEBSwitchFile(const char *fileId)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | const char * | ID of the file to switch to |


### onTEBFileUploadProgress
File upload progress callback 
``` C++
virtual void onTEBFileUploadProgress(const char *path, int currentBytes, int totalBytes, int uploadSpeed, double percent)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| path | const char * | Path of the file being uploaded |
| currentBytes | int | Size of the uploaded file in bytes |
| totalBytes | int | Total file size in bytes |
| uploadSpeed | int | File upload speed in bytes/s |
| percent | double | File upload progress. Value range: [0, 1] |


### onTEBFileUploadStatus
File upload status callback 
``` C++
virtual void onTEBFileUploadStatus(const char *path, TEduBoardUploadStatus status, int errorCode, const char *errorMsg)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| path | const char * | Path of the file being uploaded |
| status | TEduBoardUploadStatus | File upload status |
| errorCode | int | File upload error code |
| errorMsg | const char * | File upload error information |



