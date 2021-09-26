
## Concepts
There are three user statuses:
- Running in the foreground (Online)
- Running in the background (PushOnline)
- Not logged in (Offline)

>!The PushOnline status exists only on mobile clients (Android, iOS, and iPad) but not on PC, Mac, Linux, Mini Program, and web clients.

### Running in the foreground (Online)
The Online status means that a smooth TCP connection is maintained between the client and the IM server. In this condition, the client can send messages to the IM server and receive messages from it.

**When a user opens an app, the status is Online.**

When an app starts, a TCP persistent connection is established between the client and the IM server. The IM server saves the online information of clients, such as network links, platforms, and versions. When the app is running, the IM SDK regularly sends heartbeats to confirm the online status of the user.

>?Heartbeat: every two minutes, the IM SDK sends a heartbeat packet to the server to confirm the online status of the user.

### Running in the background (PushOnline)
When a client is in the PushOnline status, the TCP persistent connection between the client and the IM server is disconnected. In this case, messages pushed offline can be received.
In the following scenarios, the user’s status is PushOnline:

- After using an app, the user switches the app to the background, and then the app process is killed by the mobile phone operating system (OS) or the user directly kills the app process.
 If the app is in the keep-alive allowlist of the mobile phone OS, the OS will not kill the app process after the user switches the app to the background. In this case, the status is still Online. One criterion for distinguishing between Online and PushOnline is whether the app process is killed, that is, whether the TCP persistent connection between the client and IM server is disconnected.
- The user disconnects the client from the network (for example, by enabling the airplane mode on the mobile phone) or the client’s network is completely unavailable (for example, when the user enters a tunnel).
 In such circumstances, the client cannot even send TCP FIN or RST packets, and it will take 400 seconds before the heartbeat packet times out. After that, the user’s status will change to PushOnline.

>!The PushOnline status exists only on mobile clients (Android, iOS, and iPad) but not on PC, Mac, Linux, Mini Program, and web clients.

### Not logged in (Offline)
Offline refers to the status before a user enters the account and password for login. In this case, the user cannot receive online and offline message pushes.
In the following scenarios, the user’s status is Offline:

- The user logs out or has not logged in to the app since downloading it.
- The user does not log in again within 7 days after the user’s status changes to PushOnline. In this case, the status changes to Offline.

## Querying the Online Status of Users
The app backend can query the online status of multiple users via the [v4/openim/querystate](https://intl.cloud.tencent.com/document/product/1047/35477) RESTful API.
Currently, the IM SDK cannot get the online status of users.

## User Online Status Change Notifications
IM can notify the app backend of user login and logout events. For more information, see [Status Change Callback](https://intl.cloud.tencent.com/document/product/1047/34357).

## Real-Time Perception of Status Changes
### Android/iOS/iPad/PC/Mac/Linux
In most cases, the changes of user status can be perceived in real time. For example:
- When a user logs in, the user’s status changes to Online.
- When a user logs out, the user’s status changes to Offline.
- When a user kills the client process or when a user switches the app to the background and the client process is killed by the mobile phone OS, the user’s status changes to PushOnline.

In the following special case, it will take 400 seconds before the heartbeat times out. After that, the IM CVM instance can perceive the status change:
When the network is completely unavailable and the client cannot even send TCP FIN or RST packets, it will take 400 seconds before the heartbeat times out. After that, the IM CVM instance can perceive that the user’s status changes to PushOnline. This commonly occurs when the user disconnects the client from the network (for example, by enabling the airplane mode on the mobile phone) or the user enters a tunnel with no network signal.

### Web
When a user logs in on the web client, the IM CVM can perceive in real time that the user’s status changes to Online.

The timeliness of status change in various exit/disconnection scenarios is as follows:
- Page closing can be perceived in real time, and the user's status will change to Offline.
- It will take 60s before a network disconnection is perceived if the page is not closed, and the user's status will change to Offline.
- Actively calling the `destroy` API can be perceived in real time, and the status will change to Offline.

### Mini PROGRAM
When a user logs in on the Mini Program client, the IM CVM can perceive in real time that the user’s status changes to Online.

The timeliness of status change in various exit/disconnection scenarios is as follows:
- When the user clicks in the upper-right corner to exit, the status change to Offline can be perceived in 5s.
- When the user disconnects the client from the internet (for example, by enabling airplane mode on the phone), it will take 60s before the status change to Offline is perceived.
- When the user switches WeChat to the background, it will take about 30s before the status changes to Offline.
- Force stopping the WeChat process can be perceived in real time, and the status will change to Offline.
- Actively calling the `destroy` API can be perceived in real time, and the status will change to Offline.

## Multi-Device Login
### Force offline
By default, the IM SDK does not allow multi-device login (for example, simultaneous login on a PC and an Android device). Instead, it forces the previous online device to go offline and allows only the last logged-in device to stay online. For more information on the force offline logic, see:

- [Initialization (Android)](https://intl.cloud.tencent.com/document/product/1047/36255)
- [Initialization (iOS)](https://intl.cloud.tencent.com/document/product/1047/39159)


### Multi-Client login
IM allows you to modify the multi-client login policy in the [console](https://console.cloud.tencent.com/im). Currently, the following multi-client login policies are supported:
- Single-Platform login: a user can be online only on the Android, iPhone, iPad, Windows, Mac, or web platform.
- Dual-Platform login: a user can be concurrently online on the Android, iPhone, iPad, Windows, or Mac platform and the web platform.
- Triple-Platform login: a user can be concurrently online on the Android, iPhone, or iPad platform, the Windows or Mac platform, and the web platform.
- Multi-Platform login: a user can be concurrently online on the Android, iPhone, iPad, Windows, Mac, and web platforms.

By default, a user can be online on only one device for each platform (for example, one Android client will force another Android client to go offline). For users on Flagship Edition, you can configure the maximum number of instances that they can log in to on the Android, iPhone, iPad, Windows, or Mac platform. In addition, you can configure the maximum number of instances that all users can log in to on the web platform.
