## TEduBoardController
Whiteboard controller 

## Creating and Terminating Instances

### TEduBoardController
Creates a whiteboard controller instance. 
``` Java
TEduBoardController(Context context)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| context | Context | Application's context environment |



## Setting TEduBoardCallback

### addCallback
Sets the event callback listener. 
``` Java
void addCallback(TEduBoardCallback callback)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| callback | TEduBoardCallback | Event callback listener |

#### Warning
We recommend that you call this method before running init to handle the error. 


### removeCallback
Deletes the event callback listener. 
``` Java
void removeCallback(TEduBoardCallback callback)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| callback | TEduBoardCallback | Event callback listener |



## Basic Process APIs

### Init
Initializes the whiteboard. 
``` Java
void init(TEduBoardAuthParam authParam, int roomId, final TEduBoardInitParam initParam)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| authParam | TEduBoardAuthParam | Authorization parameter |
| roomId | int | Classroom ID, which is a 32-bit integer. Value range: [1, 4294967294] |
| initParam | final TEduBoardInitParam | An optional parameter, which specifies a series of attribute values for initializing the whiteboard. |

#### Warning
When Tencent Cloud IMSDK is used for real-time data synchronization, only one whiteboard instance is supported. If multiple whiteboard instances are created, the doodle status may be abnormal.

#### Description
You can use initParam.timSync to specify whether to use Tencent Cloud IMSDK for real-time data synchronization. When initParam.timSync is set to True, the system tries to use Tencent Cloud IMSDK as the signaling channel to receive and send data in real time (in this case, only message receiving and sending are automatically implemented, while users must manually perform the initialization, room entry, and other operations.) Currently, only IMSDK 4.3.118 and later are supported. 


### uninit
Uninitializes the whiteboard and releases internal resources. 
``` Java
void uninit()
```
#### Warning
This API is related to the end of billing. Users must call this API when exiting the classroom. 

#### Description
Billing will end after the whiteboard object is terminated. 


### getBoardRenderView
Obtains the whiteboard rendering view. 
``` Java
View getBoardRenderView()
```
#### Response
Whiteboard rendering view 

#### Warning
Calling this API does not work until you receive the onTEBBoardInit callback.

#### Description
After you obtain the view by calling this API, the view will be added to the view tree. After this addition, you must call removeView. 


### addSyncData
Adds whiteboard synchronization data. 
``` Java
void addSyncData(String data)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| data | String | Synchronization data from other members in the room |

#### Description
This API is used to sync data between whiteboard instances. When the built-in IM is used as the signaling channel, you do not need to call this API. 


### setDataSyncEnable
Sets whether to enable data synchronization for the whiteboard. 
``` Java
void setDataSyncEnable(boolean enable)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| enable | boolean | Whether to enable data synchronization |

#### Description
After a whiteboard instance is created, data synchronization is enabled by default. If this feature is disabled, none of local whiteboard operations will be synchronized to the remote end or server. 


### isDataSyncEnable
Checks whether data synchronization is enabled for the whiteboard. 
``` Java
boolean isDataSyncEnable()
```
#### Response
Whether data synchronization is enabled or not. Valid values: true for enabled, and false for disabled. 


### reset
Resets the whiteboard. 
``` Java
void reset()
```
#### Description
After this API is called, all whiteboard pages and files will be deleted. 


### getSyncTime
Obtains the synchronization timestamp. 
``` Java
long getSyncTime()
```
#### Response
Synchronization timestamp in milliseconds 


### syncRemoteTime
Synchronizes the remote timestamp. 
``` Java
void syncRemoteTime(String userId, long timestamp)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| userId | String | Remote user ID |
| timestamp | long | Synchronization timestamp for the remote user, in milliseconds |


### getVersion
Obtains the SDK version number. 
``` Java
static String getVersion()
```
#### Response
SDK version number 



## Doodle APIs

### setDrawEnable
Sets whether the whiteboard allows doodle. 
``` Java
void setDrawEnable(boolean enable)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| enable | boolean | Whether doodle is allowed for the whiteboard or not. Valid values: true for yes, false for no |

#### Description
After a whiteboard instance is created, doodle is allowed for the whiteboard by default. 


### isDrawEnable
Checks whether doodle is allowed for the whiteboard. 
``` Java
boolean isDrawEnable()
```
#### Response
Whether doodle is allowed for the whiteboard or not. Valid values: true for yes, and false for no. 


### setAccessibleUsers
Sets users whose drawings can be operated. 
``` Java
void setAccessibleUsers(List< String > users)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| users | List< String > | Users for which operations are allowed. The null value indicates all users. |

#### Description
This API has the following effects:
1. The ERASER tool can erase only the doodles drawn by the users specified by the users parameter, but cannot erase the doodles drawn by other users.
2. The POINTSELECT and SELECT tools can select only the doodles drawn by the users specified by the users parameter, but cannot select the doodles drawn by other users.
3. The clear API can clear only selected doodles and the doodles drawn by the users specified by the users parameter. It cannot clear backgrounds or the doodles drawn by other users.
4. This API has no impact on other features of the whiteboard that are not listed here. 


### setGlobalBackgroundColor
Sets the background color of all whiteboards. 
``` Java
void setGlobalBackgroundColor(TEduBoardColor color)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| color | TEduBoardColor | Global background color to set |

#### Description
When this API is called, the background color of all whiteboards is changed, and the default background color of newly created whiteboards will be the global background color. 


### getGlobalBackgroundColor
Obtains the global background color of whiteboards. 
``` Java
TEduBoardColor getGlobalBackgroundColor()
```
#### Response
Global background color 


### setBackgroundColor
Sets the background color of the current whiteboard page. 
``` Java
void setBackgroundColor(TEduBoardColor color)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| color | TEduBoardColor | Background color to set |

#### Description
After a whiteboard page is created, the default background color is set by the setDefaultBackgroundColor API. 


### getBackgroundColor
Obtains the background color of the current whiteboard page. 
``` Java
TEduBoardColor getBackgroundColor()
```
#### Response
Background color of the current whiteboard page 


### setToolType
Sets the whiteboard tool to use. 
``` Java
void setToolType(int type)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| type | int | Whiteboard tool to set |


### getToolType
Obtains the whiteboard tool in use. 
``` Java
int getToolType()
```
#### Response
Whiteboard tool in use 


### setCursorIcon
Sets the cursor icon for the whiteboard tool. 
``` Java
void setCursorIcon(int type, TEduBoardCursorIcon icon)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| type | int | Type of the whiteboard tool for which you want to set the cursor icon |
| icon | TEduBoardCursorIcon | Cursor icon to set |


### setBrushColor
Sets the brush color. 
``` Java
void setBrushColor(TEduBoardColor color)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| color | TEduBoardColor | Brush color to set |

#### Description
The brush color applies to all doodles. 


### getBrushColor
Obtains the brush color. 
``` Java
TEduBoardColor getBrushColor()
```
#### Response
Brush color 


### setBrushThin
Sets the brush thickness. 
``` Java
void setBrushThin(int thin)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| thin | int | Brush thickness to set |

#### Description
The brush thickness applies to all doodles. If the actual pixel value (thin * whiteboard height/10000) px is less than 1 px, the doodle line will be almost invisible. 


### getBrushThin
Obtains the brush thickness. 
``` Java
int getBrushThin()
```
#### Response
Brush thickness 


### setTextColor
Sets the text color. 
``` Java
void setTextColor(TEduBoardColor color)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| color | TEduBoardColor | Text color to set |


### getTextColor
Obtains the text color. 
``` Java
TEduBoardColor getTextColor()
```
#### Response
Text color 


### setTextSize
Sets the text size. 
``` Java
void setTextSize(int size)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| size | int | Text size to set |

#### Description
This API defines the actual pixel value, that is, (size * whiteboard height/10000) px. 


### getTextSize
Obtains the text size. 
``` Java
int getTextSize()
```
#### Response
Text size 


### setTextStyle
Sets the text style. 
``` Java
void setTextStyle(int style)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| style | int | Text style to set |


### getTextStyle
Obtains the text style. 
``` Java
int getTextStyle()
```
#### Response
Text style 


### clear
Clears the doodle on the current whiteboard page. 
``` Java
void clear(boolean clearBackground)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| clearBackground | boolean | Whether or not to clear the background color and background image simultaneously |


### clear
Clears the doodle on the current whiteboard page. 
``` Java
void clear(boolean clearBackground, boolean clearSelectedOnly)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| clearBackground | boolean | Whether or not to clear the background color and background image simultaneously |
| clearSelectedOnly | boolean | Whether or not to clear the selected doodle only |

#### Warning
Currently, you cannot clear the background image while clearing the selected doodle. 


### setLineStyle
Sets the line style. 
``` Java
void setLineStyle(TEduBoardLineStyle style)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| style | TEduBoardLineStyle | Line style to set |

#### Warning
The dotted-line style is supported in Android 4.4 and later. In versions earlier than 4.4, if the dotted-line style is set, it will be replaced by the solid-line style. 


### getLineStyle
Obtains the line style. 
``` Java
TEduBoardLineStyle getLineStyle()
```
#### Response
Line style 


### setOvalDrawMode
Sets the oval drawing mode. 
``` Java
void setOvalDrawMode(int drawMode)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| drawMode | int | Oval drawing mode to set |


### getOvalDrawMode
Obtains the oval drawing mode. 
``` Java
int getOvalDrawMode()
```
#### Response
Oval drawing mode 


### setBackgroundImage
Sets the background image of the current whiteboard page. 
``` Java
void setBackgroundImage(String url, int mode)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| url | String | URL of the background image to set, which is UTF8-coded |
| mode | int | Image filling alignment mode to use |

#### Description
If the URL is a valid local file address, the file is automatically uploaded to COS. If the URL is a website address, it supports HTTPS links by default. For versions earlier than Android 5.0, the default mode is MIXED_CONTENT_ALWAYS_ALLOW, which means that WebView is always allowed to load HTTPS and HTTP requests simultaneously. Starting from Android 5.0, the default mode is MIXED_CONTENT_NEVER_ALLOW, which means that WebView is never allowed to load HTTPS and HTTP requests simultaneously. When obtaining the whiteboard rendering view control through getBoardRenderView, you can set WebSettings as follows: WebSettings settings = (WebView) mWebView.getSettings(); if(Build.VERSION.SDK_INT>=Build.VERSION_CODES.LOLLIPOP) { settings.setMixedContentMode(0); }. For systems later than Android P, network requests with restricted plaintext traffic and non-encrypted traffic requests are prohibited by the system. To resolve this problem, refer to the following methods:


### setBackgroundH5
Sets the background H5 page of the current whiteboard page. 
``` Java
void setBackgroundH5(String url)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| url | String | URL of the background H5 page to set |

#### Description
This API and the setBackgroundImage API are mutually exclusive. 


### undo
Undoes the last action on the current whiteboard page. 
``` Java
void undo()
```

### redo
Redoes the last undone action on the current whiteboard page. 
``` Java
void redo()
```

### setHandwritingEnable
Sets whether to enable handwriting for the whiteboard. 
``` Java
void setHandwritingEnable(boolean enable)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| enable | boolean | [Required] Whether handwriting is enabled or not. Valid values: true for yes, and false for no. |

#### Description
After a whiteboard is created, handwriting is disabled for the whiteboard by default. 


### isHandwritingEnable
Checks whether handwriting is enabled for the whiteboard. 
``` Java
boolean isHandwritingEnable()
```
#### Response
Whether handwriting is enabled or not 



## Whiteboard Page Operation APIs

### addBoard
Adds a whiteboard page. 
``` Java
String addBoard(String url)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| url | String | URL of the background image to use, which is UTF8-coded. The null value indicates that no background image is specified. |

#### Response
Whiteboard ID 

#### Warning
Whiteboard pages will be added to the default file (with the file ID ::DEFAULT). Whiteboard pages cannot be added for user-uploaded files. 


### deleteBoard
Deletes a whiteboard page. 
``` Java
void deleteBoard(String boardId)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| boardId | String | ID of the whiteboard to delete. The null value indicates the current page. |

#### Warning
Only whiteboard pages in the default file (with file ID ::DEFAULT) can be deleted. The default whiteboard page (with whiteboard ID ::DEFAULT) cannot be deleted. 


### prevStep
Goes to the previous step. Each step corresponds to an animation effect of the PowerPoint file. If no displayed animation effect is available, calling this API goes to the previous slide. 
``` Java
void prevStep()
```

### nextStep
Goes to the next step. 
``` Java
void nextStep()
```
#### Description
Each step corresponds to an animation effect of the PowerPoint file. If no animation effect that has not yet been displayed is available, calling this API goes to the next slide. 


### prevBoard
Goes to the previous page. 
``` Java
void prevBoard()
```
#### Description
If the current whiteboard page is the first page of the current file, calling this API does not work. 


### nextBoard
Goes to the next page. 
``` Java
void nextBoard()
```
#### Description
If the current whiteboard page is the last page of the current file, calling this API does not work. 


### gotoBoard
Redirects to the specified whiteboard page. 
``` Java
void gotoBoard(String boardId)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| boardId | String | ID of the whiteboard page to redirect to |

#### Description
This API is used to redirect to any whiteboard page in any file. 


### prevBoard
Goes to the previous page. 
``` Java
void prevBoard(boolean resetStep)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| resetStep | boolean | Whether or not to reset the PowerPoint animation steps after redirecting to the specified slide |

#### Description
If the current whiteboard page is the first page of the current file, calling this API does not work. 


### nextBoard
Goes to the next page. 
``` Java
void nextBoard(boolean resetStep)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| resetStep | boolean | Whether or not to reset the PowerPoint animation steps after redirecting to the specified slide |

#### Description
If the current whiteboard page is the last page of the current file, calling this API does not work. 


### gotoBoard
Redirects to the specified whiteboard page. 
``` Java
void gotoBoard(String boardId, boolean resetStep)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| boardId | String | ID of the whiteboard page to redirect to |
| resetStep | boolean | Whether or not to reset the PowerPoint animation steps after redirecting to the specified slide |

#### Description
This API is used to redirect to any whiteboard page in any file. 


### getCurrentBoard
Obtains the ID of the current whiteboard page. 
``` Java
String getCurrentBoard()
```
#### Response
ID of the current whiteboard page 


### getBoardList
Obtains the whiteboard list of all files. 
``` Java
List<String> getBoardList()
```
#### Response
Whiteboard list of all files 


### setBoardRatio
Sets the aspect ratio of the current whiteboard page. 
``` Java
void setBoardRatio(String ratio)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| ratio | String | Whiteboard aspect ratio to set |

#### Description
The format of the value is similar to "4:3" and "16:9". 


### getBoardRatio
Obtains the aspect ratio of the current whiteboard page. 
``` Java
String getBoardRatio()
```
#### Response
Whiteboard aspect ratio, in the same format as the setBoardRatio parameter 


### setBoardScale
Sets the scale of the current whiteboard page. 
``` Java
void setBoardScale(int scale)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| scale | int | Whiteboard scale to set |

#### Description
The value range is [100, 300], and the actual scale is scale/100. 


### getBoardScale
Obtains the scale of the current whiteboard page. 
``` Java
int getBoardScale()
```
#### Response
Whiteboard scale, in the same format as the SetBoardScale parameter 


### setBoardContentFitMode
Sets the whiteboard content self-adaption mode. 
``` Java
void setBoardContentFitMode(int mode)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| mode | int | Whiteboard content self-adaption mode to set |

#### Description
Setting the self-adaption mode affects all subsequent whiteboard content operations. In addition, the AddTranscodeFile API is affected. 


### getBoardContentFitMode
Obtains the whiteboard content self-adaption mode. 
``` Java
int getBoardContentFitMode()
```
#### Response
Whiteboard content self-adaption mode 


### refresh
Refreshes the current whiteboard page and triggers the onTEBRefresh callback. 
``` Java
void refresh()
```
#### Warning
If the current whiteboard contains PowerPoint, HTML5, image, or video content, refreshing the whiteboard triggers the corresponding callback. 


### syncAndReload
Syncs local data that failed to be sent to the remote end and refreshes the local data. 
``` Java
void syncAndReload()
```
#### Warning
Reload is to reload historical data, which will trigger all callbacks except those for onTEBInit during whiteboard initialization. 

#### Description
Usage: this API is used after network recovery to synchronize local data to the remote end and fetch remote data to the local end. Call timing: the API is called after network recovery. Use restrictions: (1) This API supports only version 2.4.9 and later. (2) Before the historical data is load successfully, this API cannot be repeatedly called. Otherwise, the callback alarm TEDU_BOARD_WARNING_ILLEGAL_OPERATION will be triggered. 



## File Operation APIs

### addImagesFile
Imports images in batches. 
``` Java
String addImagesFile(List< String > urls)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| urls | List< String > | List of URLs of images to use. These URLs are UTF8-coded. |

#### Response
ID of the newly added file 


### applyFileTranscode
Initiates a file transcoding request. 
``` Java
void applyFileTranscode(final String path, final TEduBoardTranscodeConfig config)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| path | final String | Path of the file for transcoding, which is UTF8-coded |
| config | final TEduBoardTranscodeConfig | Transcoding parameter |

#### Warning
This API is designed to enable users to quickly use the transcoding feature in the access stage. Generally, we do not recommend that you use this API in production environments. We recommend that you initiate transcoding requests in production environments by using backend service APIs. 

#### Description
Transcoding is supported for PowerPoint, PDF, and Word files. PowerPoint files are transcoded into HTML5 animations by default, and original animation effects of the PowerPoint file can be restored. Other files are transcoded into static images. PowerPoint animation transcoding rate is about 1 sec/slide, whereas the transcoding rate of any files into static images is about 0.5 sec/page. The transcoding progress and result will be returned through the onTEBFileTranscodeProgress callback. For more information, see the description document of the callback. 


### getFileTranscodeProgress
Actively queries the file transcoding progress. 
``` Java
void getFileTranscodeProgress(final String taskId)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| taskId | final String | Transcoding task ID obtained from the onTEBFileTranscodeProgress callback |

#### Warning
This API is used only in special business scenarios to actively query the file transcoding progress. After applyFileTranscode is called, the SDK will automatically trigger the onTEBFileTranscodeProgress callback according to schedule. Normally, you do not need to actively call this API. 

#### Description
The transcoding progress and result will be returned through the onTEBFileTranscodeProgress callback. For more information, see the description document of the callback. 


### addTranscodeFile
Adds a transcoding file. 
``` Java
String addTranscodeFile(final TEduBoardTranscodeFileResult result)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| result | final TEduBoardTranscodeFileResult | File transcoding result |

#### Response
File ID 

#### Warning
If the passed-in file URL is repeated, the file ID returned will be a null string. 
Before the corresponding onTEBAddTranscodeFile callback is received, you cannot use the returned file ID to query file information. 

#### Description
The field information of TEduBoardTranscodeFileResult can be retrieved by:
1. Using the client applyFileTranscode for transcoding. The transcoding result will be used to call this API.
2. (Recommended) Using the server RESTful API for transcoding. Only four fields of the transcoding result (title, resolution, url, and pages) need to be passed in. The field relationships between the server and the client are: Title -> title, Resolution -> resolution, ResultUrl -> url, and Pages -> pages. For details, see the [transcoding document](https://cloud.tencent.com/document/product/1137/40260).


### addImageElement
Adds image resources. 
``` Java
void addImageElement(String url)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| url | String | [Required] Image address. Local and online images in png/jpg/gif/svg format are supported. If the URL is a valid local file address, the file is automatically uploaded to COS. The upload progress callback is onTEBFileUploadProgress, and the upload result callback is onTEBFileUploadStatus. |


### deleteFile
Deletes a file. 
``` Java
void deleteFile(String fileId)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | String | ID of the file to delete |

#### Description
When the file ID is nullptr, it indicates the current file. The default file cannot be deleted. 


### switchFile
Switches to another file. 
``` Java
void switchFile(String fileId)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | String | ID of the file to switch to |

>? The file ID is required. If it is null or a null string, file switching will fail. 


### switchFile
Switches files. 
``` Java
void switchFile(String fileId, String boardId, int stepIndex)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | String | ID of the file to switch to |
| boardId | String | Switch files and redirect to this whiteboard page |
| stepIndex | int | Redirect to the whiteboard page and switch to this animation |

#### Warning
This API can only be used for file switching. If the passed-in fileId is the current file ID, the SDK will ignore other parameters and do not perform any operations. 

>? The file ID is required. If it is null or a null string, file switching will fail. 


### getCurrentFile
Obtains the current file ID. 
``` Java
String getCurrentFile()
```
#### Response
Current file ID 


### getFileInfoList
Obtains the file information list of all uploaded files on the whiteboard. 
``` Java
List<TEduBoardFileInfo> getFileInfoList()
```
#### Response
File information list 


### getFileInfo
Obtains the file information of the specified file on the whiteboard. 
``` Java
TEduBoardFileInfo getFileInfo(String fid)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fid | String | - |

#### Response
File information 


### getFileBoardList
Obtains the whiteboard ID list of the specified file. 
``` Java
List<String> getFileBoardList(String fileId)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | String | File ID |

#### Response
Whiteboard ID list 


### clearFileDraws
Clears all whiteboard doodles of the specified file. 
``` Java
void clearFileDraws(String fileId)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | String | File ID |


### getThumbnailImages
Obtains the thumbnail of the specified file, excluding the default file (fileId=#DEFAULT). 
``` Java
List<String> getThumbnailImages(String fileId)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | String | File ID |

#### Response
Thumbnail URL list 

>? When you call the RESTful API to request transcoding, the "thumbnail_resolution" parameter is required to enable the thumbnail feature. Otherwise, the returned thumbnail URL is invalid. 


### addVideoFile
Adds a video file. 
``` Java
String addVideoFile(String url)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| url | String | File playback address |

#### Response
File ID 

#### Warning
In the TBS environment, due to the restrictions of the X5 kernel and video resource I-frame interval, precise synchronization cannot be achieved on Android. For example, for a 10-second video with an I-frame interval of 5 seconds, when the system seeks the 4-second position, it starts playing the video from 0 seconds on TBS. Mobile clients support mp4 and m3u8 formats, while desktop clients support mp4, m3u8, flv, and rtmp formats. In addition, the status change callback onTEBVideoStatusChange will be triggered. 


### showVideoControl
Shows or hides the video control bar. 
``` Java
void showVideoControl(boolean show)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| show | boolean | Whether to show the control bar or not |

#### Warning
This is a global control item that applies to all video files. It specifies whether to show or hide the default video control bar. By default, the default video control bar is displayed. The UI style of the control bar varies on different platforms. 


### playVideo
Plays a video. 
``` Java
void playVideo()
```
#### Warning
This API is valid only for the current file.

#### Description
This API triggers the status change callback onTEBVideoStatusChange. It is usually used when a custom video control bar is used. When the app is switched back to the frontend on a mobile client, play (the default behavior of WebView) is called. 


### pauseVideo
Pauses a video. 
``` Java
void pauseVideo()
```
#### Warning
This API is valid only for the current file.

#### Description
This API triggers the status change callback onTEBVideoStatusChange. It is usually used when a custom video control bar is used. When the app is switched to the backend on a mobile client, pause (the default behavior of WebView) is called. 


### seekVideo
Jumps to a specified time point in a video (only for VOD videos). 
``` Java
void seekVideo(float time)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| time | float | Playback progress in seconds |

#### Warning
This API is valid only for the current file.

#### Description
This API triggers the status change callback onTEBVideoStatusChange. It is usually used when a custom video control bar is used. 


### setSyncVideoStatusEnable
Sets whether to synchronize local video operations to the remote end. 
``` Java
void setSyncVideoStatusEnable(boolean enable)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| enable | boolean | [Required] Whether to synchronize or not |

#### Warning
This is a global control item that applies to all video files.

#### Description
This API specifies whether the triggering of the play/pause/seek API and control bar events affects the remote end. The default value is true. Usually, it is set to false for students and true for teachers. 


### startSyncVideoStatus
This is an internal start timer that syncs the video status to the remote end according to a schedule (only for mp4 files). 
``` Java
void startSyncVideoStatus(int interval)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| interval | int | [Optional] Synchronization interval, for example, 5 seconds |

#### Warning
This API is valid only for the current file.

#### Description
This API is usually called after the video is loaded successfully on the teacher’s end. After file switching, the timer is automatically terminated. 


### stopSyncVideoStatus
Stops syncing the video status. 
``` Java
void stopSyncVideoStatus()
```
#### Warning
This API is valid only for the current file. 


### addH5File
Adds an H5 file. 
``` Java
String addH5File(String url)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| url | String | [Required] Webpage address |

#### Response
File ID 

#### Warning
Only display but not interaction is supported. 


### snapshot
Creates a whiteboard snapshot. 
``` Java
void snapshot(TEduBoardSnapshotInfo info)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| info | TEduBoardSnapshotInfo | Snapshot information |





