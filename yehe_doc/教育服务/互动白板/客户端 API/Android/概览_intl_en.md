## TEduBoardController
Main API classes for whiteboard features 

| Class | Description |
| --- | --- |
| TEduBoardController | Whiteboard controller |

### Creating and terminating instances
| API | Description |
| --- | --- |
| TEduBoardController | Creates a whiteboard controller instance |

### Setting TEduBoardCallback
| API | Description |
| --- | --- |
| addCallback | Sets the event callback listener |
| removeCallback | Deletes the event callback listener |

### Basic process APIs
| API | Description |
| --- | --- |
| init | Initializes the whiteboard |
| uninit | Uninitializes the whiteboard and releases internal resources |
| getBoardRenderView | Obtains the whiteboard rendering view |
| addSyncData | Adds whiteboard synchronization data |
| setDataSyncEnable | Sets whether to enable data synchronization for the whiteboard |
| isDataSyncEnable | Checks whether data synchronization is enabled for the whiteboard |
| reset | Resets the whiteboard |
| getSyncTime | Obtains the synchronization timestamp |
| syncRemoteTime | Syncs the remote timestamp |
| getVersion | Obtains the SDK version number |

### Doodle APIs
| API | Description |
| --- | --- |
| setDrawEnable | Sets whether the whiteboard allows doodle |
| isDrawEnable | Checks whether doodle is allowed for the whiteboard |
| setAccessibleUsers | Sets users whose drawings can be operated |
| setGlobalBackgroundColor | Sets the background color of all whiteboards |
| getGlobalBackgroundColor | Obtains the global background color of whiteboards |
| setBackgroundColor | Sets the background color of the current whiteboard page |
| getBackgroundColor | Obtains the background color of the current whiteboard page |
| setToolType | Sets the whiteboard tool to use |
| getToolType | Obtains the whiteboard tool in use |
| setCursorIcon | Sets the cursor icon for the whiteboard tool |
| setBrushColor | Sets the brush color |
| getBrushColor | Obtains the brush color |
| setBrushThin | Sets the brush thickness |
| getBrushThin | Obtains the brush thickness |
| setTextColor | Sets the text color |
| getTextColor | Obtains the text color |
| setTextSize | Sets the text size |
| getTextSize | Obtains the text size |
| setTextStyle | Sets the text style |
| getTextStyle | Obtains the text style |
| clear | Clears the doodle on the current whiteboard page |
| clear | Clears the doodle on the current whiteboard page |
| setLineStyle | Sets the line style |
| getLineStyle | Obtains the line style |
| setOvalDrawMode | Sets the oval drawing mode |
| getOvalDrawMode | Obtains the oval drawing mode |
| setBackgroundImage | Sets the background image of the current whiteboard page |
| setBackgroundH5 | Sets the background H5 page of the current whiteboard page |
| undo | Undoes the last action on the current whiteboard page |
| redo | Redoes the last undone action on the current whiteboard page |
| setHandwritingEnable | Sets whether to enable handwriting for the whiteboard |
| isHandwritingEnable | Checks whether handwriting is enabled for the whiteboard |

### Whiteboard page operation APIs
| API | Description |
| --- | --- |
| addBoard | Adds a whiteboard page |
| deleteBoard | Deletes a whiteboard page |
| prevStep | Goes to the previous step. Each step corresponds to an animation effect of the PowerPoint file. If no animation effect that has been displayed is available, calling this API redirects to the previous page |
| nextStep | Goes to the next step |
| prevBoard | Goes to the previous page |
| nextBoard | Goes to the next page |
| gotoBoard | Redirects to the specified whiteboard page |
| prevBoard | Goes to the previous page |
| nextBoard | Goes to the next page |
| gotoBoard | Redirects to the specified whiteboard page |
| getCurrentBoard | Obtains the ID of the current whiteboard page |
| getBoardList | Obtains the whiteboard list of all files |
| setBoardRatio | Sets the aspect ratio of the current whiteboard page |
| getBoardRatio | Obtains the aspect ratio of the current whiteboard page |
| setBoardScale | Sets the scale of the current whiteboard page |
| getBoardScale | Obtains the scale of the current whiteboard page |
| setBoardContentFitMode | Sets the whiteboard content self-adaption mode |
| getBoardContentFitMode | Obtains the whiteboard content self-adaption mode |
| refresh | Refreshes the current whiteboard page and triggers the onTEBRefresh callback |
| syncAndReload | Synchronizes local data that failed to be sent to the remote end and refreshes the local data |

### File operation APIs
| API | Description |
| --- | --- |
| addImagesFile | Imports images in batches |
| applyFileTranscode | Initiates a file transcoding request |
| getFileTranscodeProgress | Actively queries the file transcoding progress |
| addTranscodeFile | Adds a file for transcoding |
| addImageElement | Adds image resources |
| deleteFile | Deletes a file |
| switchFile | Switches to another file |
| switchFile | Switches files |
| getCurrentFile | Obtains the current file ID |
| getFileInfoList | Obtains the file information list of all uploaded files on the whiteboard |
| getFileInfo | Obtains the file information of the specified file on the whiteboard |
| getFileBoardList | Obtains the whiteboard ID list of the specified file |
| clearFileDraws | Clears all whiteboard doodles of the specified file |
| getThumbnailImages | Obtains the thumbnail of the specified file, excluding the default file (fileId=#DEFAULT) |
| addVideoFile | Adds a video file |
| showVideoControl | Shows or hides the video control bar |
| playVideo | Plays a video |
| pauseVideo | Pauses a video |
| seekVideo | Goes to a specified time point in a video (only for VOD videos) |
| setSyncVideoStatusEnable | Sets whether to sync local video operations to the remote end |
| startSyncVideoStatus | Serves as an internal start timer that synchronizes the video status to the remote end according to the schedule (only for mp4 files) |
| stopSyncVideoStatus | Stops syncing the video status |
| addH5File | Adds an H5 file |
| snapshot | Creates a whiteboard snapshot |


## TEduBoardCallback
Callback API classes for whiteboard features 

| Class | Description |
| --- | --- |
| TEduBoardCallback | Whiteboard event callback API |

### General event callbacks
| API | Description |
| --- | --- |
| onTEBError | Whiteboard error callback |
| onTEBWarning | Whiteboard warning callback |

### Basic process callbacks
| API | Description |
| --- | --- |
| onTEBInit | Callback for whiteboard initialization completion |
| onTEBHistroyDataSyncCompleted | Callback for the completion of whiteboard historical data synchronization |
| onTEBSyncData | Whiteboard synchronization data callback |
| onTEBUndoStatusChanged | Callback for the whiteboard undo status change |
| onTEBRedoStatusChanged | Callback for the whiteboard redo status change |

### Doodle feature callbacks
| API | Description |
| --- | --- |
| onTEBImageStatusChanged | Callback for the whiteboard image status change |
| onTEBSetBackgroundImage | Callback for setting the whiteboard background image |
| onTEBAddImageElement | Callback for adding image elements |
| onTEBBackgroundH5StatusChanged | Callback for the whiteboard background H5 status change |

### Whiteboard page operation callbacks
| API | Description |
| --- | --- |
| onTEBAddBoard | Callback for adding a whiteboard page |
| onTEBDeleteBoard | Callback for deleting a whiteboard page |
| onTEBGotoBoard | Callback for redirecting to a whiteboard page |
| onTEBGotoStep | Callback for whiteboard page animation steps |
| onTEBRectSelected | Callback for the selection made by the selection tool |
| onTEBRefresh | Callback for refreshing a whiteboard |

### File operation callbacks
| API | Description |
| --- | --- |
| onTEBAddTranscodeFile | Callback for adding a file for transcoding |
| onTEBDeleteFile | Callback for deleting a file |
| onTEBSwitchFile | Callback for switching files |
| onTEBFileUploadProgress | File upload progress callback |
| onTEBFileUploadStatus | File upload status callback |
| onTEBFileTranscodeProgress | File transcoding progress callback |
| onTEBH5FileStatusChanged | H5 file status callback |
| onTEBAddImagesFile | Callback for adding a batch of image files |
| onTEBVideoStatusChanged | Video file status callback |
| onTEBSnapshot | Callback for creating a whiteboard snapshot |


## Definitions of Key Classes

| Class | Description |
| --- | --- |
| TEduBoardToolType | Whiteboard tool type |
| TEduBoardLineType | Line type |
| TEduBoardArrowType | Arrow type |
| TEduBoardOvalDrawMode | Oval drawing mode |
| TEduBoardImageFitMode | Alignment mode of whiteboard image filling |
| TEduBoardImageStatus | Whiteboard image status |
| TEduBoardTextStyle | Whiteboard text style |
| TEduBoardUploadStatus | Whiteboard upload status |
| TEduBoardBackgroundH5Status | H5 background status |
| TEduBoardContentFitMode | Whiteboard content self-adaption mode |
| TEduBoardFileTranscodeStatus | File transcoding status |
| TEduBoardVideoStatus | Video file status |
| TEduBoardH5FileStatus | H5 file status |
| TEduBoardAuthParam | Authorization parameters |
| TEduBoardColor | Color parameters |
| TEduBoardInfo | Whiteboard information |
| TEduBoardFileInfo | File information |
| TEduBoardInitParam | Whiteboard initialization parameters |
| TEduBoardLineStyle | Line style |
| TEduBoardTranscodeFileResult | File transcoding result |
| TEduBoardTranscodeConfig | File transcoding parameters |
| TEduBoardCursorIcon | Cursor icon |
| TEduBoardSnapshotInfo | Snapshot information |


## Error Codes

| Class | Description |
| --- | --- |
| TEduBoardErrorCode | Whiteboard error code (critical) |
| TEduBoardWarningCode | Whiteboard error code (warning) |


