## Description of the Server-Side Recording Callback[](id:date)

### Notes
Subject to the network conditions, the sequence of the notifications received by your server may be different from the sequence of the events that actually occurred.  
The service offers a retry mechanism, but it is not guaranteed that all messages can arrive.  
In view of the above, it is not recommended that your core business logic depend on the message notification service.

### Network protocol

If the callback URL, i.e., the URL of an HTTP(S) API, is configured in the console, then the POST method should be supported and transferred data should be encoded with UTF-8.

### HTTP header parameters

<table>
<tr><th>Parameter</th><th>Type</th><th>Required</th><th>Description</th></tr>
<tr>
<td>Signature</td>
<td>String</td>
<td>Yes</td>
<td>Signature. For more information, see <a href="#Signature">Signature generation</a>.</td>
</tr></table>

### Signature generation[](id:Signature)

Signature = HMAC-SH1 ( strContent, SecretKey )

- **strContent**: Original signature string, which is the entire JSON content of `body` (the length is subject to `Content-Length`).
- **body**: JSON content called back to the business. The entire content in [Sample callback](#example) is `body`.
- **SecretKey**: Application permission key, which can be viewed in **Details** in the [console](https://console.tencentcloud.com/gamegme).
- **HMAC-SH1**: Signature algorithm.


### Callback parameters

<table>
<thead><tr>
<th width="20%">Name</th>
<th width="20%">Type</th>
 <th width="60%">Description</th>  
</tr></thead>
<tbody><tr>
<td>BizID</td>
<td>Integer</td> 
<td>Application's `AppID`, which can be viewed in **Details** in the <a href="https://console.tencentcloud.com/gamegme">console</a>.</td> 
</tr>
<tr>
<td>RoomID</td>
<td>String</td> 
<td>Room ID</td> 
</tr>
<tr>
<td>UserID</td>
<td>String</td> 
<td>User ID</td> 
</tr>
<tr>
<td>RecordMode</td>
<td>Integer</td> 
<td >Recording mode. Valid values:<ul style="margin:0">
	<li/>`0`: Single stream
	<li/>`1`: Mixed stream
</ul ></td>
</tr>
<tr>
<td>Timestamp</td>
<td>Integer</td> 
<td>Timestamp in seconds when the callback is sent</td> 
</tr>
<tr>
<td>TaskID</td>
<td>Integer</td> 
<td>The task ID assigned by the cloud recording service, which uniquely identifies a recording process and becomes invalid after a recording task ends. When you use the custom recording mode, the task ID can be obtained through the response parameter when recording starts. It needs to be saved by the business as a request parameter for subsequent operations on the recording task.
</td> 
</tr>
<tr>
<td>EventType</td>
<td>Integer</td> 
<td>Event type</td> 
</tr>
</tr>
<tr>
<td>Detail</td>
<td><a href="#EventDetail">EventDetail</a></td> 
<td>Event details, whose format is specified by `EventType`.</td> 
</tr>
</table>



### `EventDetail` event details[](id:EventDetail)

| EventType | Description             | Detail                                                         |
| --------- | --------------- | ------------------------------------------------------------ |
| 1         | Recording started.   | <ul><li>`SeqNo`: Segment number of the `Number` type</li><li> `FileName`: Filename of the `String` type</li></ul> |
| 2         | Recording is completed.   | <ul><li>`SeqNo`: Segment number of the `Number` type</li><li> `FileName`: Filename of the `String` type</li></ul> |
| 3         | The audio file has been uploaded.   | <ul><li>`SeqNo`: Segment number of the `Number` type</li><li> `FileName`: Filename of the `String` type</li></ul> |


### Sample callback[](id:example)

```json
{
    "BizID":1400000000,
    "RoomID":"100",
    "UserID":"999",
    "TaskID":446946705284000000,
    "RecordMode":1,
    "Timestamp":1675930605,
    "EventType":1,
    "Detail":{
    	"SeqNo":0,
    	"FileName":"1400000000_100_999/2023-02-09-16-16-45_446946705284000000_audio.mp3"
    }
}
```