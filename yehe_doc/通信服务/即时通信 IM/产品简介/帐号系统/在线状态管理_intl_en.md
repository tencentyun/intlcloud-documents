## Concepts
Three types of user status are defined:
- Online: the frontend is running.
- PushOnline: the backend is running.
- Offline: the user is not logged in to the app.

> PushOnline only exists on mobile phones that run Android or iOS, not on PCs or web apps.

### Online
The Online status means that a smooth TCP connection is established between the client and the IM server. In this status, the client can send messages to the IM server and receive messages from it.

** When a user starts an app, the user is in the Online status.**

When an app starts, a TCP persistent connection is established between the client and the IM server. The IM server saves the online information of the client, such as network link information and platform version. When the app is running, the IM SDK periodically sends heartbeat packets to confirm the online status of the user.

> Heartbeat: the IM SDK sends a heartbeat packet to the server at an interval of 2 minutes to confirm the user’s online status.

### PushOnline
The PushOnline status means that the TCP persistent connection between the client and the IM server has been ended. At this time, the user can receive the offline push notifications of messages.
The user is in PushOnline status in the following scenarios:

- The app process is killed by the operating system of the mobile phone after the user no longer needs to use the app and switches the app to the background, or the user proactively kills the app process.
 If the app is in the keepalive allowlist of the operating system of the mobile phone, the app process will not be killed by the operating system of the mobile phone after the user switches the app to the background. At this time, the user is still in Online status. One of the criteria to distinguish Online from PushOnline is whether the app process has been killed, that is, whether the TCP persistent connection between the client and the IM server has been ended.
- The user proactively disconnects the client from the network, such as when a user enables airplane mode on the mobile phone, or the client network is completely unavailable, such as when the user enters a tunnel that does not have any network signal.
 In this special case, the client cannot even send the FIN or RST packet over TCP. When the IM server fails to receive any heartbeat packet within 400 seconds, the user status changes to PushOnline.

> PushOnline only exists on mobile phones that run Android or iOS, not on PCs or web apps.

### Offline
The Offline status means that the user does not enter the account and password for login. In this status, the user can receive neither online messages nor offline push notifications for messages.
The user is in Offline status in the following scenarios:

- The user logs out of the app, or has never logged in to the app after downloading the app.
- The user has not logged in to the app within 7 days after the user status changes to PushOnline.

## Querying Users' Online Status
The app backend can query the online status of multiple users by calling a RESTful API. For more information, see [RESTful API: Querying Users’ Online Status](https://intl.cloud.tencent.com/document/product/1047/35477).
Currently, the IM SDK cannot obtain users’ online status.

## User Online Status Change Notifications
IM can notify the app backend of the user connection and disconnection events. For more information, see [Status Change Callback](https://intl.cloud.tencent.com/document/product/1047/34357).

## Real-time Perception of Status Changes
For more information, see [Status Change Callback](https://intl.cloud.tencent.com/document/product/1047/34357#.E5.9B.9E.E8.B0.83.E7.9A.84.E5.AE.9E.E6.97.B6.E6.80.A7).

## Multi-Device Login
### Force offline
By default, the IM SDK does not allow multi-device login, for example, simultaneous login on a PC and an Android device. Instead, it forces the previous online device to go offline and allows only the last logged-in device to stay online. For more information on the force offline logic, see the following documents:

- [User status changes (Android)](https://intl.cloud.tencent.com/document/product/1047/34312)
- [User status changes (iOS)](https://intl.cloud.tencent.com/document/product/1047/34313)


### Multi-device online
You can modify the multi-device login policy in the IM [console](https://console.cloud.tencent.com/im) to allow users to stay online simultaneously on a PC and mobile phone, or on a PC, an iOS device, and an Android device. When multi-device login is enabled, users can stay online simultaneously on different devices with different platforms, but not on devices with the same platform. For example, simultaneous login on two iOS devices will trigger force offline.
