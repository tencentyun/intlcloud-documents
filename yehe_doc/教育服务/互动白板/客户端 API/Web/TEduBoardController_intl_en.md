## TEduBoard
Whiteboard controller 

## Creating and Terminating Instances

### TEduBoard
Creates a whiteboard 
```JavaScript
TEduBoard(TEduBoardInitParam initParams)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| initParams | TEduBoardInitParam | [Required] Whiteboard initialization parameters |


### destroy
Terminates a whiteboard 
```JavaScript
void destroy()
```


## Setting TEduBoardCallback

### on
Enables event listening 
```JavaScript
void on(String name, Function callback)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| name | String | [Required] Event to listen on |
| callback | Function | [Required] Event processing callback |


### off
Cancels event listening 
```JavaScript
void off(String name, Function callback)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| name | String | [Required] Event to stop listening on |
| callback | Function | [Required] Event processing callback |



## Basic Process APIs

### addSyncData
Adds whiteboard synchronization data 
```JavaScript
void addSyncData(Object data)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| data | Object | [Required] Synchronization data sent by a member in the room |

>? This API is used to sync data between multiple whiteboards 


### getVersion
Obtains the SDK version number 
```JavaScript
String getVersion()
```
#### Response
SDK version number 


### setDataSyncEnable
Sets whether data synchronization is enabled for the whiteboard 
```JavaScript
void setDataSyncEnable(Boolean enable)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| enable | Boolean | [Required] Whether data synchronization is enabled |

#### Description
After a whiteboard instance is created, data synchronization is enabled by default. If data synchronization is disabled, none of the local whiteboard operations will be synchronized to the remote end or to the server 


### isDataSyncEnable
Checks whether data synchronization is enabled for the whiteboard 
```JavaScript
Boolean isDataSyncEnable()
```
#### Response
Whether data synchronization is enabled. Valid values: true for enabled, and false for disabled 


### reset
Resets the whiteboard 
```JavaScript
void reset()
```
#### Description
After this API is called, all whiteboard pages and files will be deleted 


### getSyncTime
Obtains the synchronization timestamp 
```JavaScript
Number getSyncTime()
```
#### Response
Synchronization timestamp in milliseconds 


### syncRemoteTime
Syncs the remote timestamp 
```JavaScript
void syncRemoteTime(String userId, Number timestamp)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| userId | String | [Required] Remote user ID |
| timestamp | Number | [Required] Sync timestamp of the remote user, in milliseconds |



## Doodle APIs

### setDrawEnable
Sets whether the whiteboard allows doodle 
```JavaScript
void setDrawEnable(Boolean enable)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| enable | Boolean | [Required] Whether doodle is allowed for the whiteboard. Valid values: true for yes, false for no |

#### Description
After a whiteboard instance is created, doodle is allowed for the whiteboard by default 


### isDrawEnable
Checks whether doodle is allowed for the whiteboard 
```JavaScript
Boolean isDrawEnable()
```
#### Response
Whether doodle is allowed for the whiteboard. Valid values: true for yes, and false for no 


### setAccessibleUsers
Sets users whose drawings can be operated 
```JavaScript
void setAccessibleUsers(Array users)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| users | Array | [Required] Users whose drawings can be operated. The [] value or null indicates all users |

#### Description
This API has the following effects:
1. The eraser tool can only erase the doodles drawn by the users specified by the users parameter, but cannot erase the doodles drawn by other users
2. The point select and select tools can only select the doodles drawn by the users specified by the users parameter, but cannot select the doodles drawn by other users
3. The clear API can only clear selected doodles and the doodles drawn by the users specified by the users parameter. It cannot clear backgrounds or the doodles drawn by other users
4. This API has no impact on the other features of the whiteboard that are not listed here 


### setGlobalBackgroundColor
Sets the background color of all whiteboards 
```JavaScript
void setGlobalBackgroundColor(Color color)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| color | Color | [Required] Global background color to be set |

#### Description
When this API is called, the background color of all whiteboards will be changed, and the default background color of the newly created whiteboards will be the global background color 


### getGlobalBackgroundColor
Obtains the global background color of the whiteboards 
```JavaScript
Color getGlobalBackgroundColor()
```
#### Response
Global background color 


### setBackgroundColor
Sets the background color of the current whiteboard page 
```JavaScript
void setBackgroundColor(Color color)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| color | Color | [Required] Background color to be set |

#### Description
After a whiteboard page is created, the default background color is set by the SetDefaultBackgroundColor API 


### getBackgroundColor
Obtains the background color of the current whiteboard page 
```JavaScript
Color getBackgroundColor()
```
#### Response
Background color of the current whiteboard page 


### setToolType
Sets the whiteboard tool to be used 
```JavaScript
void setToolType(TEduBoardToolType type)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| type | TEduBoardToolType | [Required] Whiteboard tool to be set |


### getToolType
Obtains the whiteboard tool in use 
```JavaScript
TEduBoardToolType getToolType()
```
#### Response
Whiteboard tool in use 


### setCursorIcon
Sets the cursor icon for the whiteboard tool 
```JavaScript
void setCursorIcon(TEduBoardToolType toolType, TEduBoardCursorIcon cursorIcon)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| toolType | TEduBoardToolType | [Required] Whiteboard tool type for which the cursor icon is to be set |
| cursorIcon | TEduBoardCursorIcon | [Required] Cursor icon to be set |


### setBrushColor
Sets the brush color 
```JavaScript
void setBrushColor(Color color)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| color | Color | [Required] Brush color to be set |

#### Description
The set brush color applies to all doodles 


### getBrushColor
Obtains the brush color 
```JavaScript
Color getBrushColor()
```
#### Response
Brush color 


### setBrushThin
Sets the brush thickness 
```JavaScript
void setBrushThin(Number thin)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| thin | Number | [Required] Brush thickness to be set |

#### Description
The brush thickness applies to all doodles. If the actual pixel value (thin * whiteboard height/10000) px is less than 1 px, the doodle line will be almost invisible 


### getBrushThin
Obtains the brush thickness 
```JavaScript
Number getBrushThin()
```
#### Response
Brush thickness 


### setTextColor
Sets the text color 
```JavaScript
void setTextColor(Color color)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| color | Color | [Required] Text color to be set |


### getTextColor
Obtains the text color 
```JavaScript
Color getTextColor()
```
#### Response
Text color 


### setTextSize
Sets the text size 
```JavaScript
void setTextSize(Number size)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| size | Number | [Required] Text size to set |

#### Description
This API defines the actual pixel value, which equals to size * whiteboard height/10000) px 


### getTextSize
Obtains the text size 
```JavaScript
Number getTextSize()
```
#### Response
Text size 


### setTextStyle
Sets the text style 
```JavaScript
void setTextStyle(TEduBoardTextStyle style)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| style | TEduBoardTextStyle | [Required] Text style to be set |


### getTextStyle
Obtains the text style 
```JavaScript
TEduBoardTextStyle getTextStyle()
```
#### Response
Text style 


### setLineStyle
Sets the line style 
```JavaScript
void setLineStyle(TEduBoardLineStyle style)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| style | TEduBoardLineStyle | [Required] Line style to be set |


### getLineStyle
Obtains the line style 
```JavaScript
TEduBoardLineStyle getLineStyle()
```
#### Response
Line style 


### setOvalDrawMode
Sets the oval drawing mode 
```JavaScript
void setOvalDrawMode(TEduBoardOvalDrawMode drawMode)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| drawMode | TEduBoardOvalDrawMode | [Required] Oval drawing mode to be set |


### getOvalDrawMode
Obtains the oval drawing mode 
```JavaScript
TEduBoardOvalDrawMode getOvalDrawMode()
```
#### Response
Oval drawing mode 


### clear
Clears doodles on the current whiteboard page 
```JavaScript
void clear(Boolean clearBackground, Boolean clearSelectedOnly)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| clearBackground | Boolean | [Optional] Whether to clear the background color and background image simultaneously |
| clearSelectedOnly | Boolean | [Optional] Whether to clear the selected doodle only |

#### Warning
Currently, you cannot clear the background image while clearing the selected doodle 


### setBackgroundImage
Sets the background image of the current whiteboard page 
```JavaScript
void setBackgroundImage(String url, TEduBoardImageFitMode mode)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| url | String | [Required] URL of the background image to be set, which is UTF8-coded |
| mode | TEduBoardImageFitMode | [Optional] Image padding and alignment modes to be used |

#### Description
In addition to setting an online image as the background, you can upload a local image as the background. You can pass an Object into the url parameter in the following format: 
``` 
{
   data: document.getElementById('uploadFile').files[0], //fileObject object from the input label
   userData: 'xxx' //Passthrough data, which will be returned in the file upload progress callback
}
```



### setBackgroundH5
Sets the background H5 page of the current whiteboard page 
```JavaScript
void setBackgroundH5(String url)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| url | String | [Required] URL of the background H5 page to be set |

#### Description
This API and the SetBackgroundImage API are mutually exclusive 


### undo
Undoes the last action on the current whiteboard page 
```JavaScript
void undo()
```

### redo
Redoes the last undone action on the current whiteboard page 
```JavaScript
void redo()
```

### resize
Recalculates the whiteboard size and renders the whiteboard 
```JavaScript
void resize()
```


## Whiteboard Page Operation APIs

### addBoard
Adds a whiteboard page 
```JavaScript
String addBoard(String url, TEduBoardImageFitMode mode)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| url | String | [Optional] URL of the background image to be used. The null value indicates that no background image is specified |
| mode | TEduBoardImageFitMode | [Optional] Image padding and alignment modes to be used |

#### Response
Whiteboard ID 

#### Warning
Whiteboard pages will be added to the default file (with the file ID ::DEFAULT). Whiteboard pages cannot be added for user-uploaded files 


### deleteBoard
Deletes a whiteboard page 
```JavaScript
void deleteBoard(String boardId)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| boardId | String | [Optional] ID of the whiteboard to be deleted. The null value indicates the current page |

#### Warning
Only whiteboard pages in the default file (with file ID ::DEFAULT) can be deleted. The default whiteboard page (with whiteboard ID ::DEFAULT) cannot be deleted 


### prevStep
Goes to the previous step. Each step corresponds to an animation effect of the PowerPoint file. If no displayed animation effect is available, calling this API will redirect you to the previous slide 
```JavaScript
void prevStep()
```

### nextStep
Goes to the next step 
```JavaScript
void nextStep()
```
#### Description
Each step corresponds to an animation effect of the PowerPoint file. If no animation effect that has not yet been displayed is available, calling this API will redirect you to the next slide 


### prevBoard
Goes to the previous page 
```JavaScript
void prevBoard(Boolean resetStep)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| resetStep | Boolean | [Optional] Whether to reset the PowerPoint animation steps after redirection to the specified slide |

#### Description
If the current whiteboard page is the first page of the current file, calling this API will not work 


### nextBoard
Goes to the next page 
```JavaScript
void nextBoard(Boolean resetStep)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| resetStep | Boolean | [Optional] Whether to reset the PowerPoint animation steps after redirection to the specified slide |

#### Description
If the current whiteboard page is the last page of the current file, calling this API will not work 


### gotoBoard
Redirects to the specified whiteboard page 
```JavaScript
void gotoBoard(String boardId, Boolean resetStep)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| boardId | String | [Required] ID of the whiteboard page to be redirected to |
| resetStep | Boolean | [Optional] Whether to reset the PowerPoint animation steps after redirection to the specified slide |

#### Description
This API is used to redirect to any whiteboard page in any file 


### getCurrentBoard
Obtains the ID of the current whiteboard page 
```JavaScript
String getCurrentBoard()
```
#### Response
ID of the current whiteboard page 


### getBoardList
Obtains the whiteboard list of all files 
```JavaScript
Array getBoardList()
```
#### Response
Whiteboard list of all files 


### setBoardRatio
Sets the aspect ratio of the current whiteboard page 
```JavaScript
void setBoardRatio(String ratio)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| ratio | String | [Required] Whiteboard aspect ratio to be set |

#### Description
The format of the value is similar to "4:3" and "16:9" 


### getBoardRatio
Obtains the aspect ratio of the current whiteboard page 
```JavaScript
String getBoardRatio()
```
#### Response
Whiteboard aspect ratio, in the same format as the setBoardRatio parameter 


### setBoardScale
Sets the scale of the current whiteboard page 
```JavaScript
void setBoardScale(Number scale)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| scale | Number | [Required] Whiteboard scale to be set |

#### Description
The value range is [100, 300], and the actual scale is scale/100 


### getBoardScale
Obtains the scale of the current whiteboard page 
```JavaScript
Number getBoardScale()
```
#### Response
Whiteboard scale, in the same format as the SetBoardScale parameter 


### setBoardContentFitMode
Sets the whiteboard content self-adaption mode 
```JavaScript
void setBoardContentFitMode(TEduBoardContentFitMode mode)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| mode | TEduBoardContentFitMode | [Required] Whiteboard content self-adaption mode to be set |

#### Description
Setting the self-adaption mode affects all subsequent whiteboard content operations and the AddTranscodeFile API 


### getBoardContentFitMode
Obtains the whiteboard content self-adaption mode 
```JavaScript
TEduBoardContentFitMode getBoardContentFitMode()
```
#### Response
Whiteboard content self-adaption mode 



## File Operation APIs

### applyFileTranscode
Initiates a file transcoding request 
```JavaScript
void applyFileTranscode(Object fileObj, TEduBoardTranscodeConfig config)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileObj | Object | [Required] File object for transcoding. For more information, see the Description section below |
| config | TEduBoardTranscodeConfig | [Required] Transcoding parameters |

#### Warning
This API is designed to enable users to quickly use the transcoding feature during access. Generally, we do not recommend that you use this API in production environments. We recommend that you initiate transcoding requests in production environments by using backend service APIs

#### Description
The format of the fileObj parameter is as follows: 
``` 
{
   data: document.getElementById('uploadFile').files[0], //fileObject object from the input label
   userData: 'xxx' //Passthrough data, which will be returned in the file transcoding progress callback
}
```

- This API can be used to transcode PowerPoint, PDF, and Word files
- By default, PowerPoint files are transcoded to H5 animations, and original PowerPoint animation effects can be restored. Other files are transcoded to static images
- The transcoding speed of PowerPoint animations is 1s/page, and the static transcoding speed of other files is 0.5s/page
- The transcoding progress and result will be returned through the onTEBFileTranscodeProgress callback. For more information, please refer to the callback documentation 


### getFileTranscodeProgress
Actively queries the file transcoding progress 
```JavaScript
void getFileTranscodeProgress(Object data)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| data | Object | [Required] File information. For more information, see the Description section below |

#### Warning
This API is used only in special business scenarios to actively query the file transcoding progress. After applyFileTranscode is called, the SDK will automatically trigger the TEB_TRANSCODEPROGRESS callback according to the schedule. Normally, you do not need to actively call this API

#### Description
The format of the data parameter is as follows: 
``` 
{
    taskId: "xxxxx" //taskId from the TEB_TRANSCODEPROGRESS callback
}
```
 The transcoding progress and result will be returned through the onTEBFileTranscodeProgress callback. For more information, please refer to the callback documentation 


### addTranscodeFile
Adds a file for transcoding 
```JavaScript
String addTranscodeFile(TEduBoardTranscodeFileResult result, bool needSwitch)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| result | TEduBoardTranscodeFileResult | File transcoding result |
| needSwitch | bool | Whether to immediately redirect to the added file for transcoding. Default value: true |

#### Response
File ID 

#### Warning
If the passed-in file URL is repeated, the file ID returned will be a null string 
Before the corresponding TEB_TRANSCODEPROGRESS callback is received, you cannot use the returned file ID to query file information

#### Description
The field information of TEduBoardTranscodeFileResult can be retrieved by:
1. Using the client ApplyFileTranscode for transcoding. The transcoding result will be used to call this API
2. Using the server RESTful API for transcoding. Only four fields of the transcoding result need to be passed in. The field relationships between the server and the client are: Title -> title, Resolution -> resolution, ResultUrl -> url, and Pages -> pages. For details, see [Transcoding Events](https://cloud.tencent.com/document/product/1137/40260) documentation


### addImagesFile
Imports image files to the whiteboard in batches 
```JavaScript
String addImagesFile(Array urls, bool needSwitch)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| urls | Array | List of UTF8-coded background image URLs to use. For example, ['https://www.xxx.com/xxxx.jpg', 'https://www.xxx.com/xxxx.jpg'] |
| needSwitch | bool | Whether to immediately redirect to the added file for transcoding. Default value: true |

#### Response
ID of the newly added file 


### deleteFile
Deletes a file 
```JavaScript
void deleteFile(String fileId)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | String | [Optional] ID of the file to be deleted |

>? If the file ID is null, it indicates the current file. The default file cannot be deleted 


### switchFile
Switches files. 
```JavaScript
void switchFile(String fileId, String boardId, Number stepIndex)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | String | [Required] ID of the file to be switched to |
| boardId | String | [Optional] Switch files and redirect to this whiteboard page |
| stepIndex | Number | [Optional] Redirect to the whiteboard page and switch to this animation |

#### Warning
This API can only be used for file switching. If the passed-in fileId is the current file ID, the SDK will ignore other parameters and not perform any operations 

>? The file ID is required. If it is null or a null string, file switching will fail 


### getCurrentFile
Obtains the current file ID. 
```JavaScript
String getCurrentFile()
```
#### Response
Current file ID 


### getFileInfo
Obtains the file information of the specified file on the whiteboard 
```JavaScript
TEduBoardFileInfo getFileInfo(String fileId)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | String | [Required] ID of the file whose information is to be obtained |

#### Response
File information 


### getFileInfoList
Obtains the file information list of all uploaded files on the whiteboard 
```JavaScript
Array getFileInfoList()
```
#### Response
File information list 


### getFileBoardList
Obtains the whiteboard ID list of the specified file 
```JavaScript
Array getFileBoardList(String fileId)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | String | [Required] File ID |

#### Response
Whiteboard ID list 


### getThumbnailImages
Obtains the thumbnail of the specified file, excluding the default file (fileId=#DEFAULT) 
```JavaScript
Array getThumbnailImages(String fileId)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | String | [Required] File ID |

#### Response
Thumbnail URL list 

>? When you call the RESTful API to request transcoding, the "thumbnail_resolution" parameter is required to enable the thumbnail feature. Otherwise, the returned thumbnail URL will be invalid 


### clearFileDraws
Clears all whiteboard doodles of the specified file 
```JavaScript
void clearFileDraws(String fileId)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | String | [Required] File ID |


### hasVideoPermission
Sets whether to authorize video file playback 
```JavaScript
boolean hasVideoPermission()
```
#### Response
Whether to authorize video file playback 

#### Warning
To play video files on a mobile phone, you must authorize the whiteboard to play video files before the whiteboard is initialized. Otherwise, video files cannot be played 


### applyVideoPermission
Authorizes video file playback 
```JavaScript
String applyVideoPermission()
```
#### Warning
To play video files on a mobile phone, you must authorize the whiteboard to play video files before the whiteboard is initialized. Otherwise, video files cannot be played 


### addVideoFile
Adds a video file 
```JavaScript
String addVideoFile(String url)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| url | String | [Required] File address |

#### Response
File ID 

#### Warning
The following js files are required: 
``` 
<script src="https://resources-tiw.qcloudtrtc.com/board/third/videojs/video.min.js"></script>
<link href="https://resources-tiw.qcloudtrtc.com/board/third/videojs/video-js.min.css" rel="stylesheet">
```


>? This API supports video files in mp4, m3u8, and hls formats and triggers the status change callback TEB_VIDEO_STATUS_CHANGED 


### addVODFile
Adds a video file (internal API) 
```JavaScript
String addVODFile(String appId, String vodId, String extParam)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| appId | String | VOD application ID |
| vodId | String | VOD file ID |
| extParam | String | Additional parameters of VOD videos, such as plugins and hlsConfig |

#### Response
Whiteboard file ID 

#### Warning
The following css or js files are required: 
``` 
<link href="https://imgcache.qq.com/open/qcloud/video/tcplayer/tcplayer.min.css" rel="stylesheet">
<script src="https://imgcache.qq.com/open/qcloud/video/tcplayer/libs/hls.min.0.12.4.js"></script>
<script src="https://imgcache.qq.com/open/qcloud/video/tcplayer/tcplayer.min.js"></script>
```


>? Only files from the Tencent Cloud VOD system are supported 


### setVODExtParam
Sets additional parameters of VOD videos, such as plugins and hlsConfig
```JavaScript
String setVODExtParam(String fileId, Object extParam)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | String | Whiteboard file ID |
| extParam | Object | Additional parameters of the VOD video |

#### Warning
Call this API after receiving the TEB_VODEXTPARAM callback 


### showVideoControl
Shows or hides the video control bar 
```JavaScript
void showVideoControl(bool show)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| show | bool | Whether to display the video control bar |

#### Warning
This is a global control item that applies to all video files. It specifies whether to show or hide the default video control bar. By default, the default video control bar is displayed. The UI style of the control bar varies by platforms 


### playVideo
Plays a video 
```JavaScript
void playVideo()
```
#### Warning
This API is valid only for the current file and will trigger the TEB_VIDEO_STATUS_CHANGED callback. It is usually called when a custom video control bar is used 


### pauseVideo
Pauses a video 
```JavaScript
void pauseVideo()
```
#### Warning
This API is valid only for the current file and will trigger the TEB_VIDEO_STATUS_CHANGED callback. It is usually called when a custom video control bar is used 


### seekVideo
Redirects to a specified time point in a video (only for VOD videos) 
```JavaScript
void seekVideo(float time)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| time | float | Playback progress in seconds |

#### Warning
This API is valid only for the current file and will trigger the TEB_VIDEO_STATUS_CHANGED callback. It is usually called when a custom video control bar is used 


### muteVideo
Mutes a video 
```JavaScript
void muteVideo(boolean muted)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| muted | boolean | Whether to mute the video |

#### Warning
This API is valid only for the current file. Muting does not affect the remote end. Due to user privacy policy restrictions, videos are played in mute mode in the WeChat and mobile browsers 


### setSyncVideoStatusEnable
Sets whether to sync local video operations to the remote end 
```JavaScript
void setSyncVideoStatusEnable(bool enable)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| enable | bool | [Required] Whether to sync |

#### Warning
This is a global control item that applies to all video files 

>? This API controls whether the triggering of the videoPlay, videoPause, and videoSeek APIs and the control bar events affects the remote end. The default value is true 


### startSyncVideoStatus
This is an internal start timer that syncs the video status to the remote end according to the schedule (only for mp4 files) 
```JavaScript
void startSyncVideoStatus(int interval)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| interval | int | [Optional] Synchronization interval |

#### Warning
This API is valid only for the current file 

>? This API is usually called after the video is loaded successfully on the teacher’s end. After file switching, the timer is automatically terminated 


### stopSyncVideoStatus
Stops syncing the video status 
```JavaScript
void stopSyncVideoStatus()
```
#### Warning
This API is valid only for the current file 


### addH5File
Adds an H5 file 
```JavaScript
String addH5File(String url)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| url | String | [Required] Webpage address |

#### Response
File ID 

#### Warning
Only display, and not interaction, is supported 


### addImageElement
Adds an image element 
```JavaScript
void addImageElement(String url)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| url | String | [Required] URL of the image element to be added, which is UTF8-coded |

#### Description
In addition to setting an online image as the image element, you can upload a local image as the image element. You can pass an Object into the url parameter in the following format: 
``` 
{
   data: document.getElementById('uploadFile').files[0], //fileObject object from the input label
   userData: 'xxx' //Passthrough data, which will be returned in the file upload progress callback
}
```



### setHandwritingEnable
Sets whether handwriting is enabled for the whiteboard 
```JavaScript
void setHandwritingEnable(Boolean enable)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| enable | BOOL | [Required] Whether handwriting is enabled. Valid values: true for yes, and false for no |

#### Description
After a whiteboard is created, handwriting is disabled for the whiteboard by default 


### isHandwritingEnable
Checks whether handwriting is enabled for the whiteboard 
```JavaScript
Boolean isHandwritingEnable()
```
#### Response
Whether handwriting is enabled 


### refresh
Refreshes the current whiteboard page and triggers the TEB_REFRESH callback 
```JavaScript
void refresh()
```
#### Warning
If the current whiteboard contains PowerPoint, HTML5, image, or video content, refreshing the whiteboard will trigger the corresponding callback 


### addAckData
Confirms whether data is sent successfully 
```JavaScript
void addAckData(Object data)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| data | Object | TEB_SYNCDATA callback data |


### syncAndReload
Syncs local data that failed to be sent to the remote end and refreshes the local data 
```JavaScript
Boolean syncAndReload()
```
#### Warning
Reload is to reload historical data, which will trigger all callbacks except those for onTEBInit during whiteboard initialization 

#### Description
Usage: this API is used after network recovery to synchronize local data to the remote end and fetch remote data to the local end. Call timing: the API is called after network recovery. Use limits: (1) This API only supports version 2.4.9 and later. (2) This API cannot be repeatedly called until the historical data is loaded successfully. Otherwise, the callback alarm TEDU_BOARD_WARNING_ILLEGAL_OPERATION will be triggered. (3) This API must be used with the addAckData API. After whiteboard data is successfully sent, please call the addAckData API to confirm 


### snapshot
Creates a whiteboard snapshot 
```JavaScript
void snapshot(TEduBoardSnapshotInfo param)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| param | TEduBoardSnapshotInfo | Snapshot parameters |
``` 
{
   //Call the API - userData passthrough data will be returned in the TEB_SNAPSHOT event callback
   teduBoard.snapshot({userData: '/snapshot/snapshot.png'});
   //Listen to events - The image field indicates a Base64 image, and the userdata field is the passthrough field
   teduBoard.on(TEduBoard.EVENT.TEB_SNAPSHOT, ({image, userData}) => {});
}
```


