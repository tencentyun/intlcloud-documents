## TEduBoardController
Main API classes for whiteboard features 

| Class | Description |
| --- | --- |
| TEduBoardController | Whiteboard controller |

### Creating and terminating instances
| API | Description |
| --- | --- |
| CreateTEduBoardController | Creates a whiteboard controller instance. |
| DestroyTEduBoardController | Terminates the whiteboard controller. |

### Logging APIs
| API | Description |
| --- | --- |
| GetTEduBoardVersion | Obtains the SDK version number. |
| SetTEduBoardLogFilePath | Sets the whiteboard log file path. |

### Advanced feature APIs
| API | Description |
| --- | --- |
| EnableTEduBoardOffscreenRender | Enables whiteboard off-screen rendering. |
| GetTEduBoardRenderProcessHandler | Obtains the internal CefRenderProcessHandler of the SDK. |

### Setting TEduBoardCallback
| API | Description |
| --- | --- |
| AddCallback | Sets the event callback listener. |
| RemoveCallback | Deletes the event callback listener. |

### Basic process APIs
| API | Description |
| --- | --- |
| Init | Initializes the whiteboard. |
| GetBoardRenderView | Obtains the whiteboard rendering view. |
| Refresh | Refreshes the current whiteboard page and triggers the onTEBRefresh callback. |
| SyncAndReload | Syncs local data that failed to be sent to the remote end and refreshes the local data. |
| AddSyncData | Adds whiteboard synchronization data. |
| SetDataSyncEnable | Sets whether to enable data synchronization for the whiteboard. |
| IsDataSyncEnable | Checks whether data synchronization is enabled for the whiteboard. |
| Reset | Resets the whiteboard. |
| SetBoardRenderViewPos | Sets the position and size of the whiteboard rendering view. |
| GetSyncTime | Obtains the synchronization timestamp. |
| SyncRemoteTime | Syncs the remote timestamp. |
| CallExperimentalAPI | Calls the whiteboard experimental API. |

### APIs for Off-Screen Rendering Input Events
| API | Description |
| --- | --- |
| SendKeyEvent | Sends the keyboard event to the whiteboard. |
| SendMouseClickEvent | Sends the mouse click event to the whiteboard. |
| SendMouseMoveEvent | Sends the mouse movement event to the whiteboard. |
| SendMouseWheelEvent | Sends the mouse wheel event to the whiteboard. |
| SendTouchEvent | Sends the touch event to the whiteboard. |

### Doodle APIs
| API | Description |
| --- | --- |
| SetDrawEnable | Sets whether the whiteboard allows doodling. |
| IsDrawEnable | Check whether doodling is allowed for the whiteboard. |
| SetHandwritingEnable | Sets whether to enable handwriting for the whiteboard. |
| IsHandwritingEnable | Checks whether handwriting is enabled for the whiteboard. |
| SetAccessibleUsers | Sets users whose drawings can be operated. |
| SetGlobalBackgroundColor | Sets the background color of all whiteboards. |
| GetGlobalBackgroundColor | Obtains the global background color of whiteboards. |
| SetBackgroundColor | Sets the background color of the current whiteboard page. |
| GetBackgroundColor | Obtains the background color of the current whiteboard page. |
| SetToolType | Sets the whiteboard tool to use. |
| GetToolType | Obtains the whiteboard tool in use. |
| SetCursorIcon | Sets the cursor icon for the whiteboard tool. |
| SetBrushColor | Sets the brush color. |
| GetBrushColor | Obtains the brush color. |
| SetBrushThin | Sets the brush thickness. |
| GetBrushThin | Obtains the brush thickness. |
| SetTextColor | Sets the text color. |
| GetTextColor | Obtains the text color. |
| SetTextSize | Sets the text size. |
| GetTextSize | Obtains the text size. |
| SetTextStyle | Sets the text style. |
| GetTextStyle | Obtains the text style. |
| SetLineStyle | Sets the line style. |
| GetLineStyle | Obtains the line style. |
| SetOvalDrawMode | Sets the oval drawing mode. |
| GetOvalDrawMode | Obtains the oval drawing mode. |
| Clear | Clears doodles on the current whiteboard page. |
| SetBackgroundImage | Sets the background image of the current whiteboard page. |
| SetBackgroundH5 | Sets the background H5 page of the current whiteboard page. |
| Undo | Undoes the last action of the current whiteboard page. |
| Redo | Redoes the last undone action on the current whiteboard page. |

### Whiteboard page operation APIs
| API | Description |
| --- | --- |
| AddBoard | Adds a whiteboard page. |
| AddImageElement | Adds image resources. |
| AddElement | Add a whiteboard element. |
| RemoveElement | Deletes a whiteboard element. |
| DeleteBoard | Deletes a whiteboard page. |
| PrevStep | Goes to the previous step. Each step corresponds to an animation effect of the PowerPoint file. If no animation effect that has been displayed is available, calling this API redirects to the previous page. |
| NextStep | Goes to the next step. |
| PrevBoard | Goes to the previous page. |
| NextBoard | Goes to the next page. |
| GotoBoard | Redirects to the specified whiteboard page. |
| GetCurrentBoard | Obtains the ID of the current whiteboard page. |
| GetBoardList | Obtains the whiteboard list of all files. |
| SetBoardRatio | Sets the aspect ratio of the current whiteboard page. |
| GetBoardRatio | Obtains the aspect ratio of the current whiteboard page. |
| SetBoardScale | Sets the scale of the current whiteboard page. |
| GetBoardScale | Obtains the scale of the current whiteboard page. |
| SetBoardContentFitMode | Sets the whiteboard content self-adaption mode. |
| GetBoardContentFitMode | Obtains the whiteboard content self-adaption  mode. |
| Snapshot | Creates a whiteboard snapshot. |

### File operation APIs
| API | Description |
| --- | --- |
| ApplyFileTranscode | Initiates a file transcoding request. |
| GetFileTranscodeProgress | Actively queries the file transcoding progress. |
| AddTranscodeFile | Adds a file for transcoding. |
| AddImagesFile | Adds an image file. |
| AddVideoFile | Adds a video file. |
| ShowVideoControl | Shows or hides the video control bar. |
| PlayVideo | Plays a video. |
| PauseVideo | Pauses a video. |
| SeekVideo | Goes to a specified time point in a video (only for VOD videos). |
| SetSyncVideoStatusEnable | Sets whether to sync local video operations to the remote end. |
| StartSyncVideoStatus | Serves as an internal start timer that synchronizes the video status to the remote end according to schedule (only for mp4 files). |
| StopSyncVideoStatus | Stops syncing the video status. |
| AddH5File | Adds an H5 file. |
| DeleteFile | Deletes a file. |
| SwitchFile | Switches to another file. |
| GetCurrentFile | Obtains the current file ID. |
| GetFileInfo | Obtains the file information of the specified file on the whiteboard. |
| GetFileInfoList | Obtains the file information list of all uploaded files on the whiteboard. |
| GetFileBoardList | Obtains the whiteboard ID list of the specified file. |
| GetThumbnailImages | Obtains the thumbnail of the specified file, excluding the default file (fileId=#DEFAULT). |
| ClearFileDraws | Clears all whiteboard doodles of the specified file. |


## TEduBoardCallback
Callback API classes for whiteboard features 

| Class | Description |
| --- | --- |
| TEduBoardCallback | Whiteboard event callback delegate |

### Common event callbacks
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
| onTEBRectSelected | Callback after the rectangle selection tool selects certain content. This callback is triggered only after the tool selects a doodle or an image element. |
| onTEBRefresh | Callback for refreshing a whiteboard |
| onTEBOffscreenPaint | Whiteboard off-screen rendering callback |
| onTEBAudioCallbackStarted | Whiteboard audio startup callback |
| onTEBAudioCallbackPacket | Whiteboard audio packet callback |
| onTEBAudioCallbackStopped | Whiteboard audio stop callback |

### Doodle feature callbacks
| API | Description |
| --- | --- |
| onTEBImageStatusChanged | Callback for the whiteboard image status change |
| onTEBSetBackgroundImage | Callback for setting the whiteboard background image |
| onTEBAddImageElement | Callback for adding whiteboard image elements |
| onTEBAddElement | Callback for adding whiteboard elements |
| onTEBBackgroundH5StatusChanged | Callback for the whiteboard background H5 status change |

### Whiteboard page operation callbacks
| API | Description |
| --- | --- |
| onTEBAddBoard | Callback for adding a whiteboard page |
| onTEBDeleteBoard | Callback for deleting a whiteboard page |
| onTEBGotoBoard | Callback for redirecting to a whiteboard page |
| onTEBGotoStep | Callback for whiteboard page animation steps |
| onTEBSnapshot | Callback for creating a whiteboard snapshot |

### File operation callbacks
| API | Description |
| --- | --- |
| onTEBFileTranscodeProgress | File transcoding progress callback |
| onTEBAddTranscodeFile | Callback for adding a file for transcoding |
| onTEBAddImagesFile | Callback for adding a batch of image files |
| onTEBVideoStatusChanged | Video file status callback |
| onTEBH5FileStatusChanged | H5 file status callback |
| onTEBDeleteFile | Callback for deleting a file |
| onTEBSwitchFile | Callback for switching files |
| onTEBFileUploadProgress | File upload progress callback |
| onTEBFileUploadStatus | File upload status callback |


## Definitions of Key Classes

| Class | Description |
| --- | --- |
| TEduBoardAuthParam | Whiteboard authorization parameters |
| TEduBoardColor | Color parameters |
| TEduBoardInitParam | Whiteboard initialization parameters |
| TEduBoardLineStyle | Line style |
| TEduBoardCursorIcon | Cursor icon |
| TEduBoardSnapshotInfo | Snapshot information |
| TEduBoardTranscodeConfig | File transcoding parameters |
| TEduBoardTranscodeFileResult | File transcoding result |
| TEduBoardInfo | Whiteboard information |
| TEduBoardInfoList | Whiteboard information list |
| TEduBoardFileInfo | File information |
| TEduBoardKeyEvent | Keyboard event |
| TEduBoardMouseEvent | Mouse event |
| TEduBoardTouchEvent | Touch event |
| TEduBoardRect | Rectangle area |
| TEduBoardFileInfoList | File information list |
| TEduBoardStringList | String list |

#### Enumerated values
| Enumerated Value | Description |
| --- | --- |
| TEduBoardToolType | Whiteboard tool |
| TEduBoardElementType | Whiteboard element type |
| TEduBoardImageFitMode | Alignment mode of whiteboard image filling |
| TEduBoardImageStatus | Whiteboard image status |
| TEduBoardTextStyle | Whiteboard text style |
| TEduBoardUploadStatus | Whiteboard upload status |
| TEduBoardBackgroundH5Status | H5 background status |
| TEduBoardContentFitMode | Whiteboard content self-adaption mode |
| TEduBoardLineType | Line type |
| TEduBoardArrowType | Arrow type |
| TEduBoardOvalDrawMode | Oval drawing mode |
| TEduBoardFileTranscodeStatus | File transcoding status |
| TEduBoardH5FileStatus | H5 file status |
| TEduBoardVideoStatus | Video file status |
| TEduBoardKeyEventType | Keyboard event type |
| TEduBoardMouseButtonType | Mouse click type |
| TEduBoardTouchEventType | Touch event type |
| TEduBoardPointType | Point device type |
| TEduBoardEventFlag | Event flag |


## Error Codes

#### Enumerated values
| Enumerated Value | Description |
| --- | --- |
| TEduBoardErrorCode | Whiteboard error codes (critical) |
| TEduBoardWarningCode | Whiteboard error codes (warning) |


