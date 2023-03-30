
>## 1. Chat SDK Error Codes
>>?For web SDK error codes, see [here](https://web.sdk.qcloud.com/im/doc/en/module-ERROR_CODE.html). 
>
>### Common error codes
>
>| Error Code | Description                                                  |
>| ---------- | ------------------------------------------------------------ |
>| 4001       | File message failed: The corresponding URL is not a storage resource assigned by Chat. |
>| 4002       | File message failed: Internal server network error.          |
>| 4003       | Image message failed: Incorrect format returned by CI.       |
>| 4004       | Image message failed: Invalid image format.                  |
>| 4005       | File message failed: Illegal or blocked files cannot be sent. |
>| 6015       | Operation in progress. Optimize the control over API calls. For example, if another initialization operation is performed before the first initialization operation is called back, the system returns this error code. |
>| 6017       | Invalid parameter. Check the error information to locate the invalid parameter. |
>| 6022       | Local I/O operation error. Check whether you have the read/write permission or whether the disk is full. |
>| 6027       | Incorrect JSON format. Check the error information to locate the specific field. |
>| 6028       | Insufficient memory. A memory leak may occur. Analyze and identify the location with high memory usage by using the Instrument tool on the iOS platform or the Profiler tool on the Android platform. |
>| 6001       | PB parsing failed. Internal error.                           |
>| 6002       | PB serialization failed. Internal error.                     |
>| 6013       | The Chat SDK has not been initialized. Try again after the Chat SDK is initialized and the response is returned through callback. |
>| 6005       | Failed to load the local database, possibly due to file corruption. |
>| 6019       | Operation on the local database failed. This error may be caused by a lack of permissions for some directories or file corruption in the database. |
>| 7001       | Cross-thread error. Cross-thread operations are not supported. Internal error. |
>| 7002       | TinyId is empty. Internal error. Check whether the UserID exists and is valid. |
>| 7003       | Invalid UserID. A UserID cannot be empty and must be printable ASCII characters (0x20-0x7e) containing up to 32 bytes in length. |
>| 7004       | The file does not exist. Check whether the file path is correct. |
>| 7005       | The file size exceeds the limit. The maximum permitted size of an uploaded file is 100 MB. |
>| 7006       | The file is empty. The file cannot be 0 bytes. When uploading an image, audio, video, or document, ensure that the file is generated correctly. |
>| 7007       | Failed to open the file. Check whether the file exists or has been opened exclusively, which causes the SDK to fail to open it. |
>| 7008       | Exceeded the API call frequency limit. Check and control the API call frequency. |
>| 7009       | The SDK is terminated while it is executing. For example, the SDK execution is terminated by calling unInit during login. |
>| 7010       | The database operation failed.                               |
>| 7011       | The queried data does not exist in the database.             |
>| 7012       | An internal error occurred in the SDK.                       |
>| 7013       | The current package does not support this API. Please upgrade to the Flagship Edition package. |
>| 7014       | Invalid request. Check the API call meets requirements.      |
>| 7015       | Sensitive words found in SDK local content moderation.       |
>
>### Account error codes
>
>| Error Code | Description                                                  |
>| ---------- | ------------------------------------------------------------ |
>| 6014       | You have not logged in to the Chat SDK or have been forcibly logged out. Log in to the Chat SDK first and try again after a successful callback. To check whether you are online, use TIMManager getLoginUser. |
>| 6026       | This user account was not logged in during auto login. Call the login API to log in to the account again. |
>| 6206       | UserSig has expired. Get a new valid UserSig and log in again. For more information about how to get a UserSig, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
>| 6208       | You have been logged out because your account is logged in on another device. Please log in again. |
>| 7501       | Login in process. For example, if another login or autoLogin operation is performed before the first login or autoLogin operation is called back, the system returns this error code. |
>| 7502       | Logout in process. For example, if another logout operation is performed before the first logout operation is called back, the system returns this error code. |
>| 7503       | Failed to initialize the TLS SDK. Internal error.            |
>| 7504       | The TLS SDK has not been initialized. Internal error.        |
>| 7505       | The TRANS packet format of the TLS SDK is incorrect. Internal error. |
>| 7506       | Failed to decrypt the TLS SDK. Internal error.               |
>| 7507       | Failed to send the request to the TLS SDK. Internal error.   |
>| 7508       | Request to the TLS SDK timed out. Internal error.            |
>
>### Message error codes
>
>| Error Code | Description                                                  |
>| ---------- | ------------------------------------------------------------ |
>| 6004       | The session is invalid. Check your login status when initiating getConversation. If you initiate getConversation offline, the system returns this error code. |
>| 6006       | File transfer authentication failed. We recommend that you check whether the file format is correct. |
>| 6007       | Failed to get the server list via FTP.                       |
>| 6008       | Failed to upload the file via FTP. Check your network connection. If you want to upload an image, ensure that the image can be opened. |
>| 6031       | Failed to upload the file. Check whether the uploaded image can be opened properly. |
>| 6009       | Failed to download the file via FTP. Check whether your network is connected or whether the file or audio has expired. Currently, resource files are stored for up to 7 days. |
>| 6010       | HTTP request failed. Check whether the URL is valid. You can try to visit the URL via a web browser. |
>| 6016       | Invalid message elem of the Chat SDK. For more information, you can check the error information to locate the specific field. |
>| 6021       | Invalid object. The TIMImage object is user-generated or an incorrect value is assigned to the object. |
>| 8001       | The message length exceeds the limit of 12 KB. The length of a message is the sum of the lengths of all elements in the message, and the length of an element is the sum of the lengths of all fields of the element. |
>| 8002       | Message key error. This is an internal error. The key of the network request packet is not consistent with that of the response packet. |
>| 8003       | The image conversion HTTP request failed.                    |
>| 8004       | Thumbnail conversion failed due to reasons such as CI pornographic recognition. |
>| 8005       | The number of nested levels of combined forwarded messages exceeds the upper limit of 100. |
>| 8006       | Message modification conflict. The message that you request to modify is modified by another user. |
>| 8010       | The signaling request ID is invalid or has been processed.   |
>| 8011       | The signaling request is not authorized, such as canceling an invitation not initiated by the current user. |
>| 8012       | The signaling invitation already exists.                     |
>| 8020       | Failed to cancel the message because the message does not exist or has been sent successfully. |
>| 8021       | Failed to send the message because the message has been canceled. |
>
>### Group error codes
>
>| Error Code | Description                                                  |
>| ---------- | ------------------------------------------------------------ |
>| 8501       | Invalid group ID (unique group identifier). A custom group ID must be printable ASCII characters (0x20-0x7e) containing up to 48 bytes in length. To avoid confusion with the default group IDs assigned by Chat, a custom group ID cannot be prefixed with @TGS#. |
>| 8502       | Invalid group name. A group name can be up to 30 bytes in length and must be encoded in UTF-8. If the group name contains a Chinese character, the Chinese character may be expressed in multiple bytes. Check the length of the string in bytes. |
>| 8503       | Invalid group introduction. A group introduction can be up to 240 bytes in length and must be encoded in UTF-8. If the group introduction contains a Chinese character, the Chinese character may be expressed in multiple bytes. Check the length of the string in bytes. |
>| 8504       | Invalid group notice. A group notice can be up to 300 bytes in length and must be encoded in UTF-8. If the group notice contains a Chinese character, the Chinese character may be expressed in multiple bytes. Check the length of the string in bytes. |
>| 8505       | Invalid URL of the group profile photo. The URL of a group profile photo can be up to 100 bytes in length. You can try to access the URL via a web browser. |
>| 8506       | Invalid group name card. A group name card can be up to 50 bytes in length and must be encoded in UTF-8. If the group name card contains a Chinese character, the Chinese character may be expressed in multiple bytes. Check the length of the string in bytes. |
>| 8507       | Exceeded the maximum number of group members allowed upon group creation and invitation. For the Pro Edition, a group can contain up to 200 members, which can be extended to 2,000. For the Ultimate Edition, a group can contain up to 2,000 members, which can be extended to 6,000. Audio-video chat groups and broadcasting chat rooms have no limit on the number of members in a group. |
>| 8508       | A private group cannot be joined via app. Any group member can invite non-members to join the group without the invitees' confirmation. |
>| 8509       | You cannot invite a group member whose role is group owner. Ensure that the role field is entered correctly. |
>| 8510       | You cannot invite 0 members. Ensure that the member field is entered correctly. |
>| 8511       | Group attribute API operation limits: the Create, Delete, and Update APIs each can be called by the backend for up to five times per second. The Read API can be called by the SDK for up to 20 times per five seconds. |
>| 8512       | Operation limit of the API for getting the number of online users: The Read API can be called only once per 60 seconds. |
>| 8513       | Operation limit of the API for getting profiles: The Read API can be called only once per second. |
>| 8514       | Operation limit of the API for getting the list of groups that you have joined: The Read API can be called only once per second. |
>| 8515       | Group member marking is not allowed.                         |
>
>
>### Relationship chain error codes
>
>| Error Code | Description                                                  |
>| ---------- | ------------------------------------------------------------ |
>| 9001       | Invalid profile field. The profile supports standard fields and custom fields. The keyword in a custom field must contain letters and can be up to 8 bytes in length. A custom field cannot exceed 500 bytes in length. |
>| 9002       | Invalid remarks. The remarks field can be up to 96 bytes in length and must be encoded in UTF-8. If the remarks field contains a Chinese character, the Chinese character may be expressed in multiple bytes. Check the length of the string in bytes. |
>| 9003       | Invalid friend request. The friend request field can be up to 120 bytes in length and must be encoded in UTF-8. If the friend request field contains a Chinese character, the Chinese character may be expressed in multiple bytes. Check the length of the string in bytes. |
>| 9004       | The source field of the friend request is invalid. The source field must be prefixed with “AddSource_Type\_”. |
>| 9005       | Invalid friend list name. A friend list name cannot be empty, can be up to 30 bytes in length, and must be encoded in UTF-8. If the friend list name contains a Chinese character, the Chinese character may be expressed in multiple bytes. Check the length of the string in bytes. |
>| 9006       | Exceeded the quantity limit.                                 |
>
>### Network error codes
>
>| Error Code | Description                                                  |
>| ---------- | ------------------------------------------------------------ |
>| 9501       | SSO encryption failed. Internal error.                       |
>| 9502       | SSO decryption failed. Internal error.                       |
>| 9503       | SSO has not been authenticated. The login process may not be completed. Complete the login process and then try again. |
>| 9504       | Failed to compress the data packet. Internal error.          |
>| 9505       | Failed to decompress the data packet. Internal error.        |
>| 9506       | The call frequency exceeds the frequency limit. You can initiate up to 5 requests per second. |
>| 9507       | The network request queue exceeds the maximum number (1,000) of concurrent requests allowed. For example, when users keep sending messages when the network is abnormal, the network request queue will keep adding new requests without consumption and quickly reach the maximum number of requests. |
>| 9508       | The network is disconnected, no connection has been set up, or no network is detected when setting up a socket connection. |
>| 9509       | A network connection has been established, but is created repeatedly. Internal error. |
>| 9510       | Network connection setup timed out. Try again after the network recovers. |
>| 9511       | The network connection setup has been rejected by the server due to frequent connection requests. |
>| 9512       | No available route to the network. Try again after the network recovers. |
>| 9513       | Insufficient buffer capacity for calls. The system is too busy. Internal error. |
>| 9514       | The peer end has reset the connection, possibly because the server is overloaded. The SDK automatically initiates reconnection. Try again after the network is reconnected and the callback function `onConnSucc` on iOS or `onConnected` on Android is called successfully. |
>| 9515       | Invalid socket. Internal error.                              |
>| 9516       | Failed to parse the IP address. Internal error. The local `imsdk_config` file may be corrupted and can cause the system to read an invalid IP address. |
>| 9517       | Invalid connection. The network is connected to an intermediate node or is reset by the server. This is an internal error. The SDK automatically initiates reconnection. Try again after the network is reconnected and the callback function `onConnSucc` on iOS or `onConnected` on Android is called successfully. |
>| 9518       | The request packet timed out when waiting to enter the sending queue. This usually occurs when the network connection setup is slow or the network is frequently disconnected and reconnected. Check whether the network connection is normal. |
>| 9519       | The request packet entered the Chat SDK sending queue but timed out while waiting to enter the network layer of the operating system. This usually occurs when the local network is restricted or disconnected or the local network and the Chat SDK backend are not connected. We recommend that you run the Chat SDK in different network environments to check whether this issue is caused by the current network environment. |
>| 9520       | The request packet entered the network layer of the operating system from the Chat SDK sending queue but timed out while waiting for a response packet from the server. This usually occurs when the local network is restricted or disconnected or the local network and the Chat SDK backend are not connected. We recommend that you run the Chat SDK in different network environments to check whether this issue is caused by the current network environment. |
>| 9521       | The request packet has entered the sending queue, certain data has been sent, but the remaining data timed out when waiting to be sent. This usually occurs because the upstream bandwidth is insufficient or the network is connected when the error is called back. Please check whether the network connection is normal. |
>| 9522       | The request packet length exceeds the maximum limit of 1 MB. |
>| 9523       | The request packet has entered the sending queue but timed out when waiting to enter the network buffer of the system. This usually occurs because too many packets are to be sent, the sending thread is too busy to handle the packets, or the network is disconnected when the error code is called back. |
>| 9524       | The request packet has entered the network buffer of the system but timed out when waiting for the server to return packets. This usually occurs because the request packet does not leave the client device, is discarded in an intermediate route, or is dropped accidentally by the server, the response packet is discarded by the network layer of the system, or the network is disconnected when the error code is called back. |
>| 9525       | The request packet has entered the sending queue, certain data has been sent, but the remaining data timed out when waiting to be sent. This usually occurs because the upstream bandwidth is insufficient or the network is disconnected when the error code is called back. Please check whether the network connection is normal. |
>
>## 2. Server Error Codes
>
>### Access layer error codes
>
>| Error Code | Description                                                  |
>| ---------- | ------------------------------------------------------------ |
>| -302       | The number of server connections exceeds the limit. The server refused to provide services. |
>| -10001     | Key expired. A key is an internal credential generated based on the UserSig. The validity period of a key is less than or equal to that of the UserSig. Call the `TIMManager.getInstance().login` API again to generate a new key. |
>| -10003     | Ticket expired. A ticket is an internal credential generated based on the UserSig. The validity period of a ticket is less than or equal to that of the UserSig. Call the `TIMManager.getInstance().login` API again to generate a new ticket. |
>| -10004     | Ticket verification failed. Call the `TIMManager.getInstance().login` API again to generate a new ticket. |
>| -10005     | The key cannot be empty.                                     |
>| -10006     | The account in `Key` does not match the account in the request packet header. |
>| -10007     | Verification code delivery timed out.                        |
>| -10008     | The key and ticket are required.                             |
>| -10009     | Cookie mismatch.                                             |
>| -10106     | Decryption with the key failed too many times. Instruct the device to call the `TIMManager.getInstance().login` API to generate a new key. |
>| -10108     | Overdue prepayment.                                          |
>| -10109     | The format of the request packet is incorrect.               |
>| -10110     | The SDKAppID is blocklisted.                                 |
>| -10111     | The SDKAppID is on the service CMD blocklist.                |
>| -10112     | The SDKAppID has been disabled.                              |
>| -10113     | The request exceeds the frequency limit allowed for the user. The frequency limit is set for the number of requests per second based on a specific protocol. |
>| -10114     | Packet loss due to system overload. The connected server has too many requests to process and therefore refuses to provide services. |
>| -20009     | The frequency of terminals accessing APIs exceeds the limit. |
>
>### Resource file error codes
>
>| Error Code | Description                                                  |
>| ---------- | ------------------------------------------------------------ |
>| 114000     | The resource file to be sent does not exist.                 |
>| 114001     | The resource file to be sent cannot be accessed.             |
>| 114002     | The file size exceeds the limit allowed.                     |
>| 114003     | Sending canceled by the user. For example, the user logs out in the sending process. |
>| 114004     | Failed to read the file.                                     |
>| 114005     | Resource file (such as an image, document, audio, or video) transfer timed out, usually due to network issues. |
>| 114011     | Invalid parameter.                                           |
>| 115066     | File MD5 verification failed.                                |
>| 115068     | Segment MD5 verification failed.                             |
>
>### Common backend error codes
>
>| Error Code | Description                                                  |
>| ---------- | ------------------------------------------------------------ |
>| 60002      | An error occurred when parsing the HTTP request. Check the format of the HTTP request URL. |
>| 60003      | An error occurred when parsing the JSON data of the HTTP request. Check the JSON format. |
>| 60004      | `UserID` or `UserSig` in the request URI or JSON packet is incorrect. |
>| 60005      | `UserID` or `UserSig` in the request URI or JSON packet is incorrect. |
>| 60006      | Invalid SDKAppID. Check the validity of the SDKAppID.        |
>| 60007      | The RESTful API call exceeds the frequency limit. Please reduce the request frequency. |
>| 60008      | The service request timed out or the format of the HTTP request is incorrect. Please check and try again. |
>| 60009      | Requested resource error. Please check the request URL.      |
>| 60010      | Set the `UserID` field of the RESTful API request to the admin account of the app. |
>| 60011      | The SDKAppID request exceeds the frequency limit. Please reduce the request frequency. |
>| 60012      | SDKAppID is required when calling the RESTful API. Check the SDKAppID in the request URL. |
>| 60013      | An error occurred when parsing the JSON data in the HTTP response packet. |
>| 60014      | Account switching timed out.                                 |
>| 60015      | The type of the UserID in the request packet is incorrect. Ensure that the UserID is in string format. |
>| 60016      | The SDKAppID is disabled.                                    |
>| 60017      | The request is disabled.                                     |
>| 60018      | Too many requests. Try again later.                          |
>| 60019      | Too many requests. Try again later.                          |
>| 60020      | Your Pro Edition standard billing plan has expired and been disabled. To repurchase the standard billing plan, log in to [Instant Messaging Purchase Page](https://buy.cloud.tencent.com/avc). The new standard billing plan will take effect 5 minutes later. |
>| 60021      | The source IP of the RESTful API call is invalid.            |
>| 80001      | The text in the message contains sensitive content and cannot be delivered. |
>| 80002      | The outgoing message packet exceeds the length limit of 8 KB. Reduce the packet size and try again. |
>| 80003      | The message was not sent because the callback failed or timed out before the one-to-one or group message was sent. Configure the [policy for handling callback timeouts before event occurrence](https://intl.cloud.tencent.com/document/product/1047/34354) in the console. |
>| 80004      | The image in the message contains sensitive content and cannot be delivered. |
>
>
>### Account error codes
>
>| Error Code | Description                                                  |
>| ---------- | ------------------------------------------------------------ |
>| 70001      | UserSig expired. Please generate a new one. It is recommended that the UserSig validity period be set to not less than 24 hours. |
>| 70002      | The value of UserSig is 0 bytes. Check whether the passed-in UserSig is correct. |
>| 70003      | Invalid UserSig. Call the API provided on the official website to [generate a UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
>| 70005      | Invalid UserSig. Call the API provided on the official website to [generate a UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
>| 70009      | UserSig authentication failed, probably because the private key or key of another SDKAppID was mistakenly used to generate the UserSig. Use the private key or key of the desired SDKAppID to [generate a UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
>| 70013      | The UserID in the request does not match the UserID used to generate the UserSig. You can verify the UserSig on the **[Auxiliary Tools](https://console.cloud.tencent.com/im/tool-usersig)** page of the Chat console. |
>| 70014      | The SDKAppID in the request does not match the SDKAppID used to generate the UserSig. You can verify the UserSig on the **[Auxiliary Tools](https://console.cloud.tencent.com/im/tool-usersig)** page of the Chat console. |
>| 70016      | UserSig authentication failed because the public key does not exist. [Obtain the key](https://intl.cloud.tencent.com/document/product/1047/34540) in the Chat console. |
>| 70020      | SDKAppID not found. Check the app information in the Chat console. |
>| 70050      | Too many UserSig authentication attempts. Check whether the UserSig is correct and try again in one minute. You can verify the UserSig on the **[Auxiliary Tools](https://console.cloud.tencent.com/im/tool-usersig)** page of the Chat console. |
>| 70051      | The account is blocklisted.                                  |
>| 70107      | The requested UserID does not exist.                         |
>| 70114      | Login is restricted for security reasons. Please reduce the login frequency. |
>| 70169      | Server timeout. Try again later.                             |
>| 70202      | Server timeout. Try again later.                             |
>| 70206      | Invalid batch quantity in the request.                       |
>| 70402      | Invalid parameter. Check whether the required fields are all set and whether the parameter settings meet the protocol requirements. |
>| 70403      | Request failed. App admin permissions are required to perform this operation. |
>| 70398      | The number of accounts exceeds the limit allowed. To create more than 100 accounts, upgrade your app to the Pro Edition. For specific steps, see [Purchase Guide](https://www.tencentcloud.com/document/product/1047/36021). |
>| 70500      | Internal server error. Try again later.                      |
>| 71000      | Failed to delete the account. Only Free accounts can be deleted. Your current app is of the Pro Edition and therefore cannot be deleted. |
>| 72000      | Your app is now using the Trial Edition, and the free daily active users (DAU) quota was exceeded. To lift the restriction, upgrade your app to the Pro Edition or Flagship Edition. For detailed directions, see [Purchase Guide](https://www.tencentcloud.com/document/product/1047/36021). |
>| 72001      | Please enable user status query and status change notification settings in the Chat console. For operation details, see [Operation Guide](https://intl.cloud.tencent.com/document/product/1047/49562). |
>
>### Profile error codes
>
>| Error Code | Description                                                  |
>| ---------- | ------------------------------------------------------------ |
>| 40001      | Incorrect request parameters. Check the request parameters based on the error description. |
>| 40002      | Incorrect request parameters. You need to specify the user account whose profile is to be pulled. |
>| 40003      | The requested user account does not exist.                   |
>| 40004      | The request requires the app admin permission.               |
>| 40006      | Internal server error. Try again later.                      |
>| 40007      | No permission to read profile fields. For more information, see [Profile Fields](https://intl.cloud.tencent.com/document/product/1047/33520). |
>| 40008      | No permission to write profile fields. For more information, see [Profile Fields](https://intl.cloud.tencent.com/document/product/1047/33520). |
>| 40009      | The tag of the profile field does not exist.                 |
>| 40601      | The value of the profile field exceeds the length limit of 500 bytes. |
>| 40605      | Incorrect value of the standard profile field. For more information, see [Standard Profile Fields](https://intl.cloud.tencent.com/document/product/1047/33520). |
>| 40610      | Incorrect value type of the standard profile field. For more information, see [Standard Profile Fields](https://intl.cloud.tencent.com/document/product/1047/33520). |
>
>### Relationship chain error codes
>
>| Error Code | Description                                                  |
>| ---------- | ------------------------------------------------------------ |
>| 30001      | Incorrect request parameters. Check the request parameters based on the error description. |
>| 30002      | SDKAppID mismatch.                                           |
>| 30003      | The requested user account does not exist.                   |
>| 30004      | The request requires the app admin permission.               |
>| 30006      | Internal server error. Please try again.                     |
>| 30007      | Network timeout. Please try again later.                     |
>| 30008      | A write conflict has occurred due to concurrent writes. You are advised to use batch processing. |
>| 30009      | The backend prohibits this user from initiating a friend request. |
>| 30010      | The maximum number of friends has been reached.              |
>| 30011      | The maximum number of friend lists has been reached.         |
>| 30012      | The maximum number of pending friend requests has been reached. |
>| 30013      | The maximum number of blocklisted users has been reached.    |
>| 30014      | The other party has reached the maximum number of friends.   |
>| 30515      | This user cannot be added as a friend because this user is in your blocklist. |
>| 30516      | The other party has set the friend verification mode to reject all new friend requests. |
>| 30525      | This user cannot be added as a friend because you are in this user's blocklist. |
>| 30539      | The request is pending. If user A sends a friend request to user B who has set the friend verification mode to `AllowType_Type_NeedConfirm`, only a pending relationship can be established between users A and B. This return code is used to distinguish from the return code indicating friending success. The caller can capture this error and send a notification to user A. |
>| 30540      | The friend request was filtered by the security policy. Do not initiate friend requests too frequently. |
>| 30614      | The pending request does not exist.                          |
>| 31704      | There is no friend relationship with the account to be deleted. |
>| 31707      | The friend deletion request was filtered by the security policy. Do not initiate friend deletion requests too frequently. |
>| 31804      | The requested user account does not exist.                   |
>
>### Error codes for recent contacts
>
>| Error Code | Description                                                  |
>| ---------- | ------------------------------------------------------------ |
>| 50001      | The requested user account does not exist.                   |
>| 50002      | Incorrect request parameters. Check the request parameters based on the error description. |
>| 50003      | The request requires the app admin permission.               |
>| 50004      | Internal server error. Please try again.                     |
>| 50005      | Network timeout. Please try again later.                     |
>| 51006      | When you are modifying conversation mark, the number of conversations is empty or exceeds the upper limit of 100. |
>| 51007      | Failed to replace GroupID with GroupCode because an internal error occurred or the group was disbanded. |
>| 51008      | The total number of conversations in the conversation group exceeds 1,000. |
>| 51009      | The conversation group does not exist when a deletion attempt is made. |
>| 51010      | The number of conversation groups exceeds the upper limit of 20. |
>| 51011      | The conversation group name contains more than 32 bytes.     |
>| 51012      | Exceeded the maximum number of conversations pinned to the top. The maximum number of conversations pinned to the top is 50, and this limit cannot be increased. |
>
>### Message error codes
>
>| Error Code    | Description                                                  |
>| ------------- | ------------------------------------------------------------ |
>| 20001         | Invalid request packet.                                      |
>| 20002         | Invalid UserSig or A2.                                       |
>| 20003         | The UserID of the sender or recipient is invalid or does not exist. Check whether the UserID has been imported into the Chat console. |
>| 20004         | Network exception. Please try again.                         |
>| 20005         | Internal server error. Please try again.                     |
>| 20006         | The callback prior to sending a one-to-one chat message was triggered, and the App backend returned a response to forbid the message. |
>| 20007         | The one-to-one chat message cannot be sent to the other party because the sender is in the blocklist of the other party.<br>The message delivery status is displayed as failed by default. You can log in to the Chat console to change the message delivery status displayed in this scenario. For specific steps, see [Blocklist check](https://intl.cloud.tencent.com/document/product/1047/34419). |
>| 20008         | The SDKAppID of the sender does not match the SDKAppID of the recipient, because the SDKAppID is switched on the client but the data is not cleared in the database. To rectify this problem, clear the original database after switching the SDKAppID. |
>| 20009         | The message cannot be sent because the sender and the intended recipient are not friends. This problem occurs only when friend verification is configured for one-to-one chats. |
>| 20010         | The one-to-one chat message cannot be sent, because the sender is not a friend of the intended recipient (one-way relationship). |
>| 20011         | The one-to-one chat message cannot be sent, because the intended recipient is not a friend of the sender (one-way relationship). |
>| 20012         | This message cannot be sent, because the sender has been muted. |
>| 20016         | The message cannot be recalled after the time limit was reached, which is 2 minutes by default. |
>| 20018         | An internal error occurs when deleting roaming messages.     |
>| 20022         | The message to recall does not exist. Please check.          |
>| 20023         | The message has been recalled.                               |
>| 20028         | Concurrent modification of messages caused a conflict. Please try again. |
>| 21005         | The set token request arrived at the backend before the login request. Be sure to log in first, and then set token. |
>| 22001         | No offline push certificate has been uploaded.               |
>| 22002         | Network exception. Please try again.                         |
>| 22003         | The uploaded token is empty.                                 |
>| 22004         | The uploaded token exceeds 256 bytes in length.              |
>| 22005         | The login request data exceeds 1024 bytes.                   |
>| 22006         | Request frequency over the limit.                            |
>| 90001         | Failed to parse the JSON format. Check whether the JSON request packet meets JSON specifications. |
>| 90002         | The MsgBody field in the JSON request packet is not in the message format or is not of the Array type. For more information, see the definition in [TIMMsgElement Objects](https://intl.cloud.tencent.com/document/product/1047/33527). |
>| 90003         | There is no `To_Account` in the JSON request packet or the account it specifies does not exist. |
>| 90005         | The JSON request packet does not contain the `MsgRandom` field, or the `MsgRandom` field is not of the integer type. |
>| 90006         | The JSON request packet does not contain the `MsgTimeStamp` field, or the `MsgTimeStamp` field is not of the integer type. |
>| 90007         | The `MsgBody` field in the JSON request packet is not of the array type. Change the type of the `MsgBody` field to `Array`. |
>| 90008         | The JSON request packet does not contain the `From_Account` field, or the account specified by `From_Account` does not exist. |
>| 90009         | The request requires the app admin permission.               |
>| 90010         | The JSON request packet is not in the message format. For more information, see the definition in [TIMMsgElement Objects](https://intl.cloud.tencent.com/document/product/1047/33527). |
>| 90011         | The number of target user accounts for batch message sending exceeds the limit of 500. Decrease the value of `To_Account`. |
>| 90012         | `To_Account` is not registered or does not exist. Check whether `To_Account` has been imported into the Chat console or is incorrectly spelled. |
>| 90018         | The number of requested accounts exceeds the limit.          |
>| 90022         | `TagsOr` and `TagsAnd` in the push conditions contain repeated tags. |
>| 90024         | Pushes are too frequent. The interval between every two pushes must be greater than 1s. |
>| 90026         | Incorrect offline message storage period. The value cannot exceed 7 days. |
>| 90030         | The attribute length is 0 bytes or exceeds 50 bytes.         |
>| 90031         | The `SyncOtherMachine` field in the JSON request packet is not of the integer type. |
>| 90032         | The number of tags in the push conditions exceeds 10, or the number of tags in the tag adding request exceeds 10. |
>| 90033         | Invalid attribute.                                           |
>| 90034         | The tag length exceeds 50 bytes.                             |
>| 90040         | A tag in the push conditions is null.                        |
>| 90043         | `OfflinePushInfo` in the JSON request packet does not comply with the message format description. For more information, see the definition in [OfflinePushInfo Objects](https://intl.cloud.tencent.com/document/product/1047/33527). |
>| 90044         | The `MsgLifeTime` field in the JSON request packet is not of the integer type. |
>| 90045         | The all-user push feature is not enabled.                    |
>| 90047         | The number of pushes exceeds the daily quota (default quota: 100). |
>| 90048         | The requested user account does not exist.                   |
>| 90054         | Invalid `MsgKey` in the recall request.                      |
>| 90055         | The packet for batch message sending is too long. Currently, the maximum message packet length supported is 8 KB. |
>| 90994         | Internal service error. Please try again.                    |
>| 90995         | Internal service error. Please try again.                    |
>| 91000         | Internal service error. Please try again.                    |
>| 90992         | Internal service error. Please try again. If this error code is returned for all requests and the app has enabled third-party callback, check whether the app server returns callback results to the Chat backend properly. |
>| 93000         | The JSON packet exceeds the length limit of 8 KB.            |
>| 91101         | The web instance is forcibly logged out during long polling because the number of concurrent online web instances exceeds the limit allowed. |
>| 120001-130000 | Custom error code returned by webhook for a one-to-one chat. |
>
>### Group error codes
>
>| Error Code | Description                                                  |
>| ---------- | ------------------------------------------------------------ |
>| 10002      | Internal server error. Please try again.                     |
>| 10003      | Incorrect API name in the request. Check the API name and try again. |
>| 10004      | Invalid parameter. Check whether the request is correct based on the error description. |
>| 10005      | The request packet carries too many accounts.                |
>| 10006      | The operation exceeds the frequency limit. Please reduce the call rate. |
>| 10007      | Insufficient operation permission. (For example, a common member in a public group cannot remove a member from the group. Only the app admin has the permission to do so.) |
>| 10009      | The group owner is not allowed to leave the group.           |
>| 10010      | The group does not exist or has been deleted.                |
>| 10011      | Failed to parse the JSON packet. Check whether the packet complies with JSON specifications. |
>| 10012      | Invalid UserID. Check whether the UserID that initiated the operation is entered correctly. |
>| 10013      | The user is already a member of the group.                   |
>| 10014      | The user in the request cannot be added to the group, because the number of group members has reached the upper limit. If you are adding group members in batches, try reducing the number of users being added. |
>| 10015      | Invalid group ID, indicating that the group does not exist or has been deleted. |
>| 10016      | The App backend rejected this operation through a third-party callback. |
>| 10017      | The message cannot be sent due to muting. Check whether the sender is muted. |
>| 10018      | The response packet exceeds the length limit of 1 MB due to excessive request content. Try to reduce the amount of data in individual single requests. |
>| 10019      | The requested UserID does not exist.                         |
>| 10021      | The group ID is already in use. Specify another group ID.    |
>| 10023      | The message exceeds the frequency limit. Try again later.    |
>| 10024      | This invitation or app request has already been processed.   |
>| 10025      | The group ID is already in use. The operator is the group owner and therefore can use the group ID directly. |
>| 10026      | The command word in the SDKAppID request is forbidden.       |
>| 10030      | The message to be recalled does not exist.                   |
>| 10031      | The message cannot be recalled after the time limit is reached, which is 2 minutes by default. |
>| 10032      | The message to be recalled cannot be recalled.               |
>| 10033      | This type of group does not support message recalls.         |
>| 10034      | This type of message cannot be deleted.                      |
>| 10035      | Audio-video chat rooms and broadcasting chat rooms do not support message deletion. |
>| 10036      | The number of audio-video chat rooms exceeds the limit allowed. To purchase a prepaid package of “Chat audio-video chat rooms”, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350). |
>| 10037      | The number of groups that can be created and joined by a single user exceeds the limit allowed. To purchase or upgrade a prepaid package of "Expanding the number of groups that can be created and joined by a single user", see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350). |
>| 10038      | Exceeded the limit on the number of group members. To purchase or upgrade the prepaid plan to increase the maximum number of members in a single group, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350). (After upgrade, you need to call the [group profile modification API](https://intl.cloud.tencent.com/document/product/1047/34962) to modify the maximum number of members allowed per group.) |
>| 10041      | The app (SDKAppID) is configured not to support group message recalls. |
>| 10044      | This type of group (such as AVChatRoom group) does not support getting roaming messages. |
>| 10045      | The size of the custom attribute key exceeds the limit of 32 bytes. |
>| 10046      | The size of a single value of the custom attribute exceeds the limit of 4,000 bytes. |
>| 10047      | The number of keys in the custom attribute exceeds the limit of 16. |
>| 10048      | The total size of the values of all keys of the custom attribute exceeds the upper limit of 16,000 bytes. |
>| 10049      | The write operation of the custom attribute triggers frequency control. |
>| 10050      | The deleted custom attribute does not exist.                 |
>| 10051      | Message deletion exceeds the maximum scope limit.            |
>| 10052      | There is no message in the group during message deletion.    |
>| 10053      | The number of group @ objects exceeds the upper limit of 30. |
>| 10054      | There are too many members in the group. Please pull by page. |
>| 10056      | Competition conflict for custom attribute write operation. Please get the latest custom attribute before writing. |
>| 10058      | You are now using the Free Edition, and the free quota of 100 groups is exceeded. To create more groups, you need to purchase a package. |
>| 10059      | To use this feature, you need to purchase the Ultimate Edition. |
>| 10060      | The number of members in the group exceeds the upper limit for a read receipt group. |
>| 10061      | Online messages do not support read receipts.                |
>| 10062      | The read receipt doesn't exist.                              |
>| 10062      | The read receipt doesn't exist.                              |
>| 10063      | The number of keys in the group counter exceeds the limit of 20. |
>| 11000      | The community group feature is not enabled.                  |
>
>### Offline push error codes
>
>| Error Code | Description                                                  |
>| ---------- | ------------------------------------------------------------ |
>| -195       | Google Push failed to build a push object, usually due to a certificate error. |
>| -196       | Parameter missing: `intent` is selected, but no value is specified for `intent`. |
>| -197       | Certificate error. Check the certificate related parameters. |
>| -198       | Vendor response error.                                       |
>| -199       | Vendor network exception.                                    |
>| -200       | Chat backend network error.                                  |
>| -201       | Validity check failed, for example, token or certificate ID error. |
>| -202       | Object build failed before push to vendors.                  |
>| -203       | Exceeded Huawei's daily push limit.                          |
>
>
>
>### Operations data error codes
>
>| Error Code | Description                                                  |
>| ---------- | ------------------------------------------------------------ |
>| 1001       | Invalid request. Check whether the Request URL is correct.   |
>| 1002       | Invalid parameter. Check whether the account is the admin, required fields are specified, and the values meet protocol requirements. |
>| 1003       | System error.                                                |
>| 1004       | The file has not been generated yet, or no message is delivered in the requested period. |
>| 1005       | File expired.                                                |
>
>
>## 3. Chat SDK V3 Error Codes
>
>| Error Code | Description                                                  |
>| ---------- | ------------------------------------------------------------ |
>| 6003       | No success results for a batch operation.                    |
>| 6011       | Invalid recipient.                                           |
>| 6012       | Request timed out.                                           |
>| 6018       | INIT CORE module failed.                                     |
>| 6020       | `SessionNode` is null.                                       |
>| 6023       | This error is returned (during login) when you log out before login is complete. |
>| 6024       | The TLS SDK is not initialized.                              |
>| 6025       | The TLS SDK failed to find the corresponding user information. |
>| 6100       | The QALSDK failed to perform the BIND operation due to unknown reasons. |
>| 6101       | SSO ticket is missing.                                       |
>| 6102       | Repeated BIND.                                               |
>| 6103       | `TinyId` is empty.                                           |
>| 6104       | `GUID` is empty.                                             |
>| 6105       | Failed to parse the registration packet.                     |
>| 6106       | Registration timed out.                                      |
>| 6107       | BIND operation in progress.                                  |
>| 6120       | An unknown error occurred when sending the packet.           |
>| 6121       | No network connection when sending the request packet.       |
>| 6122       | No network connection when sending the response packet.      |
>| 6123       | No permission to send request packets.                       |
>| 6124       | SSO error.                                                   |
>| 6125       | Request timed out.                                           |
>| 6126       | Response timed out.                                          |
>| 6127       | Resending failed.                                            |
>| 6128       | Not actually sent during resending.                          |
>| 6129       | The stored data is filtered.                                 |
>| 6130       | Delivery overloaded.                                         |
>| 6131       | Data logic error.                                            |
>| 6150       | proxy_manager did not finish data sync to the server.        |
>| 6151       | proxy_manager is synchronizing data to the server.           |
>| 6152       | proxy_manager failed to sync data.                           |
>| 6153       | The request parameters of proxy_manager were found to be invalid in local check. |
>| 6160       | Request fields from the group assistant contain non-preset fields. |
>| 6161       | The group assistant did not enable the local storage of the group profile. |
>| 6162       | Failed to load the group profile.                            |
>| 6200       | No network connection when sending the request.              |
>| 6201       | No network connection when sending the response.             |
>| 6205       | QALSDK service not ready.                                    |
>| 6207       | Account authentication failed due to `TinyId` conversion failure. Check whether the UserID exists and is valid. |
>| 6209       | The app did not attempt to connect to the network after being started. |
>| 6210       | QALSDK execution failed.                                     |
>| 6211       | Invalid request due to invalid `toMsgService`.               |
>| 6212       | The request queue is full.                                   |
>| 6213       | You have been logged out because your account is logged in on another device. |
>| 6214       | Service suspended.                                           |
>| 6215       | Incorrect SSO signature.                                     |
>| 6216       | Invalid SSO cookie.                                          |
>| 6217       | Incorrect packet length. This error occurs when the TLS SDK performs verification on response packets during login. |
>| 6218       | Status report from OPENSTATSVC to OPENMSG timed out during login. |
>| 6219       | Failed to parse the response packet when OPENSTATSVC reported status to OPENMSG during login. |
>| 6220       | TLS SDK decryption during login failed.                      |
>| 6221       | Wi-Fi requires authentication.                               |
>| 6222       | Canceled by the user.                                        |
>| 6223       | The message cannot be recalled after the time limit is reached, which is 2 minutes by default. |
>| 6224       | The UGC extension package is missing.                        |
>| 6226       | Auto login failed because the local ticket expired. Manual login with the UserSig is needed. |
>| 6300       | No available SSO for short connections.                      |
>| 70101      | Ticket expired. This error is returned during login.         |
>| 90101      | The Chat SDK has been initialized and does not need to be re-initialized. |
>| 115000     | OpenBDH error code.                                          |
>| 6250       | No network connection when sending the request. Please try again after the network connection is recovered. |
>| 6251       | No network connection when sending the response. Please try again after the network connection is recovered. |
>| 6252       | QALSDK execution failed.                                     |
>| 6253       | Invalid request due to invalid `toMsgService`.               |
>| 6254       | The request queue is full.                                   |
>| 6255       | You have been logged out because your account is logged in on another device. |
>| 6256       | The service is suspended.                                    |
>| 6257       | Incorrect SSO signature.                                     |
>| 6258       | Invalid SSO cookie.                                          |
>
>
>>!If the problem persists,  [Submit a Ticket](https://console.cloud.tencent.com/workorder/category) with the API, error code, and error information to our tech support staff.
