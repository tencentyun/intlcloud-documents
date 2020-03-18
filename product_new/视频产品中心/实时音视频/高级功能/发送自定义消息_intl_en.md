## Introduction

The TRTC SDK provides the ability to send custom messages. With this feature, any user can broadcast their own custom messages to other users in the same video room.

## Supported Platforms

| iOS | Android | macOS | Windows | WeChat Mini Program | Chrome Browser |
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|     ✔  |    ✔    |    ✔   |    ✔    |    ✖    |   ✖    |

## How It Works
A user's custom message will be combined into the audio/video data streams and transmitted to other users in the same room alongside. As audio/video channels themselves are not completely reliable, in order to improve the reliability, the TRTC SDK implements a reliability guarantee mechanism internally.

![](https://main.qcloudimg.com/raw/cc11b0e81970929ef28d2074c8297753.jpg)

## Sending Messages

Messages are sent by calling the `sendCustomCmdMsg` API of TRTCCloud, and the following four parameters need to be specified during sending:


| Parameter Name | Description |
|:--------:|:--------------|
| cmdID | Message ID. Value range: 1–10. Messages in different business types should use different `cmdIDs`. |
| data | Message to be sent, which can contain up to 1 KB (1,000 bytes) of data. |
| reliable | Whether reliable sending is enabled; if yes, the recipient needs to temporarily store the data of a certain period to wait for re-sending, which will cause certain delay. |
| ordered | Whether orderly sending is enabled, i.e., whether the data should be received in the same order in which it is sent; if yes, the recipient needs to temporarily store and sort messages, which will cause certain delay. |

>! `reliable` and `ordered` must be set to the same value (`YES` or `NO`) and cannot be set to different values currently.

- **Objective-C**

``` Objective-C
// Sample code for sending a custom message
- (void)sendHello {
    // Command word for the custom message. A set of rules needs to be customized according to the business needs. 0x1 is used as an example to send a text broadcast message
    NSInteger cmdID = 0x1;
    NSData *data = [@"Hello" dataUsingEncoding:NSUTF8StringEncoding];
    // `reliable` and `ordered` need to be consistent for now. Orderly sending is used as an example here
    [trtcCloud sendCustomCmdMsg:cmdID data:data reliable:YES ordered:YES];
}
```

- **Java**

``` java
// Sample code for sending a custom message
public void sendHello() {
    try {
        // Command word for the custom message. A set of rules needs to be customized according to the business needs. 0x1 is used as an example to send a text broadcast message
        int cmdID = 0x1;
        String hello = "Hello";
        byte[] data = hello.getBytes("UTF-8");
        // `reliable` and `ordered` need to be consistent for now. Orderly sending is used as an example here
        trtcCloud.sendCustomCmdMsg(cmdID, data, true, true);
				
    } catch (UnsupportedEncodingException e) {
        e.printStackTrace();
    }
}
```

- **C++**

``` C++
// Sample code for sending a custom message
void sendHello()
{
    // Command word for the custom message. A set of rules needs to be customized according to the business needs. 0x1 is used as an example to send a text broadcast message

    uint32_t cmdID = 0x1;
    uint8_t* data = { '1', '2', '3' };
    uint32_t dataSize = 3;  // Length of data

    // `reliable` and `ordered` need to be consistent for now. Orderly sending is used as an example here
    trtcCloud->sendCustomCmdMsg(cmdID, data, dataSize, true, true);
}
```
- **C#**

```c#
// Sample code for sending a custom message
private void sendHello()
{
    // Command word for the custom message. A set of rules needs to be customized according to the business needs. 0x1 is used as an example to send a text broadcast message

    uint cmdID = 0x1;
    byte[] data = { '1', '2', '3' };
    uint dataSize = 3;  // Length of data

    // `reliable` and `ordered` need to be consistent for now. Orderly sending is used as an example here
    mTRTCCloud.sendCustomCmdMsg(cmdID, data, dataSize, true, true);
}
```


## Receiving Messages

After a user in a room uses `sendCustomCmdMsg` to send a custom message, other users in the room can receive the message through the `onRecvCustomCmdMsg` API in the SDK callback.

- **Objective-C**

``` Objective-C
// Receive and process messages sent by other users in the room
- (void)onRecvCustomCmdMsgUserId:(NSString *)userId cmdID:(NSInteger)cmdId seq:(UInt32)seq message:(NSData *)message
{
	// Receive the message sent by `userId`
    switch (cmdId)  // `cmdId` agreed upon between sender and receiver
    {
    case 0:
        // Process the message with `cmdId` = 0
        break;
    case 1:
        // Process the message with `cmdId` = 1
        break;
    case 2:
        // Process the message with `cmdId` = 2
        break;
    default:
        break;
    }
}

```

- **Java**

``` java
// Inherit `TRTCCloudListener` and implement the `onRecvCustomCmdMsg` method to receive and process messages sent by others in the room
public void onRecvCustomCmdMsg(String userId, int cmdId, int seq, byte[] message) {
	// Receive the message sent by `userId`
    switch (cmdId)  // `cmdId` agreed upon between sender and receiver
    {
    case 0:
        // Process the message with `cmdId` = 0
        break;
    case 1:
        // Process the message with `cmdId` = 1
        break;
    case 2:
        // Process the message with `cmdId` = 2
        break;
    default:
        break;
    
}
```

- **C++**

``` C++
// Receive and process messages sent by other users in the room
void TRTCCloudCallbackImpl::onRecvCustomCmdMsg(
                            const char* userId, int32_t cmdId, uint32_t seq, const uint8_t* msg, uint32_t msgSize)
{
    // Receive the message sent by `userId`
    switch (cmdId)  // `cmdId` agreed upon between sender and receiver
    {
    case 0:
        // Process the message with `cmdId` = 0
        break;
    case 1:
        // Process the message with `cmdId` = 1
        break;
    case 2:
        // Process the message with `cmdId` = 2
        break;
    default:
        break;
    }
}
```

* **C#**

```c#
// Receive and process messages sent by other users in the room
public void onRecvCustomCmdMsg(string userId, int cmdId, uint seq, byte[] msg, uint msgSize)
{
    // Receive the message sent by `userId`
    switch (cmdId)  // `cmdId` agreed upon between sender and receiver
    {
    case 0:
        // Process the message with `cmdId` = 0
        break;
    case 1:
        // Process the message with `cmdId` = 1
        break;
    case 2:
        // Process the message with `cmdId` = 2
        break;
    default:
        break;
    }
}
```

## Use Limits

Since custom messages have a higher transmission priority than audio/video data, if too many of them are sent, audio/video data may be interfered with, resulting in video lagging or blurring. Therefore, the following frequency limits apply to custom messages:

- As custom messages are broadcast to all users in the same room, up to 30 messages can be sent per second.
- A data packet (i.e., data size) can be of up to 1 KB; if the threshold is exceeded, the packet is very likely to be discarded by the intermediate router or server.
- A client can send up to 8 KB of data in total per second, that is, if each data packet is of 1 KB, up to 8 packets can be sent per second.








