The event callback service can notify your server of TRTC events in the form of HTTP/HTTPS requests. It has integrated some events under the room event group and media event group. You can provide the callback configuration information required to enable the service.

[](id:deploy)
## Configuration Information
You can configure callback information in the TRTC console, and will receive event callback notifications after the configuration. For detailed directions, please see [Callback Configuration](https://intl.cloud.tencent.com/document/product/647/39559).


>!You need to provide the following information for the configuration:
>- **Required**: a HTTP/HTTPS server address to receive callback notifications
>- **Optional**: a custom key containing up to 32 uppercase and lowercase letters and digits, which is needed for the calculation of signatures

## Timeout and Retry
A notification will be considered failed if the callback server does not receive a response from your server within 5 seconds of message sending. It will try again immediately after the first failure and retry **10 seconds** after every subsequent failure. No retries will be made 1 minute after the first try.

[](id:format)
## Format of Callback Messages

Callback messages are sent to your server in the form of HTTP/HTTPS POST requests, which consist of the following parts.

- **Character encoding**: UTF-8
- **Request**: JSON for the request body
- **Response**: HTTP STATUS CODE = 200. The server ignores the content of the response packet. For protocol-friendliness, we recommend adding `JSON: `{"code":0}` to the response.
- **Package body sample**: below is an example of the package body for room entry under the room event group.
<dx-codeblock>
::: JSON JSON
{
	"EventGroupId": 1,        #Room event group
	"EventType": 103,        #Room entry event
	"CallbackTs": 1615554923704,        #Callback time, in milliseconds
	"EventInfo": {
		"RoomId": 12345,        #Numeric room number
		"EventTs": 1608441737,        #Event occurrence time, in seconds
		"UserId": "test",        #User ID
		"UniqueId": 1615554922656,        #Unique identifier
		"Role": 20,        #User role: anchor
		"Reason": 1        #Reason: voluntary entry
		}
}
:::
</dx-codeblock>



## Fields
[](id:message)
### Callback message fields

- The header of a callback message contains the following fields.
<table id="header">
<tr><th>Field</th><th>Value</th></tr></thead><tr>
<td>Content-Type</td><td>Application/JSON</td>
</tr><tr>
<td>Sign</td><td>Signature value</td>
</tr><tr>
<td>SdkAppId</td><td>SDK application ID</td>
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
<td>Unix timestamp (ms) when the event callback server sends the callback request</td>
</tr><tr>
<td>EventInfo</td>
<td>JSON Object</td>
<td><a href="#event_infor">Event information</a></td>
</tr>
</tbody></table>

[](id:eventId)
### Event group ID

| Field            | Value   | Description       |
| ----------------- | ---- | ---------- |
| EVENT_GROUP_ROOM  | 1    | Room event group |
| EVENT_GROUP_MEDIA | 2    | Media event group |

[](id:event_type)
### Event type

| Field                  | Value   | Description             |
| ----------------------- | ---- | ---------------- |
| EVENT_TYPE_CREATE_ROOM  | 101  | Creating room         |
| EVENT_TYPE_DISMISS_ROOM | 102  | Closing room         |
| EVENT_TYPE_ENTER_ROOM   | 103  | Entering room        |
| EVENT_TYPE_EXIT_ROOM    | 104  | Leaving room          |
|  EVENT_TYPE_CHANGE_ROLE   | 105  |    Switching roles      |
| EVENT_TYPE_START_VIDEO  | 201  | Starting pushing video data |
| EVENT_TYPE_STOP_VIDEO   | 202  | Stopping pushing video data |
| EVENT_TYPE_START_AUDIO  | 203  | Starting pushing audio data |
| EVENT_TYPE_STOP_AUDIO   | 204  | Stopping pushing audio data |
| EVENT_TYPE_START_ASSIT  | 205  | Starting pushing substream data |
| EVENT_TYPE_STOP_ASSIT   | 206  | Stopping pushing substream data |

[](id:event_infor)
### Event information

| Field  | Type   | Description                              |
| ------- | ------ | --------------------------------- |
RoomId      |     String/Number       |     Room ID (same type as Room ID on the client)    |
| EventTs | Number | Unix timestamp (s) of event occurrence    |
| userID | String | User ID |
| UniqueId  | Number | [Unique identifier](#UniqueId) (option: carried by the room event group)                            |
| Role    | Number | [Role type](#role_type) (option: carried during room entry/exit)  |
|TerminalType  |  Number    |   [Terminal type](#terminal) (option: carried during room entry) |
|UserType  |  Number   |    [User type](#usertype) (option: carried during room entry) |
| Reason  | Number | [Reason](#reason) (option: carried during room entry/exit) |

>?[](id:UniqueId) **Definition of unique identifier:** when a user experiences unusual events such as network change, abnormal exit and reentry, your callback server may receive multiple callbacks of the entry and exit of the same user. A unique identifier can help identify that the multiple exits and entries are from the same user.

[](id:role_type)
### Role type

| Field             | Value   | Description |
| ------------------ | ---- | ---- |
| MEMBER_TRTC_ANCHOR | 20   | Anchor |
| MEMBER_TRTC_VIEWER | 21   | Audience |


[](id:terminal)
### Terminal type
| Field             | Value   | Description |
| ------------------ | ---- | ---- |
| TERMINAL_TYPE_WINDOWS | 1 | Windows   |
| TERMINAL_TYPE_ANDRIOD | 2  | Android |
| TERMINAL_TYPE_IOS | 3  | iOS |
| TERMINAL_TYPE_LINUX | 4  | Linux |
| TERMINAL_TYPE_OTHER | 100  | Other |

[](id:usertype)
### User type
| Field             | Value   | Description |
| ------------------ | ---- | ---- |
| USER_TYPE_WEBRTC | 1 | WebRTC   |
| USER_TYPE_NATIVE_SDK | 3  | Native SDK |

[](id:reason)

### Reason

| Field    | Description                              |
| -------  | --------------------------------- |
|Room entry   |<li/>1: voluntary entry <li/>2: entry after network change<li/>3: timeout and retry <li/>4: entry in co-anchoring |
|Room exit | <li/>1: voluntary exit <li/>2: exit due to timeout <li/>3: exit because the user was removed from the room <li/>4: exit due to the cancelling of co-anchoring <li/>5: force killing|




### Signature calculation
Signatures are calculated using the HMAC SHA256 encryption algorithm. Upon receiving a callback message, your server will calculate the signature using the same method, and if the result matches, it means that the callback is from TRTC and is not forged. See below for the calculation method.
```
// In the formula below, `key` is the secret key used to calculate a signature.
Sign = base64(hmacsha256(key, body))
```

>! `body` is the original package body of the callback request you receive. Do not make any modifications. Below is an example.
>```
>body="{\n\t\"EventGroupId\":\t1,\n\t\"EventType\":\t103,\n\t\"CallbackTs\":\t1615554923704,\n\t\"EventInfo\":\t{\n\t\t\"RoomId\":\t12345,\n\t\t\"EventTs\":\t1608441737,\n\t\t\"UserId\":\t\"test\",\n\t\t\"UniqueId\":\t1615554922656,\n\t\t\"Role\":\t20,\n\t\t\"Reason\":\t1\n\t}\n}"
>```
```

```