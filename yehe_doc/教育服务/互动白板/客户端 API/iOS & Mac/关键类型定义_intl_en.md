
## TEduBoardToolType
Whiteboard tools 


| Enumerated Value | Description |
| --- | --- |
| TEDU_BOARD_TOOL_TYPE_MOUSE | Mouse |
| TEDU_BOARD_TOOL_TYPE_PEN | Brush |
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



## TEduBoardImageFitMode
TIW image padding and alignment modes. When the image is zoomed in proportionally based on the width, the effect of left and right alignments are the same as that of central alignment. When the image is zoomed in proportionally based on the height, the effect of top and bottom alignments are the same as that of central alignment. 


| Enumerated Value | Description |
| --- | --- |
| TEDU_BOARD_IMAGE_FIT_MODE_CENTER | Center-aligned with the width or height as the reference and scaled up proportionally |
| TEDU_BOARD_IMAGE_FIT_MODE_LEFT | Left-aligned with the width or height as the reference and scaled up proportionally |
| TEDU_BOARD_IMAGE_FIT_MODE_TOP | Top-aligned with the width or height as the reference and scaled up proportionally |
| TEDU_BOARD_IMAGE_FIT_MODE_RIGHT | Right-aligned with the width or height as the reference and scaled up proportionally |
| TEDU_BOARD_IMAGE_FIT_MODE_BOTTOM | Bottom-aligned with the width or height as the reference and scaled up proportionally |



## TEduBoardContentFitMode
Whiteboard content self-adaption modes. The content can be images, files, and PPT animations. 


| Enumerated Value | Description |
| --- | --- |
| TEDU_BOARD_CONTENT_FIT_MODE_NONE | Do not use content self-adaption. In this default mode, do not automatically adjust the whiteboard aspect ratio and scale the content proportionally in a center-aligned fashion. In addition, the content width and height are less than or equal to the whiteboard width and height respectively. |
| TEDU_BOARD_CONTENT_FIT_MODE_CENTER_INSIDE | Automatically adjust the whiteboard aspect ratio to be consistent with the content. Spread the content all over the whiteboard and scale the whiteboard proportionally in a center-aligned fashion. In addition, the whiteboard width and height are less than or equal to the container width and height respectively. |
| TEDU_BOARD_CONTENT_FIT_MODE_CENTER_COVER | Automatically adjust the whiteboard aspect ratio to be consistent with the content. Spread the content all over the whiteboard and scale the whiteboard proportionally in a center-aligned fashion. In addition, the whiteboard width and height are greater than or equal to the container width and height respectively. |



## TEduBoardImageStatus
Whiteboard image statuses 


| Enumerated Value | Description |
| --- | --- |
| TEDU_BOARD_IMAGE_STATUS_LOADING | The background image is being loaded. |
| TEDU_BOARD_IMAGE_STATUS_LOAD_DONE | The background image has been loaded. |
| TEDU_BOARD_IMAGE_STATUS_LOAD_ABORT | The loading of the background image was aborted. |
| TEDU_BOARD_IMAGE_STATUS_LOAD_ERROR | An error occurred when loading the background image. |
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



## TEduBoardLineType
Line types 


| Enumerated Value | Description |
| --- | --- |
| TEDU_BOARD_LINE_TYPE_SOLID | Solid line |
| TEDU_BOARD_LINE_TYPE_DOTTED | Dotted line |



## TEduBoardArrowType
Arrow types 


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
| TEDU_BOARD_FILE_TRANSCODE_UPLOADING | File uploading |
| TEDU_BOARD_FILE_TRANSCODE_CREATED | Transcoding task initiated |
| TEDU_BOARD_FILE_TRANSCODE_QUEUED | Transcoding task pending |
| TEDU_BOARD_FILE_TRANSCODE_PROCESSING | Transcoding |
| TEDU_BOARD_FILE_TRANSCODE_FINISHED | Transcoding completed |



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



## TEduBoardH5FileStatus
H5 file statuses 


| Enumerated Value | Description |
| --- | --- |
| TEDU_BOARD_H5_FILE_STATUS_LOADING | Loading |
| TEDU_BOARD_H5_FILE_STATUS_LOADED | Loading completed |




## TEduBoardInfo
Whiteboard information 

#### Attribute list

| Attribute | Type | Description |
| --- | --- | --- |
| boardId | NSString * | Whiteboard ID |
| backgroundUrl | NSString * | URL of the background image or background H5 page |
| backgroundColor | TEColor * | Whiteboard background color |


## TEduBoardFileInfo
File information 

#### Attribute list

| Attribute | Type | Description |
| --- | --- | --- |
| fileId | NSString * | File ID |
| title | NSString * | File name |
| downloadURL | NSString * | File download address |
| pageIndex | int | Current page number |
| pageCount | int | Total pages |
| boardInfoList | NSArray< TEduBoardInfo * > * | Whiteboard information list |


## TEduBoardAuthParam
Authorization parameters 

#### Attribute list

| Attribute | Type | Description |
| --- | --- | --- |
| sdkAppId | int | Application ID |
| userId | NSString * | User ID |
| userSig | NSString * | Signature |


## TEduBoardInitParam
Whiteboard  initialization parameters 

#### Attribute list

| Attribute | Type | Description |
| --- | --- | --- |
| ratio | NSString * | Default whiteboard aspect ratio, whose format is similar to "4:3" and "16:9". Default value: "16:9" |
| drawEnable | BOOL | Whether doodle is allowed or not. Default value: YES |
| globalBackgroundColor | TEColor * | Global background color |
| toolType | TEduBoardToolType | Whiteboard tool. Default value: TEDU_BOARD_TOOL_TYPE_PEN |
| brushColor | TEColor * | Brush color |
| brushThin | int | Brush thickness. Default value: 100 |
| textColor | TEColor * | Text color |
| textSize | int | Text thickness. Default value: 320 |
| textStyle | TEduBoardTextStyle | Text style. Default value: TEDU_BOARD_TEXT_STYLE_NORMAL |
| timSync | BOOL | Whether or not Tencent Cloud IMSDK is used for real-time data synchronization. Default value: YES |
| dataSyncEnable | BOOL | Whether or not data synchronization is enabled. If no, no local whiteboard operations will be synced to the remote end. |
| preloadDepth | int | Image pre-loading depth. The default value is 5, which indicates that the previous and next 5 pages are pre-loaded. |
| smoothLevel | float | Smoothing coefficient. Default value: 0. Value range: [0, 1] |
| boardContentFitMode | TEduBoardContentFitMode | Whiteboard content self-adaption mode. Default value: TEDU_BOARD_CONTENT_FIT_MODE_NONE |
| imageTimeout | int | Image loading timeout period in seconds. Default value: 10s |
| progressEnable | BOOL | Whether or not to enable the loading icon, which is used during image loading and PowerPoint file loading. Default value: false |
| progressBarUrl | NSString * | Custom loading icon. It is valid only when progressEnable = true. Supported icon formats are jpg, gif, png, and svg. |


## TEduBoardLineStyle
Line styles 

#### Attribute list

| Attribute | Type | Description |
| --- | --- | --- |
| lineType | TEduBoardLineType | Line type. Default value: TEDU_BOARD_LINE_TYPE_SOLID |
| startArrowType | TEduBoardArrowType | Start-point arrow type. Default value: TEDU_BOARD_ARROW_TYPE_NONE |
| endArrowType | TEduBoardArrowType | End-point arrow type. Default value: TEDU_BOARD_ARROW_TYPE_NONE |


## TEduBoardTranscodeConfig
File transcoding parameters 

#### Attribute list

| Attribute | Type | Description |
| --- | --- | --- |
| minResolution | NSString * | Minimum resolution of the transcoded file. It can be used to enhance the resolution of the transcoded file. The format of the value is similar to 960x540, where the width and height are separated by letter x. |
| isStaticPPT | BOOL | Whether or not to enable static transcoding for PowerPoint files (transcoding into static images). By default, PowerPoint files are transcoded into HTML5 animations, which takes a relatively long time. |
| thumbnailResolution | NSString * | Resolution of the thumbnail generated for the file. By default, no thumbnail is generated (generating thumbnails will increase the amount of transcoding time). The format of the value is similar to 200x200, where the width and height are separated by letter x. |


## TEduBoardTranscodeFileResult
File transcoding results 

#### Attribute list

| Attribute | Type | Description |
| --- | --- | --- |
| taskId | NSString * | Task ID |
| status | TEduBoardFileTranscodeStatus | Transcoding status |
| progress | NSInteger | Transcoding progress in percentage |
| title | NSString * | File title |
| resolution | NSString * | File resolution, for example, "1024x768" |
| pages | NSInteger | Total pages of the file |
| url | NSString * | Transcoding result URL |
| thumbnailResolution | NSString * | Resolution of the thumbnail generated for the file, for example, "200x200" |
| thumbnailUrl | NSString * | Thumbnail URL generated for the file |


## TEduBoardCursorIcon
Cursor icon information 

#### Attribute list

| Attribute | Type | Description |
| --- | --- | --- |
| cursor | NSString * | Built-in cursor icon of the browser. For more information on possible values, see the [reference document](https://developer.mozilla.org/zh-CN/docs/Web/CSS/cursor). |
| url | NSString * | URL of the custom cursor icon. For more information on the format restrictions, see the [reference document](https://developer.mozilla.org/zh-CN/docs/Web/CSS/cursor/url). |
| offsetX | UInt32 | Horizontal offset of the custom cursor icon |
| offsetY | UInt32 | Vertical offset of the custom cursor icon |


## TEduBoardSnapshotInfo
Snapshot information 

#### Attribute list

| Attribute | Type | Description |
| --- | --- | --- |
| path | NSString * | Local path where the snapshot file is stored. The path includes the file name and extension, and supports only png files. For example, aaa/bbb/ccc/xxx.png. |


