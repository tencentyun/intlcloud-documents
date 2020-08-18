## TEduBoardCallback
Whiteboard event callback API 

## Common Event Callbacks

### TEB_ERROR
Whiteboard error callback 
``` C++
function TEB_ERROR(TEduBoardErrorCode code, String msg)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| code | TEduBoardErrorCode | Error code. For more information, see the definitions of TEduBoardErrorCode |
| msg | String | Error information, which is UTF8-coded |


### TEB_WARNING
Whiteboard alarm callback 
``` C++
function TEB_WARNING(TEduBoardWarningCode code, String msg)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| code | TEduBoardWarningCode | Error code. For more information, see the definitions of TEduBoardWarningCode |
| msg | String | Error information, which is UTF8-coded |



## Basic Process Callbacks

### TEB_INIT
Whiteboard initialization completion callback 
``` C++
function TEB_INIT()
```
#### Description
If this callback is returned, the whiteboard is running normally (in this case, the whiteboard is blank and no historical data has been pulled) 


### TEB_HISTROYDATA_SYNCCOMPLETED
Callback for the completion of the whiteboard historical data synchronization 
``` C++
function TEB_HISTROYDATA_SYNCCOMPLETED()
```

### TEB_SYNCDATA
Whiteboard synchronization data callback 
``` C++
function TEB_SYNCDATA(Object data)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| data | Object | Whiteboard synchronization data |

#### Description
When this callback is returned, you need to send the callback data to other members in the room through signaling channels. After the recipients receive the callback data, call the AddSyncData API to add the data to the whiteboard to sync the data. This callback is used to sync data between multiple whiteboards. This callback is not returned during real-time data synchronization using Tencent Cloud IMSDK 


### TEB_OPERATE_CANUNDO_STATUS_CHANGED
Callback for the whiteboard undo status change 
``` C++
function TEB_OPERATE_CANUNDO_STATUS_CHANGED(Boolean canUndo)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| canUndo | Boolean | Whether the whiteboard allows undo operations |


### TEB_OPERATE_CANREDO_STATUS_CHANGED
Callback for the whiteboard redo status change 
``` C++
function TEB_OPERATE_CANREDO_STATUS_CHANGED(Boolean canRedo)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| canRedo | Boolean | Whether the whiteboard allows redo operations |



## Doodle Feature Callbacks

### TEB_IMAGE_STATUS_CHANGED
Callback for the whiteboard image status change 
``` C++
function TEB_IMAGE_STATUS_CHANGED(TEduBoardImageStatus status, Object data)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| status | TEduBoardImageStatus | New whiteboard image status |
| data | Object | Information about the current image |

#### Description
The format of the data parameter is as follows: 
``` 
{
     currentBoardId: "xxx",          //ID of the current whiteboard
     imgUrl: "http://xxxx",          //URL of the image to be loaded
     currentImgUrl: "http://xxxxx",  //Image URL in the current img label
}
```



### TEB_SETBACKGROUNDIMAGE
Callback for setting the whiteboard background image 
``` C++
function TEB_SETBACKGROUNDIMAGE(String fileName, String fileUrl, String userData)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileName | String | File name |
| fileUrl | String | File download address |
| userData | String | userData passed through the upload API |

#### Description
This callback is returned only when setBackgroundImage is called locally. When this callback is returned, the background image has been uploaded or downloaded successfully and is displayed 


### TEB_ADDIMAGEELEMENT
Callback for setting the whiteboard background image 
``` C++
function TEB_ADDIMAGEELEMENT(String fileName, String fileUrl, String userData)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileName | String | File name |
| fileUrl | String | File download address |
| userData | String | userData passed through the upload API |

#### Description
This callback is returned only when addImageElement is called locally. When this callback is returned, the background image has been uploaded or downloaded successfully and is displayed 


### TEB_H5BACKGROUND_STATUS_CHANGED
Callback for the whiteboard background H5 status change 
``` C++
function TEB_H5BACKGROUND_STATUS_CHANGED(TEduBoardBackgroundH5Status status, Object data)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| status | TEduBoardBackgroundH5Status | New whiteboard image status |
| data | Object | Current whiteboard background data |

#### Description
The format of the data parameter is as follows: 
``` 
{
     currentBoardId: "xxx",          //ID of the current whiteboard
     url: "http://xxxx",             //H5 background URL of the current whiteboard
}
```




## Whiteboard Page Operation Callbacks

### TEB_ADDBOARD
Callback for adding a whiteboard page 
``` C++
function TEB_ADDBOARD(Array boardList, String fileId)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| boardList | Array | List of IDs of the added whiteboard pages. After using a whiteboard page, you do not need to call the Release method to release it. The SDK will release it automatically |
| fileId | String | ID of the file to which the added whiteboard pages belong. The value must be ::DEFAULT in the current version |


### TEB_DELETEBOARD
Callback for deleting a whiteboard page 
``` C++
function TEB_DELETEBOARD(Array boardList, String fileId)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| boardList | Array | List of IDs of the deleted whiteboard pages. After using a whiteboard page, you do not need to call the Release method to release it. The SDK will release it automatically |
| fileId | String | ID of the file to which the deleted whiteboard pages belong. The value must be ::DEFAULT in the current version |


### TEB_GOTOBOARD
Callback for redirecting to a whiteboard page 
``` C++
function TEB_GOTOBOARD(String boardId, String fileId)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| boardId | String | ID of the whiteboard page to be redirected to |
| fileId | String | ID of the file to which the whiteboard page to be redirected to belongs |


### TEB_GOTOSTEP
Callback for the whiteboard page animation steps 
``` C++
function TEB_GOTOSTEP(Number currentStep, Number totalStep)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| currentStep | Number | Current step of the current whiteboard page animation. Value range: [0, totalStep) |
| totalStep | Number | Total number of steps of the current whiteboard page animation |


### TEB_RECTSELECTED
Callback for selecting certain content by the rectangle tool. This callback is triggered only after the tool selects a doodle or an image element 
``` C++
function TEB_RECTSELECTED()
```

### TEB_REFRESH
Callback for refreshing the current whiteboard page 
``` C++
function TEB_REFRESH()
```

### TEB_SNAPSHOT
Callback for creating a whiteboard snapshot 
``` C++
function TEB_SNAPSHOT(Object data)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| data | Object | Snapshot data |

#### Description
The format of the data parameter is as follows: 
``` 
{
     image: "",          //Base64
     userData: "",       //Passthrough data
}
```




## File Operation Callbacks

### TEB_TRANSCODEPROGRESS
File transcoding progress callback 
``` C++
function TEB_TRANSCODEPROGRESS(TEduBoardTranscodeFileResult result)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| result | TEduBoardTranscodeFileResult | File transcoding result |


### TEB_ADDTRANSCODEFILE
Callback for adding a file for transcoding 
``` C++
function TEB_ADDTRANSCODEFILE(String fileId)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | String | ID of the added file |

#### Description
This callback is triggered only after the file is loaded successfully 


### TEB_DELETEFILE
Callback for deleting a file 
``` C++
function TEB_DELETEFILE(String fileId)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | String | ID of the file to be deleted |


### TEB_SWITCHFILE
Callback for switching to another file 
``` C++
function TEB_SWITCHFILE(String fileId)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | String | ID of the file to be switched to |


### TEB_FILEUPLOADPROGRESS
File upload progress callback 
``` C++
function TEB_FILEUPLOADPROGRESS(Object data)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| data | Object | Progress-related information |

#### Description
The format of the data parameter is as follows: 
``` 
{
     loaded: 50,     //Size of the uploaded file in bytes
     total: 100,     //Total file size in bytes
     speed: 10,      //File upload speed in bytes/s
     percent: 0.5,   //File upload percentage in decimal format. For example, 0.5 indicates 50%
     userData: "xx", //userData passed through the upload API
     fid: "xxx"      //File ID
}
```



### TEB_FILEUPLOADSTATUS
File upload status callback 
``` C++
function TEB_FILEUPLOADSTATUS(TEduBoardUploadStatus status, Object data)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| status | TEduBoardUploadStatus | File upload status |
| data | Object | ID of the file being uploaded |

#### Description
The format of the data parameter is as follows: 
``` 
{
     code: 0,                    //Error code. 0: successful
     errorMsg: "xx",             //Error information
     fid: "xxx"                  //File ID
     fileName: "xx",             //File name
     fileUrl: "http://xxx",      //File download address
     picUrls: ["xx", "xx"],      //Preview address of each transcoded page
     userData: "xx",             //userData passed through the upload API
}
```



### TEB_FILEUPLOADPROGRESS
File upload progress callback 
``` C++
function TEB_FILEUPLOADPROGRESS(Object data)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| data | Object | Progress-related information |

#### Description
The format of the data parameter is as follows: 
``` 
{
     loaded: 50,     //Size of the uploaded file in bytes
     total: 100,     //Total file size in bytes
     speed: 10,      //File upload speed in bytes/s
     percent: 0.5,   //File upload percentage in decimal format. For example, 0.5 indicates 50%
     userData: "xx", //userData passed through the upload API
     fid: "xxx"      //File ID
}
```



### TEB_ADDIMAGESFILE
Callback for adding a file for transcoding 
``` C++
function TEB_ADDIMAGESFILE(String fileId)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| fileId | String | ID of the added file |

#### Description
This callback is triggered only after the file is loaded successfully 


### TEB_VIDEO_STATUS_CHANGED
Callback for setting the H5 file 
``` C++
function TEB_VIDEO_STATUS_CHANGED(Object data)
```
#### Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| data | Object | Callback data. The format of the data parameter is as follows: |

``` 
   {
        fileId: '',     //File ID
        status: 1,      //File status TEduBoardH5FileStatus
   }

  
   This callback can be received only when addH5File is called locally
  /
function TEB_H5FILE_STATUS_CHANGED(Object data);

```
