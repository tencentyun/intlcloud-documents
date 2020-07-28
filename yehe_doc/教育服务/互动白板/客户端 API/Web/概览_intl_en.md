## TEduBoardController
Main API classes for whiteboard features 

| Class | Description |
| --- | --- |
| TEduBoard | Whiteboard controller |

### Creating and terminating instances
| API | Description |
| --- | --- |
| TEduBoard | Creates a whiteboard. |
| destroy | Terminates a whiteboard. |

### Setting TEduBoardCallback
| API | Description |
| --- | --- |
| on | Enables event listening. |
| off | Cancels event listening. |

### Basic process APIs
| API | Description |
| --- | --- |
| addSyncData | Adds whiteboard synchronization data. |
| getVersion | Obtains the SDK version number. |
| setDataSyncEnable | Sets whether to enable data synchronization for the whiteboard. |
| isDataSyncEnable | Checks whether data synchronization is enabled for the whiteboard. |
| reset | Resets the whiteboard. |
| getSyncTime | Obtains the synchronization timestamp. |
| syncRemoteTime | Syncs the remote timestamp. |

### Doodle APIs
| API | Description |
| --- | --- |
| setDrawEnable | Sets whether the whiteboard allows doodle. |
| isDrawEnable | Checks whether doodle is allowed for the whiteboard. |
| setAccessibleUsers | Sets users whose drawings can be operated. |
| setGlobalBackgroundColor | Sets the background color of all whiteboards. |
| getGlobalBackgroundColor | Obtains the global background color of whiteboards. |
| setBackgroundColor | Sets the background color of the current whiteboard page. |
| getBackgroundColor | Obtains the background color of the current whiteboard page. |
| setToolType | Sets the whiteboard tool to use. |
| getToolType | Obtains the whiteboard tool in use. |
| setCursorIcon | Sets the cursor icon for the whiteboard tool. |
| setBrushColor | Sets the brush color. |
| getBrushColor | Obtains the brush color. |
| setBrushThin | Sets the brush thickness. |
| getBrushThin | Obtains the brush thickness. |
| setTextColor | Sets the text color. |
| getTextColor | Obtains the text color. |
| setTextSize | Sets the text size. |
| getTextSize | Obtains the text size. |
| setTextStyle | Sets the text style. |
| getTextStyle | Obtains the text style. |
| setLineStyle | Sets the line style. |
| getLineStyle | Obtains the line style. |
| setOvalDrawMode | Sets the oval drawing mode. |
| getOvalDrawMode | Obtains the oval drawing mode. |
| clear | Clears doodles on the current whiteboard page. |
| setBackgroundImage | Sets the background image of the current whiteboard page. |
| setBackgroundH5 | Sets the background H5 page of the current whiteboard page. |
| undo | Undoes the last action on the current whiteboard page. |
| redo | Redoes the last undone action on the current whiteboard page. |
| resize | Recalculates the whiteboard size and performs rendering. |

### Whiteboard page operation APIs
| API | Description |
| --- | --- |
| addBoard | Adds a whiteboard page. |
| deleteBoard | Deletes a whiteboard page. |
| prevStep | Goes to the previous step. Each step corresponds to an animation effect of the PowerPoint file. If no animation effect that has been displayed is available, calling this API redirects to the previous page. |
| nextStep | Goes to the next step. |
| preBoard | Goes to the previous page. |
| nextBoard | Goes to the next page. |
| gotoBoard | Redirects to a specified whiteboard page. |
| getCurrentBoard | Obtains the ID of the current whiteboard page. |
| getBoardList | Obtains the whiteboard list of all files. |
| setBoardRatio | Sets the aspect ratio of the current whiteboard page. |
| getBoardRatio | Obtains the aspect ratio of the current whiteboard page. |
| setBoardScale | Sets the scale of the current whiteboard page. |
| getBoardScale | Obtains the scale of the current whiteboard page. |
| setBoardContentFitMode | Sets the whiteboard content self-adaption mode. |
| getBoardContentFitMode | Obtains the whiteboard content self-adaption mode. |

### File operation APIs
| API | Description |
| --- | --- |
| applyFileTranscode | Initiates a file transcoding request. |
| getFileTranscodeProgress | Actively queries the file transcoding progress. |
| addTranscodeFile | Adds a file for transcoding. |
| addImagesFile | Imports images to the whiteboard in batches. |
| deleteFile | Deletes a file. |
| switchFile | Switches to another file. |
| getCurrentFile | Obtains the current file ID. |
| getFileInfo | Obtains the file information of the specified file on the whiteboard. |
| getFileInfoList | Obtains the file information list of all uploaded files on the whiteboard. |
| getFileBoardList | Obtains the whiteboard ID list of the specified file. |
| getThumbnailImages | Obtains the thumbnail of the specified file, excluding the default file (fileId=#DEFAULT). |
| clearFileDraws | Clears all whiteboard doodles of the specified file. |
| hasVideoPermission | Sets whether to authorize video file playback. |
| applyVideoPermission | Authorizes video file playback. |
| addVideoFile | Adds a video file. |
| addVODFile | Adds a video file (internal API) |
| setVODExtParam | Sets extra parameters of VOD videos, such as plugins and hlsConfig. |
| showVideoControl | Shows or hides the video control bar. |
| playVideo | Plays a video. |
| pauseVideo | Pauses a video. |
| seekVideo | Goes to a specified time point in a video (only for VOD videos). |
| muteVideo | Mutes a video. |
| setSyncVideoStatusEnable | Sets whether to sync local video operations to the remote end. |
| startSyncVideoStatus | Serves as an internal start timer that synchronizes the video status to the remote end according to schedule (only for mp4 files). |
| stopSyncVideoStatus | Stops syncing the video status. |
| addH5File | Adds an H5 file. |
| addImageElement | Adds image resources. |
| setHandwritingEnable | Sets whether to enable handwriting for the whiteboard. |
| isHandwritingEnable | Checks whether handwriting is enabled for the whiteboard. |
| refresh | Refreshes the current whiteboard page and triggers the onTEBRefresh callback. |
| addAckData | Confirms whether data is sent successfully. |
| syncAndReload | Syncs local data that failed to be sent to the remote end and refreshes the local data. |
| snapshot | Creates a whiteboard snapshot. |


## TEduBoardCallback
Callback API classes for whiteboard features 

| Class | Description |
| --- | --- |
| TEduBoardCallback | Whiteboard event callback delegate |

### Common event callbacks
| API | Description |
| --- | --- |
| TEB_ERROR | Whiteboard error callback |
| TEB_WARNING | Whiteboard warning callback |

### Basic process callbacks
| API | Description |
| --- | --- |
| TEB_INIT | Callback for whiteboard initialization completion |
| TEB_HISTROYDATA_SYNCCOMPLETED | Callback for the completion of whiteboard historical data synchronization |
| TEB_SYNCDATA | Whiteboard synchronization data callback |
| TEB_OPERATE_CANUNDO_STATUS_CHANGED | Callback for the whiteboard undo status change |
| TEB_OPERATE_CANREDO_STATUS_CHANGED | Callback for the whiteboard redo status change |

### Doodle feature callbacks
| API | Description |
| --- | --- |
| TEB_IMAGE_STATUS_CHANGED | Callback for the whiteboard image status change |
| TEB_SETBACKGROUNDIMAGE | Callback for setting the whiteboard background image |
| TEB_ADDIMAGEELEMENT | Callback for adding an image element |
| TEB_H5BACKGROUND_STATUS_CHANGED | Callback for the whiteboard background H5 status change |

### Whiteboard page operation callbacks
| API | Description |
| --- | --- |
| TEB_ADDBOARD | Callback for adding a whiteboard page |
| TEB_DELETEBOARD | Callback for deleting a whiteboard page |
| TEB_GOTOBOARD | Callback for redirecting to a whiteboard page |
| TEB_GOTOSTEP | Callback for whiteboard page animation steps |
| TEB_RECTSELECTED | Callback after the rectangle selection tool selects certain content. This callback is triggered only after the tool selects a doodle or an image element. |
| TEB_REFRESH | Callback for refreshing the current whiteboard page |
| TEB_SNAPSHOT | Callback for creating a whiteboard snapshot |

### File operation callbacks
| API | Description |
| --- | --- |
| TEB_TRANSCODEPROGRESS | File transcoding progress callback |
| TEB_ADDTRANSCODEFILE | Callback for adding a file for transcoding |
| TEB_DELETEFILE | Callback for deleting a file |
| TEB_SWITCHFILE | Callback for switching files |
| TEB_FILEUPLOADPROGRESS | File upload progress callback |
| TEB_FILEUPLOADSTATUS | File upload status callback |
| TEB_FILEUPLOADPROGRESS | File upload progress callback |
| TEB_ADDIMAGESFILE | Callback for adding a file for transcoding |
| TEB_VIDEO_STATUS_CHANGED | Callback for setting the H5 file |


## Definitions of Key Classes

| Class | Description |
| --- | --- |
| TEduBoardInitParam | H5 file loading status |
| TEduBoardLineStyle | Line style |
| TEduBoardCursorIcon | Cursor icon |
| TEduBoardTranscodeConfig | File transcoding parameters |
| TEduBoardTranscodeFileResult | File transcoding result |
| TEduBoardInfo | Whiteboard information |
| TEduBoardFileInfo | File information |
| TEduBoardSnapshotInfo | Snapshot information |

#### Enumerated values
| Enumerated Value | Description |
| --- | --- |
| TEduBoardToolType | Whiteboard tool |
| TEduBoardImageFitMode | Alignment mode of whiteboard image filling |
| TEduBoardImageStatus | Whiteboard image status |
| TEduBoardTextStyle | Whiteboard text style |
| TEduBoardUploadStatus | Whiteboard upload status |
| TEduBoardBackgroundH5Status | H5 background status |
| TEduBoardContentFitMode | Whiteboard content self-adaption mode |
| TEduBoardLineType | Line type |
| TEduBoardArrowType | Arrow type |
| TEduBoardOvalDrawMode | Oval drawing mode |


## Error Codes

#### Enumerated values
| Enumerated Value | Description |
| --- | --- |
| TEduBoardErrorCode | Whiteboard error codes (critical) |
| TEduBoardWarningCode | Whiteboard error codes (warning) |


