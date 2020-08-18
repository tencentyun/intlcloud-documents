## TEduBoardController
Main API classes for the whiteboard features 

| Class | Description |
| --- | --- |
| TEduBoardController | Whiteboard controller |

### Setting TEduBoardCallback
| API | Description |
| --- | --- |
| addDelegate: | Sets the event callback listener |
| removeDelegate: | Deletes the event callback listener |

### Basic process APIs
| API | Description |
| --- | --- |
| initWithAuthParam:roomId:initParam: | Initializes the whiteboard |
| unInit | Uninitializes the whiteboard |
| getBoardRenderView | Obtains the whiteboard rendering view |
| addSyncData: | Adds the whiteboard synchronization data |
| setDataSyncEnable: | Sets whether data synchronization is enabled for the whiteboard |
| isDataSyncEnable | Checks whether data synchronization is enabled for the whiteboard |
| getSyncTime | Obtains the synchronization timestamp |
| syncRemoteTime:timestamp: | Syncs the remote timestamp |
| reset | Resets the whiteboard |
| getVersion | Obtains the version number |

### Doodle APIs
| API | Description |
| --- | --- |
| setAccessibleUsers: | Sets users whose drawings can be operated |
| setDrawEnable: | Sets whether doodle is allowed for the whiteboard |
| isDrawEnable | Checks whether doodle is allowed for the whiteboard |
| setGlobalBackgroundColor: | Sets the background color of all whiteboards |
| getGlobalBackgroundColor | Obtains the global background color of whiteboards |
| setBackgroundColor: | Sets the background color of the current whiteboard page |
| getBackgroundColor | Obtains the background color of the current whiteboard page |
| setBackgroundImage:mode: | Sets the background image of the current whiteboard page |
| setBackgroundH5: | Sets the background H5 page of the current whiteboard page |
| setToolType: | Sets the whiteboard tool to be used |
| getToolType | Obtains the whiteboard tool in use |
| setBrushColor: | Sets the brush color |
| getBrushColor | Obtains the brush color |
| setBrushThin: | Sets the brush thickness |
| getBrushThin | Obtains the brush thickness |
| setTextColor: | Sets the text color |
| getTextColor | Obtains the text color |
| setTextStyle: | Sets the text style |
| getTextStyle | Obtains the text style |
| setTextSize: | Sets the text size |
| getTextSize | Obtains the text size |
| setLineStyle: | Sets the line style |
| getLineStyle | Obtains the line style |
| setOvalDrawMode: | Sets the oval drawing mode |
| getOvalDrawMode | Obtains the oval drawing mode |
| undo | Undoes the last action on the current whiteboard page |
| redo | Redoes the last undone action on the current whiteboard page |
| clear | Clears doodles, the background color, and the background image |
| clearDraws | Clears doodles |
| clearBackground:andSelected: | Clears doodles on the current whiteboard page |
| setCursorIcon:cursorIcon: | Sets the cursor icon for the whiteboard tool |

### Whiteboard page operation APIs
| API | Description |
| --- | --- |
| addBoardWithBackgroundImage: | Adds a whiteboard page |
| deleteBoard: | Deletes a whiteboard page |
| prevStep | Goes to the previous step. Each step corresponds to an animation effect of the PowerPoint file. If no animation effect that has been displayed is available, calling this API will redirect you to the previous page |
| nextStep | Goes to the next step |
| preBoard | Goes to the previous page |
| nextBoard | Goes to the next page |
| gotoBoard: | Redirects to the specified whiteboard page |
| preBoard: | Goes to the previous page |
| nextBoard: | Goes to the next page |
| gotoBoard:resetStep: | Redirects to the specified whiteboard page |
| getCurrentBoard | Obtains the ID of the current whiteboard page |
| getBoardList | Obtains the whiteboard list of all files |
| setBoardRatio: | Sets the aspect ratio of the current whiteboard page |
| getBoardRatio | Obtains the aspect ratio of the current whiteboard page |
| setBoardScale: | Sets the scale of the current whiteboard page |
| getBoardScale | Obtains the scale of the current whiteboard page |
| setBoardContentFitMode: | Sets the whiteboard content self-adaption mode |
| getBoardContentFitMode | Obtains the whiteboard content self-adaption mode |
| addImageElement: | Adds image resources |
| setHandwritingEnable: | Sets whether handwriting is enabled for the whiteboard |
| isHandwritingEnable | Checks whether handwriting is enabled for the whiteboard |
| refresh | Refreshes the current whiteboard page and triggers the onTEBRefresh callback |
| syncAndReload | Syncs local data that failed to be sent to the remote end and refreshes the local data |
| snapshot: | Creates a whiteboard snapshot |

### File operation APIs
| API | Description |
| --- | --- |
| applyFileTranscode:config: | Initiates a file transcoding request |
| getFileTranscodeProgress: | Actively queries the file transcoding progress |
| addTranscodeFile: | Adds a file for transcoding |
| deleteFile: | Deletes a file |
| switchFile: | Switches to another file |
| switchFile:boardId:stepIndex: | Switches to another file |
| getCurrentFile | Obtains the current file ID |
| getFileInfo: | Obtains the file information of the specified file on the whiteboard |
| getFileInfoList | Obtains the file information list of all uploaded files on the whiteboard |
| getFileBoardList: | Obtains the whiteboard ID list of the specified file |
| getThumbnailImages: | Obtains the thumbnail of the specified file, excluding the default file (fileId=#DEFAULT) |
| clearFileDraws: | Clears all whiteboard doodles of the specified file |
| addVideoFile: | Adds a video file |
| showVideoControl: | Shows or hides the video control bar |
| playVideo | Plays a video |
| pauseVideo | Pauses a video |
| seekVideo: | Goes to the specified time point in a video (only for VOD videos) |
| setSyncVideoStatusEnable: | Sets whether to sync local video operations to the remote end |
| startSyncVideoStatus: | Serves as an internal start timer that synchronizes the video status to the remote end according to the schedule (only for mp4 files) |
| stopSyncVideoStatus | Stops syncing the video status |
| addH5File: | Adds an H5 file |
| addImagesFile: | Imports images to the whiteboard in batches |


## TEduBoardDelegate
Callback API classes for the whiteboard features 

| Class | Description |
| --- | --- |
| TEduBoardDelegate-p | Whiteboard event callback APIs |

### Common event callbacks
| API | Description |
| --- | --- |
| onTEBError:msg: | Whiteboard error callback |
| onTEBWarning:msg: | Whiteboard warning callback |

### Basic process callbacks
| API | Description |
| --- | --- |
| onTEBInit | Callback for the completion of whiteboard initialization |
| onTEBHistroyDataSyncCompleted | Callback for the completion of whiteboard historical data synchronization |
| onTEBSyncData: | Whiteboard synchronization data callback |
| onTEBUndoStatusChanged: | Callback for the whiteboard undo status change |
| onTEBRedoStatusChanged: | Callback for the whiteboard redo status change |

### Doodle feature callbacks
| API | Description |
| --- | --- |
| onTEBImageStatusChanged:url:status: | Callback for the whiteboard image status change |
| onTEBSetBackgroundImage: | Callback for setting the whiteboard background image |
| onTEBAddImageElement: | Callback for adding image elements |
| onTEBBackgroundH5StatusChanged:url:status: | Callback for setting the whiteboard background H5 status change |

### Whiteboard operation callbacks
| API | Description |
| --- | --- |
| onTEBAddBoard:fileId: | Callback for adding a whiteboard page |
| onTEBDeleteBoard:fileId: | Callback for deleting a whiteboard page |
| onTEBGotoBoard:fileId: | Callback for redirecting to a whiteboard page |
| onTEBGotoStep:totalStep: | Callback for whiteboard page animation steps |
| onTEBRectSelected | Callback for the selection made by the selection tool |
| onTEBRefresh | Callback for refreshing a whiteboard |
| onTEBSnapshot:errorCode:errorMsg: | Callback for creating a whiteboard snapshot |

### File operation callbacks
| API | Description |
| --- | --- |
| onTEBFileTranscodeProgress:path:errorCode:errorMsg: | Callback for the file transcoding progress |
| onTEBAddTranscodeFile: | Callback for adding a file for transcoding |
| onTEBDeleteFile: | Callback for deleting a file |
| onTEBSwitchFile: | Callback for switching files |
| onTEBFileUploadProgress:currentBytes:totalBytes:uploadSpeed:percent: | Callback for the file upload progress |
| onTEBFileUploadStatus:status:errorCode:errorMsg: | Callback for the file upload status |
| onTEBH5FileStatusChanged:status: | H5 file status callback |
| onTEBVideoStatusChanged:status:progress:duration: | Video file status callback |
| onTEBAddImagesFile: | Callback for batch adding image files |


## Definitions of Key Classes

| Class | Description |
| --- | --- |
| TEduBoardInfo | Whiteboard information |
| TEduBoardFileInfo | File information |
| TEduBoardAuthParam | Authorization parameters |
| TEduBoardInitParam | Whiteboard initialization parameters |
| TEduBoardLineStyle | Line style |
| TEduBoardTranscodeConfig | File transcoding parameters |
| TEduBoardTranscodeFileResult | File transcoding result |
| TEduBoardCursorIcon | Cursor icon |
| TEduBoardSnapshotInfo | Snapshot information |

#### Enumerated values
| Enumerated Value | Description |
| --- | --- |
| TEduBoardToolType | Whiteboard tool type |
| TEduBoardImageFitMode | Whiteboard image padding and alignment mode. When the image is zoomed in proportionally based on its width, the effect of the left and right alignments are the same as that of the central alignment. When the image is zoomed in proportionally based on its height, the effect of the top and bottom alignments are the same as that of the central alignment |
| TEduBoardContentFitMode | Whiteboard content self-adaption mode. The content can be images, files, and PPT animations |
| TEduBoardImageStatus | Whiteboard image status |
| TEduBoardTextStyle | Whiteboard text style |
| TEduBoardUploadStatus | Whiteboard upload status |
| TEduBoardBackgroundH5Status | H5 background status |
| TEduBoardLineType | Line type |
| TEduBoardArrowType | Arrow type |
| TEduBoardOvalDrawMode | Oval drawing mode |
| TEduBoardFileTranscodeStatus | File transcoding status |
| TEduBoardVideoStatus | Video file status |
| TEduBoardH5FileStatus | H5 file status |


## Error Codes

#### Enumerated values
| Enumerated Value | Description |
| --- | --- |
| TEduBoardErrorCode | Whiteboard error codes (critical) |
| TEduBoardWarningCode | Whiteboard error codes (warning) |


