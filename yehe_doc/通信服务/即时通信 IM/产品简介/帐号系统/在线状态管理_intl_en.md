
## Concepts
Each user has one of the following three statuses:
- Running in the foreground (Online)
- Running in the background (PushOnline)
- Not yet logged in (Offline)

>! The PushOnline status exists only on mobile terminals (Android/iOS) and does not exist on PC or web terminals.

### Running in the foreground (Online)
Online: when a client is online, a smooth TCP connection is maintained between the client and the IM server. In this case, the client can send messages to the IM server and receive messages from it.

**When a user opens an app, the status is Online.**

When the app starts, a TCP persistent connection is established between the client and the IM server. The IM server saves the online information of clients, such as network linkages and platform versions. The IM SDK sends regular heartbeats to confirm the online status of the user during app operations.

>? Heartbeat: every two minutes, the IM SDK sends a heartbeat packet to the server to confirm the user’s online status.

### Running in the background (PushOnline)
PushOnline: when a client is in the PushOnline status, the TCP persistent connection between the client and the IM server is disconnected. In this case, messages pushed offline can be received.
In the following scenarios, the user’s status is PushOnline:

- After using an app, the user switches the app to the background, and then the app process is killed by the mobile phone operating system or the user directly kills the app process.
 If the app is in the keep-alive allowlist of the operating system of the mobile phone, the app process will not be killed by the operating system after the user switches the app to the background. In that case, the status is still Online. One of the criteria for distinguishing between Online and PushOnline is whether the app process is killed, that is, whether the TCP persistent connection between the client and IM server is disconnected.
- The user disconnects the client from the network (for example, by enabling Airplane mode on the mobile phone) or the client’s network is completely unavailable (for example, when the user enters a tunnel).
 In such circumstances, the client cannot even send the FIN or RST packets over TCP, and the IM server will need to wait for the 400-second heartbeat timeout interval to expire before the user’s status changes to PushOnline.

>! The PushOnline status exists only on mobile terminals (Android/iOS) and does not exist on PC or web terminals.

### Not yet logged in (Offline)
Offline: this refers to the status before a user inputs the account and password for login. In this case, the user cannot receive messages pushed online or offline.
In the following scenarios, the user’s status is Offline:

- The user logs out or has not logged in to the app since downloading it.
- The user does not log in again within 7 days after the user’s status changes to PushOnline. In this case, the status changes to Offline.

## Querying Users’ Online Statuses
The app backend can query the online statuses of multiple users. For more information, see [RESTful API: Obtaining Users’ Online Statuses](https://intl.cloud.tencent.com/document/product/1047/35477).
Currently, the IM SDK cannot obtain users’ online statuses.

## User Online Status Change Notifications
IM can notify the app backend of user login and logout events. For more information, see [Status Change Callback](https://intl.cloud.tencent.com/document/product/1047/34357).

## Real-Time Perception of Status Changes
### Android, iOS, and PC
In most cases, users’ status changes can be perceived in real time. For example:
- When the user logs in, the user’s status changes to Online.
- When the user logs out, the user’s status changes to Offline.
- When the user kills the client process or when a user switches the app to the background and the client process is killed by the mobile phone operating system, the user’s status changes to PushOnline.

In the following special case, the IM CVM instance detects the status change only after the 400-second heartbeat timeout interval expires:
When the network is completely unavailable, and the client cannot even send the FIN or RST packets over TCP, the IM CVM instance will wait until the 400-second heartbeat timeout interval expires before perceiving that the user’s status has changed to PushOnline. This commonly occurs when the user disconnects the client from the network (for example, by enabling Airplane mode on the mobile phone) or the user enters a tunnel with no network signal.

### Web
When the user logs in on the web terminal, the IM CVM can perceive that the user’s status changes to Online in real time.
When a user’s network is unavailable or when a user directly closes the web page, the IM CVM needs to wait until the heartbeat timeout interval expires before perceiving that the user’s status changes to Offline.

## Multi-Device Login
### Force offline
By default, the IM SDK does not allow multi-device login (for example, simultaneous login on a PC and Android devices). Instead, it forces the previous online device to go offline and allows only the last logged-in device to stay online. For more information on the force offline logic, see:

- [Android user status change](https://intl.cloud.tencent.com/document/product/1047/36255)
- [iOS user status change]


### Multi-device online
You can modify the multi-device login policy in IM [Console](https://console.cloud.tencent.com/im) to allow users to stay online simultaneously on a PC and mobile phone, or on a PC, iOS device, and Android device. When multi-device login is enabled, users can stay online simultaneously on different devices with different platforms, but not on devices with the same platform. For example, simultaneous login on two iOS devices will trigger force offline.
