## Concepts
### Online
When a client is online, a smooth TCP connection is maintained between the client and the IM server. In this condition, the client can send messages to the IM server and receive messages from it.

When an app starts, a TCP persistent connection is established between the client and the IM server. The IM server saves the online information of clients, such as network linkages and platform versions. After the persistent connection is established, the IM SDK sends regular heartbeats to confirm the online status of the user during app operations. When the TCP connection between an iOS or Android client and IM is disconnected, the client continues to receive offline push messages even though it is not online.

>Heartbeat: Every two minutes, the IM SDK sends a heartbeat packet to the server to confirm the user’s online status.

### Connection
Connection refers to the action by which a TCP persistent connection is established between an app client and the IM server.

### Disconnection
Disconnection occurs in the following scenarios:
1. The app client logs out.
2. IM detects the disconnection of the TCP persistent connection between the app client and the IM server. The server relies on heartbeat packet timeout to determine disconnection. When no heartbeat packet is present between the client and the server for 400 seconds, the IM server determines that the user has gone offline exceptionally (this situation is more commonly seen on the Android platform.)
>To differentiate among online, connection, and disconnection, you need to check whether a network connection is present between the client and the IM backend. iOS and Android users can still receive offline push messages even when they are not online.

## Querying Users’ Online Statuses
The app backend can query the online status of multiple users. For more information, see [RESTful API: Obtaining Users’ Online Statuses](https://cloud.tencent.com/document/product/269/2566).
Currently, the IM SDK cannot obtain users’ online statuses.

## User Online Status Change Notifications
IM can notify the app backend of user connection and disconnection events. For more information, see [Status Change Callback](https://cloud.tencent.com/document/product/269/2570).


## Multi-Device Login
### Force offline
By default, the IM SDK does not allow multi-device login (for example, simultaneous login on a PC and Android devices). Instead, it forces the previous online device to go offline and allows only the last logged-in device to stay online. For more information on the force offline logic, see:

- [Android User Status Changes](https://cloud.tencent.com/document/product/269/9229#.E7.94.A8.E6.88.B7.E7.8A.B6.E6.80.81.E5.8F.98.E6.9B.B4)
- [iOS User Status Changes](https://cloud.tencent.com/document/product/269/9148#.E7.94.A8.E6.88.B7.E7.8A.B6.E6.80.81.E5.8F.98.E6.9B.B4)


### Multi-device online
You can modify the multi-device login policy in IM [Console](https://console.cloud.tencent.com/im) to allow users to stay online simultaneously on a PC and mobile phone, or on a PC, iOS device, and Android device. When multi-device login is enabled, users can stay online simultaneously on different devices with different platforms, but not on devices with the same platform. For example, simultaneous login on two iOS devices will trigger force offline.
