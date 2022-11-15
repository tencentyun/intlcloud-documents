## Heartbeat Connection
This section describes how to maintain a heartbeat connection between the client and the backend. The heartbeat can be used to detect whether the user is still connected and used to collect and manage data such as user connection duration. In this way, if the user exits due to an error, the backend can more quickly repossess the concurrency the user was occupying, and make it available to other users.
### Sequence diagram
![](https://qcloudimg.tencent-cloud.cn/raw/ff17676e26edbdda33036b615fe6d55a.jpg)

### Directions
1. The client regularly sends heartbeat messages to the backend. The backend maintains the user connectivity based on the heartbeat messages.
2. The backend regularly checks whether the user is still connected. If the user heartbeat times out, the backend will call the [DestroySession()](https://intl.cloud.tencent.com/document/product/1158/49967) API to terminate the session and close the application, and the client will disconnect from the application.