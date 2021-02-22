The event callback service can send notifications about TRTC events in the form of HTTP/HTTPS requests to your server. Currently, you can register callbacks for room events (`Room Event`) and media events (`Media Event`). Follow the directions below to configure callbacks in the TRTC console.

<span id="deploy"></span>
## Configuration Information
You can configure callbacks in the TRTC console. After configuration, you will receive notifications about TRTC events.


>?You need to provide the following information for the configuration:
>- **Required**: a HTTP/HTTPS server address to receive callback notifications
>- **Optional**: a custom key containing up to 32 uppercase and lowercase letters and digits, which is needed for the calculation of signatures

## Timeout and Retry
A notification will be considered failed if the callback server does not receive a response from your server within 5 seconds of message sending. It will try again immediately after the first failure and retry **10 seconds** after every subsequent failure. No retries will be made 1 minute after the first try.

<span id="format)"></span>
## Format of Callback Messages

Callback messages are sent to your server in the form of HTTP/HTTPS POST requests, which consist of the following parts.

- Character encoding: UTF-8
- Request: JSON for the request body
- Response: HTTP STATUS CODE = 200. The server ignores the content of the response packet. For protocol-friendliness, we recommend adding `JSON: `{"code":0}`` to the response.


## Parameters
<span id="message"></span>
### Callback message parameters

- The header of a callback message contains the following fields.
<table id="header">
<tr><th>Field</th><th>Value</th></tr></thead><tr>
<td>Content-Type</td><td>application/json</td>
</tr><tr>
<td>Sign</td><td>Signature value</td>
</tr><tr>
<td>SdkAppId</td><td>sdk application id</td>
</tr></table>
- The body of a callback message contains the following fields.
<table id="body">
<tr><th>Field</th><th>Type</th><th>Description</th>
</tr><tr>
<td>EventGroupId</td><td>Number</td>
<td><a href="#eventId">Event group ID</a></td>
</tr><tr>
<td>EventType</td>
<td>Number</td>
<td><a href="#event_type">Type of called back event</a></td>
</tr><tr>
<td>CallbackTs</td>
<td>Number</td>
<td>Unix timestamp (ms) of the sending of the callback request by the event callback server</td>
</tr><tr>
<td>EventInfo</td>
<td>JSON Object</td>
<td><a href="#event_infor">Event information</a></td>
</tr>
</tbody></table>

<span id="eventId)"></span>
### Event group ID

| Field            | Value   | Description       |
| ----------------- | ---- | ---------- |
| EVENT_GROUP_ROOM  | 1    | Room event group |
| EVENT_GROUP_MEDIA | 2    | Media event group |

<span id="event_type)"></span>
### Event type

| Field                  | Value   | Description             |
| ----------------------- | ---- | ---------------- |
| EVENT_TYPE_CREATE_ROOM  | 101  | Creating room         |
| EVENT_TYPE_DISMISS_ROOM | 102  | Closing room         |
| EVENT_TYPE_ENTER_ROOM   | 103  | Entering room        |
| EVENT_TYPE_EXIT_ROOM    | 104  | Exiting room          |
| EVENT_TYPE_START_VIDEO  | 201  | Starting pushing video data |
| EVENT_TYPE_STOP_VIDEO   | 202  | Stopping pushing video data |
| EVENT_TYPE_START_AUDIO  | 203  | Starting pushing audio data |
| EVENT_TYPE_STOP_AUDIO   | 204  | Stopping pushing audio data |
| EVENT_TYPE_START_ASSIT  | 205  | Starting pushing substream data |
| EVENT_TYPE_STOP_ASSIT   | 206  | Stopping pushing substream data |

<span id="event_infor)"></span>
### Event information

| Field  | Type   | Description                              |
| ------- | ------ | --------------------------------- |
RoomId      |     String/Number       |     Room ID (same type as Room ID on the client)    |
| EventTs | Number | Unix timestamp (in seconds) of event    |
| userID | String | User ID |
| Role    | Number | [Role type](#role_type) (option: carried during room entry/exit)  |
| Reason  | Number | [Reason](#reason) (option: carried during room entry/exit) |

<span id="role_type)"></span>
### Role type

| Field             | Value   | Description |
| ------------------ | ---- | ---- |
| MEMBER_TRTC_ANCHOR | 20   | Anchor |
| MEMBER_TRTC_VIEWER | 21   | Viewer |

<span id="reason)"></span>
### Reason

| Field    | Description                              |
| -------  | --------------------------------- |
|Room entry   |<li/>1: successful entry <li/>2: entry after network switch<li/>3: timeout and retry <li/>4: entry in co-anchoring |
|Room exit | <li/>1: successful exit <li/>2: exit due to timeout <li/>3: exit after the user entered the room via another client <li/>4: exit due to user deletion <li/>5: cancelling of co-anchoring <li/>6: force killing |



### Signature calculation
Signatures are calculated using the HMAC SHA256 encryption algorithm. Upon receiving a callback message, your server will calculate the signature using the same method, and if the result matches, it means that the callback is from TRTC and is not forged. See below for the calculation method.
```
// In the formula below, `key` is the secret key used to calculate a signature.
Sign = base64(hmacsha256(key, body))
```



