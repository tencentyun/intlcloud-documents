## TEduBoardController
Whiteboard controller 

## Setting TEduBoardCallback

### addDelegate:
Sets the event callback listener. 
``` Objective-C
- (void)addDelegate:(id< TEduBoardDelegate >)delegate 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| delegate | id< TEduBoardDelegate > | Event callback listener |

#### Warning
We recommend that you call this method before running Init to handle the error. 


### removeDelegate:
Deletes the event callback listener. 
``` Objective-C
- (void)removeDelegate:(id< TEduBoardDelegate >)delegate 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| delegate | id< TEduBoardDelegate > | Event callback listener |



## Basic Process APIs

### initWithAuthParam:roomId:initParam:
Initializes the whiteboard. 
``` Objective-C
- (instancetype)initWithAuthParam:(TEduBoardAuthParam *)authParam roomId:(UInt32)roomId initParam:(TEduBoardInitParam *)initParam 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| authParam | TEduBoardAuthParam * | Authorization parameters |
| roomId | UInt32 | Classroom ID |
| initParam | TEduBoardInitParam * | An optional parameter, which specifies a series of attribute values for initializing the whiteboard |

#### Warning
When Tencent Cloud IMSDK is used for real-time data synchronization, only one whiteboard instance is supported. If multiple whiteboard instances are created, the doodle status may be abnormal.

#### Description
You can use initParam.timSync to specify whether to use Tencent Cloud IMSDK for real-time data synchronization. When initParam.timSync is set to True, the system tries to use Tencent Cloud IMSDK as the signaling channel to receive and send data in real time (in this case, only message receiving and sending are automatically implemented, while users must manually perform the initialization, room entry, and other operations.) Currently, only IMSDK 4.3.118 and later are supported. 


### unInit
Uninitializes the whiteboard. 
``` Objective-C
- (void)unInit
```
#### Warning
After you call this API, internal resources will be released and the whiteboard feature will become invalid. 


### getBoardRenderView
Obtains the whiteboard rendering view. 
``` Objective-C
- (TEView *)getBoardRenderView
```
#### Response
Whiteboard rendering view 


### addSyncData:
Adds whiteboard synchronization data. 
``` Objective-C
- (void)addSyncData:(NSString *)data 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| data | NSString * | Synchronization data from other members in the room |

#### Description
This API is used to sync data between whiteboard instances. When the built-in IM is used as the signaling channel, you do not need to call this API. 


### setDataSyncEnable:
Sets whether to enable data synchronization for the whiteboard. 
``` Objective-C
- (void)setDataSyncEnable:(BOOL)enable 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| enable | bool | Whether to enable data synchronization |

#### Description
After a whiteboard instance is created, data synchronization is enabled by default. If this feature is disabled, none of local whiteboard operations will be synchronized to the remote end or server. 


### isDataSyncEnable
Checks whether data synchronization is enabled for the whiteboard. 
``` Objective-C
- (BOOL)isDataSyncEnable
```
#### Response
Whether data synchronization is enabled or not. Valid values: true for enabled, and false for disabled. 


### getSyncTime
Obtains the synchronization timestamp. 
``` Objective-C
- (uint64_t)getSyncTime
```
#### Response
Synchronization timestamp in milliseconds 


### syncRemoteTime:timestamp:
Synchronizes the remote timestamp. 
``` Objective-C
- (void)syncRemoteTime:(NSString *)userId timestamp:(uint64_t)timestamp 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| userId | NSString * | Remote user ID |
| timestamp | uint64_t | Synchronization timestamp for the remote user, in milliseconds |


### reset
Resets the whiteboard. 
``` Objective-C
- (void)reset
```
#### Description
After this API is called, all whiteboard pages and files will be deleted. 


### getVersion
Obtains the version number. 
``` Objective-C
+ (NSString *)getSDKVersion
```
#### Response
Version number 



## Doodle APIs

### setAccessibleUsers:
Sets users whose drawings can be operated. 
``` Objective-C
- (void)setAccessibleUsers:(NSArray< NSString * > *)users 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| users | NSArray< NSString * > * | Users for which operations are allowed. The null value indicates all users. |

#### Description
This API has the following effects:
1. The ERASER tool can erase only the doodles drawn by the users specified by the users parameter, but cannot erase the doodles drawn by other users.
2. The POINTSELECT and SELECT tools can select only the doodles drawn by the users specified by the users parameter, but cannot select the doodles drawn by other users.
3. The clear API can clear only selected doodles and the doodles drawn by the users specified by the users parameter. It cannot clear backgrounds or the doodles drawn by other users.
4. This API has no impact on other features of the whiteboard that are not listed here. 


### setDrawEnable:
Sets whether the whiteboard allows doodle. 
``` Objective-C
- (void)setDrawEnable:(BOOL)enable 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| enable | BOOL | Whether doodle is allowed for the whiteboard or not. Valid values: true for yes, false for no |

#### Description
After a whiteboard instance is created, doodle is allowed for the whiteboard by default. 


### isDrawEnable
Checks whether doodle is allowed for the whiteboard. 
``` Objective-C
- (BOOL)isDrawEnable
```
#### Response
Whether doodle is allowed for the whiteboard or not. Valid values: true for yes, and false for no. 


### setGlobalBackgroundColor:
Sets the background color of all whiteboards. 
``` Objective-C
- (void)setGlobalBackgroundColor:(TEColor *)color 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| color | TEColor * | Global background color to set |

#### Description
When this API is called, the background color of all whiteboards is changed, and the default background color of newly created whiteboards will be the global background color. 


### getGlobalBackgroundColor
Obtains the global background color of whiteboards. 
``` Objective-C
- (TEColor *)getGlobalBackgroundColor
```
#### Response
Global background color 


### setBackgroundColor:
Sets the background color of the current whiteboard page. 
``` Objective-C
- (void)setBackgroundColor:(TEColor *)color 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| color | TEColor * | Background color to set |

#### Description
After a whiteboard page is created, the default background color is set by the SetDefaultBackgroundColor API. 


### getBackgroundColor
Obtains the background color of the current whiteboard page. 
``` Objective-C
- (TEColor *)getBackgroundColor
```
#### Response
Background color of the current whiteboard page 


### setBackgroundImage:mode:
Sets the background image of the current whiteboard page. 
``` Objective-C
- (void)setBackgroundImage:(NSString *)url mode:(TEduBoardImageFitMode)mode 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| url | NSString * | URL of the background image to set, which is UTF8-coded |
| mode | TEduBoardImageFitMode | Image padding and alignment mode to use |

#### Description
When the URL is a valid local file address, the file will be automatically uploaded to COS. 


### setBackgroundH5:
Sets the background H5 page of the current whiteboard page. 
``` Objective-C
- (void)setBackgroundH5:(NSString *)url 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| url | NSString * | URL of the background H5 page to set |

#### Description
This API and the SetBackgroundImage API are mutually exclusive. 


### setToolType:
Sets the whiteboard tool to use. 
``` Objective-C
- (void)setToolType:(TEduBoardToolType)type 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| type | TEduBoardToolType | Whiteboard tool to set |


### getToolType
Obtains the whiteboard tool in use. 
``` Objective-C
- (TEduBoardToolType)getToolType
```
#### Response
Whiteboard tool in use 


### setBrushColor:
Sets the brush color. 
``` Objective-C
- (void)setBrushColor:(TEColor *)color 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| color | TEColor * | Brush color to set |

#### Description
The set brush color applies to all doodles. 


### getBrushColor
Obtains the brush color. 
``` Objective-C
- (TEColor *)getBrushColor
```
#### Response
Brush color 


### setBrushThin:
Sets the brush thickness. 
``` Objective-C
- (void)setBrushThin:(UInt32)thin 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| thin | UInt32 | Brush thickness to set |

#### Description
The brush thickness applies to all doodles. If the actual pixel value (thin * whiteboard height/10000) px is less than 1 px, the doodle line will be almost invisible. 


### getBrushThin
Obtains the brush thickness. 
``` Objective-C
- (UInt32)getBrushThin
```
#### Response
Brush thickness 


### setTextColor:
Sets the text color. 
``` Objective-C
- (void)setTextColor:(TEColor *)color 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| color | TEColor * | Text color to set |


### getTextColor
Obtains the text color. 
``` Objective-C
- (TEColor *)getTextColor
```
#### Response
Text color 


### setTextStyle:
Sets the text style. 
``` Objective-C
- (void)setTextStyle:(TEduBoardTextStyle)style 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| style | TEduBoardTextStyle | Text style to set |


### getTextStyle
Obtains the text style. 
``` Objective-C
- (TEduBoardTextStyle)getTextStyle
```
#### Response
Text style 


### setTextSize:
Sets the text size. 
``` Objective-C
- (void)setTextSize:(UInt32)size 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| size | UInt32 | Text size to set |

#### Description
This API defines the actual pixel value, that is, (size * whiteboard height/10000) px. 


### getTextSize
Obtains the text size. 
``` Objective-C
- (UInt32)getTextSize
```
#### Response
Text size 


### setLineStyle:
Sets the line style. 
``` Objective-C
- (void)setLineStyle:(TEduBoardLineStyle *)style 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| style | TEduBoardLineStyle * | Line style to set |


### getLineStyle
Obtains the line style. 
``` Objective-C
- (TEduBoardLineStyle *)getLineStyle
```
#### Response
Line style 


### setOvalDrawMode:
Sets the oval drawing mode. 
``` Objective-C
- (void)setOvalDrawMode:(TEduBoardOvalDrawMode)mode 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| mode | TEduBoardOvalDrawMode | Oval drawing mode to set |


### getOvalDrawMode
Obtains the oval drawing mode. 
``` Objective-C
- (TEduBoardOvalDrawMode)getOvalDrawMode
```
#### Response
Oval drawing mode 


### undo
Undoes the last action on the current whiteboard page. 
``` Objective-C
- (void)undo
```

### redo
Redoes the last undone action on the current whiteboard page. 
``` Objective-C
- (void)redo
```

### clear
Clears doodles, the background color, and the background image. 
``` Objective-C
- (void)clear
```

### clearDraws
Clears doodles. 
``` Objective-C
- (void)clearDraws
```

### clearBackground:andSelected:
Clears the doodle on the current whiteboard page. 
``` Objective-C
- (void)clearBackground:(BOOL)background andSelected:(BOOL)selected 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| background | BOOL | Whether or not to clear the background color and background image simultaneously |
| selected | BOOL | Whether or not to clear only the selected doodles |

#### Warning
Currently, you cannot clear the background image while clearing the selected doodle. 


### setCursorIcon:cursorIcon:
Sets the cursor icon for the whiteboard tool. 
``` Objective-C
- (void)setCursorIcon:(TEduBoardToolType)toolType cursorIcon:(TEduBoardCursorIcon *)cursorIcon 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| toolType | TEduBoardToolType | Whiteboard tool for which the cursor icon is to be set |
| cursorIcon | TEduBoardCursorIcon * | Cursor icon to set |



## Whiteboard Page Operation APIs

### addBoardWithBackgroundImage:
Adds a whiteboard page. 
``` Objective-C
- (NSString *)addBoardWithBackgroundImage:(NSString *)url 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| url | NSString * | URL of the background image to use, which is UTF8-coded. The nullptr value indicates that no background image is specified. |

#### Response
Whiteboard ID 

#### Warning
Whiteboard pages will be added to the default file (with the file ID ::DEFAULT). Whiteboard pages cannot be added for user-uploaded files.

#### Description
The SDK manages the memory for storing the return value, so you do not need to dump the memory on your own. 


### deleteBoard:
Deletes a whiteboard page. 
``` Objective-C
- (void)deleteBoard:(NSString *)boardId 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| boardId | NSString * | ID of the whiteboard to delete. The nullptr value indicates the current page. |

#### Warning
Only whiteboard pages in the default file (with file ID ::DEFAULT) can be deleted. The default whiteboard page (with whiteboard ID ::DEFAULT) cannot be deleted. 


### prevStep
Goes to the previous step. Each step corresponds to an animation effect of the PowerPoint file. If no displayed animation effect is available, calling this API goes to the previous slide. 
``` Objective-C
- (void)prevStep
```

### nextStep
Goes to the next step. 
``` Objective-C
- (void)nextStep
```
#### Description
Each step corresponds to an animation effect of the PowerPoint file. If no animation effect that has not yet been displayed is available, calling this API goes to the next slide. 


### preBoard
Goes to the previous page. 
``` Objective-C
- (void)preBoard
```
#### Description
If the current whiteboard page is the first page of the current file, calling this API does not work. 


### nextBoard
Goes to the next page. 
``` Objective-C
- (void)nextBoard
```
#### Description
If the current whiteboard page is the last page of the current file, calling this API does not work. 


### gotoBoard:
Redirects to the specified whiteboard page. 
``` Objective-C
- (void)gotoBoard:(NSString *)boardId 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| boardId | NSString * | ID of the whiteboard page to redirect to |

#### Description
This API is used to redirect to any whiteboard page in any file. 


### preBoard:
Goes to the previous page. 
``` Objective-C
- (void)preBoard:(BOOL)resetStep 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| resetStep | BOOL | Whether or not to reset the PowerPoint animation steps after redirecting to the specified slide |

#### Description
If the current whiteboard page is the first page of the current file, calling this API does not work. 


### nextBoard:
Goes to the next page. 
``` Objective-C
- (void)nextBoard:(BOOL)resetStep 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| resetStep | BOOL | Whether or not to reset the PowerPoint animation steps after redirecting to the specified slide |

#### Description
If the current whiteboard page is the last page of the current file, calling this API does not work. 


### gotoBoard:resetStep:
Redirects to the specified whiteboard page. 
``` Objective-C
- (void)gotoBoard:(NSString *)boardId resetStep:(BOOL)resetStep 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| boardId | NSString * | ID of the whiteboard page to redirect to |
| resetStep | BOOL | Whether or not to reset the PowerPoint animation steps after redirecting to the specified slide |

#### Description
This API is used to redirect to any whiteboard page in any file. 


### getCurrentBoard
Obtains the ID of the current whiteboard page. 
``` Objective-C
- (NSString *)getCurrentBoard
```
#### Response
ID of the current whiteboard page

#### Description
The SDK manages the memory for storing the return value, so you do not need to dump the memory on your own. 


### getBoardList
Obtains the whiteboard list of all files. 
``` Objective-C
- (NSArray< NSString * > *)getBoardList
```
#### Response
Whiteboard list of all files 


### setBoardRatio:
Sets the aspect ratio of the current whiteboard page. 
``` Objective-C
- (void)setBoardRatio:(NSString *)ratio 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| ratio | NSString * | Whiteboard aspect ratio to set |

#### Description
The format of the value is similar to "4:3" and "16:9". 


### getBoardRatio
Obtains the aspect ratio of the current whiteboard page. 
``` Objective-C
- (NSString *)getBoardRatio
```
#### Response
Whiteboard aspect ratio, in the same format as the setBoardRatio parameter 


### setBoardScale:
Sets the scale of the current whiteboard page. 
``` Objective-C
- (void)setBoardScale:(UInt32)scale 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| scale | UInt32 | Whiteboard scale to set |

#### Description
The value range is [100, 300], and the actual scale is scale/100. 


### getBoardScale
Obtains the scale of the current whiteboard page. 
``` Objective-C
- (UInt32)getBoardScale
```
#### Response
Whiteboard scale, in the same format as the SetBoardScale parameter 


### setBoardContentFitMode:
Sets the whiteboard content self-adaption mode. 
``` Objective-C
- (void)setBoardContentFitMode:(TEduBoardContentFitMode)mode 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| mode | TEduBoardContentFitMode | Whiteboard content self-adaption mode |

#### Description
Setting the self-adaption mode affects all subsequent whiteboard content operations. In addition, the AddTranscodeFile API is affected. 


### getBoardContentFitMode
Obtains the whiteboard content self-adaption mode. 
``` Objective-C
- (TEduBoardContentFitMode)getBoardContentFitMode
```
#### Response
Whiteboard content self-adaption mode 


### addImageElement:
Adds image resources. 
``` Objective-C
- (void)addImageElement:(NSString *)url 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| url | NSString * | [Required] Image address. Local and online images in png/jpg/gif/svg format are supported. If the URL is a valid local file address, the file is automatically uploaded to COS. The upload progress callback is onTEBFileUploadProgress, and the upload result callback is onTEBFileUploadStatus. |


### setHandwritingEnable:
Sets whether to enable handwriting for the whiteboard. 
``` Objective-C
- (void)setHandwritingEnable:(BOOL)enable 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| enable | BOOL | [Required] Whether handwriting is enabled or not. Valid values: true for yes, and false for no |

#### Description
After a whiteboard is created, handwriting is disabled for the whiteboard by default. 


### isHandwritingEnable
Checks whether handwriting is enabled for the whiteboard. 
``` Objective-C
- (BOOL)isHandwritingEnable
```
#### Response
Whether handwriting is enabled or not 


### refresh
Refreshes the current whiteboard page and triggers the onTEBRefresh callback. 
``` Objective-C
- (void)refresh
```
#### Warning
If the current whiteboard contains PowerPoint, HTML5, image, or video content, refreshing the whiteboard triggers the corresponding callback. 


### syncAndReload
Syncs local data that failed to be sent to the remote end and refreshes the local data. 
``` Objective-C
- (void)syncAndReload
```
#### Warning
Reload is to reload historical data, which will trigger all callbacks except those for onTEBInit during whiteboard initialization. 

#### Description
Usage: this API is used after network recovery to synchronize local data to the remote end and fetch remote data to the local end. Call timing: the API is called after network recovery. Use restrictions: (1) This API supports only version 2.4.9 and later. (2) Before the historical data is load successfully, this API cannot be repeatedly called. Otherwise, the callback alarm TEDU_BOARD_WARNING_ILLEGAL_OPERATION will be triggered. 


### snapshot:
Creates a whiteboard snapshot. 
``` Objective-C
- (void)snapshot:(TEduBoardSnapshotInfo *)info 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| info | TEduBoardSnapshotInfo * | Snapshot information |



## File Operation APIs

### applyFileTranscode:config:
Initiates a file transcoding request. 
``` Objective-C
- (void)applyFileTranscode:(NSString *)path config:(TEduBoardTranscodeConfig *)config 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| path | NSString * | Path of the file for transcoding, which is UTF8-coded |
| config | TEduBoardTranscodeConfig * | Transcoding parameters |

#### Warning
This API is designed to enable users to quickly use the transcoding feature in the access stage. Generally, we do not recommend that you use this API in production environments. We recommend that you initiate transcoding requests in production environments by using backend service APIs. 

#### Description
Transcoding is supported for PowerPoint, PDF, and Word files. PowerPoint files are transcoded into HTML5 animations by default, and original animation effects of the PowerPoint file can be restored. Other files are transcoded into static images. PowerPoint animation transcoding rate is about 1 sec/slide, whereas the transcoding rate of any files into static images is about 0.5 sec/page. The transcoding progress and result will be returned through the onTEBFileTranscodeProgress callback. For more information, see the description document of the callback. 


### getFileTranscodeProgress:
Actively queries the file transcoding progress. 
``` Objective-C
- (void)getFileTranscodeProgress:(NSString *)taskId 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| taskId | NSString * | Transcoding task ID obtained from the onTEBFileTranscodeProgress callback |

#### Warning
This API is used only in special business scenarios to actively query the file transcoding progress. After ApplyFileTranscode is called, the SDK will automatically trigger the onTEBFileTranscodeProgress callback according to schedule. Normally, you do not need to actively call this API. 

#### Description
The transcoding progress and result will be returned through the onTEBFileTranscodeProgress callback. For more information, see the description document of the callback. 


### addTranscodeFile:
Adds a file for transcoding. 
``` Objective-C
- (NSString *)addTranscodeFile:(TEduBoardTranscodeFileResult *)result 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| result | TEduBoardTranscodeFileResult * | File transcoding result |

#### Response
File ID 

#### Warning
If the passed-in file URL is repeated, the file ID returned will be a null string. 
Before the corresponding onTEBAddTranscodeFile callback is received, you cannot use the returned file ID to query file information. 

#### Description
The field information of TEduBoardTranscodeFileResult can be retrieved by:
1. Using the client ApplyFileTranscode for transcoding. The transcoding result will be used to call this API.
2. (Recommended) Using the server RESTful API for transcoding. Only four fields of the transcoding result (title, resolution, url, and pages) need to be passed in. The field relationships between the server and the client are: Title -> title, Resolution -> resolution, ResultUrl -> url, and Pages -> pages. For details, see the [transcoding document](https://cloud.tencent.com/document/product/1137/40260).


### deleteFile:
Deletes a file. 
``` Objective-C
- (void)deleteFile:(NSString *)fileId 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | NSString * | ID of the file to delete |

#### Description
When the file ID is nullptr, it indicates the current file. The default file cannot be deleted. 


### switchFile:
Switches to another file. 
``` Objective-C
- (void)switchFile:(NSString *)fileId 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | NSString * | ID of the file to switch to |

#### Warning
This API can only be used for file switching. If the passed-in fileId is the current file ID, the SDK will ignore other parameters and do not perform any operations.

#### Description
The file ID is required. If it is nullptr or a null string, file switching will fail. 


### switchFile:boardId:stepIndex:
Switches files. 
``` Objective-C
- (void)switchFile:(NSString *)fileId boardId:(NSString *)boardId stepIndex:(NSInteger)stepIndex 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | NSString * | ID of the file to switch to |
| boardId | NSString * | Switch files and redirect to this whiteboard page |
| stepIndex | NSInteger | Redirect to the whiteboard page and switch to this animation |

#### Warning
This API can only be used for file switching. If the passed-in fileId is the current file ID, the SDK will ignore other parameters and do not perform any operations.

#### Description
The file ID is required. If it is nullptr or a null string, file switching will fail. 


### getCurrentFile
Obtains the current file ID. 
``` Objective-C
- (NSString *)getCurrentFile
```
#### Response
Current file ID 


### getFileInfo:
Obtains the file information of the specified file on the whiteboard. 
``` Objective-C
- (TEduBoardFileInfo *)getFileInfo:(NSString *)fileId 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | NSString * | - |

#### Response
File information 

#### Warning
Each time this API is called, the returned value is stored in the same memory. To save the returned information, copy it once it is returned. 


### getFileInfoList
Obtains the file information list of all uploaded files on the whiteboard. 
``` Objective-C
- (NSArray< TEduBoardFileInfo * > *)getFileInfoList
```
#### Response
File information list 

#### Warning
If you no longer need the return value, you do not have to delete it yourself. However, you must call its release method to release the occupied memory space. 


### getFileBoardList:
Obtains the whiteboard ID list of the specified file. 
``` Objective-C
- (NSArray< NSString * > *)getFileBoardList:(NSString *)fileId 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | NSString * | File ID |

#### Response
Whiteboard ID list 

#### Warning
If you no longer need the return value, you do not have to delete it yourself. However, you must call its release method to release the occupied memory space. 


### getThumbnailImages:
Obtains the thumbnail of the specified file, excluding the default file (fileId=#DEFAULT). 
``` Objective-C
- (NSArray *)getThumbnailImages:(NSString *)fileId 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | NSString * | File ID |

#### Response
Thumbnail URL list

#### Description
When you call the RESTful API to request transcoding, the "thumbnail_resolution" parameter is required to enable the thumbnail feature. Otherwise, the returned thumbnail URL is invalid. 


### clearFileDraws:
Clears all whiteboard doodles of the specified file. 
``` Objective-C
- (void)clearFileDraws:(NSString *)fileId 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | NSString * | File ID |


### addVideoFile:
Adds a video file. 
``` Objective-C
- (NSString *)addVideoFile:(NSString *)url 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| url | NSString * | File playback address |

#### Response
File ID

#### Description
This API supports video files in mp4, m3u8, and hls formats and triggers the status change callback onTEBVideoStatusChanged. 


### showVideoControl:
Shows or hides the video control bar. 
``` Objective-C
- (void)showVideoControl:(BOOL)show 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| show | BOOL | Whether the video control bar is displayed or not |

#### Warning
This is a global control item that applies to all video files. It specifies whether to show or hide the default video control bar. By default, the default video control bar is displayed. The UI style of the control bar varies on different platforms. 


### playVideo
Plays a video. 
``` Objective-C
- (void)playVideo
```
#### Warning
This API is valid only for the current file.

#### Description
This API triggers the status change callback onTEBVideoStatusChange. It is usually used when a custom video control bar is used. When the app is switched back to the frontend on a mobile client, play (the default behavior of WebView) is called. 


### pauseVideo
Pauses a video. 
``` Objective-C
- (void)pauseVideo
```
#### Warning
This API is valid only for the current file.

#### Description
This API triggers the status change callback onTEBVideoStatusChanged. It is usually used when a custom video control bar is used. When the app is switched to the backend on a mobile client, pause (the default behavior of WebView) is called. 


### seekVideo:
Jumps to a specified time point in a video (only for VOD videos). 
``` Objective-C
- (void)seekVideo:(CGFloat)time 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| time | CGFloat | Playback progress in seconds |

#### Warning
This API is valid only for the current file.

#### Description
This API triggers the status change callback onTEBVideoStatusChanged. It is usually used when a custom video control bar is used. 


### setSyncVideoStatusEnable:
Sets whether to synchronize local video operations to the remote end. 
``` Objective-C
- (void)setSyncVideoStatusEnable:(BOOL)enable 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| enable | BOOL | [Required] Whether to sync or not |

#### Warning
This is a global control item that applies to all video files.

#### Description
This API specifies whether the triggering of the play/pause/seek API and control bar events affects the remote end. The default value is true. Usually, it is set to false for students and true for teachers. 


### startSyncVideoStatus:
This is an internal start timer that syncs the video status to the remote end according to a schedule (only for mp4 files). 
``` Objective-C
- (void)startSyncVideoStatus:(NSInteger)interval 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| interval | NSInteger | [Optional] Synchronization interval, for example, 5 seconds |

#### Warning
This API is valid only for the current file.

#### Description
This API is usually called after the video is loaded successfully on the teacher’s end. After file switching, the timer is automatically terminated. 


### stopSyncVideoStatus
Stops syncing the video status. 
``` Objective-C
- (void)stopSyncVideoStatus
```
#### Warning
This API is valid only for the current file. 


### addH5File:
Adds an H5 file. 
``` Objective-C
- (NSString *)addH5File:(NSString *)url 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| url | NSString * | [Required] Webpage address |

#### Response
File ID 

#### Warning
Only display but not interaction is supported. 


### addImagesFile:
Imports image files to the whiteboard in batches. 
``` Objective-C
- (NSString *)addImagesFile:(NSArray< NSString * > *)urls 
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| urls | NSArray< NSString * > * | List of URLs of the background images to use. These URLs are UTF8-coded. |

#### Response
IDs of the added files 

