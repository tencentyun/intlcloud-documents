## Closing the Application
This section describes how to close the application. We recommend you release concurrencies promptly when the application is closed, so that the concurrencies can be made available to other users more quickly.

### Sequence diagram
![](https://qcloudimg.tencent-cloud.cn/raw/403c7649a628776ffdc0b12fbfee85f1.jpg)

### Directions
1. The business client actively requests the business backend to close the application.
2. The business backend calls the [DestroySession](https://intl.cloud.tencent.com/document/product/1158/49967) API to terminate the session and close the cloud application actively. Then, the business client disconnects from the cloud application.
