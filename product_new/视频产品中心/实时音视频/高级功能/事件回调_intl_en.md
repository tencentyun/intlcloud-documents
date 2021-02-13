The event callback service can notify your server of TRTC events in the form of HTTP/HTTPS requests. It has integrated certain events under the room event group and media event group. You can provide relevant configuration information to Tencent Cloud to activate this service.

<span id="deploy"></span>
## Configuration Information
You can configure callback information in the TRTC console. After completing the configuration, you can receive event callback notifications. <!--For detailed directions, please see [Callback Configuration](https://cloud.tencent.com/document/product/647/52428).-->


>!You need to prepare the following information in advance:
>- **Required**: HTTP/HTTPS server address for receiving callback notifications.
>- **Optional**: custom key used for signature calculation, which can contain up to 32 uppercase and lowercase letters and digits.

## Retry After Timeout
If the event callback server doesn't receive a response from your server within 5 seconds after sending a message notification, it will consider that the notification has failed. After the initial notification fails, it will retry immediately, and for subsequent failures, it will continue to retry at intervals of **10 seconds** until the message lasts for more than 1 minute.

<span id="format"></span>
## Event Callback Message Format

An event callback message is sent to your server as an HTTP/HTTPS POST request, where:

- Character encoding format: UTF-8.
- Request: the body format is JSON.
- Response: HTTP STATUS CODE = 200. The server ignores the specific content of the response packet. For more accurate connection, we recommend you add JSON: {"code":0} to the response.


## Parameter Description
<span id="message"></span>

### Callback message parameters

- The header of the event callback message contains the following fields:
<table id="header">
<tr><th>Field</th><th>Value</th></tr></thead><tr>
<td>Content-Type</td><td>application/json</td>
</tr><tr>
<td>Sign</td><td>Signature value</td>
</tr><tr>
<td>SdkAppId</td><td>SDK application ID</td>
</tr></table>
- The body of the event callback message contains the following fields:
<table id="body">
<tr><th>Field</th><th>Type</th><th>Description</th>
</tr><tr>
<td>EventGroupId</td><td>Number</td>
<td><a href="#eventId">Event group ID</a></td>
</tr><tr>
<td>EventType</td>
<td>Number</td>
<td><a href="#event_type">Event type in the callback notification</a></td>
</tr><tr>
<td>CallbackTs</td>
<td>Number</td>
<td>The Unix timestamp in milliseconds when the event callback server sends the callback request to your server</td>
</tr><tr>
<td>EventInfo</td>
<td>JSON Object</td>
<td><a href="#event_infor">Event information</a></td>
</tr>
</tbody></table>

<span id="eventId"></span>
### Event group ID

| Field            | Value   | Description       |
| ----------------- | ---- | ---------- |
| EVENT_GROUP_ROOM  | 1    | Room event group |
| EVENT_GROUP_MEDIA | 2    | Media event group |

<span id="event_type"></span>
### Event type

| Field                  | Value   | Description             |
| ----------------------- | ---- | ---------------- |
| EVENT_TYPE_CREATE_ROOM  | 101  | Room creation         |
| EVENT_TYPE_DISMISS_ROOM | 102  | Room dismissal         |
| EVENT_TYPE_ENTER_ROOM   | 103  | Room entry         |
| EVENT_TYPE_EXIT_ROOM    | 104  | Room exit         |
| EVENT_TYPE_START_VIDEO  | 201  | Video data push start |
| EVENT_TYPE_STOP_VIDEO   | 202  | Video data push end |
| EVENT_TYPE_START_AUDIO  | 203  | Audio data push start |
| EVENT_TYPE_STOP_AUDIO   | 204  | Audio data push end |
| EVENT_TYPE_START_ASSIT  | 205  | Substream data push start |
| EVENT_TYPE_STOP_ASSIT   | 206  | Substream data push end |

<span id="event_infor"></span>
### Event information

| Field  | Type   | Description                              |
| ------- | ------ | --------------------------------- |
| RoomId      |     String/Number       |     Room name (in the same type as the room ID on the client)    |
| EventTs | Number | Unix timestamp in seconds when the event occurs    |
| UserId  | String | User ID                            |
| Role    | Number | [Role type](#role_type) (option: carried during room entry/exit)  |
| Reason  | Number | [Specific reason](#reason) (option: carried during room entry/exit) |

<span id="role_type"></span>
### Role type

| Field             | Value   | Description |
| ------------------ | ---- | ---- |
| MEMBER_TRTC_ANCHOR | 20   | Anchor |
| MEMBER_TRTC_VIEWER | 21   | Viewer |


<span id="reason"></span>
### Specific reason

| Field | Description                                                         |
| ------ | ------------------------------------------------------------ |
| Room entry   | <li/>1: normal room entry<li/>2: network switch<li/>3: retry after timeout<li/>4: co-anchoring room entry |
| Room exit   | <li/>1: normal room exit<li/>2: exit after timeout<li/>3: local room exit after the user enters a room on another device<li/>4: room user deletion<li/>5: room exit after co-anchoring cancellation<li/>6: force kill |



### Signature calculation
A signature is calculated with the HMAC SHA256 encryption algorithm. After your event callback receiving server receives a callback message, it will calculate the signature in the same way. If the two signatures are the same, it means that the event callback is from TRTC and not forged. The signature calculation process is as follows:
```
// In the signature (Sign) calculation formula, `key` is the encryption key used to calculate the signature.
Sign = base64(hmacsha256(key, body))
```
