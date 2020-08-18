## TEduBoardToolType
Whiteboard tools 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| TEDU_BOARD_TOOL_TYPE_MOUSE | int | Mouse |
| TEDU_BOARD_TOOL_TYPE_PEN | int | Pen |
| TEDU_BOARD_TOOL_TYPE_ERASER | int | Eraser |
| TEDU_BOARD_TOOL_TYPE_LASER | int | Laser pointer |
| TEDU_BOARD_TOOL_TYPE_LINE | int | Line |
| TEDU_BOARD_TOOL_TYPE_OVAL | int | Hollow oval |
| TEDU_BOARD_TOOL_TYPE_RECT | int | Hollow rectangle |
| TEDU_BOARD_TOOL_TYPE_OVAL_SOLID | int | Solid oval |
| TEDU_BOARD_TOOL_TYPE_RECT_SOLID | int | Solid rectangle |
| TEDU_BOARD_TOOL_TYPE_POINT_SELECT | int | Point selection tool |
| TEDU_BOARD_TOOL_TYPE_RECT_SELECT | int | Rectangle selection tool |
| TEDU_BOARD_TOOL_TYPE_TEXT | int | Text tool |
| TEDU_BOARD_TOOL_TYPE_ZOOM_DRAG | int | Whiteboard scaling and moving tool |


## TEduBoardLineType
Line types 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| TEDU_BOARD_LINE_TYPE_SOLID | int | Solid line |
| TEDU_BOARD_LINE_TYPE_DOTTED | int | Dotted line |


## TEduBoardArrowType
Arrow types 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| TEDU_BOARD_ARROW_TYPE_NONE | int | No arrow |
| TEDU_BOARD_ARROW_TYPE_NORMAL | int | Normal arrow |
| TEDU_BOARD_ARROW_TYPE_SOLID | int | Solid arrow |


## TEduBoardOvalDrawMode
Oval drawing modes 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| TEDU_BOARD_OVAL_DRAW_MODE_FIX_START | int | Fixed start point. The midpoint between the start point and the end point is the circle center |
| TEDU_BOARD_OVAL_DRAW_MODE_FIX_CENTER | int | Fixed circle center. The start point is the circle center |


## TEduBoardImageFitMode
Alignment modes of the whiteboard image filling 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| TEDU_BOARD_IMAGE_FIT_MODE_CENTER | int | Center-aligned with the width or height as the reference and scaled up proportionally |
| TEDU_BOARD_IMAGE_FIT_MODE_LEFT | int | Left-aligned with the width or height as the reference and scaled up proportionally |
| TEDU_BOARD_IMAGE_FIT_MODE_TOP | int | Top-aligned with the width or height as the reference and scaled up proportionally |
| TEDU_BOARD_IMAGE_FIT_MODE_RIGHT | int | Right-aligned with the width or height as the reference and scaled up proportionally |
| TEDU_BOARD_IMAGE_FIT_MODE_BOTTOM | int | Bottom-aligned with the width or height as the reference and scaled up proportionally |


## TEduBoardImageStatus
Whiteboard image statuses 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| TEDU_BOARD_IMAGE_STATUS_LOADING | int | The background image is being loaded |
| TEDU_BOARD_IMAGE_STATUS_LOAD_DONE | int | The background image has been loaded |
| TEDU_BOARD_IMAGE_STATUS_LOAD_ABORT | int | The loading of the background image was interrupted |
| TEDU_BOARD_IMAGE_STATUS_LOAD_ERROR | int | An error occurred when loading the background image |
| TEDU_BOARD_IMAGE_STATUS_LOAD_TIMEOUT | int | The loading of the background image timed out |
| TEDU_BOARD_IMAGE_STATUS_LOAD_CANCEL | int | The loading of the background image was canceled |
| TEDU_BOARD_IMAGE_STATUS_READ_ERROR | int | An error occurred when loading the local image |


## TEduBoardTextStyle
Whiteboard text styles 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| TEDU_BOARD_TEXT_STYLE_NORMAL | int | Normal |
| TEDU_BOARD_TEXT_STYLE_BOLD | int | Bold |
| TEDU_BOARD_TEXT_STYLE_ITALIC | int | Italic |
| TEDU_BOARD_TEXT_STYLE_BOLD_ITALIC | int | Bold and italic |


## TEduBoardUploadStatus
Whiteboard upload statuses 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| TEDU_BOARD_UPLOAD_STATUS_SUCCEED | int | Uploaded successfully |
| TEDU_BOARD_UPLOAD_STATUS_FAILED | int | Failed to upload |


## TEduBoardBackgroundH5Status
H5 background statuses 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| TEDU_BOARD_BACKGROUND_H5_STATUS_LOADING | int | H5 background is being loaded |
| TEDU_BOARD_BACKGROUND_H5_STATUS_LOAD_FINISH | int | H5 background has been loaded |


## TEduBoardContentFitMode
Whiteboard content self-adaption modes 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| TEDU_BOARD_CONTENT_FIT_MODE_NONE | int | Do not use content self-adaption. In this default mode, do not automatically adjust the whiteboard aspect ratio and scale the content proportionally in a center-aligned fashion. In addition, the content width and height are less than or equal to the whiteboard width and height respectively |
| TEDU_BOARD_CONTENT_FIT_MODE_CENTER_INSIDE | int | Automatically adjust the whiteboard aspect ratio to be consistent with the content. Spread the content all over the whiteboard and scale the whiteboard proportionally in a center-aligned fashion. In addition, the whiteboard width and height are less than or equal to the container width and height respectively |
| TEDU_BOARD_CONTENT_FIT_MODE_CENTER_COVER | int | Automatically adjust the whiteboard aspect ratio to be consistent with the content. Spread the content all over the whiteboard and scale the whiteboard proportionally in a center-aligned fashion. In addition, the whiteboard width and height are greater than or equal to the container width and height respectively |


## TEduBoardFileTranscodeStatus
File transcoding statuses 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| TEDU_BOARD_FILE_TRANSCODE_ERROR | int | Transcoding error |
| TEDU_BOARD_FILE_TRANSCODE_UPLOADING | int | File uploading |
| TEDU_BOARD_FILE_TRANSCODE_CREATED | int | Transcoding task initiated |
| TEDU_BOARD_FILE_TRANSCODE_QUEUE | int | Transcoding task pending |
| TEDU_BOARD_FILE_TRANSCODE_PROCESSING | int | Transcoding |
| TEDU_BOARD_FILE_TRANSCODE_FINISHED | int | Transcoding completed |


## TEduBoardVideoStatus
Video file statuses 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| TEDU_BOARD_VIDEO_STATUS_ERROR | int | Playback error |
| TEDU_BOARD_VIDEO_STATUS_LOADING | int | Loading |
| TEDU_BOARD_VIDEO_STATUS_LOADED | int | Loading completed |
| TEDU_BOARD_VIDEO_STATUS_PLAYED | int | Playback started |
| TEDU_BOARD_VIDEO_STATUS_TIMEUPDATE | int | Time status updated |
| TEDU_BOARD_VIDEO_STATUS_PAUSED | int | Paused |
| TEDU_BOARD_VIDEO_STATUS_SEEKED | int | Seeking |
| TEDU_BOARD_VIDEO_STATUS_ENDED | int | Ended |


## TEduBoardH5FileStatus
H5 file statuses 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| TEDU_BOARD_H5_FILE_STATUS_LOADING | int | Loading |
| TEDU_BOARD_H5_FILE_STATUS_LOADED | int | Loading completed |


## TEduBoardAuthParam
Authorization parameters 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| sdkAppId | int | SDKAppID |
| userId | String | User ID |
| userSig | String | User signature |




## TEduBoardColor
Color parameters 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| red | int | Red component |
| green | int | Green component |
| blue | int | Blue component |
| alpha | int | Transparent component |



### TEduBoardColor
Initializes the color value 
``` Java
TEduBoardColor(int color)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| color | int | - |


### TEduBoardColor
Initializes the color value 
``` Java
TEduBoardColor(final String color)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| color | final String | Color value string, whose format is similar to ::RRGGBB and ::AARRGGBB |


### toHex
Generates a hexadecimal color string, whose format is similar to ::AARRGGBB 
``` Java
String toHex()
```
#### Response
#XXXXXX corresponding string 


### toRGBA
Generates a hexadecimal color string, whose format is similar to rgba (red, green, blue, alpha) 
``` Java
String toRGBA()
```
#### Response
#XXXXXX corresponding string 





## TEduBoardInfo
Whiteboard information 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| boardId | String | Whiteboard ID |
| backgroundUrl | String | URL of the background image or background H5 page |
| backgroundColor | TEduBoardColor | Whiteboard background color |




## TEduBoardFileInfo
File information 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| fileId | String | File ID |
| title | String | File name |
| downloadUrl | String | File download address |
| pageCount | int | Total pages of the file |
| pageIndex | int | Currently displayed page of the file |
| boardInfoList | List< TEduBoardInfo > | Whiteboard information list |




## TEduBoardInitParam
Whiteboard initialization parameters 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| ratio | String | Default whiteboard aspect ratio, whose format is similar to "4:3" and "16:9" |
| drawEnable | boolean | Whether doodle is allowed |
| globalBackgroundColor | TEduBoardColor | Global background color |
| toolType | int | Whiteboard tool |
| brushColor | TEduBoardColor | Brush color |
| brushThin | int | Brush thickness |
| textColor | TEduBoardColor | Text color |
| textSize | int | Text size |
| textStyle | int | Text style |
| timSync | boolean | Whether to use Tencent Cloud IMSDK for real-time data synchronization |
| preloadDepth | int | Image pre-loading depth. The default value is 5, which indicates that the previous and next 5 pages are pre-loaded |
| smoothLevel | float | Smoothness level of handwriting. Default value: 0. Value range: [0, 1] |
| dataSyncEnable | boolean | Whether to enable data synchronization |
| contentFitMode | int | Content self-adaption mode |
| progressEnable | boolean | Whether to enable the loading icon, which is used during image loading and PowerPoint file loading. Default value: false |
| progressBarUrl | String | Custom loading icon. It is valid only when processEnable = true. Supported icon formats are jpg, gif, png, and svg |
| imageTimeout | int | Image loading timeout period, in seconds |


## TEduBoardLineStyle
Line styles 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| lineType | int | Line type |
| startArrowType | int | Start-arrow type |
| endArrowType | int | End-arrow type |


## TEduBoardTranscodeFileResult
File transcoding results 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| status | int | Transcoding status |
| taskid | String | Task ID |
| pages | int | Total pages of the file |
| progress | float | Transcoding progress |
| resolution | String | File resolution |
| url | String | Transcoding result URL |
| thumbnailResolution | String | Resolution of the thumbnail generated for the file |
| thumbnailUrl | String | Thumbnail URL generated for the file |
| title | String | File title |




## TEduBoardTranscodeConfig
File transcoding parameters 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| minResolution | String | Minimum resolution of the transcoded file. It can be used to enhance the resolution of the transcoded file. The format of the value is similar to 960x540, where the width and height are separated by letter x |
| isStaticPPT | boolean | Whether to enable static transcoding for PowerPoint files (transcoding into static images). By default, PowerPoint files are transcoded into HTML5 animations, which may take a long time |
| thumbnailResolution | String | Resolution of the thumbnail generated for the file. By default, no thumbnail is generated (generating thumbnails will increase the transcoding time). The format of the value is similar to 200x200, where the width and height are separated by letter x |




## TEduBoardCursorIcon
Cursor icon information 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| cursor | String | Built-in cursor icon of the browser. For more information, see the [reference document](https://developer.mozilla.org/zh-CN/docs/Web/CSS/cursor) |
| url | String | URL of the custom cursor icon. For more information, see the [reference document](https://developer.mozilla.org/zh-CN/docs/Web/CSS/cursor/url) |
| offsetX | int | Horizontal offset of the custom cursor icon |
| offsetY | int | Vertical offset of the custom cursor icon |




## TEduBoardSnapshotInfo
Snapshot information 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| path | String | Local path where the snapshot file is stored. The path includes the file name and extension, and only supports png files. For example, aaa/bbb/ccc/xxx.png |




