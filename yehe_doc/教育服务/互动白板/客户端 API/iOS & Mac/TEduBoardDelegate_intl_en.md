## TEduBoardDelegate-p
Whiteboard event callback delegate 

## Common Event Callbacks

### onTEBError:msg:
Whiteboard error callback 
``` Objective-C
- (void)onTEBError:(TEduBoardErrorCode)code msg:(NSString *)msg 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| code | TEduBoardErrorCode | Error code. For more information, see the definitions of TEduBoardErrorCode. |
| msg | NSString * | Error information, which is UTF8-coded |


### onTEBWarning:msg:
Whiteboard alarm callback 
``` Objective-C
- (void)onTEBWarning:(TEduBoardWarningCode)code msg:(NSString *)msg 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| code | TEduBoardWarningCode | Error code. For more information, see the definitions of TEduBoardWarningCode. |
| msg | NSString * | Error information, which is UTF8-coded |



## Basic Process Callbacks

### onTEBInit
Whiteboard initialization completion callback 
``` Objective-C
- (void)onTEBInit
```
#### Description
If this callback is returned, the whiteboard is running normally (in this case, the whiteboard is blank and no historical data has been pulled.) 


### onTEBHistroyDataSyncCompleted
Callback for the completion of whiteboard historical data synchronization 
``` Objective-C
- (void)onTEBHistroyDataSyncCompleted
```

### onTEBSyncData:
Whiteboard synchronization data callback 
``` Objective-C
- (void)onTEBSyncData:(NSString *)data 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| data | NSString * | Whiteboard synchronization data (a JSON string) |

#### Description
When this callback is returned, you need to send the callback data to other members in the room through signaling channels. After the recipients receive the callback data, call the addSyncData API to add the data to the whiteboard to sync the data. This callback is used to sync data between multiple whiteboards. This callback is not returned during real-time data synchronization by using Tencent Cloud IMSDK. 


### onTEBUndoStatusChanged:
Callback for the whiteboard undo status change 
``` Objective-C
- (void)onTEBUndoStatusChanged:(BOOL)canUndo 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| canUndo | BOOL | Whether the whiteboard allows undo operations or not |


### onTEBRedoStatusChanged:
Callback for the whiteboard redo status change 
``` Objective-C
- (void)onTEBRedoStatusChanged:(BOOL)canRedo 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| canRedo | BOOL | Whether the whiteboard allows redo operations or not |



## Doodle Feature Callbacks

### onTEBImageStatusChanged:url:status:
Callback for the whiteboard image status change 
``` Objective-C
- (void)onTEBImageStatusChanged:(NSString *)boardId url:(NSString *)url status:(TEduBoardImageStatus)status 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| boardId | NSString * | Whiteboard ID |
| url | NSString * | Whiteboard image URL |
| status | TEduBoardImageStatus | New whiteboard image status |


### onTEBSetBackgroundImage:
Callback for setting the whiteboard background image 
``` Objective-C
- (void)onTEBSetBackgroundImage:(NSString *)url 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| url | NSString * | URL that you passed in when calling SetBackgroundImage  |

#### Description
This callback is returned only when SetBackgroundImage is called locally. When this callback is returned, the background image has been uploaded or downloaded successfully and is displayed. 


### onTEBAddImageElement:
Callback for adding image elements 
``` Objective-C
- (void)onTEBAddImageElement:(NSString *)url 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| url | NSString * | URL that you passed in when calling SetBackgroundImage |

#### Description
This callback is returned only when addImageElement is called locally. When this callback is returned, the background image has been uploaded or downloaded successfully and is displayed. 


### onTEBBackgroundH5StatusChanged:url:status:
Callback for the whiteboard background H5 status change 
``` Objective-C
- (void)onTEBBackgroundH5StatusChanged:(NSString *)boardId url:(NSString *)url status:(TEduBoardBackgroundH5Status)status 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| boardId | NSString * | Whiteboard ID |
| url | NSString * | Whiteboard image URL |
| status | TEduBoardBackgroundH5Status | New whiteboard image status |



## Whiteboard Operation Callbacks

### onTEBAddBoard:fileId:
Callback for adding a whiteboard page 
``` Objective-C
- (void)onTEBAddBoard:(NSArray *)boardIds fileId:(NSString *)fileId 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| boardIds | NSArray * | List of IDs of the added whiteboard pages. After using a whiteboard page, you do not need to call the Release method to release the page. Instead, the SDK will automatically release the page. |
| fileId | NSString * | ID of the file to which the added whiteboard pages belong. The value must be ::DEFAULT in the current version. |


### onTEBDeleteBoard:fileId:
Callback for deleting a whiteboard page 
``` Objective-C
- (void)onTEBDeleteBoard:(NSArray *)boardIds fileId:(NSString *)fileId 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| boardIds | NSArray * | List of IDs of the deleted whiteboard pages. After using a whiteboard page, you do not need to call the Release method to release the page. Instead, the SDK will automatically release the page. |
| fileId | NSString * | ID of the file to which the deleted whiteboard pages belong. The value must be ::DEFAULT in the current version. |


### onTEBGotoBoard:fileId:
Callback for redirecting to a whiteboard page 
``` Objective-C
- (void)onTEBGotoBoard:(NSString *)boardId fileId:(NSString *)fileId 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| boardId | NSString * | ID of the whiteboard page to redirect to |
| fileId | NSString * | ID of the file to which the whiteboard page to redirect to belongs |


### onTEBGotoStep:totalStep:
Callback for whiteboard page animation steps 
``` Objective-C
- (void)onTEBGotoStep:(uint32_t)currentStep totalStep:(uint32_t)totalStep 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| currentStep | uint32_t | Current step of the current whiteboard page animation. Value range: [0, totalStep) |
| totalStep | uint32_t | Total steps of the current whiteboard page animation |


### onTEBRectSelected
Callback for the selection made by the selection tool 
``` Objective-C
- (void)onTEBRectSelected
```
#### Description
This callback is triggered only after the rectangle selection tool selects a doodle or image element. 


### onTEBRefresh
Callback for refreshing a whiteboard 
``` Objective-C
- (void)onTEBRefresh
```

### onTEBSnapshot:errorCode:errorMsg:
Creates a whiteboard snapshot. 
``` Objective-C
- (void)onTEBSnapshot:(NSString *)path errorCode:(TEduBoardErrorCode)code errorMsg:(NSString *)msg 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| path | NSString * | Local storage path of the snapshot |
| code | TEduBoardErrorCode | Error code. If 0 is returned, the snapshot has been obtained. |
| msg | NSString * | Error information |



## File Operation Callbacks

### onTEBFileTranscodeProgress:path:errorCode:errorMsg:
File transcoding progress callback 
``` Objective-C
- (void)onTEBFileTranscodeProgress:(TEduBoardTranscodeFileResult *)result path:(NSString *)path errorCode:(NSString *)errorCode errorMsg:(NSString *)errorMsg 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| result | TEduBoardTranscodeFileResult * | File transcoding result |
| path | NSString * | Local storage path of the file being transcoded |
| errorCode | NSString * | File transcoding error code. If no error occurs, the value is the null string (""). |
| errorMsg | NSString * | File transcoding error information. If no error occurs, the value is the null string (""). |


### onTEBAddTranscodeFile:
Callback for adding a file for transcoding 
``` Objective-C
- (void)onTEBAddTranscodeFile:(NSString *)fileId 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | NSString * | ID of the added file |

#### Description
This callback is triggered only after the file is loaded successfully. 


### onTEBDeleteFile:
Callback for deleting a file 
``` Objective-C
- (void)onTEBDeleteFile:(NSString *)fileId 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | NSString * | ID of the file to delete |


### onTEBSwitchFile:
Callback for switching to another file 
``` Objective-C
- (void)onTEBSwitchFile:(NSString *)fileId 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | NSString * | ID of the file to switch to |


### onTEBFileUploadProgress:currentBytes:totalBytes:uploadSpeed:percent:
File upload progress callback 
``` Objective-C
- (void)onTEBFileUploadProgress:(NSString *)path currentBytes:(int)currentBytes totalBytes:(int)totalBytes uploadSpeed:(int)uploadSpeed percent:(float)percent 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| path | NSString * | Path of the file being uploaded |
| currentBytes | int | Size already uploaded in bytes |
| totalBytes | int | Total file size in bytes |
| uploadSpeed | int | File upload speed in bytes |
| percent | float | File upload progress. Value range: [0, 1] |


### onTEBFileUploadStatus:status:errorCode:errorMsg:
File upload status callback 
``` Objective-C
- (void)onTEBFileUploadStatus:(NSString *)path status:(TEduBoardUploadStatus)status errorCode:(int)errorCode errorMsg:(NSString *)errorMsg 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| path | NSString * | Path of the file being uploaded |
| status | TEduBoardUploadStatus | File upload status |
| errorCode | int | File upload error code |
| errorMsg | NSString * | File upload error information |


### onTEBH5FileStatusChanged:status:
H5 file status callback 
``` Objective-C
- (void)onTEBH5FileStatusChanged:(NSString *)fileId status:(TEduBoardH5FileStatus)status 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | NSString * | File ID |
| status | TEduBoardH5FileStatus | File status |


### onTEBVideoStatusChanged:status:progress:duration:
Video file status callback 
``` Objective-C
- (void)onTEBVideoStatusChanged:(NSString *)fileId status:(TEduBoardVideoStatus)status progress:(CGFloat)progress duration:(CGFloat)duration 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | NSString * | File ID |
| status | TEduBoardVideoStatus | File status |
| progress | CGFloat | Current progress in seconds (only for mp4 files) |
| duration | CGFloat | Total duration in seconds (only for mp4 files) |


### onTEBAddImagesFile:
Callback for adding a batch of image files 
``` Objective-C
- (void)onTEBAddImagesFile:(NSString *)fileId 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | NSString * | ID of the added file |

#### Description
This callback is triggered only after the file is loaded successfully. 



