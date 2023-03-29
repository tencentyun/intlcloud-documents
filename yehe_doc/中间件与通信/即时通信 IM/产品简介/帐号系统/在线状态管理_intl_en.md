
## Concepts
There are three user statuses:
- Running in the foreground (Online)
- Running in the background (PushOnline)
- Not logged in (Offline)

>!The PushOnline status exists only on mobile clients (Android, iOS, iPad) and does not exist on PC, macOS, Linux, or web clients.

### Running in the foreground (Online)
The Online status means that a smooth TCP connection is maintained between the client and the Chat server. In this condition, the client can send messages to the Chat server and receive messages from it.

**When a user opens an app, the status is Online.**

When an app starts, a TCP persistent connection is established between the client and the Chat server. The Chat server saves the online information of clients, such as network links, platforms, and versions. When the app is running, the Chat SDK regularly sends heartbeats to confirm the online status of the user.

>?Heartbeat: every two minutes, the Chat SDK sends a heartbeat packet to the server to confirm the online status of the user.

### Running in the background (PushOnline)
When a client is in the PushOnline status, the TCP persistent connection between the client and the Chat server is disconnected. In this case, messages pushed offline can be received.
In the following scenarios, the user’s status is PushOnline:

- After using an app, the user switches the app to the background, and then the app process is killed by the mobile phone operating system (OS) or the user directly kills the app process.
 If the app is in the keep-alive allowlist of the mobile phone OS, the OS will not kill the app process after the user switches the app to the background. In this case, the status is still Online. One criterion for distinguishing between Online and PushOnline is whether the app process is killed, that is, whether the TCP persistent connection between the client and Chat server is disconnected.
- The user disconnects the client from the network (for example, by enabling the airplane mode on the mobile phone) or the client’s network is completely unavailable (for example, when the user enters a tunnel).
 In such circumstances, the client cannot even send TCP FIN or RST packets, and it will take 400 seconds before the heartbeat packet times out. After that, the user’s status will change to PushOnline.

>!The PushOnline state exists only on mobile clients (Android, iOS, iPad) and does not exist on PC, macOS, Linux, mini program, and web clients.

### Not logged in (Offline)
Offline refers to the status before a user enters the username and password for login. In this case, the user cannot receive online and offline message pushes.
In the following scenarios, the user’s status is Offline:

- The user logs out or has not logged in to the app since downloading it.
- The user does not log in again within 7 days after the user’s status changes to PushOnline. In this case, the status changes to Offline.

## Querying the Online Status of Users
The app backend can query the online status of multiple users via the [v4/openim/querystate](https://intl.cloud.tencent.com/document/product/1047/35477) RESTful API.
Currently, the Chat SDK cannot get the online status of users.

## User Online Status Change Notifications
Chat can notify the app backend of user login and logout events. For more information, see [Status Change Callback](https://intl.cloud.tencent.com/document/product/1047/34357).

## Real-Time Status Change Detection
### Android/iOS/iPad/PC/macOS/Linux
In most cases, the changes of user status can be perceived in real time. For example:
- When a user logs in, the user’s status changes to Online.
- When a user logs out, the user’s status changes to Offline.
- When a user kills the client process or when a user switches the app to the background and the client process is killed by the mobile phone OS, the user’s status changes to PushOnline.

In the following special case, it will take 400 seconds before the heartbeat times out. After that, the Chat CVM instance can detect the status change:
When the network is completely unavailable and the client cannot even send TCP FIN or RST packets, it will take 400 seconds before the heartbeat times out. After that, the Chat CVM instance can perceive that the user’s status changes to PushOnline. This commonly occurs when the user disconnects the client from the network (for example, by enabling the airplane mode on the mobile phone) or the user enters a tunnel with no network signal.

### Web
When a user logs in on the web client, the Chat CVM can detect in real time that the user’s status changes to Online.

The timeliness of status change in various exit/disconnection scenarios is as follows:
- Page closing can be perceived in real time, and the user's status will change to Offline.
- It will take 60s before a network disconnection is perceived if the page is not closed, and the user's status will change to Offline.
- Actively calling the `destroy` API can be perceived in real time, and the status will change to Offline.

### Mini Program
When a user logs in on the mini program client, the Chat CVM can detect in real time that the user’s status changes to Online.

The timeliness of status change in various exit/disconnection scenarios is as follows:
- When the user clicks in the upper-right corner to exit, the status change to Offline can be perceived in 5s.
- When the user disconnects the client from the internet (for example, by enabling airplane mode on the phone), it will take 60s before the status change to Offline is perceived.
- Actively calling the `destroy` API can be perceived in real time, and the status will change to Offline.

## Multi-Device Login
### Force offline
By default, the Chat SDK does not allow multi-device login (for example, simultaneous login on a PC and an Android device). Instead, it forces the previous online device to go offline and allows only the last logged-in device to stay online. For more information on the force offline logic, see:

- [Multi-Client Login and Kickout](https://intl.cloud.tencent.com/document/product/1047/47971)


### Multi-device online
Chat allows you to modify the multi-client login policy in the [console](https://console.cloud.tencent.com/im). Currently, the following multi-client login policies are supported:
- Single-Platform login: a user can be online only on the Android, iPhone, iPad, Windows, macOS, or web platform.
- Dual-Platform login: a user can be concurrently online on the Android, iPhone, iPad, Windows, or macOS platform and the web platform.
- Triple-Platform login: a user can be concurrently online on the Android, iPhone, or iPad platform, the Windows or macOS platform, and the web platform.
- Multi-Platform login: a user can be concurrently online on the Android, iPhone, iPad, Windows, macOS, and web platforms.

By default, a user can be online on only one device for each platform (for example, one Android client will force another Android client to go offline). For users on Ultimate Edition, you can configure the maximum number of instances that they can log in to on the Android, iPhone, iPad, Windows, or macOS platform. In addition, you can configure the maximum number of instances that all users can log in to on the web platform.

Concurrent login is a key tool to improve the user experience. You can configure the maximum number of concurrent logins for a specific platform, so that forced logout won't occur when a user logs in to multiple devices on the same platform.
>?The "concurrent logins on multiple devices on the same platform" feature is only available on the Chat Ultimate edition. To use it, [purchase the Ultimate edition](https://www.tencentcloud.com/document/product/1047/34349). For more information, see [Pricing](https://www.tencentcloud.com/zh/document/product/1047/34349#.E5.9F.BA.E7.A1.80.E6.9C.8D.E5.8A.A1.E8.AF.A6.E6.83.85).
)。
