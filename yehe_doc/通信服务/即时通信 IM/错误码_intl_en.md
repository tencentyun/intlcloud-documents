## 1. IM SDK Error Codes
>For Web SDK error codes, see [Error Code Table](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html).

### General error codes

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 0 | No error. |
| 6017 | A parameter is invalid. Check whether the parameter complies with requirements. For more information, check the error information to locate the specific field. |
| 6022 | Local I/O operation error. Check whether you have the read and write permissions or whether the disk is full. |
| 6027 | Incorrect JSON format. Check whether the parameters meet the requirements of the API. For more information, you can check the error information to locate the specific field. |
| 6028 | Insufficient memory. A memory leak may occur. Analyze and identify the location with high memory usage by using the Instrument tool on the iOS platform or the Profiler tool on the Android platform. |
| 6001 | PB parsing failed due to an internal error. |
| 6002 | PB serialization failed due to an internal error. |
| 6013 | The IM SDK has not been initialized. Try again after the IM SDK is initialized and the response is returned through callback. |
| 6005 | Failed to load the local database, possibly due to file corruption. |
| 6019 | Operation on the local database failed. This error may be caused by a lack of permissions for some directories or file corruption in the database. |
| 7001 | Cross-thread error. Cross-thread operations are not possible. This is an internal error. |
| 7002 | TinyId is empty. This is an internal error. |
| 7003 | Invalid UserID. A UserID cannot be empty and must be printable ASCII characters (0x20-0x7e) pf up to 32 bytes in length. |
| 7004 | The file does not exist. Check whether the file path is correct. |
| 7005 | The file size exceeds the limit. The maximum permitted size of an uploaded file is 28 MB. |
| 7006 | The file is empty. The file cannot be 0 bytes. When uploading an image, audio, video, or document, ensure that the file is generated correctly. |
| 7007 | Failed to open the file. Check whether the file exists or has been opened exclusively, which causes the SDK to fail to open it. |

### Account error codes

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 6014 | You have not logged in to the IM SDK or have been forcibly logged out. Log in to the IM SDK first and try again after successful callback. To check whether you are online, use TIMManager getLoginUser. |
| 6026 | This user account was not logged in during auto login. Call the login API to log in to the user account again. |
| 6206 | UserSig has expired. Get a new valid UserSig and log in again. For more information on how to get a UserSig, see [Generating a UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| 6208 | You have been logged out because your account is logged in on another device. Log in again. |
| 7501 | Login in process. For example, if another login or autoLogin operation is performed before the first login or autoLogin operation is called back, the system returns this error code. |
| 7502 | Logout in process. For example, if another logout operation is performed before the first logout operation is called back, the system returns this error code. |
| 7503 | Failed to initialize the TLS SDK due to an internal error. |
| 7504 | The TLS SDK has not been initialized due to an internal error. |
| 7505 | The TRANS packet format of the TLS SDK is incorrect due to an internal error. |
| 7506 | Failed to decrypt the TLS SDK due to an internal error. |
| 7507 | Failed to send the request to the TLS SDK due to an internal error. |
| 7508 | Request to the TLS SDK timed out due to an internal error. |

### Message error codes

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 6004 | Session is invalid. Check your login status when initiating getConversation. If you initiate getConversation offline, the system returns this error code. |
| 6006 | File transfer authentication failed. We recommend that you check whether the file format is correct. |
| 6007 | Failed to get the server list via FTP. |
| 6008 | Failed to upload the file via FTP. Check your network connection. If you want to upload an image, ensure that the image can be opened. |
| 6009 | Failed to download the file via FTP. Check whether your network is connected or the file or audio has expired. Currently, resource files are stored for up to 7 days. |
| 6010 | HTTP request failed. Check whether the URL is valid. You can try to visit the URL via a web browser. |
| 6016 | Invalid message elem of the IM SDK. For more information, you can check the error information to locate the specific field. |
| 6021 | Invalid object. The TIMImage object is user-generated or an incorrect value is assigned to the object. |
| 8001 | The message length exceeds the limit of 8 KB. The length of a message is the sum of the length of all elems in the message, and the length of an elem is the sum of the length of all fields of the elem. |
| 8002 | Message KEY error due to an internal error. The KEY of the network request packet is not consistent with that of the response packet. |
| 8003 | HTTP request for image conversion failed. |

### Group error codes

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 8501 | Invalid Group ID. A custom group ID must be printable ASCII characters (0x20-0x7e) of up to 48 bytes in length. To avoid confusion with the default group IDs assigned by IM, a custom group ID cannot be prefixed with @TGS#. |
| 8502 | Invalid group name. A group name can be up to 30 bytes in length and must be encoded in UTF-8. If the group name contains a Chinese character, the Chinese character may be expressed in multiple bytes. Check the length of the string in bytes. |
| 8503 | Invalid group introduction. A group introduction can be up to 240 bytes in length and must be encoded in UTF-8. If the group introduction contains a Chinese character, the Chinese character may be expressed in multiple bytes. Check the length of the string in bytes. |
| 8504 | Invalid group notice. A group notice can be up to 300 bytes in length and must be encoded in UTF-8. If the group notice contains a Chinese character, the Chinese character may be expressed in multiple bytes. Check the length of the string in bytes. |
| 8505 | Invalid URL of the group profile photo. The URL of a group profile photo can be up to 100 bytes in length. You can try to access the URL via a web browser. |
| 8506 | Invalid group name card. A group name card can be up to 50 bytes in length and must be encoded in UTF-8. If the group name card contains a Chinese character, the Chinese character may be expressed in multiple bytes. Check the length of the string in bytes. |
| 8507 | The number of group members exceeds the limit allowed upon group creation and invitation. Private group: up to 200 members. Public group: up to 2,000 members. Chat room: up to 6,000 members. Audio-video chat room: unlimited. Broadcasting chat rooms: unlimited. |
| 8508 | A private group cannot be joined via application. Any group member can invite non-members to join the group without the invitees’ confirmation. |
| 8509 | You cannot invite a group member whose role is group owner. Ensure that the role field is entered correctly. |
| 8510 | You cannot invite 0 members. Ensure that the member field is entered correctly. |


### Relationship chain error codes

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 9001 | Invalid profile field. The profile supports standard fields and custom fields. The keyword in a custom field must contain letters and can be up to 8 bytes in length. A custom field cannot exceed 500 bytes in length. |
| 9002 | Invalid remarks. The remarks field can be up to 96 bytes in length and must be encoded in UTF-8. If the remarks field contains a Chinese character, the Chinese character may be expressed in multiple bytes. Check the length of the string in bytes. |
| 9003 | Invalid friend request. The friend request field can be up to 120 bytes in length and must be encoded in UTF-8. If the friend request field contains a Chinese character, the Chinese character may be expressed in multiple bytes. Check the length of the string in bytes. |
| 9004 | The source field of the friend request is invalid. The source field must be prefixed with “AddSource_Type\_”. |
| 9005 | Invalid friend group name field. A friend group name cannot be empty, can be up to 30 bytes in length, and must be encoded in UTF-8. If the friend group name contains a Chinese character, the Chinese character may be expressed in multiple bytes. Check the length of the string in bytes. |

### Network error codes

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 9501 | SSO encryption failed due to an internal error. |
| 9502 | SSO decryption failed due to an internal error. |
| 9503 | SSO has not been authenticated. The login process may have not been completed. Complete the login process and then try again. |
| 9504 | Failed to compress the data packet due to an internal error. |
| 9505 | Failed to decompress the data packet due to an internal error. |
| 9506 | The call exceeds the frequency limit. You can initiate up to 5 requests per second. |
| 9507 | The network request queue exceeds the maximum number of concurrent requests allowed. You can initiate up to 1,000 requests at a time. For example, if you keep sending messages when the network is abnormal, the number of messages in the network request queue will keep growing and soon reach the maximum. |
| 9508 | The network is disconnected, no connection has been set up, or no network is detected when setting up a socket connection. |
| 9509 | A network connection has been established, but is created repeatedly due to an internal error. |
| 9510 | Network connection setup timed out. Try again after the network recovers. |
| 9511 | The network connection setup has been rejected by the server due to frequent connection requests. |
| 9512 | No available route to the network. Try again after the network recovers. |
| 9513 | Insufficient buffer capacity for calls. The system is too busy due to an internal error. |
| 9514 | The opposite end has reset the connection, possibly because the server is overloaded. The SDK automatically initiates reconnection. Try again after the network is reconnected and the callback function onConnSucc on iOS or onConnected on Android is called successfully. |
| 9515 | Invalid socket due to an internal error. |
| 9516 | Failed to parse the IP address due to an internal error. The local imsdk_config file may be corrupted and can cause the system to read an invalid IP address. |
| 9517 | Invalid connection. The network is connected to an intermediate node or is reset by the server due to an internal error. The SDK automatically initiates reconnection. Try again after the network is reconnected and the callback function onConnSucc on iOS or onConnected on Android is called successfully. |
| 9518 | The request packet timed out when waiting to enter the sending queue. This error occurs when the network connection setup is slow or the network is frequently disconnected and reconnected. Check whether the network connection is normal. |
| 9519 | The request packet has entered the IM SDK sending queue but timed out when waiting to enter the network layer of the operating system. This is possibly due to the restriction or failure of the local network or a failed connection between the local network and the IM SDK backend. We recommend that you run the IM SDK in a different network environment to check whether the problem is caused by the current network environment. |
| 9520 | The request packet has entered the network layer of the operating system from the IM SDK sending queue but timed out when waiting for the server to return packets. This is possibly due to the restriction or failure of the local network or failed connection between the local network and the IM SDK backend. We recommend that you run the IM SDK in a different network environment to check whether the problem is caused by the current network environment. |

## 2. Server Error Codes

### Access layer error codes during SSO

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| -302 | The number of SSO connections exceeds the limit allowed. The server refused to provide services. |
| -10001 | D2 expired. D2 is an internal credential generated based on the UserSig. The validity period of D2 is less than or equal to that of the UserSig.<br>Call the TIMManager.getInstance().login API again to generate a new D2. |
| -10003 | A2 expired. A2 is an internal credential generated based on the UserSig. The validity period of A2 is less than or equal to that of the UserSig.<br>Call the TIMManager.getInstance().login API again to generate a new A2. |
| -10004 | A2 failed to pass authentication or was filtered by a security policy when handling downstream packets.<br>Call the TIMManager.getInstance().login API again to generate a new A2. |
| -10005 | The D2Key used for encryption cannot be empty. |
| -10006 | The uin in D2 does not match the uin in the SSO packet header. |
| -10007 | Verification code delivery timed out. |
| -10008 | IMEI and A2 must be contained. |
| -10106 | SSO decryption with D2key failed too many times. Instruct the device to reset and refresh D2. |
| -10109 | The format of the request packet is incorrect. |
| -10110 | The SDKAppID is blocked. |
| -10111 | The SDKAppID is on the service cmd blocklist. |
| -10112 | The SDKAppID has been disabled. |
| -10113 | The request exceeds the frequency limit allowed for the user. The frequency limit is set for the number of requests per second based on a specific protocol. |
| -10114 | Packet loss due to system overload. The connected server has too many requests to process and therefore refuses to provide services. |

### Resource file error codes

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 114000 | The resource file to be sent does not exist. |
| 114001 | The resource file to be sent cannot be accessed. |
| 114002 | The file size exceeds the limit allowed. |
| 114003 | Sending canceled by the user. For example, the user logs out in the sending process. |
| 114004 | Failed to read the file. |
| 114005 | Resource file (such as an image, document, audio, or video) transfer timed out, usually due to network issues. |
| 114011 | Invalid parameter. |
| 115066 | File MD5 verification failed. |
| 115068 | Shard MD5 verification failed. |

### Common backend error codes

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 60002 | An error occurred when parsing the HTTP request. Check the format of the HTTP request URL. |
| 60003 | An error occurred when parsing the JSON data of the HTTP request. Check the JSON format. |
| 60004 | The request URI or the UserID or UserSig in the JSON packet is incorrect. |
| 60005 | The request URI or the UserID or UserSig in the JSON packet is incorrect. |
| 60006 | Invalid SDKAppID. Check the validity of the SDKAppID. |
| 60007 | The RESTful API call exceeds the frequency limit. Try again later. |
| 60008 | Service request timed out or HTTP request format error. Check the error and try again later. |
| 60009 | Incorrect request resource. Check the request URL. |
| 60010 | Set the UserID field of the RESTful API request to the admin account of the app. |
| 60011 | The SDKAppID request exceeds the frequency limit. Try again later. |
| 60012 | SDKAppID is required for the RESTful API. Please check the SDKAppID parameter in the URL. |
| 60013 | An error occurs when parsing the JSON data in the HTTP response packet. |
| 60014 | Account switching timed out. |
| 60015 | The type of the UserID in the request packet is incorrect. Ensure that the UserID is in string format. |
| 60016 | SDKAppID is disabled. |
| 60017 | The request is disabled. |
| 60018 | Too many requests. Try again later. |
| 60019 | Too many requests. Try again later. |
| 80001 | The text was filtered due to security policies. Check whether the text contains security-sensitive words. |
| 80002 | The outgoing message packet exceeds the length limit of 8 KB. Reduce the packet size and try again later. |

### Account error codes

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 70001 | UserSig expired. You must generate a new one. We recommend that you set the validity period of a UserSig to no less than 24 hours. |
| 70002 | The length of UserSig is 0. Check whether the passed-in UserSig is correct. |
| 70003 | Invalid UserSig. Call the API provided on the official website to [Generate a UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| 70005 | Invalid UserSig. Call the API provided on the official website to [Generate a UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| 70009 | UserSig authentication failed, probably because the private key or key of another SDKAppID was mistakenly used to generate the UserSig. Use the private key or key of the desired SDKAppID to [Generate a UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| 70013 | The UserID in the request does not match the UserID used to generate the UserSig. You can verify the UserSig on the **[Auxiliary Tools](https://console.cloud.tencent.com/im-detail/tool-usersig)** page of the IM console. |
| 70014 | The SDKAppID in the request does not match the SDKAppID used to generate the UserSig. You can verify the UserSig on the **[Auxiliary Tools](https://console.cloud.tencent.com/im-detail/tool-usersig)** page of the IM console. |
| 70016 | UserSig authentication failed because the public key does not exist. [Obtain the key](https://intl.cloud.tencent.com/document/product/1047/34540) in the IM console. |
| 70020 | SDKAppID not found. Check the app information in the IM console. |
| 70050 | You are attempting UserSig authentication too often. Check whether the UserSig is correct and try again after 1 minute. You can verify the UserSig on the **[Auxiliary Tools](https://console.cloud.tencent.com/im-detail/tool-usersig)** page of the IM console. |
| 70051 | The account is blocked. |
| 70107 | The requested UserID does not exist. |
| 70114 | Login is restricted for security reasons. You are attempting to log in too often. |
| 70169 | Server timed out. Try again later. |
| 70202 | Server timed out. Try again later. |
| 70206 | Invalid batch quantity in the request. |
| 70402 | Invalid parameter. Check whether required fields are specified and the values meet protocol requirements. |
| 70403 | Request failed. You need app admin permission to perform this action. |
| 70398 | The number of accounts exceeds the limit. To create more than 100 accounts, upgrade your app to the professional edition. For details, see the [Purchase Guide](https://intl.cloud.tencent.com/document/product/1047/34351). |
| 70500 | Internal server error. Try again later. |
| 71000 | Failed to delete the account. Only trial accounts can be deleted. Your current app is in the Pro Edition and therefore cannot be deleted. |

### Profile error codes

| Error Code | Description |
| ------ | ------------------------------------------------------ |
| 40001 | Incorrect request parameters. Check the request parameters based on the error description. |
| 40002 | Incorrect request parameters. You need to specify the UserID whose profile is to be retrieved. |
| 40003 | The requested UserID does not exist. |
| 40004 | The request requires app admin permission. |
| 40005 | Profile fields contain sensitive words. |
| 40006 | Internal server error. Try again later. |
| 40007 | No permission to read profile fields. For more information, see [Profile Fields](https://intl.cloud.tencent.com/document/product/1047/33520). |
| 40008 | No permission to write profile fields. For more information, see [Profile Fields](https://intl.cloud.tencent.com/document/product/1047/33520). |
| 40009 | The Tag of the profile field does not exist. |
| 40601 | The Value of the profile field exceeds the length limit of 500 bytes. |
| 40605 | Incorrect Value of the standard profile field. For more information, see [Standard Profile Fields](https://intl.cloud.tencent.com/document/product/1047/33520). |
| 40610 | Incorrect Value type of the standard profile field. For more information, see [Standard Profile Fields](https://intl.cloud.tencent.com/document/product/1047/33520). |

### Relationship chain error codes

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 30001 | Incorrect request parameters. Check the request parameters based on the error description. |
| 30002 | The SDKAppID does not match other parameters. |
| 30003 | The requested UserID does not exist. |
| 30004 | The request requires app admin permission. |
| 30005 | The relationship chain field contains sensitive words. |
| 30006 | Internal server error. Try again later. |
| 30007 | Network timed out. Try again later. |
| 30008 | A write conflict occurred due to concurrent write operations. We recommend that you write the data in batches. |
| 30009 | The backend prohibits this user from initiating a friend request. |
| 30010 | You have reached the limit of friends. |
| 30011 | You have reached the limit of friend groups. |
| 30012 | You have reached the limit of pending friend requests. |
| 30013 | You have reached the limit of blocked users. |
| 30014 | The other party has reached the limit of friends. |
| 30515 | You cannot add this user as a friend because this user is in your blocklist. |
| 30516 | The other party has set the friend verification mode to reject all new friend requests. |
| 30525 | You cannot add this user as a friend because you are in this user’s blocklist. |
| 30539 | The request is pending. If user A sends a friend request to user B who has set the friend verification mode to AllowType_Type_NeedConfirm, only a pending relationship can be established between users A and B. This return code is used to distinguish the result from the return code indicating friending success. The caller can capture this error and send a notification to user A. |
| 30540 | The friend request was filtered by the security policy. Do not initiate friend requests too frequently. |
| 30614 | The pending request does not exist. |
| 31704 | There is no friend relationship with the account to be deleted. |
| 31707 | The friend deletion request was filtered by the security policy. Do not initiate friend deletion requests too frequently. |
| 31804 | The requested UserID does not exist. |

### Error codes for recent contacts

| Error Code | Description |
| ------ | ---------------------------------------------- |
| 50001 | The requested UserID does not exist. |
| 50002 | Incorrect request parameters. Check the request parameters based on the error description. |
| 50003 | The request requires app admin permission. |
| 50004 | Internal server error. Try again later. |
| 50005 | Network timed out. Try again later. |

### Message error codes

| Error Code | Description |
| --------------- | ------------------------------------------------------------ |
| 20001 | Invalid request packet. |
| 20002 | UserSig or A2 expired. |
| 20003 | The UserID of the sender or recipient is invalid or does not exist. Check whether the UserID has been imported into the IM console. |
| 20004 | Network exception. Try again later. |
| 20005 | Internal server error. Try again later. |
| 20006 | The callback prior to sending a one-to-one chat message was triggered, and the app backend returned a response to forbid the message. |
| 20007 | The one-to-one chat message cannot be sent to the other party because the sender is in the blocklist of the other party.<br>The message delivery status is displayed as failed by default. You can log in to the IM console to change the message delivery status displayed in this scenario. For specific steps, see [Blocklist check](https://intl.cloud.tencent.com/document/product/1047/34419). |
| 20008 | The SDKAppID of the sender does not match the SDKAppID of the recipient, because the SDKAppID is switched on the client but the data is not cleared in the database. To rectify this problem, clear the original database after switching the SDKAppID. |
| 20009 | The message cannot be sent because the sender and the intended recipient are not friends. This problem occurs only when friend verification is configured for one-to-one chats. |
| 20010 | The one-to-one chat message cannot be sent because the sender is not a friend of the intended recipient (one-way relationship). |
| 20011 | The one-to-one chat message cannot be sent because the intended recipient is not a friend of the sender (one-way relationship). |
| 20012 | This message cannot be sent because the sender has been muted. |
| 20016 | The message cannot be recalled after the time limit is reached, which is 2 minutes by default. |
| 20018 | An internal error occurs when deleting roaming messages. |
| 20022 | The message to be recalled does not exist. Please check. |
| 20023 | The message has been recalled. |
| 21005 | The set token request arrived at the backend before the login request. Be sure to log in first, and then set token. |
| 22001 | No offline push certificate has been uploaded. |
| 22002 | Network exception. Try again later. |
| 22003 | The uploaded token is empty. |
| 22004 | The uploaded token exceeds 256 bytes in length. |
| 22005 | The login request data exceeds 1024 bytes. |
| 90001 | Failed to parse the JSON format. Check whether the JSON request packet meets JSON specifications. |
| 90002 | The MsgBody field in the JSON request packet is not in the message format or is not of the Array type. For more information, see the definition in [TIMMsgElement Objects](https://intl.cloud.tencent.com/document/product/1047/33527). |
| 90003 | The JSON request packet does not contain the To_Account field or To_Account does not exist. |
| 90005 | The JSON request packet does not contain the MsgRandom field or the MsgRandom field is not of the Integer type. |
| 90006 | The JSON request packet does not contain the MsgTimeStamp field or the MsgTimeStamp field is not of the Integer type. |
| 90007 | The MsgBody field in the JSON request packet is not of the Array type. Change the type of the MsgBody field to Array. |
| 90008 | There is no `From_Account` in the JSON request packet or the account it specifies does not exist. |
| 90009 | The request requires app admin permission. |
| 90010 | The JSON request packet is not in the message format. For more information, see the definition in [TIMMsgElement Objects](https://intl.cloud.tencent.com/document/product/1047/33527). |
| 90011 | The number of target UserIDs for batch message sending exceeds the limit of 500. Reduce the number of target UserIDs in To_Account. |
| 90012 | To_Account is not registered or does not exist. Check whether To_Account has been imported into the IM console or is incorrectly spelled. |
| 90018 | The number of requested accounts exceeded the limit. |
| 90022 | `TagsOr` and `TagsAnd` in the push condition have duplicate tags. |
| 90024 | Pushes are too often. The push interval must be longer than 1 second. |
| 90026 | Incorrect offline message storage period. The value cannot exceed 7 days. |
| 90030 | The attribute length is 0 or greater than 50. |
| 90031 | The SyncOtherMachine field in the JSON request packet is not of the Integer type. |
| 90032 | The number of tags is greater than 10 in the push condition or in the tag addition request.   |
| 90033 | Invalid attributes.   |
| 90034 | Tag length is greater than 50.  |
| 90040 | One empty tag exist in the push conditions.         |
| 90043 | The format of the OfflinePushInfo field in the JSON request packet is invalid. For more information, see [Message Element OfflinePushInfo](https://intl.cloud.tencent.com/document/product/1047/33527#.E7.A6.BB.E7.BA.BF.E6.8E.A8.E9.80.81-offlinepushinfo-.E8.AF.B4.E6.98.8E). |
| 90044 | The MsgLifeTime field in the JSON request packet is not of the Integer type. |
| 90045 | The "all member push" feature is not enabled.        |
| 90047 | The number of pushes exceeded the daily limit (100 by default). |
| 90048 | The requested UserID does not exist. |
| 90054 | Invalid MsgKey in the recall request. |
| 90055 | The batch message packet exceeded the maximum size of 8 KB.| 
| 90994 | Internal server error. Try again later. |
| 90995 | Internal server error. Try again later. |
| 91000 | Internal server error. Try again later. |
| 90992 | Internal server error. Try again later. If this error code is returned for all requests and the app has enabled third-party callback, check whether the app server returns callback results to the IM backend normally. |
| 93000 | The JSON packet exceeds the length limit of 8 KB. |
| 91101 | The web instance was forcibly logged out during long polling because the number of concurrent online web instances exceeds the limit allowed. |
| 120001 - 130000 | Custom error code returned by third-party callback for a one-to-one chat. |

### Group error codes

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 10002 | Internal server error. Try again later. |
| 10003 | Incorrect API name in the request. Check the API name and try again later. |
| 10004 | Invalid parameter. Check whether the request is correct based on the error description. |
| 10005 | The request packet carries too many accounts. |
| 10006 | The operation exceeds the frequency limit. Try again later. |
| 10007 | The user does not have sufficient operation permissions. For example, a common member in a public group attempts to remove a member from the group, but only the app admin has the permission to do so. |
| 10009 | The group owner is not allowed to quit the group. |
| 10010 | The group doesn’t exist or has been deleted. |
| 10011 | Failed to parse the JSON packet. Check whether the packet complies with JSON specifications. |
| 10012 | Invalid UserID. Check whether the UserID that initiated the operation is entered correctly. |
| 10013 | The invitee is already a group member. |
| 10014 | The user in the request cannot be added to the group, because the number of group members has reached the upper limit. If you are adding group members in batches, try reducing the number of users being added. |
| 10015 | Invalid group ID. Check whether the group ID is entered correctly. |
| 10016 | The app backend rejected this operation through a third-party callback. |
| 10017 | The message cannot be sent due to muting. Check whether the sender is muted. |
| 10018 | The response packet exceeds the length limit of 1 MB due to excessive request content. Try to reduce the amount of data in individual requests. |
| 10019 | The requested UserID does not exist. |
| 10021 | The group ID is already in use. Specify another group ID. |
| 10023 | The message exceeds the frequency limit. Try again later. |
| 10024 | This invitation or request has already been processed. |
| 10025 | The group ID is already in use. The operator is the group owner and therefore can use the group ID directly. |
| 10026 | The command word in the SDKAppID request is forbidden. |
| 10030 | The message to be recalled does not exist. |
| 10031 | The message cannot be recalled after the time limit is reached, which is 2 minutes by default. |
| 10032 | The message to be recalled cannot be recalled. |
| 10033 | This type of group does not support message recalls. |
| 10034 | This type of message cannot be deleted. |
| 10035 | Audio-video chat rooms and broadcasting chat rooms do not support message deletion. |
| 10036 | The limit on the number of audio-video chat rooms that can be created has been exceeded. To purchase the “IM audio-video chat room” postpaid plan, see the pricing description. |
| 10037 | The limit on the number of groups a single user can create and join has been exceeded. To purchase or upgrade the “number of groups a single user can create and join” postpaid plan, see the pricing description. |
| 10038 | The limit on the number of group members has been exceeded. To purchase or upgrade the “increase maximum number of group members” postpaid plan, see the pricing description. |
| 10041 | This SDKAppID has disabled group message recalls. |


### Operation data error codes

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 1001 | Invalid request. Check whether the Request URL is correct. |
| 1002 | Invalid parameter. Check whether the account is the admin, required fields are specified, and the values meet protocol requirements. |
| 1003 | System error. |
| 1004 | The file has not been generated yet, or no message was delivered in the requested period. |
| 1005 | File expired. |


## 3. IM SDK V3 Error Codes

| Error Code | Description |
| ------ | ------------------------------------------------------ |
| 6003 | Batch operation failed. |
| 6011 | Invalid recipient. |
| 6012 | Request timed out. |
| 6018 | INIT CORE module failed. |
| 6020 | SessionNode is null. |
| 6023 | This error is returned (during login) when you log out before login is complete. |
| 6024 | The TLS SDK is not initialized. |
|
