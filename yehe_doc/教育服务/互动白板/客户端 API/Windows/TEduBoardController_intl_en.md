## Creating and Terminating Instances

### CreateTEduBoardController
Creates a whiteboard controller instance. 
``` C++
EDUSDK_API TEduBoardController* CreateTEduBoardController(bool disableCefInit=false, const char *cefRenderPath=nullptr)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| disableCefInit | bool | Whether the CEF framework initialization is disabled or not. Generally, you can use the default value |
| cefRenderPath | const char * | Path of the executable program of the custom Render process when the internal CEF initialization of the SDK is used, which is UTF8-coded. If the value is null or nullptr, the built-in Render process of the SDK is used |

#### Response
Whiteboard controller instance pointer 

#### Warning
This API must be called in the main thread. 

>? As the SDK is implemented based on the CEF framework (BSD-licensed), if your program is using the CEF framework, conflict may occur. To solve the conflict, implement the following solutions:
> 1. Choose one of the two following methods to enable your own Render process:
> - Set disableCefInit to false and set cefRenderPath to point to your own Render process
> - Set disableCefInit to true and initialize CEF yourself
> 2. Follow the instructions below to call RenderProcessHandler of the SDK in your Render process:
> - After the Render process is launched, call the API to obtain an sdkHandler instance: CefRefPtr<CefRenderProcessHandler> sdkHandler = (CefRenderProcessHandler*)GetTEduBoardRenderProcessHandler();
> - In CefApp in the Render process, rewrite the GetRenderProcessHandler method. The preceding sdkHandler is always returned
> - If you need a custom CefRenderProcessHandler, the custom Handler can be returned in step 2. Then, in the following methods of the custom Handler, call the corresponding methods of sdkHandler:
> 		- OnBrowserCreated
> 		- OnBrowserDestroyed
> 		- OnContextCreated 


### DestroyTEduBoardController
Terminates the whiteboard controller. 
``` C++
EDUSDK_API void DestroyTEduBoardController(TEduBoardController **ppBoardController)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| ppBoardController | TEduBoardController ** | Pointer to the whiteboard controller |

#### Description
The ppBoardController pointer is automatically set as null. 



## Logging APIs

### GetTEduBoardVersion
Obtains the SDK version number. 
``` C++
const EDUSDK_API char* GetTEduBoardVersion()
```
#### Response
SDK version number

#### Description
The SDK manages the memory for storing the return value, so you do not need to release the memory on your own. 


### SetTEduBoardLogFilePath
Sets the whiteboard log file path. 
``` C++
EDUSDK_API bool SetTEduBoardLogFilePath(const char *logFilePath)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| logFilePath | const char * | Path of the whiteboard log file to be set, including the file name and extension. This path is UTF8-coded. If it is null or nullptr, the default path is used |

#### Response
Whether the whiteboard log file path is set successfully or not 

#### Warning
You must call this API before CreateTEduBoardController is called for the first time. Otherwise, calling this API will fail.

#### Description

- Default path (Windows): "%AppData%/../Local/TEduBoard/teduboard.log"
- Default path (Linux): "~/TEduBoard/teduboard.log" 



## Advanced Feature APIs

### EnableTEduBoardOffscreenRender
Enables whiteboard off-screen rendering. 
``` C++
EDUSDK_API bool EnableTEduBoardOffscreenRender(uint32_t maxFps=30)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| maxFps | uint32_t | Maximum frame rate of off-screen rendering. Value range: [1, 60] |

#### Response
Whether off-screen rendering is enabled or not 

#### Warning
You must call this API before CreateTEduBoardController is called for the first time. Otherwise, calling this API will fail.

#### Description
When off-screen rendering is enabled, the SDK no longer creates a whiteboard view but throws the pixel data of the whiteboard off-screen rendering through the onTEBOffscreenPaint callback API. 


### GetTEduBoardRenderProcessHandler
Obtains the internal CefRenderProcessHandler of the SDK. 
``` C++
EDUSDK_API void* GetTEduBoardRenderProcessHandler()
```
#### Response
Internal CefRenderProcessHandler of the SDK 

#### Description
For more information on how to use this API, see the description of the CreateTEduBoardController API. 



## TEduBoardController
Whiteboard controller 

## Setting TEduBoardCallback

### AddCallback
Sets the event callback listener. 
``` C++
virtual void AddCallback(TEduBoardCallback *callback)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| callback | TEduBoardCallback * | Event callback listener |

#### Warning
We recommend that you call this method before running Init to resolve the error. 


### RemoveCallback
Deletes the event callback listener. 
``` C++
virtual void RemoveCallback(TEduBoardCallback *callback)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| callback | TEduBoardCallback * | Event callback listener |



## Basic Process APIs

### Init
Initializes the whiteboard. 
``` C++
virtual void Init(const TEduBoardAuthParam &authParam, uint32_t roomId, const TEduBoardInitParam &initParam=TEduBoardInitParam())=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| authParam | const TEduBoardAuthParam & | Authorization parameters |
| roomId | uint32_t | Classroom ID, which is a 32-bit integer. Value range: [1, 4294967294] |
| initParam | const TEduBoardInitParam & | An optional parameter, which specifies a series of attribute values for initializing the whiteboard |

#### Warning
When Tencent Cloud IMSDK is used for real-time data synchronization, only one whiteboard instance is supported. If multiple whiteboard instances are created, the doodle status may become abnormal.

#### Description
You can use initParam.timSync to specify whether Tencent Cloud IMSDK is used for real-time data synchronization. When initParam.timSync is set to True, the system tries to use Tencent Cloud IMSDK as the signaling channel to receive and send data in real time (in this case, only message receiving and sending are automatically implemented, and users must manually perform initialization, room entry, and other operations). Currently, only IMSDK 4.3.118 and later are supported. 


### GetBoardRenderView
Obtains the whiteboard rendering view. 
``` C++
virtual WINDOW_HANDLE GetBoardRenderView()=0
```
#### Response
Whiteboard rendering view 


### Refresh
Refreshes the current whiteboard page and triggers the onTEBRefresh callback. 
``` C++
virtual void Refresh()=0
```
#### Warning
If the current whiteboard contains PowerPoint, HTML5, image, or video content, refreshing the whiteboard will trigger the corresponding callback. 


### SyncAndReload
Syncs local data that failed to be sent to the remote end and refreshes the local data. 
``` C++
virtual void SyncAndReload()=0
```
#### Warning
Reload is to reload historical data, which will trigger all callbacks except those for onTEBInit during whiteboard initialization. 

#### Description
Usage: this API is used after network recovery to synchronize local data to the remote end and fetch remote data to the local end. Call timing: this API is called after network recovery. Use limits: this API cannot be repeatedly called until the historical data is loaded successfully. Otherwise, the callback alarm TEDU_BOARD_WARNING_ILLEGAL_OPERATION will be triggered. 


### AddSyncData
Adds whiteboard synchronization data. 
``` C++
virtual void AddSyncData(const char *data)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| data | const char * | Synchronization data from a member in the room |

#### Description
This API is used to sync data between whiteboard instances. When the built-in IM is used as the signaling channel, you do not need to call this API. 


### SetDataSyncEnable
Sets whether data synchronization is enabled for the whiteboard. 
``` C++
virtual void SetDataSyncEnable(bool enable)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| enable | bool | Whether data synchronization is enabled |

#### Description
After a whiteboard instance is created, data synchronization is enabled by default. If data synchronization is disabled, none of the local whiteboard operations will be synchronized to the remote end or to the server. 


### IsDataSyncEnable
Checks whether data synchronization is enabled for the whiteboard. 
``` C++
virtual bool IsDataSyncEnable()=0
```
#### Response
Whether data synchronization is enabled or not. Valid values: true for enabled, and false for disabled. 


### Reset
Resets the whiteboard. 
``` C++
virtual void Reset()=0
```
#### Description
After this API is called, all whiteboard pages and files will be deleted. 


### SetBoardRenderViewPos
Sets the position and size of the whiteboard rendering view. 
``` C++
virtual void SetBoardRenderViewPos(int32_t x, int32_t y, uint32_t width, uint32_t height)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| x | int32_t | X component of the position of the whiteboard rendering view to be set |
| y | int32_t | Y component of the position of the whiteboard rendering view to be set |
| width | uint32_t | Width of the whiteboard rendering view to be set |
| height | uint32_t | Height of the whiteboard rendering view to be set |

#### Description
When a parent window is available for the whiteboard rendering view, (x, y) indicates the position relative to the parent window. 


### GetSyncTime
Obtains the synchronization timestamp. 
``` C++
virtual uint64_t GetSyncTime()=0
```
#### Response
Synchronization timestamp in milliseconds 


### SyncRemoteTime
Syncs the remote timestamp. 
``` C++
virtual void SyncRemoteTime(const char *userId, uint64_t timestamp)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| userId | const char * | Remote user ID |
| timestamp | uint64_t | Synchronization timestamp for the remote user, in milliseconds |


### CallExperimentalAPI
Calls the whiteboard experimental API. 
``` C++
virtual const char* CallExperimentalAPI(const char *apiExp)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| apiExp | const char * | Whiteboard JS code to be executed |

#### Response
A string converted from the returned value after JS execution 



## APIs for Off-screen Rendering Input Events

### SendKeyEvent
Sends a keyboard event to the whiteboard. 
``` C++
virtual void SendKeyEvent(const TEduBoardKeyEvent &event)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| event | const TEduBoardKeyEvent & | Keyboard event to be sent |


### SendMouseClickEvent
Sends a mouse click event to the whiteboard. 
``` C++
virtual void SendMouseClickEvent(const TEduBoardMouseEvent &event, TEduBoardMouseButtonType type, bool mouseUp, int clickCount)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| event | const TEduBoardMouseEvent & | Mouse event to be sent |
| type | TEduBoardMouseButtonType | Mouse click type |
| mouseUp | bool | Whether the mouse button is released |
| clickCount | int | Number of clicks |


### SendMouseMoveEvent
Sends a mouse movement event to the whiteboard. 
``` C++
virtual void SendMouseMoveEvent(const TEduBoardMouseEvent &event, bool mouseLeave)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| event | const TEduBoardMouseEvent & | Mouse event to be sent |
| mouseLeave | bool | Whether the mouse cursor has been removed from the whiteboard or not |


### SendMouseWheelEvent
Sends a mouse wheel event to the whiteboard. 
``` C++
virtual void SendMouseWheelEvent(const TEduBoardMouseEvent &event, int deltaX, int deltaY)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| event | const TEduBoardMouseEvent & | Mouse event to be sent |
| deltaX | int | Wheel motion increment in the X direction |
| deltaY | int | Wheel motion increment in the Y direction |


### SendTouchEvent
Sends a touch event to the whiteboard. 
``` C++
virtual void SendTouchEvent(const TEduBoardTouchEvent &event)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| event | const TEduBoardTouchEvent & | Touch event to be sent |



## Doodle APIs

### SetDrawEnable
Sets whether the whiteboard allows doodling. 
``` C++
virtual void SetDrawEnable(bool enable)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| enable | bool | Whether doodling is allowed for the whiteboard. Valid values: true for yes, false for no |

#### Description
After a whiteboard instance is created, doodling is allowed for the whiteboard by default. 


### IsDrawEnable
Checks whether doodling is allowed for the whiteboard. 
``` C++
virtual bool IsDrawEnable()=0
```
#### Response
Whether doodling is allowed for the whiteboard or not. Valid values: true for yes, and false for no. 


### SetHandwritingEnable
Sets whether handwriting is enabled for the whiteboard. 
``` C++
virtual void SetHandwritingEnable(bool enable)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| enable | bool | Whether handwriting is enabled or not. Valid values: true for yes, and false for no |

#### Description
After a whiteboard is created, handwriting is disabled for the whiteboard by default. 


### IsHandwritingEnable
Checks whether handwriting is enabled for the whiteboard. 
``` C++
virtual bool IsHandwritingEnable()=0
```
#### Response
Whether handwriting is enabled or not 


### SetAccessibleUsers
Sets users whose drawings can be operated. 
``` C++
virtual void SetAccessibleUsers(const char **users, uint32_t userCount)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| users | const char ** | Users for which operations are allowed. The nullptr value indicates all users |
| userCount | uint32_t | Number of users contained in the users parameter |

#### Description
This API has the following effects:
1. The eraser tool can erase only the doodles drawn by the users specified by the users parameter, but cannot erase the doodles drawn by other users.
2. The point select and select tools can select only the doodles drawn by the users specified by the users parameter, but cannot select the doodles drawn by other users.
3. The clear API can clear only selected doodles and the doodles drawn by the users specified by the users parameter. It cannot clear backgrounds or the doodles drawn by other users.
4. This API has no impact on the other features of the whiteboard that are not listed here. 


### SetGlobalBackgroundColor
Sets the background color of all whiteboards. 
``` C++
virtual void SetGlobalBackgroundColor(const TEduBoardColor &color)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| color | const TEduBoardColor & | Global background color to be set |

#### Description
When this API is called, the background color of all whiteboards will be changed, and the default background color of the newly created whiteboards will be the global background color. 


### GetGlobalBackgroundColor
Obtains the global background color of the whiteboards. 
``` C++
virtual TEduBoardColor GetGlobalBackgroundColor()=0
```
#### Response
Global background color 


### SetBackgroundColor
Sets the background color of the current whiteboard page. 
``` C++
virtual void SetBackgroundColor(const TEduBoardColor &color)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| color | const TEduBoardColor & | Background color to be set |

#### Description
After a whiteboard page is created, the default background color is set by the SetDefaultBackgroundColor API. 


### GetBackgroundColor
Obtains the background color of the current whiteboard page. 
``` C++
virtual TEduBoardColor GetBackgroundColor()=0
```
#### Response
Background color of the current whiteboard page 


### SetToolType
Sets the whiteboard tool to be used. 
``` C++
virtual void SetToolType(TEduBoardToolType type)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| type | TEduBoardToolType | Whiteboard tool to be set |


### GetToolType
Obtains the whiteboard tool in use. 
``` C++
virtual TEduBoardToolType GetToolType()=0
```
#### Response
Whiteboard tool in use 


### SetCursorIcon
Sets the cursor icon for the whiteboard tool. 
``` C++
virtual void SetCursorIcon(TEduBoardToolType type, const TEduBoardCursorIcon &icon)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| type | TEduBoardToolType | Whiteboard tool type for which the cursor icon is to be set |
| icon | const TEduBoardCursorIcon & | Cursor icon to be set |


### SetBrushColor
Sets the brush color. 
``` C++
virtual void SetBrushColor(const TEduBoardColor &color)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| color | const TEduBoardColor & | Brush color to be set |

#### Description
The brush color applies to all doodles. 


### GetBrushColor
Obtains the brush color. 
``` C++
virtual TEduBoardColor GetBrushColor()=0
```
#### Response
Brush color 


### SetBrushThin
Sets the brush thickness. 
``` C++
virtual void SetBrushThin(uint32_t thin)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| thin | uint32_t | Brush thickness to be set |

#### Description
The brush thickness applies to all doodles. If the actual pixel value (thin * whiteboard height/10000) px is less than 1 px, the doodle line will be almost invisible. 


### GetBrushThin
Obtains the brush thickness. 
``` C++
virtual uint32_t GetBrushThin()=0
```
#### Response
Brush thickness 


### SetTextColor
Sets the text color. 
``` C++
virtual void SetTextColor(const TEduBoardColor &color)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| color | const TEduBoardColor & | Text color to be set |


### GetTextColor
Obtains the text color. 
``` C++
virtual TEduBoardColor GetTextColor()=0
```
#### Response
Text color 


### SetTextSize
Sets the text size. 
``` C++
virtual void SetTextSize(uint32_t size)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| size | uint32_t | Text size to be set |

#### Description
This API defines the actual pixel value; that is, (size * whiteboard height/10000) px. 


### GetTextSize
Obtains the text size. 
``` C++
virtual uint32_t GetTextSize()=0
```
#### Response
Text size 


### SetTextStyle
Sets the text style. 
``` C++
virtual void SetTextStyle(TEduBoardTextStyle style)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| style | TEduBoardTextStyle | Text style to be set |


### GetTextStyle
Obtains the text style. 
``` C++
virtual TEduBoardTextStyle GetTextStyle()=0
```
#### Response
Text style 


### SetLineStyle
Sets the line style. 
``` C++
virtual void SetLineStyle(const TEduBoardLineStyle &style)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| style | const TEduBoardLineStyle & | Line style to be set |


### GetLineStyle
Obtains the line style. 
``` C++
virtual TEduBoardLineStyle GetLineStyle()=0
```
#### Response
Line styles 


### SetOvalDrawMode
Sets the oval drawing mode. 
``` C++
virtual void SetOvalDrawMode(TEduBoardOvalDrawMode drawMode)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| drawMode | TEduBoardOvalDrawMode | Oval drawing mode to be set |


### GetOvalDrawMode
Obtains the oval drawing mode. 
``` C++
virtual TEduBoardOvalDrawMode GetOvalDrawMode()=0
```
#### Response
Oval drawing modes 


### Clear
Clears the doodles on the current whiteboard page. 
``` C++
virtual void Clear(bool clearBackground=false, bool clearSelectedOnly=false)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| clearBackground | bool | Whether or not to clear the background color and the background image simultaneously |
| clearSelectedOnly | bool | Whether or not to clear the selected doodle only |

#### Warning
Currently, you cannot clear the background image while clearing the selected doodle. 


### SetBackgroundImage
Sets the background image of the current whiteboard page. 
``` C++
virtual void SetBackgroundImage(const char *url, TEduBoardImageFitMode mode)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| url | const char * | URL of the background image to be set, which is UTF8-coded |
| mode | TEduBoardImageFitMode | Image padding and alignment modes to be used |

#### Description
When the URL is a valid local file address, the file will be automatically uploaded to COS. 


### SetBackgroundH5
Sets the background H5 page of the current whiteboard page. 
``` C++
virtual void SetBackgroundH5(const char *url)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| url | const char * | URL of the background H5 page to be set |

#### Description
This API and the SetBackgroundImage API are mutually exclusive. 


### Undo
Undoes the last action on the current whiteboard page. 
``` C++
virtual void Undo()=0
```

### Redo
Redoes the last undone action on the current whiteboard page. 
``` C++
virtual void Redo()=0
```


## Whiteboard Page Operation APIs

### AddBoard
Adds a whiteboard page. 
``` C++
virtual const char* AddBoard(const char *url=nullptr)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| url | const char * | URL of the background image to be used, which is UTF8-coded. The nullptr value indicates that no background image is specified |

#### Response
Whiteboard ID 

#### Warning
Whiteboard pages will be added to the default file (with the file ID ::DEFAULT). Whiteboard pages cannot be added for user-uploaded files.

#### Description
The SDK manages the memory for storing the return value, so you do not need to release the memory on your own. 


### AddImageElement
Adds image resources. 
``` C++
virtual void AddImageElement(const char *url)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| url | const char * | URL of the image element to be added, which is UTF8-coded |


### AddElement
Adds whiteboard elements. 
``` C++
virtual const char* AddElement(TEduBoardElementType type, const char *url)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| type | TEduBoardElementType | Whiteboard element type |
| url | const char * | URL of the element to be used, which is UTF8-coded. The nullptr value indicates that no URL is specified |

#### Response
Element ID for subsequent deletion operations

#### Description
Elements added to the whiteboard float over the whiteboard background and can be dragged, scaled, and deleted. 


### RemoveElement
Deletes whiteboard elements. 
``` C++
virtual bool RemoveElement(const char *elementId)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| elementId | const char * | Element ID |

#### Response
Whether the element is deleted or not 


### DeleteBoard
Deletes a whiteboard page. 
``` C++
virtual void DeleteBoard(const char *boardId=nullptr)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| boardId | const char * | ID of the whiteboard to be deleted. The nullptr value indicates the current page |

#### Warning
Only whiteboard pages in the default file (with file ID ::DEFAULT) can be deleted. The default whiteboard page (with whiteboard ID ::DEFAULT) cannot be deleted. 


### PrevStep
Goes to the previous step. Each step corresponds to an animation effect of the PowerPoint file. If no displayed animation effect is available, calling this API will redirect you to the previous slide. 
``` C++
virtual void PrevStep()=0
```

### NextStep
Goes to the next step. 
``` C++
virtual void NextStep()=0
```
#### Description
Each step corresponds to an animation effect of the PowerPoint file. If no animation effect that has not yet been displayed is available, calling this API will redirect you to the next slide. 


### PrevBoard
Goes to the previous page. 
``` C++
virtual void PrevBoard(bool resetStep=false)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| resetStep | bool | Whether or not to reset the PowerPoint animation steps after redirecting to the specified slide |

#### Description
If the current whiteboard page is the first page of the current file, calling this API will not work. 


### NextBoard
Goes to the next page. 
``` C++
virtual void NextBoard(bool resetStep=false)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| resetStep | bool | Whether or not to reset the PowerPoint animation steps after redirecting to the specified slide |

#### Description
If the current whiteboard page is the last page of the current file, calling this API will not work. 


### GotoBoard
Redirects to the specified whiteboard page. 
``` C++
virtual void GotoBoard(const char *boardId, bool resetStep=false)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| boardId | const char * | ID of the whiteboard page to be redirected to |
| resetStep | bool | Whether or not to reset the PowerPoint animation steps after redirecting to the specified slide |

#### Description
This API is used to redirect to any whiteboard page in any file. 


### GetCurrentBoard
Obtains the ID of the current whiteboard page. 
``` C++
virtual const char* GetCurrentBoard()=0
```
#### Response
ID of the current whiteboard page

#### Description
The SDK manages the memory for storing the return value, so you do not need to release the memory on your own. 


### GetBoardList
Obtains the whiteboard list of all files. 
``` C++
virtual TEduBoardStringList* GetBoardList()=0
```
#### Response
Whiteboard list of all files 

#### Warning
If you no longer need the return value, you do not have to delete it yourself. However, you must call its release method to release the occupied memory space. 


### SetBoardRatio
Sets the aspect ratio of the current whiteboard page. 
``` C++
virtual void SetBoardRatio(const char *ratio)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| ratio | const char * | Whiteboard aspect ratio to be set |

#### Description
The format of the value is similar to "4:3" and "16:9". 


### GetBoardRatio
Obtains the aspect ratio of the current whiteboard page. 
``` C++
virtual const char* GetBoardRatio()=0
```
#### Response
Whiteboard aspect ratio, in the same format as the setBoardRatio parameter 


### SetBoardScale
Sets the scale of the current whiteboard page. 
``` C++
virtual void SetBoardScale(uint32_t scale)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| scale | uint32_t | Whiteboard scale to be set |

#### Description
The value range is [100, 300], and the actual scale is scale/100. 


### GetBoardScale
Obtains the scale of the current whiteboard page. 
``` C++
virtual uint32_t GetBoardScale()=0
```
#### Response
Whiteboard scale, in the same format as the SetBoardScale parameter 


### SetBoardContentFitMode
Sets the whiteboard content self-adaption mode. 
``` C++
virtual void SetBoardContentFitMode(TEduBoardContentFitMode mode)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| mode | TEduBoardContentFitMode | Whiteboard content self-adaption mode to be set |

#### Description
Setting the self-adaption mode affects all subsequent whiteboard content operations and the AddTranscodeFile API. 


### GetBoardContentFitMode
Obtains the whiteboard content self-adaption mode. 
``` C++
virtual TEduBoardContentFitMode GetBoardContentFitMode()=0
```
#### Response
Whiteboard content self-adaption modes 


### Snapshot
Creates a whiteboard snapshot. 
``` C++
virtual void Snapshot(const TEduBoardSnapshotInfo &info)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| info | const TEduBoardSnapshotInfo & | Snapshot information |



## File Operation APIs

### ApplyFileTranscode
Initiates a file transcoding request. 
``` C++
virtual void ApplyFileTranscode(const char *path, const TEduBoardTranscodeConfig &config=TEduBoardTranscodeConfig())=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| path | const char * | Path of the file to be transcoded, which is UTF8-coded |
| config | const TEduBoardTranscodeConfig & | Transcoding parameters |

#### Warning
This API is designed to enable users to quickly use the transcoding feature in the access stage. Generally, we do not recommend that you use this API in production environments. We recommend that you initiate transcoding requests in production environments by using backend service APIs. 

#### Description
Transcoding is supported for PowerPoint, PDF, and Word files. PowerPoint files are transcoded into HTML5 animations by default, and original animation effects of the PowerPoint file can be restored. Other files are transcoded into static images. The PowerPoint animation transcoding rate is about 1 sec/slide, whereas the transcoding rate of any files into static images is about 0.5 sec/page. The transcoding progress and result will be returned through the onTEBFileTranscodeProgress callback. For more information, please refer to the callback documentation. 


### GetFileTranscodeProgress
Actively queries the file transcoding progress. 
``` C++
virtual void GetFileTranscodeProgress(const char *taskId)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| taskId | const char * | Transcoding task ID obtained from the onTEBFileTranscodeProgress callback |

#### Warning
This API is used only in special business scenarios to actively query the file transcoding progress. After ApplyFileTranscode is called, the SDK will automatically trigger the onTEBFileTranscodeProgress callback according to the schedule. Normally, you do not need to actively call this API. 

#### Description
The transcoding progress and result will be returned through the onTEBFileTranscodeProgress callback. For more information, please refer to the callback documentation. 


### AddTranscodeFile
Adds a file for transcoding. 
``` C++
virtual const char* AddTranscodeFile(const TEduBoardTranscodeFileResult &result)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| result | const TEduBoardTranscodeFileResult & | File transcoding result |

#### Response
File ID 

#### Warning
If the passed-in file URL is repeated, the file ID returned will be a null string. 
Before the corresponding onTEBAddTranscodeFile callback is received, you cannot use the returned file ID to query file information. 

#### Description
The field information of TEduBoardTranscodeFileResult can be retrieved by:
1. Using the client ApplyFileTranscode for transcoding. The transcoding result will be used to call this API
2. (Recommended) Using the server RESTful API for transcoding. Only four fields of the transcoding result (title, resolution, url, and pages) need to be passed in. The field relationships between the server and the client are: Title -> title, Resolution -> resolution, ResultUrl -> url, and Pages -> pages. For details, see [Document Transcoding Events](https://cloud.tencent.com/document/product/1137/40260).


### AddImagesFile
Adds image files. 
``` C++
virtual const char* AddImagesFile(const char **urls, uint32_t urlCount)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| urls | const char ** | List of image URLs to be used. These URLs are UTF8-coded. The nullptr value is not allowed |
| urlCount | uint32_t | Number of image URLs |

#### Response
File ID 

#### Warning
If the passed-in file URL is repeated, the file ID returned will be a null string. 
Before the onTEBAddImagesFile callback is received, you cannot use the returned file ID to query file information. 

#### Description
After the file is loaded successfully, the system automatically switches to the file. 


### AddVideoFile
Adds a video file. 
``` C++
virtual const char* AddVideoFile(const char *url)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| url | const char * | File playback address |

#### Response
File ID

#### Description
Mobile clients support mp4 and m3u8 files, and the desktop client supports mp4, m3u8, flv, and rtmp files. This API triggers the status change callback onTEBVideoStatusChange. 


### ShowVideoControl
Shows or hides the video control bar. 
``` C++
virtual void ShowVideoControl(bool show)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| show | bool | Whether the video control bar is displayed or not |

#### Warning
This is a global control item that applies to all video files. It specifies whether to show or hide the default video control bar. By default, the default video control bar is displayed. The UI style of the control bar varies on different platforms. 


### PlayVideo
Plays a video. 
``` C++
virtual void PlayVideo()=0
```
#### Warning
This API is valid only for the current file.

#### Description
This API triggers the status change callback onTEBVideoStatusChange. It is usually used when a custom video control bar is used. 


### PauseVideo
Pauses a video. 
``` C++
virtual void PauseVideo()=0
```
#### Warning
This API is valid only for the current file.

#### Description
This API triggers the status change callback onTEBVideoStatusChange. It is usually used when a custom video control bar is used. 


### SeekVideo
Jumps to a specified time point in a video (only for VOD videos). 
``` C++
virtual void SeekVideo(double time)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| time | double | Playback progress in seconds |

#### Warning
This API is valid only for the current file.

#### Description
This API triggers the status change callback onTEBVideoStatusChange. It is usually used when a custom video control bar is used. 


### SetSyncVideoStatusEnable
Sets whether local video operations are synchronized to the remote end. 
``` C++
virtual void SetSyncVideoStatusEnable(bool enable)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| enable | bool | Whether to enable synchronization or not |

#### Warning
This is a global control item that applies to all video files.

#### Description
This API specifies whether the triggering of the play/pause/seek API and the control bar events affects the remote end. The default value is true. Usually, it is set to false for students and true for teachers. 


### StartSyncVideoStatus
This is an internal start timer that syncs the video status to the remote end according to the schedule (only for mp4 files). 
``` C++
virtual void StartSyncVideoStatus(uint32_t interval)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| interval | uint32_t | Synchronization interval. For example, 5 seconds |

#### Warning
This API is valid only for the current file.

#### Description
This API is usually called after the video is loaded successfully on the teacher’s end. After file switching, the timer is automatically terminated. 


### StopSyncVideoStatus
Stops syncing the video status. 
``` C++
virtual void StopSyncVideoStatus()=0
```
#### Warning
This API is valid only for the current file. 


### AddH5File
Adds an H5 file. 
``` C++
virtual const char* AddH5File(const char *url)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| url | const char * | Webpage address |

#### Response
File ID 

>? Only display, and not interaction, is supported. 


### DeleteFile
Deletes a file. 
``` C++
virtual void DeleteFile(const char *fileId)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | const char * | ID of the file to be deleted |

#### Description
When the file ID is nullptr, it indicates the current file. The default file cannot be deleted. 


### SwitchFile
Switches to another file. 
``` C++
virtual void SwitchFile(const char *fileId, const char *boardId=nullptr, int32_t stepIndex=-1)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | const char * | ID of the file to be switched to |
| boardId | const char * | Switch files and redirect to this whiteboard page |
| stepIndex | int32_t | Redirect to the whiteboard page and switch to this animation |

#### Warning
This API can only be used for file switching. If the passed-in fileId is the current file ID, the SDK will ignore other parameters and will not perform any operations. 

>? The file ID is required. If it is nullptr or a null string, file switching will fail. 


### GetCurrentFile
Obtains the current file ID. 
``` C++
virtual const char* GetCurrentFile()=0
```
#### Response
Current file ID 


### GetFileInfo
Obtains the file information of the specified file on the whiteboard. 
``` C++
virtual TEduBoardFileInfo GetFileInfo(const char *fileId)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | const char * | - |

#### Response
File information 

#### Warning
Each time this API is called, the returned value is stored in the same memory. To save the returned information, copy it once it is returned. 


### GetFileInfoList
Obtains the file information list of all uploaded files on the whiteboard. 
``` C++
virtual TEduBoardFileInfoList* GetFileInfoList()=0
```
#### Response
File information list 

#### Warning
If you no longer need the return value, you do not have to delete it yourself. However, you must call its release method to release the occupied memory space. 


### GetFileBoardList
Obtains the whiteboard ID list of the specified file. 
``` C++
virtual TEduBoardStringList* GetFileBoardList(const char *fileId)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | const char * | File ID |

#### Response
Whiteboard ID list 

#### Warning
If you no longer need the return value, you do not have to delete it yourself. However, you must call its release method to release the occupied memory space. 


### GetThumbnailImages
Obtains the thumbnail of the specified file, excluding the default file (fileId=#DEFAULT). 
``` C++
virtual TEduBoardStringList* GetThumbnailImages(const char *fileId)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | const char * | File ID |

#### Response
Thumbnail URL list 

>? When you call the RESTful API to request transcoding, the "thumbnail_resolution" parameter is required to enable the thumbnail feature. Otherwise, the returned thumbnail URL will be invalid. 


### ClearFileDraws
Clears all the whiteboard doodles of the specified file. 
``` C++
virtual void ClearFileDraws(const char *fileId)=0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | const char * | File ID |





