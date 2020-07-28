
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
| TEDU_BOARD_IMAGE_STATUS_LOAD_ERROR | An error occurred when loading the background image. |
| TEDU_BOARD_IMAGE_STATUS_LOAD_TIMEOUT | The loading of the background image timed out. |
| TEDU_BOARD_IMAGE_STATUS_LOAD_CANCEL | The loading of the background image was canceled. |



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
The whiteboard content can be images, files, and PPT animations. 


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




## TEduBoardInitParam
Whiteboard initialization parameters 

#### Attribute list

| Attribute | Type | Description |
| --- | --- | --- |
| id | String | [Required] ID of the whiteboard rendering dom node. Ensure that the node has the position: relative style. Otherwise, whiteboard positioning exceptions may occur. |
| classId | Number | [Required] Class ID |
| sdkAppId | Number | [Required] Unique ID of the Tencent Cloud application. To view the ID, log in to the [TRTC console](https://console.cloud.tencent.com/trtc). |
| userId | String | [Required] Username |
| userSig | String | [Required] Login authentication information |
| ratio | String | [Optional] Default whiteboard aspect ratio (whose format is similar to "4:3" and "16:9"). Default value: 16:9 |
| drawEnable | Boolean | [Optional] Whether doodle is allowed. Default value: true |
| textStyle | TEduBoardTextStyle | [Optional] Text style. Valid values: 0 for normal, 1 for bold, 2 for italic, 3 for bold and italic. Default value: 0 |
| textSize | Number | [Optional] Text size. Default value: 320 |
| textColor | Color | [Optional] Text color. Default value: #000000 |
| brushColor | Color | [Optional] Brush color. Default value: #ff0000 |
| brushThin | Number | [Optional] Brush thickness. Default value: 100 |
| toolType | TEduBoardToolType | [Optional] Whiteboard tool. Default value: TEDU_BOARD_TOOL_TYPE_PEN |
| globalBackgroundColor | Color | [Optional] Global background color. Default value: #ffffff |
| contentFitMode | TEduBoardContentFitMode | [Optional] Whiteboard content self-adaption mode. Default value: TEDU_BOARD_CONTENT_FIT_MODE_NONE |
| dataSyncEnable | Boolean | [Optional] Whether or not data synchronization is enabled. If no, no local whiteboard operations will be synced to the remote end. Default value: true |
| scale | Number | [Optional] Default whiteboard scale coefficient. The actual scale is scale/100. Default value: 100 |
| preloadDepth | Number | [Optional] Image pre-loading depth. The default value is 5, which indicates that the previous and next 5 pages are pre-loaded. |
| smoothLevel | Number | [Optional] Handwriting smooth coefficient. Default value: 0. Value range: [0, 1] |
| progressEnable | Boolean | [Optional] Whether the SDK built-in loading icon is used or not. Default value: false |
| progressBarUrl | String | [Optional] Custom loading icon, which is valid only when progressEnable = true. Supported icon formats are jpg, gif, png, and svg. |


## TEduBoardLineStyle
Line styles 

#### Attribute list

| Attribute | Type | Description |
| --- | --- | --- |
| lineType | TEduBoardLineType | [Optional] Line type. Default value: TEDU_BOARD_LINE_TYPE_SOLID |
| startArrowType | TEduBoardArrowType | [Optional] Start-point arrow type. Default value: TEDU_BOARD_ARROW_TYPE_NONE |
| endArrowType | TEduBoardArrowType | [Optional] End-point arrow type. Default value: TEDU_BOARD_ARROW_TYPE_NONE |


## TEduBoardCursorIcon
Cursor icon information 

#### Attribute list

| Attribute | Type | Description |
| --- | --- | --- |
| cursor | String | [Required] Built-in cursor icon of the browser. For more information on possible values, see the [reference document](https://developer.mozilla.org/zh-CN/docs/Web/CSS/cursor). |
| url | String | [Optional] URL of the custom cursor icon. For more information on the format restrictions, see the [reference document](https://developer.mozilla.org/zh-CN/docs/Web/CSS/cursor/url). |
| offsetX | Number | [Optional] Horizontal offset of the custom cursor icon. Default value: 0 |
| offsetY | Number | [Optional] Vertical offset of the custom cursor icon. Default value: 0 |


## TEduBoardTranscodeConfig
File transcoding parameters 

#### Attribute list

| Attribute | Type | Description |
| --- | --- | --- |
| minResolution | String | [Optional] Minimum resolution of the transcoded file. It can be used to enhance the resolution of the transcoded file. The format of the value is similar to 960x540, where the width and height are separated by letter x. |
| isStaticPPT | Boolean | [Optional] Whether or not to enable static transcoding for PowerPoint files (transcoding into static images). By default, PowerPoint files are transcoded into HTML5 animations, which takes a relatively long time. |
| thumbnailResolution | String | [Optional] Resolution of the thumbnail generated for the file. By default, no thumbnail is generated (generating thumbnails will increase the amount of transcoding time). The format of the value is similar to 200x200, where the width and height are separated by letter x. |


## TEduBoardTranscodeFileResult
File transcoding results 

#### Attribute list

| Attribute | Type | Description |
| --- | --- | --- |
| code | String | Error code |
| message | String | Error message |
| taskID | String | Task ID |
| status | String | Transcoding status. Valid values: "ERROR" for transcoding error, "UPLOADING" for uploading files, "CREATED" for initiating a transcoding task, "QUEUED" for queuing, "PROCESSING" for transcoding, and "FINISHED" for transcoded |
| progress | Number | Transcoding progress |
| title | String | File title |
| resolution | String | File resolution |
| pages | Number | Total pages of the file |
| resultUrl | String | Transcoding result URL |
| thumbnailResolution | String | Resolution of the thumbnail generated for the file |
| thumbnailUrl | String | Thumbnail URL generated for the file |
| userData | String | userData passed through the transcoding API |


## TEduBoardInfo
Whiteboard information 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| boardId | String | Whiteboard ID |
| backgroundUrl | String | URL of the whiteboard background image or background H5 page |
| backgroundColor | Color | Whiteboard background color |


## TEduBoardFileInfo
File information 

#### Attribute list

| Attribute | Type | Field Description |
| --- | --- | --- |
| fileId | String | File ID |
| title | String | File name |
| downloadURL | String | File download address |
| pageIndex | Number | Current page number of the file |
| pageCount | Number | Total pages of the file |
| boardInfoList | Array | Whiteboard information list |


## TEduBoardSnapshotInfo
Snapshot information 

#### Attribute list

| Attribute | Type | Description |
| --- | --- | --- |
| userData | String | Passthrough information |


