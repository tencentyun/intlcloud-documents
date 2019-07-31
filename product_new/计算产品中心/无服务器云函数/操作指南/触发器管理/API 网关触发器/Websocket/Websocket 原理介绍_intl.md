## How to Implement

The WebSocket protocol is a new network protocol based on TCP. It implements full-duplex communication between the browser and the server, i.e., allowing the server to actively send information to the client. WebSocket can send data to the client actively when there is a data push need on the server. In contrast, a server using the traditional HTTP protocol only allows a client to obtain the data that needs to be pushed through polling or long polling.

Since SCF is stateless and trigger-based (i.e., it will be triggered only when an event arrives), in order to implement WebSocket, SCF is used in conjunction with API Gateway to sustain and maintain the connection with the client through API Gateway. You can assume that API Gateway and SCF work together to implement the server. When sent by the client, a message is first passed to API Gateway which then triggers the SCF function. When the server function sends a message to the client, the function first posts the message to the reverse push link of API Gateway which then pushes the message to the client. The specific implementation architecture is as follows:
![](https://main.qcloudimg.com/raw/d51ee070556d8f6bb3be308f651bcc4b.png)

The entire lifecycle of WebSocket mainly consists of the following events:
- Connection establishment: The client requests to connect with the server and establishes a connection.
- Data upstream: The client sends data to the server through the established connection.
- Data downstream: The server sends data to the client through the established connection.
- Client disconnection: The client requests to close the established connection.
- Server disconnection: The server requests to close the established connection.

SCF and API Gateway handle the events throughout the lifecycle of WebSocket as follows:
- Connection establishment: The client establishes a WebSocket connection with API Gateway which sends a connection establishment event to SCF.
- Data upstream: The client sends data through WebSocket, and API Gateway forwards the data to SCF.
- Data downstream: SCF sends a request to the push address specified by API Gateway which then sends the data to the client through WebSocket.
- Client disconnection: The client requests to disconnect, and API Gateway sends a disconnection event to SCF.
- Server disconnection: SCF sends a disconnection request to the push address specified by API Gateway which closes the WebSocket connection after receiving the request.

Therefore, the interaction between API Gateway and SCF needs to be sustained by three types of functions:
- Registration function: This function is triggered when a WebSocket connection is requested and established between the client and API Gateway, notifying SCF of the secConnectionID of the WebSocket connection. The secConnectionID is usually recorded in the persistent store in this function for reverse push of subsequent data.
- Cleanup function: This function is triggered when the client initiates a WebSocket disconnection request, notifying SCF to prepare to disconnect the secConnectionID. The secConnectionID is usually cleaned from the persistent store in this function.
- Transfer function: This function is triggered when the client sends data through the WebSocket connection, notifying SCF of the secConnectionID of the connection and the data sent. Business data is usually processed in this function. For example, it determines whether to push data to other secConnectionIDs in the persistent storage.

>! When you need to actively push data to a secConnectionID or disconnect a secConnectionID, the reverse push address of API Gateway has to be used.

## Data Structures

### Connection establishment

1. When the client initiates a WebSocket connection establishment request, API Gateway encapsulates the agreed upon JSON data structures in the request body and sends it to the registration function using the HTTP POST method. You can get the request body from the function's event. Below is a sample:
```
{
  "requestContext": {
    "serviceName": "testsvc",
    "path": "/test/{testvar}",
    "httpMethod": "GET",
    "requestId": "c6af9ac6-7b61-11e6-9a41-93e8deadbeef",
    "identity": {
      "secretId": "abdcdxxxxxxxsdfs"
    },
    "sourceIp": "10.0.2.14",
    "stage": "prod",
    "websocketEnable":true
  },
  "websocket":{
    "action":"connecting",
    "secConnectionID":"xawexasdfewezdfsdfeasdfffa==",
    "secWebSocketProtocol":"chat,binary",
    "secWebSocketExtensions":"extension1,extension2"
  }
}
```
The data structures are detailed as below:
<table>
<tr><th>Structure name</th><th>Content</th></tr>
<tr>
 <td>requestContext</td>
 <td>Configuration information, request ID, authentication information, and source information of API Gateway where the request comes from. These include:
  <ul>
   <li>serviceName, path, and httpMethod: They point to API Gateway's service, API path, and method. </li>
	 <li>stage: It points to the environment where the request source API is located. </li>
	 <li>requestId: It identifies the unique ID of the current request. </li>
	 <li>identity: It identifies the user's authentication method and authentication information. </li>
	 <li>sourceIp: It identifies the request source IP. </li>
  </ul>
 </td>
</tr>
<tr>
 <td>websocket</td>
 <td>Details of connection establishment. These include:
   <ul>
   <li>action: The action of this request. </li>
	 <li>secConnectionID: A string that identifies the ID of the WebSocket connection. The original length is 128 bits, which is a Base64-encoded string with a total of 32 characters. </li>
	 <li>secWebSocketProtocol: String; optional field. </br>It represents the list of sub-protocols. If this field is in the original request, it will be passed to the function; otherwise, it does not appear. </li>
	 <li>secWebSocketExtensions: String; optional field. </br>It represents the list of expansions. If this field is in the original request, it will be passed to the function; otherwise, it does not appear. </li>
  </ul>
 </td>
</tr>
</table>

 >! The content of requestContext may be increased significantly during API Gateway iteration. At present, it is guaranteed that the content of the data structure will only be increased but not reduced, so that the existing structure will not be compromised.
2. When the registration function receives the connection establishment request, it needs to return the response message of whether to agree to establish the connection to API Gateway at the end of function handling. The response body has to be in JSON format, as shown in the sample below:
```
{
   "errNo":0, 
   "errMsg":"ok",
   "websocket":{
     "action":"connecting",
     "secConnectionID":"xawexasdfewezdfsdfeasdfffa==",
     "secWebSocketProtocol":"chat,binary",
     "secWebSocketExtensions":"extension1,extension2"
  }
}
```
The data structures are detailed as below:
<table>
<tr><th>Structure name</th><th>Content</th></tr>
<tr>
 <td>errNo</td>
 <td>Integer; required. </br>
 Response error code. If errNo is 0, the handshake succeeded and the connection was allowed to be established. </td>
</tr>
<tr>
 <td>errMsg</td>
 <td>String; required. </br>
 Cause of the error. If errNo is not 0, the errMsg field is valid. </td>
</tr>
<tr>
 <td>websocket</td>
 <td>Details of connection establishment. Where:
  <ul>
	 <li>action: The action of this request. </li>
	 <li>secConnectionID: A string that identifies the ID of the WebSocket connection. The original length is 128 bits, which is a Base64-encoded string with a total of 32 characters. </li>
	 <li>secWebSocketProtocol: String; optional field. </br>It is the value of a single sub-protocol. If this field is in the original request, it will be passed through to the client by API Gateway. </li>
	 <li>secWebSocketExtensions: String; optional field. </br>It is the value of a single extension. If this field is in the original request, it will be passed through to the client by API Gateway. </li>
	</ul>
 </td>
</tr>
</table>

 >! 
 > - If the SCF request times out, it will be deemed by default that the connection establishment failed.
 > - When API Gateway receives the response message from SCF, it checks the HTTP response code first. If the response code is 200, the response body was parsed. If the response code is not 200, it is deemed that SCF failed and connection establishment was refused.

### Data transfer

#### Upstream data transfer

##### Transfer request

When the client sends data through WebSocket, API Gateway encapsulates the agreed upon JSON data structures in the request body and sends it to the transfer function using the HTTP POST method. You can get the request body from the function's event. Below is a sample:
```
{
  "websocket":{
    "action":"data recv",
    "secConnectionID":"xawexasdfewezdfsdfeasdfffa==",
    "dataType":"text", 
    "data":"xxx"
  }
}
```
The data structures are detailed as below:
<table>
<tr><th>Parameter</th><th>Content</th></tr>
<tr><td>websocket</td><td>Details of data transfer. </td></tr>
<tr><td>action</td><td>The action of this request, such as "data recv". </td></tr>
<tr><td>secConnectionID</td><td>A string that identifies the ID of the WebSocket connection. The original length is 128 bits, which is a Base64-encoded string with a total of 32 characters.</td></tr>
<tr><td>dataType</td><td>Type of the transferred data. <ul><li>"binary": Binary. </li><li>"text": Text. </li></ul></td></tr>
<tr><td>data</td><td>The transferred data. If "dataType" is "binary", it is a Base64-encoded binary stream; if "dataType" is "text", it is a string. </td></tr>
<table>

##### Transfer response

After the transfer function finishes executing, it will return an HTTP response to API Gateway which will act according to the response code:
- If the response code is 200, the function was executed successfully.
- If the response code is not 200, a system failure occurred and API Gateway will actively send a FIN packet to the client.

>! API Gateway does not handle the content in the response body.

<span id="DownlinkDataCallback"></span>
#### Downstream data callback

##### Callback request

When SCF needs to push data to the client or actively disconnect, it can initiate a request, encapsulate the data in the request body, and send it to the reverse push address of API Gateway using the POST method. The request body has to be in JSON format, as shown in the sample below:
```
{
  "websocket":{
    "action":"data send", // Send data to the client
    "secConnectionID":"xawexasdfewezdfsdfeasdfffa==",
    "dataType":"text",
    "data":"xxx"
  }
}
```
```
{
  "websocket":{
    "action":"closing", // Send the disconnection request
    "secConnectionID":"xawexasdfewezdfsdfeasdfffa=="
  }
}
```
The data structures are detailed as below:

| Field | Content |
| ---------- | --- |
| websocket | Details of data transfer. |
|action | The action of this request, which can be "data send" or "closing": <ul><li>"data send": It is to send data to the client. </li><li>"closing": It is to initiate a disconnection request to the client, where the "dataType" and "data" are optional. </li></ul> |
|secConnectionID| A string that identifies the ID of the WebSocket connection. The original length is 128 bits, which is a Base64-encoded string with a total of 32 characters. |
|dataType | Type of the transferred data, including two types: <ul><li>"binary": Binary. </li> <li>"text": Text. </li></ul> |
|data | The transferred data: <ul><li>If "dataType" is "binary", it is a Base64-encoded binary stream. </li> <li>If "dataType" is "text", it is a string. </li></ul> |

##### Callback response

After the callback is over, the result of the callback can be determined based on the response code of API Gateway:
- If the response code is 200, the call succeeded.
- If the response code is not 200, a system failure occurred and API Gateway will actively send a FIN packet to the client.

In addition, the response body in JSON format can be obtained in the response result, as shown in the sample below:
```
{
   "errNo":0, 
   "errMsg":"ok"
}
```
The data structures are detailed as below:

| Field | Content |
| ---------- | --- |
| errNo | Integer; response error code. 0 means success. |
| errMsg | String; cause of the error. |


### Connection cleanup

#### The client actively disconnects

##### Logout request

When the client actively initiates a WebSocket disconnection request, API Gateway encapsulates the agreed upon JSON data structures in the request body and sends it to the cleanup function using the HTTP POST method. You can get the request body from the function's event. Below is a sample:
```
{
  "websocket":{
    "action":"closing",
    "secConnectionID":"xawexasdfewezdfsdfeasdfffa=="
  }
}
```
The data structures are detailed as below:

| Field | Content |
| ---------- | --- |
| websocket | Details of disconnection. |
| action | The action of this request, which is "closing" here. |
| secConnectionID | String. </br>This identifies the ID of the WebSocket connection. The original length is 128 bits, which is a Base64-encoded string with a total of 32 characters. |
>! In the cleanup function, you can get the secConnectionID from the event and delete the ID from the persistent store (such as a database).

##### Logout response

After the cleanup function finishes executing, it will return an HTTP response to API Gateway which will act according to the response code:
- If the response code is 200, the function was executed successfully.
- If the response code is not 200, a system failure occurred.

>! API Gateway does not handle the content in the response body.

#### The server actively disconnects

See **[Downstream data callback](#DownlinkDataCallback)**. SCF can initiate a request in the function, encapsulate the following data structures in the request body, and send it to the reverse push address of API Gateway using the POST method.
```
{
  "websocket":{
    "action":"closing", // Send the disconnection request
    "secConnectionID":"xawexasdfewezdfsdfeasdfffa=="
  }
}
```
>! When actively disconnecting the link with the client, you need to get the secConnectionID of the client's WebSocket, enter it in the data structure, and then delete the ID from the permanent store (such as a database).
