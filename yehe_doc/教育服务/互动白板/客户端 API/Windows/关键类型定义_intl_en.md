
## TEduBoardToolType
Whiteboard tools 


| Enumerated Value | Description |
| --- | --- |
| TEDU_BOARD_TOOL_TYPE_MOUSE | Mouse |
| TEDU_BOARD_TOOL_TYPE_PEN | Pen |
| TEDU_BOARD_TOOL_TYPE_ERASER | Eraser |
| TEDU_BOARD_TOOL_TYPE_LASER | Laser pen |
| TEDU_BOARD_TOOL_TYPE_LINE | Line |
| TEDU_BOARD_TOOL_TYPE_OVAL | Hollow oval |
| TEDU_BOARD_TOOL_TYPE_RECT | Hollow rectangle |
| TEDU_BOARD_TOOL_TYPE_OVAL_SOLID | Solid oval |
| TEDU_BOARD_TOOL_TYPE_RECT_SOLID | Solid rectangle |
| TEDU_BOARD_TOOL_TYPE_POINT_SELECT | Point selection tool |
| TEDU_BOARD_TOOL_TYPE_RECT_SELECT | Rectangle selection tool |
| TEDU_BOARD_TOOL_TYPE_TEXT | Text tool |
| TEDU_BOARD_TOOL_TYPE_ZOOM_DRAG | Scaling and moving tool |



## TEduBoardElementType
Whiteboard element types 


| Enumerated Value | Description |
| --- | --- |
| TEDU_BOARD_ELEMENT_H5 | H5 element |



## TEduBoardImageFitMode
Alignment modes of whiteboard image filling 


| Enumerated Value | Description |
| --- | --- |
| TEDU_BOARD_IMAGE_FIT_MODE_CENTER | Center-aligned with the width or height as the reference and scaled up proportionally |
| TEDU_BOARD_IMAGE_FIT_MODE_LEFT | Left-aligned with the width or height as the reference and scaled up proportionally |
| TEDU_BOARD_IMAGE_FIT_MODE_TOP | Top-aligned with the width or height as the reference and scaled up proportionally |
| TEDU_BOARD_IMAGE_FIT_MODE_RIGHT | Right-aligned with the width or height as the reference and scaled up proportionally |
| TEDU_BOARD_IMAGE_FIT_MODE_BOTTOM | Bottom-aligned with the width or height as the reference and scaled up proportionally |


#### Description
When the image is zoomed in proportionally based on the width, the effect of left and right alignments are the same as that of central alignment. When the image is zoomed in proportionally based on the height, the effect of top and bottom alignments are the same as that of central alignment. 


## TEduBoardImageStatus
Whiteboard image statuses 


| Enumerated Value | Description |
| --- | --- |
| TEDU_BOARD_IMAGE_STATUS_LOADING | The background image is being loaded. |
| TEDU_BOARD_IMAGE_STATUS_LOAD_DONE | The background image has been loaded. |
| TEDU_BOARD_IMAGE_STATUS_LOAD_ABORT | The loading of the background image was aborted. |
| TEDU_BOARD_IMAGE_STATUS_LOAD_ERROR | An error occurred while loading the background image. |
| TEDU_BOARD_IMAGE_STATUS_LOAD_TIMEOUT | The loading of the background image timed out. |
| TEDU_BOARD_IMAGE_STATUS_LOAD_CANCEL | The loading of the background image was canceled. |
| TEDU_BOARD_IMAGE_STATUS_READ_ERROR | Failed to read the background image. |



## TEduBoardTextStyle
Whiteboard text styles 


| Enumerated Value | Description |
| --- | --- |
| TEDU_BOARD_TEXT_STYLE_NORMAL | Normal |
| TEDU_BOARD_TEXT_STYLE_BOLD | Bold |
| TEDU_BOARD_TEXT_STYLE_ITALIC | Italic |
| TEDU_BOARD_TEXT_STYLE_BOLD_ITALIC | Bold and italic |



## TEduBoardUploadStatus
Whiteboard upload statuses 


| Enumerated Value | Description |
| --- | --- |
| TEDU_BOARD_UPLOAD_STATUS_SUCCEED | Uploaded successfully |
| TEDU_BOARD_UPLOAD_STATUS_FAILED | Failed to upload |



## TEduBoardBackgroundH5Status
H5 background statuses 


| Enumerated Value | Description |
| --- | --- |
| TEDU_BOARD_BACKGROUND_H5_STATUS_LOADING | The H5 background is being loaded. |
| TEDU_BOARD_BACKGROUND_H5_STATUS_LOAD_FINISH | The H5 background has been loaded. |



## TEduBoardContentFitMode
Whiteboard content self-adaption modes 


| Enumerated Value | Description |
| --- | --- |
| TEDU_BOARD_CONTENT_FIT_MODE_NONE | Do not use content self-adaption. In this default mode, do not automatically adjust the whiteboard aspect ratio and scale the content proportionally in a center-aligned fashion. In addition, the content width and height are less than or equal to the whiteboard width and height respectively. |
| TEDU_BOARD_CONTENT_FIT_MODE_CENTER_INSIDE | Automatically adjust the whiteboard aspect ratio to be consistent with the content. Spread the content all over the whiteboard and scale the whiteboard proportionally in a center-aligned fashion. In addition, the whiteboard width and height are less than or equal to the container width and height respectively. |
| TEDU_BOARD_CONTENT_FIT_MODE_CENTER_COVER | Automatically adjust the whiteboard aspect ratio to be consistent with the content. Spread the content all over the whiteboard and scale the whiteboard proportionally in a center-aligned fashion. In addition, the whiteboard width and height are greater than or equal to the container width and height respectively. |


#### Description
The whiteboard content can be images, files, and PowerPoint animations. 


## TEduBoardLineType
Line types 


| Enumerated Value | Description |
| --- | --- |
| TEDU_BOARD_LINE_TYPE_SOLID | Solid line |
| TEDU_BOARD_LINE_TYPE_DOTTED | Dotted line |



## TEduBoardArrowType
Arrow type 


| Enumerated Value | Description |
| --- | --- |
| TEDU_BOARD_ARROW_TYPE_NONE | No arrow |
| TEDU_BOARD_ARROW_TYPE_NORMAL | Normal arrow |
| TEDU_BOARD_ARROW_TYPE_SOLID | Solid arrow |



## TEduBoardOvalDrawMode
Oval drawing modes 


| Enumerated Value | Description |
| --- | --- |
| TEDU_BOARD_OVAL_DRAW_MODE_FIX_START | Fixed start point. The midpoint between the start point and the end point is the circle center. |
| TEDU_BOARD_OVAL_DRAW_MODE_FIX_CENTER | Fixed circle center. The start point is the circle center. |



## TEduBoardFileTranscodeStatus
File transcoding statuses 


| Enumerated Value | Description |
| --- | --- |
| TEDU_BOARD_FILE_TRANSCODE_ERROR | Transcoding error |
| TEDU_BOARD_FILE_TRANSCODE_UPLOADING | Uploading |
| TEDU_BOARD_FILE_TRANSCODE_CREATED | Transcoding task initiated |
| TEDU_BOARD_FILE_TRANSCODE_QUEUED | Transcoding task pending |
| TEDU_BOARD_FILE_TRANSCODE_PROCESSING | Transcoding |
| TEDU_BOARD_FILE_TRANSCODE_FINISHED | Transcoding completed |



## TEduBoardH5FileStatus
H5 file statuses 


| Enumerated Value | Description |
| --- | --- |
| TEDU_BOARD_H5_FILE_STATUS_LOADING | Loading |
| TEDU_BOARD_H5_FILE_STATUS_LOADED | Loading completed |



## TEduBoardVideoStatus
Video file statuses 


| Enumerated Value | Description |
| --- | --- |
| TEDU_BOARD_VIDEO_STATUS_ERROR | Playback error |
| TEDU_BOARD_VIDEO_STATUS_LOADING | Loading |
| TEDU_BOARD_VIDEO_STATUS_LOADED | Loading completed |
| TEDU_BOARD_VIDEO_STATUS_PLAYED | Playback started |
| TEDU_BOARD_VIDEO_STATUS_TIMEUPDATE | Time updated |
| TEDU_BOARD_VIDEO_STATUS_PAUSED | Paused |
| TEDU_BOARD_VIDEO_STATUS_SEEKED | Seeking |
| TEDU_BOARD_VIDEO_STATUS_ENDED | Ended |



## TEduBoardKeyEventType
Keyboard event types 


| Enumerated Value | Description |
| --- | --- |
| TEDU_BOARD_KEYEVENT_RAWKEYDOWN | The status change process of a key that is pressed |
| TEDU_BOARD_KEYEVENT_KEYDOWN | A key is pressed. For different keyboard and language types, the key press will be mapped to different characters. Therefore, when you need to enter characters, use the TEDU_BOARD_KEYEVENT_CHAR event. |
| TEDU_BOARD_KEYEVENT_KEYUP | A key is released. |
| TEDU_BOARD_KEYEVENT_CHAR | A symbol is entered. For different keyboards, regions, and operating systems, the key press event will generate different characters. Therefore, use this event for text entry. |



## TEduBoardMouseButtonType
Mouse click types 


| Enumerated Value | Description |
| --- | --- |
| TEDU_BOARD_MOUSEBUTTON_LEFT | Left mouse button |
| TEDU_BOARD_MOUSEBUTTON_MIDDLE | Middle mouse button |
| TEDU_BOARD_MOUSEBUTTON_RIGHT | Right mouse button |



## TEduBoardTouchEventType
Touch event types 


| Enumerated Value | Description |
| --- | --- |
| TEDU_BOARD_TOUCHEVENT_RELEASED | Released |
| TEDU_BOARD_TOUCHEVENT_PRESSED | Pressed |
| TEDU_BOARD_TOUCHEVENT_MOVED | Moved |
| TEDU_BOARD_TOUCHEVENT_CANCELLED | Canceled |



## TEduBoardPointType
Point device types 


| Enumerated Value | Description |
| --- | --- |
| TEDU_BOARD_POINTER_TYPE_TOUCH | Touch |
| TEDU_BOARD_POINTER_TYPE_MOUSE | Mouse |
| TEDU_BOARD_POINTER_TYPE_PEN | Pen |
| TEDU_BOARD_POINTER_TYPE_ERASER | Eraser |
| TEDU_BOARD_POINTER_TYPE_UNKNOWN | Unknown |



## TEduBoardEventFlag
Event flags 


| Enumerated Value | Description |
| --- | --- |
| TEDU_BOARD_EVENTFLAG_NONE | No flag |
| TEDU_BOARD_EVENTFLAG_CAPS_LOCK_ON | Caps Lock is on. |
| TEDU_BOARD_EVENTFLAG_SHIFT_DOWN | The Shift key is pressed. |
| TEDU_BOARD_EVENTFLAG_CONTROL_DOWN | The Ctrl key is pressed. |
| TEDU_BOARD_EVENTFLAG_ALT_DOWN | The Alt key is pressed. |
| TEDU_BOARD_EVENTFLAG_LEFT_MOUSE_BUTTON | The left mouse button is pressed. |
| TEDU_BOARD_EVENTFLAG_MIDDLE_MOUSE_BUTTON | The middle mouse button is pressed. |
| TEDU_BOARD_EVENTFLAG_RIGHT_MOUSE_BUTTON | The right mouse button is pressed. |
| TEDU_BOARD_EVENTFLAG_COMMAND_DOWN | The MacOS command key is pressed. |
| TEDU_BOARD_EVENTFLAG_NUM_LOCK_ON | Number Lock is on. |
| TEDU_BOARD_EVENTFLAG_IS_KEY_PAD | - |
| TEDU_BOARD_EVENTFLAG_IS_LEFT | The left key modifier is pressed. |
| TEDU_BOARD_EVENTFLAG_IS_RIGHT | The right key modifier is pressed. |




## TEduBoardAuthParam
Whiteboard authorization parameters 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| sdkAppId | uint32_t | SDKAppID |
| userId | const char * | User ID |
| userSig | const char * | User signature |




## TEduBoardColor
Color parameters 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| red | uint8_t | Red component |
| green | uint8_t | Green component |
| blue | uint8_t | Blue component |
| alpha | uint8_t | Transparent component |




## TEduBoardInitParam
Whiteboard initialization parameters 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| progressEnable | bool | Whether or not to enable the loading icon, which is used during image loading and PowerPoint file loading. Default value: false |
| progressBarUrl | const char * | Custom loading icon. It is valid only when processEnable = true. Supported icon formats are jpg, gif, png, and svg. |
| ratio | const char * | Default whiteboard aspect ratio (whose format is similar to "4:3" and "16:9") |
| drawEnable | bool | Whether doodling is allowed or not |
| globalBackgroundColor | TEduBoardColor | Global background color |
| toolType | TEduBoardToolType | Whiteboard tool |
| brushColor | TEduBoardColor | Brush color |
| brushThin | uint32_t | Brush thickness |
| textColor | TEduBoardColor | Text color |
| textSize | uint32_t | Text size |
| textStyle | TEduBoardTextStyle | Text style |
| timSync | bool | Whether or not to use Tencent Cloud IMSDK for real-time data synchronization |
| dataSyncEnable | bool | Whether or not data synchronization is enabled. If no, no local whiteboard operations will be synced to the remote end. |
| preloadDepth | uint32_t | Image pre-loading depth. The default value is 5, which indicates that the previous and next 5 pages are pre-loaded. |
| smoothLevel | double | Handwriting smoothness coefficient. Default value: 0. Value range: [0, 1] |
| contentFitMode | TEduBoardContentFitMode | Content self-adaption mode |
| imageTimeout | uint32_t | Image loading timeout period in seconds. Default value: 10s |
| audioCallback | bool | Whether to enable the audio callback mode or not. If yes, audio will no longer be played on the whiteboard. Instead, PCM data will be thrown through the callback. |
| experimental | const char * | Experimental parameter set, which is a dictionary-type JSON string |




## TEduBoardLineStyle
Line styles 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| lineType | TEduBoardLineType | Line type |
| startArrowType | TEduBoardArrowType | Start arrow type |
| endArrowType | TEduBoardArrowType | End arrow type |




## TEduBoardCursorIcon
Cursor icon information 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| cursor | const char * | Built-in cursor icon of the browser. For more information on possible values, see the [reference document](https://developer.mozilla.org/zh-CN/docs/Web/CSS/cursor). When a custom image is used, enter "url" for this field. |
| url | const char * | URL of the custom cursor icon. For more information on the format restrictions, see the [reference document](https://developer.mozilla.org/zh-CN/docs/Web/CSS/cursor/url). The value of this field does not need to contain "url()". |
| offsetX | uint32_t | Horizontal offset of the custom cursor icon |
| offsetY | uint32_t | Vertical offset of the custom cursor icon |




## TEduBoardSnapshotInfo
Snapshot information 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| path | const char * | Local path for storing snapshots, which is UTF8-coded |




## TEduBoardTranscodeConfig
File transcoding parameters 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| minResolution | const char * | Minimum resolution of the transcoded file. It can be used to enhance the resolution of the transcoded file. The format of the value is similar to 960x540, where the width and height are separated by letter x. |
| isStaticPPT | bool | Whether or not to enable static transcoding for PowerPoint files (transcoding into static images). By default, PowerPoint files are transcoded into HTML5 animations, which takes a relatively long time. |
| thumbnailResolution | const char * | Resolution of the thumbnail generated for the file. By default, no thumbnail is generated (generating thumbnails will increase the amount of transcoding time). The format of the value is similar to 200x200, where the width and height are separated by letter x.. |




## TEduBoardTranscodeFileResult
File transcoding results 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| taskId | char | Task ID |
| status | TEduBoardFileTranscodeStatus | Transcoding status |
| progress | double | Transcoding progress. Value range: [0, 100] |
| title | char | File title |
| resolution | char | File resolution |
| pages | uint32_t | Total pages of the file |
| url | char | Transcoding result URL |
| thumbnailResolution | char | Resolution of the thumbnail generated for the file |
| thumbnailUrl | char | URL of the thumbnail generated for the file |




## TEduBoardInfo
Whiteboard information 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| boardId | const char * | Whiteboard ID |
| backgroundUrl | const char * | URL of the whiteboard background image or background H5 page |
| backgroundColor | TEduBoardColor | Whiteboard background color |




## TEduBoardInfoList
Whiteboard information list 




### GetCount
Obtains the whiteboard information count. 
``` C++
virtual uint32_t GetCount() const =0
```
#### Response
Whiteboard information count 


### GetBoardInfo
Obtains the specified whiteboard information. 
``` C++
virtual TEduBoardInfo GetBoardInfo(uint32_t index) const =0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| index | uint32_t | Index. Value range: [0, <Number of whiteboards>) |

#### Response
Whiteboard information 



## TEduBoardFileInfo
File information 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| fileId | const char * | File ID |
| title | const char * | File name |
| downloadUrl | const char * | File download address |
| pageIndex | uint32_t | Currently displayed page of the file |
| pageCount | uint32_t | Total pages of the file |
| boardInfoList | const TEduBoardInfoList * | Whiteboard information list |




## TEduBoardKeyEvent
Keyboard event 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| type | TEduBoardKeyEventType | Keyboard event type |
| modifiers | uint32_t | Bitwise status of keyboard modifiers. For more information on possible values, see TEduBoardEventFlag. |
| windowsKeyCode | int | Windows key code, which is used for DOM specifications. On Windows, it comes from system events. On other platforms, it is determined by mapping functions (see the reference document at [https://docs.microsoft.com/en-us/windows/win32/inputdev/virtual-key-codes](https://docs.microsoft.com/en-us/windows/win32/inputdev/virtual-key-codes)). |
| nativeKeyCode | int | Actual key code generated by the platform |
| isSystemKey | int | Whether the event is a "system key press" event or not. The value is valid only for Windows (see the reference document at [http://msdn.microsoft.com/en-us/library/ms646286(VS.85).aspx](http://msdn.microsoft.com/en-us/library/ms646286(VS.85).aspx)). |
| character | wchar_t | Character generated by the key press |
| unmodifiedCharacter | wchar_t | Character generated by the key press. The impact of key modifiers (except for Shift) is ignored. This value is used to trigger shortcut keys. |
| focusOnEditableField | int | When the key press event occurs in the text editing area, the value is 1. This value is used to determine whether to intercept the transmission of certain key press events. |




## TEduBoardMouseEvent
Mouse event 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| x | int | X-axis coordinate with the upper-left corner of the view as the origin |
| y | int | Y-axis coordinate with the upper-left corner of the view as the origin |
| modifiers | uint32_t | Bitwise status of keyboard modifiers. For more information on possible values, see TEduBoardEventFlag. |




## TEduBoardTouchEvent
Touch event 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| id | int | Touch point ID. This value can be any value other than -1. Note that a maximum of 16 touch points can be tracked simultaneously. When this limit is exceeded, excessive touch points will be ignored. |
| x | float | X-axis coordinate with the upper-left corner of the view as the origin |
| y | float | Y-axis coordinate with the upper-left corner of the view as the origin |
| radiusX | float | X-axis radius in pixels. If it is not applicable, pass in 0. |
| radiusY | float | Y-axis radius in pixels. If it is not applicable, pass in 0. |
| rotationAngle | float | Rotation angle in degree. If it is not applicable, pass in 0. |
| pressure | float | Normalized pressure value of the touch point. Value range: [0,1]. If it is not applicable, pass in 0. |
| type | TEduBoardTouchEventType | Touch point status. A touch begins with the TEDU_BOARD_TOUCHEVENT_PRESSED event, followed by 0 to N TEDU_BOARD_TOUCHEVENT_MOVED events, and ends with the TEDU_BOARD_TOUCHEVENT_RELEASED or TEDU_BOARD_TOUCHEVENT_CANNELLED event. Events that do not follow this rule will be ignored. |
| modifiers | uint32_t | Bitwise status of keyboard modifiers. For more information on possible values, see TEduBoardEventFlag. |
| pointerType | TEduBoardPointType | Type of the device that triggered the event |




## TEduBoardRect
Rectangle area 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| x | int32_t | X coordinate of the rectangle start position |
| y | int32_t | Y coordinate of the rectangle start position |
| width | int32_t | Rectangle width |
| height | int32_t | Rectangle height |


## TEduBoardFileInfoList
File information list 




### GetCount
Obtains the file information count. 
``` C++
virtual uint32_t GetCount() const =0
```
#### Response
File information count 


### GetFileInfo
Obtains the specified file information. 
``` C++
virtual TEduBoardFileInfo GetFileInfo(uint32_t index) const =0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| index | uint32_t | Index. Value range: [0, <Number of files>) |

#### Response
File information 


### Release
Releases the file information list. 
``` C++
virtual void Release()=0
```
#### Warning
After using the file information list, you must call this API to release the occupied memory space. 



## TEduBoardStringList
String list 




### GetCount
Obtains the number of strings. 
``` C++
virtual uint32_t GetCount() const =0
```
#### Response
Number of strings 


### GetString
Obtains the specified string. 
``` C++
virtual const char* GetString(uint32_t index) const =0
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| index | uint32_t | Index. Value range: [0, <Number of strings>) |

#### Response
String 

#### Warning
The SDK manages the memory for storing the return value, so you do not need to dump the memory on your own. 


### Release
Releases the string list. 
``` C++
virtual void Release()=0
```
#### Warning
After using the string list, you must call this API to release the occupied memory space. 



