## 1. Error Codes of the IM SDK
>For error codes of the Web SDK, see the [Error Code Table](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html). 

### General error codes

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 0 | No error. |
| 6015 | The operation is in progress, and you need to control API calls. For example, before the callback for the first initialization operation is completed, subsequent initialization operations will return this error code. |
| 6017 | A parameter is invalid. To correct it, check whether parameters meet requirements and view the error message to locate the problematic field. |
| 6022 | A local I/O error occurred. To correct it, check whether you have the read and write permissions or whether the disk is full. |
| 6027 | The JSON format is incorrect. To correct it, check whether parameters meet API requirements and view the error message to locate the problematic field. |
| 6028 | The memory capacity is insufficient, which may result from a memory leak. To correct it, use the Instrument tool for iOS or the Profiler tool for Android to identify the items with high memory usage. |
| 6001 | Failed to perform PB parsing, which is an internal error. To correct it, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=40&source=0&data_title=%E4%BA%91%E9%80%9A%E4%BF%A1%20%20IM&step=1) to our customer service along with the used API, error code, and error message. |
| 6002 | Failed to perform PB serialization, which is an internal error. To correct it, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=40&source=0&data_title=%E4%BA%91%E9%80%9A%E4%BF%A1%20%20IM&step=1) to our customer service along with the used API, error code, and error message. |
| 6013 | The IM SDK has not been initialized. To correct it, try again after the initialization success callback. |
| 6005 | Failed to load the local database, which may result from file corruption. To correct it, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=40&source=0&data_title=%E4%BA%91%E9%80%9A%E4%BF%A1%20%20IM&step=1) to our customer service to identify the specific cause. |
| 6019 | Failed to operate the local database, which may result from the lack of permissions for some directories or database file corruption. |
| 7001 | A cross-thread error occurred, which means cross-thread operations are not allowed and is an internal error. To correct it, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=40&source=0&data_title=%E4%BA%91%E9%80%9A%E4%BF%A1%20%20IM&step=1) to our customer service along with the used API, error code, and error message. |
| 7002 | TinyId is empty, which is an internal error. To correct it, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=40&source=0&data_title=%E4%BA%91%E9%80%9A%E4%BF%A1%20%20IM&step=1) to our customer service along with the used API, error code, and error message. |
| 7003 | The UserID field is invalid. This field cannot be empty and must be composed of printable ASCII characters (0x20-0x7e) with a maximum length of 32 bytes. |
| 7004 | The file does not exist. To correct it, check whether the file path is correct. |
| 7005 | The size of the file exceeds the limit. The maximum size of uploaded files is 28 MB. |
| 7006 | The file is empty. The file size cannot be 0 bytes. If the uploaded file is an image, audio, video, or document file, check whether it was correctly generated. |
| 7007 | Failed to open the file. To correct it, check whether the file exists, or whether it has been opened exclusively so that the SDK failed to open it. |

### Error codes for accounts

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 6014 | You have not logged in to the IM SDK. To correct it, log in to the IM SDK first and try again after the success callback. If you have been forced offline, use TIMManager getLoginUser to check your online state. |
| 6026 | This user has not logged in during auto login. To correct it, call the login API to log in again. |
| 6206 | UserSig has expired. To correct it, obtain a valid UserSig and log in again. |
| 6208 | The account has been logged in on another device and the previously logged-in account was forced offline. To correct it, log in again. |
| 7501 | The login is in process. For example, before the callback for the first login or autoLogin operation is completed, subsequent login or autoLogin operations will return this error code. |
| 7502 | The logout is in process. For example, before the callback for the first logout operation is completed, subsequent logout operations will return this error code. |
| 7503 | Failed to initialize the TLS SDK, which is an internal error. To correct it, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=40&source=0&data_title=%E4%BA%91%E9%80%9A%E4%BF%A1%20%20IM&step=1) to our customer service along with the used API, error code, and error message. |
| 7504 | The TLS SDK has not been initialized, which is an internal error. To correct it, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=40&source=0&data_title=%E4%BA%91%E9%80%9A%E4%BF%A1%20%20IM&step=1) to our customer service along with the used API, error code, and error message. |
| 7505 | The TLS SDK TRANS packet format is incorrect, which is an internal error. To correct it, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=40&source=0&data_title=%E4%BA%91%E9%80%9A%E4%BF%A1%20%20IM&step=1) to our customer service along with the used API, error code, and error message. |
| 7506 | Failed to decrypt the TLS SDK, which is an internal error. To correct it, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=40&source=0&data_title=%E4%BA%91%E9%80%9A%E4%BF%A1%20%20IM&step=1) to our customer service along with the used API, error code, and error message. |
| 7507 | The TLS SDK request failed, which is an internal error. To correct it, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=40&source=0&data_title=%E4%BA%91%E9%80%9A%E4%BF%A1%20%20IM&step=1) to our customer service along with the used API, error code, and error message. |
| 7508 | The TLS SDK request timed out, which is an internal error. To correct it, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=40&source=0&data_title=%E4%BA%91%E9%80%9A%E4%BF%A1%20%20IM&step=1) to our customer service along with the used API, error code, and error message. |

### Error codes for messages

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 6004 | The conversation is invalid. This error code is returned when you try to perform getConversation without logging in. To correct it, check your logging state before performing getConversation. |
| 6006 | File transfer authentication failed. To correct it, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=40&source=0&data_title=%E4%BA%91%E9%80%9A%E4%BF%A1%20%20IM&step=1) to our customer service along with the used API, error code, and error message. |
| 6007 | Failed to obtain the server list for file transfer. To correct it, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=40&source=0&data_title=%E4%BA%91%E9%80%9A%E4%BF%A1%20%20IM&step=1) to our customer service along with the used API, error code, and error message. |
| 6008 | Failed to upload the file. To correct it, check whether your network connection is normal. If the file to be uploaded is an image, verify that the image can be correctly opened. |
| 6009 | Failed to download the file. To correct it, check whether your network connection is normal or whether the file (which can be an audio file) to be downloaded has expired. Currently, resource files can be retained for up to 7 days. |
| 6010 | The HTTP request failed. To correct it, check whether the URL is valid by visiting it in your web browser. |
| 6016 | The message elem of the IM SDK is invalid. To correct it, view the error message to locate the problematic field. |
| 6021 | The object is invalid. For example, the object is a user-generated TIMImage object, or the object is invalid due to incorrect value assignment. |
| 8001 | The message length exceeded the limit of 8 KB. The length of a message is the sum of the lengths of all elems in the message, and the length of an elem is the sum of the lengths of all fields in the elem. |
| 8002 | The message KEY is incorrect, which is an internal error. This error code is returned when the KEY in the request packet is inconsistent with that in the response packet. |
| 8003 | The HTTP request for image conversion failed. |

### Error codes for groups

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 8501 | The group ID is invalid. The ID of a custom group must be composed of ASCII characters (0x20-0x7e) with a maximum length of 48 bytes. In addition, the ID cannot start with @TGS# to distinguish it from default group IDs assigned by IM. |
| 8502 | The group name is invalid. The maximum length of the group name is 30 bytes, and the name must be encoded in UTF-8. If the group name contains Chinese characters, make sure to check its length as a single Chinese character can take several bytes. |
| 8503 | The group introduction is invalid. The maximum length of the group introduction is 240 bytes, and the introduction must be encoded in UTF-8. If the group introduction contains Chinese characters, make sure to check its length as a single Chinese character can take several bytes. |
| 8504 | The group announcement is invalid. The maximum length of the group announcement is 300 bytes, and the announcement must be encoded in UTF-8. If the group announcement contains Chinese characters, make sure to check its length as a single Chinese character can take several bytes. |
| 8505 | The group profile photo URL is invalid. The maximum length of group profile photo URL is 100 bytes. To correct it, try to visit the URL in your web browser. |
| 8506 | The group contact card is invalid. The maximum length of the group contact card is 50 bytes, and the contact card must be encoded in UTF-8. If the group contact card contains Chinese characters, make sure to check its length as a single Chinese character can take several bytes. |
| 8507 | The maximum number of group members has been reached. This error code is returned when the number of specified members for creating a group or inviting members exceeds the limit. Specifically, a Private group can contain up to 200 members, a Public group can contain up to 2,000 members, and a ChatRoom group can contain up to 6,000 members. For AVChatRoom and BChatRoom groups, there is no limit on the number of members. |
| 8508 | It is not allowed to apply to join a private group. Any group member can invite non-members to join the group without the invitees’ approval. |
| 8509 | It is not allowed to invite a group member whose role is group owner. To correct it, make sure that the role field is valid. |
| 8510 | It is not allowed to invite 0 members. To correct it, make sure that the member field is valid. |


### Error codes for the relationship chain

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 9001 | The profile field is invalid. A profile supports standard fields and custom fields. The keyword of a custom field must consist of English letters with a maximum length of 8 bytes. For the value of a custom field, its maximum length is 500 bytes. |
| 9002 | The remarks field is invalid. The maximum length of its value is 96 bytes, and the value must be encoded in UTF-8. If the value contains Chinese characters, make sure to check its length as a single Chinese character can take several bytes. |
| 9003 | The request description field of the friend request is invalid. The maximum length of its value is 120 bytes, and the value must be encoded in UTF-8. If the value contains Chinese characters, make sure to check its length as a Chinese character can take several bytes. |
| 9004 | The addition source field of the friend request is invalid. Its value must be prefixed with "AddSource_Type\_". |
| 9005 | The friend group field is invalid. This field cannot be empty. The maximum length of its value is 30 bytes, and the value must be encoded in UTF-8. If the value contains Chinese characters, make sure to check its length as a Chinese character can take several bytes. |

### Error codes for networks

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 9501 | SSO encryption failed, which is an internal error. To correct it, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=40&source=0&data_title=%E4%BA%91%E9%80%9A%E4%BF%A1%20%20IM&step=1) to our customer service along with the used API, error code, and error message. |
| 9502 | SSO decryption failed, which is an internal error. To correct it, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=40&source=0&data_title=%E4%BA%91%E9%80%9A%E4%BF%A1%20%20IM&step=1) to our customer service along with the used API, error code, and error message. |
| 9503 | Authentication was not completed for SSO. This error code is returned if the login is not completed. To correct it, try again after successful login. |
| 9504 | Data packet compression failed, which is an internal error. To correct it, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=40&source=0&data_title=%E4%BA%91%E9%80%9A%E4%BF%A1%20%20IM&step=1) to our customer service along with the used API, error code, and error message. |
| 9505 | Data packet decompression failed, which is an internal error. To correct it, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=40&source=0&data_title=%E4%BA%91%E9%80%9A%E4%BF%A1%20%20IM&step=1) to our customer service along with the used API, error code, and error message. |
| 9506 | The calling frequency limit was reached. You can initiate up to 5 requests per second. |
| 9507 | The request queue was full because the maximum number of concurrent requests was reached. You can initiate up to 1,000 requests at the same time. |
| 9508 | The network was disconnected. This error code is returned if no connection has been established, or no network connection can be detected when establishing a socket connection. |
| 9509 | The network connection has been established but repeated establishment occurred, which is an internal error. |
| 9510 | Network connection establishment timed out. To correct it, try again after your network restores to normal. |
| 9511 | The network connection request was rejected. The server rejected the request due to a high request frequency. |
| 9512 | Failed to reach an available route to the network. To correct it, try again after your network restores to normal. |
| 9513 | The system was busy and had insufficient resources to complete the call, which is an internal error. |
| 9514 | The peer end reset the connection. This error code is returned if the server is overloaded and then automatic reconnection is performed in the SDK. To correct it, try again after the onConnSucc (for iOS) or onConnected (for Android) success callback. |
| 9515 | The socket is invalid, which is an internal error. To correct it, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=40&source=0&data_title=%E4%BA%91%E9%80%9A%E4%BF%A1%20%20IM&step=1) to our customer service along with the used API, error code, and error message. |
| 9516 | Failed to parse the IP address, which is an internal error. This error code is returned if the local imsdk_config configuration file is corrupted and then an invalid IP address is read. |
| 9517 | A connection failure occurred and then automatic reconnection was performed in the SDK due to the resetting of the network connection to an intermediate node or the server, which is an internal error. To correct it, try again after the onConnSucc (for iOS) or onConnected (for Android) success callback. |
| 9518 | The request packet timed out when waiting to enter the sending queue. This error code is returned when network connection establishment is slow or frequent disconnection and reconnection occurs during packet sending. To correct it, check whether the network connection is normal. |
| 9519 | The request packet entered the sending queue but timed out when waiting to enter the system’s network buffer, which is an internal error. This error code is returned if too many data packets exist or the sending thread is overloaded. |
| 9520 | The request packet entered the system’s network buffer but timed out when waiting for the response packet from the server, which is an internal error. This error code is returned if the request packet remains on the client device, the request packet is discarded during intermediate routing, unexpected packet loss occurs on the server, or the response packet is discarded at the system’s network layer. |

## 2. Server-Side Error Codes

### Error codes for the SSO access layer

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| -302 | The maximum number of SSO connections was reached, and therefore denial of service (DoS) occurred on the server. |
| -10000 | The delivered authentication code flag was incorrect. |
| -10001 | D2 expired. |
| -10003 | This error code is returned in scenarios such as A2 authentication failure. |
| -10004 | A2 authentication failed or the request was blocked by a security policy during downstream packet processing. |
| -10005 | It is not allowed to encrypt an empty D2Key. |
| -10006 | The uin in D2 and that in the SSO packet header do not match. |
| -10007 | Verification code delivery timed out. |
| -10008 | IMEI and A2 were missing. |
| -10009 | The cookie is invalid. |
| -10101 | D2 expired. |
| -10102 | The chain was disconnected and the screen was locked. |
| -10103 | The identity expired. |
| -10104 | Automatic exit of the device occurred. |
| -10105 | Automatic exit of MSFSDK occurred. |
| -10106 | SSO D2key encryption failed too many times, and the device was notified to reset and refresh D2. |
| -10107 | Aggregation was not supported and a uniform error code was returned to the device. If this error code is returned, the device stops aggregation on this TCP persistent connection. |
| -10108 | The prepaid amount is in arrears. |
| -10109 | The request packet format is incorrect. |
| -10110 | The SDKAppID is blacklisted. |
| -10111 | The SDKAppID is blacklisted by service cmd. |
| -10112 | The SDKAppID has been deactivated. |
| -10113 | The frequency limit (for users) is triggered. It limits the number of requests per second for a certain protocol. |
| -10114 | Packet loss occurred due to overload (for the system). If this error code is returned, the connected server is processing too many requests and incurs DoS. |

### Error codes for resource files

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 114000 | The resource file to be sent does not exist. |
| 114001 | The resource file to be sent is inaccessible. |
| 114002 | The file size limit was reached. |
| 114003 | The sending was cancelled by the user. The reason may be that the user logged out during the sending. |
| 114004 | Failed to read file content. |
| 114005 | Resource file (such as an image, document, audio, or video file) transfer timed out, which is normally caused by network issues. |
| 114011 | A parameter is invalid. |
| 115066 | File MD5 verification failed. |
| 115068 | Shard MD5 verification failed. |

### Public error codes for the backend

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 60002 | An HTTP parsing error occurred. To correct it, check the format of the HTTP request URL. |
| 60003 | A JSON parsing error occurred for the HTTP request. To correct it, check the JSON format. |
| 60004 | The request URI or the UserID or UserSig in the JSON packet is incorrect. |
| 60005 | The request URI or the UserID or UserSig in the JSON packet is incorrect. |
| 60006 | SDKAppID is invalid. To correct it, check whether the SDKAppID is valid. |
| 60007 | The frequency of calling RESTful APIs exceeds the limit. To correct it, reduce the request frequency. |
| 60008 | The service request timed out or the HTTP request format is incorrect. To correct it, check for errors and try again. |
| 60009 | The requested resource is invalid. To correct it, check the request URL. |
| 60010 | The value of the UserID field in the RESTful API request must be the app admin account. |
| 60011 | The frequency of SDKAppID requests exceeds the limit. To correct it, reduce the request frequency. |
| 60012 | SDKAppID is required for the RESTful API. To correct it, check the SDKAppID in the URL. |
| 60013 | A JSON parsing error occurred for the HTTP response packet. |
| 60014 | Account replacement timed out. |
| 60015 | The UserID type of the request packet is incorrect. To correct it, check that the UserID is of the string type. |
| 60016 | The SDKAppID has been deactivated. To correct it, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=40&source=0&data_title=%E4%BA%91%E9%80%9A%E4%BF%A1%20%20IM&step=1) to confirm with our customer service. |
| 60017 | The request has been disabled. To correct it, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=40&source=0&data_title=%E4%BA%91%E9%80%9A%E4%BF%A1%20%20IM&step=1) to confirm with our customer service. |
| 60018 | Requests are too frequent. To correct it, try again later. |
| 60019 | Requests are too frequent. To correct it, try again later. |
| 60020 | Your professional-edition package has expired and deactivated. To correct it, go to the [IM purchase page](https://buy.cloud.tencent.com/avc) and purchase a new package. After payment, the package will take effect in 5 minutes. |
| 80001 | Failed to pass text security filtering. To correct it, check whether the text contains sensitive words. |
| 80002 | The length of the outgoing message packet exceeds the limit of 8 KB. To correct it, reduce the packet size and try again. |

### Error codes for accounts

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 70001 | UserSig expired. To correct it, generate a new UserSig. We recommend that the UserSig validity period is not less than 24 hours. |
| 70002 | The length of UserSig is 0. To correct it, check whether the input UserSig is correct. |
| 70003 | UserSig is invalid. To correct it, use the API provided by the official website to [generate a new UserSig](https://cloud.tencent.com/document/product/269/32688). |
| 70005 | UserSig is invalid. To correct it, use the API provided by the official website to [generate a new UserSig](https://cloud.tencent.com/document/product/269/32688). |
| 70009 | UserSig authentication failed. The reason may be that the private key or key of another SDKAppID was mistakenly used to generate the UserSig. To correct it, use the private key or key of the appropriate SDKAppID to [generate a new UserSig](https://cloud.tencent.com/document/product/269/32688). |
| 70013 | The UserID in the request and the UserID that was used to generate the UserSig do not match. To correct it, verify the UserSig on the **[Development Tools](https://console.cloud.tencent.com/im-detail/tool-usersig)** page of the IM console. |
| 70014 | The SDKAppID in the request and the SDKAppID that was used to generate the UserSig do not match. To correct it, verify the UserSig on the **[Development Tools](https://console.cloud.tencent.com/im-detail/tool-usersig)** page of the IM console. |
| 70016 | The public key does not exist and UserSig authentication failed. To correct it, [obtain a key](https://cloud.tencent.com/document/product/269/32578#.E8.8E.B7.E5.8F.96.E5.AF.86.E9.92.A5) in the IM console. |
| 70020 | SDKAppID was not found. To correct it, check the app information in the IM console. |
| 70050 | UserSig authentication attempts are too frequent. To correct it, check whether the UserSig is correct and try again one minute later. You can verify the UserSig on the **[Development Tools](https://console.cloud.tencent.com/im-detail/tool-usersig)** page of the IM console. |
| 70051 | The account is blacklisted. |
| 70052 | UserSig expired. To correct it, generate a new UserSig and try again. |
| 70107 | The requested user account does not exist. |
| 70114 | Failed to log in due to security reasons. To correct it, do not log in frequently. |
| 70169 | An internal server timeout occurred. To correct it, try again later. |
| 70202 | An internal server timeout occurred. To correct it, try again later. |
| 70206 | The batch quantity in the request is invalid. |
| 70402 | A parameter is invalid. To correct it, check whether required fields are specified and the specified fields meet protocol requirements. |
| 70403 | The request failed, and app admin permissions are required. |
| 70398 | The number of accounts exceeds the limit. To create more than 100 accounts, upgrade your app to the professional edition. For details, see the [Purchase Guide](https://cloud.tencent.com/document/product/269/32458). |
| 70500 | An internal server error occurred. To correct it, try again later. |
| 71000 | Failed to delete the account. Only trial-edition accounts can be deleted. However, your app is of the professional edition, and therefore account deletion is not supported. |

### Error codes for profiles

| Error Code | Description |
| ------ | ------------------------------------------------------ |
| 40001 | A request parameter is incorrect. To correct it, check request parameters based on the error description. |
| 40002 | The user account whose profile will be pulled is not specified in request parameters. |
| 40003 | The requested user account does not exist. |
| 40004 | The request requires app admin permissions. |
| 40005 | Profile fields contain sensitive words. |
| 40006 | An internal server error occurred. To correct it, try again later. |
| 40007 | You do not have the read permission for profile fields. For details, see [Profile Fields](https://cloud.tencent.com/document/product/269/1500#.E8.B5.84.E6.96.99.E5.AD.97.E6.AE.B5). |
| 40008 | You do not have the write permission for profile fields. For details, see [Profile Fields](https://cloud.tencent.com/document/product/269/1500#.E8.B5.84.E6.96.99.E5.AD.97.E6.AE.B5). |
| 40009 | Tag for a profile field does not exist. |
| 40601 | The length of a profile field’s Value exceeds 500 bytes. |
| 40605 | The Value of a standard profile field is incorrect. For details, see [Standard Profile Fields](https://cloud.tencent.com/document/product/269/1500#.E6.A0.87.E9.85.8D.E8.B5.84.E6.96.99.E5.AD.97.E6.AE.B5). |
| 40610 | Value types in profile fields do not match. For details, see [Standard Profile Fields](https://cloud.tencent.com/document/product/269/1500#.E6.A0.87.E9.85.8D.E8.B5.84.E6.96.99.E5.AD.97.E6.AE.B5). |

### Error codes for the relationship chain

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 30001 | A request parameter is incorrect. To correct it, check request parameters based on the error description. |
| 30002 | The SDKAppIDs do not match. |
| 30003 | The requested user account does not exist. |
| 30004 | The request requires app admin permissions. |
| 30005 | The relationship chain field contains sensitive words. |
| 30006 | An internal server error occurred. To correct it, try again. |
| 30007 | The network connection timed out. To correct it, try again later. |
| 30008 | A write conflict occurred due to concurrent writes. To correct it, we recommend that you use the batch mode. |
| 30009 | The backend prohibited this user from initiating friend requests. |
| 30010 | The maximum number of friends was reached. |
| 30011 | The maximum number of friend groups was reached. |
| 30012 | The maximum number of pending friend requests was reached. |
| 30013 | The maximum number of blacklisted users was reached. |
| 30014 | The maximum number of the other party’s friends was reached. |
| 30515 | Failed to add this user as a friend because this user is in your blacklist. |
| 30516 | The friend verification mode of the other party disallows anyone to add him/her as a friend. |
| 30525 | Failed to add this user as a friend because you are in this user’s blacklist. |
| 30539 | If A requests to add B as a friend, but the friend verification mode of B is set to "AllowType_Type_NeedConfirm", only a pending relationship can be established between A and B. This error code is used to indicate that a pending relationship was successfully created. In this way, you can differentiate between this result and the successful addition of a friend, and the caller can capture this error and provide the user with proper instructions. |
| 30540 | The friend request was blocked by the security policy. To correct it, do not initiate friend requests frequently. |
| 30614 | The requested pending request does not exist. |
| 31704 | No friendship exists with the account to be deleted. |
| 31707 | The friend deletion request was blocked by the security policy. To correct it, do not initiate friend deletion requests frequently. |
| 31804 | The requested user account does not exist. |

### Error codes for recent contacts

| Error Code | Description |
| ------ | ---------------------------------------------- |
| 50001 | The requested user account does not exist. |
| 50002 | A request parameter is incorrect. To correct it, check request parameters based on the error description. |
| 50003 | The request requires app admin permissions. |
| 50004 | An internal server error occurred. To correct it, try again. |
| 50005 | The network connection timed out. To correct it, try again later. |

### Error codes for messages

| Error Code | Description |
| --------------- | ------------------------------------------------------------ |
| 20001 | The request packet is invalid. |
| 20002 | UserSig or A2 expired. |
| 20003 | The UserID of the sender or recipient is invalid or does not exist. To correct it, check whether the UserID has been imported into IM. |
| 20004 | A network exception occurred. To correct it, try again. |
| 20005 | An internal server error occurred. To correct it, try again. |
| 20006 | The callback before sending a one-to-one chat message was triggered, and the app backend returned a response that forbids the message to be delivered. |
| 20007 | Failed to send the one-to-one chat message because the sender is in the recipient’s blacklist. <br>By default, the message delivery state is displayed as failed. To correct it, you can log in to the console to change the displayed message delivery state. For details, see [Message Retention Settings](https://cloud.tencent.com/document/product/269/38656). |
| 20009 | Failed to send the message because the sender and the recipient are not friends (this problem occurs only if friendship verification for one-to-one chat messages is enabled.) |
| 20010 | Failed to send the one-to-one chat message because the sender is not a friend of the recipient (one-way relationship). |
| 20011 | Failed to send the one-to-one chat message because the recipient is not a friend of the sender (one-way relationship). |
| 20012 | Failed to send the message because the sender has been muted. |
| 20016 | Failed to recall the message because it has exceeded the recallable period (2 minutes by default). |
| 20018 | An internal error occurred when deleting roaming messages. |
| 90001 | Failed to parse the JSON request packet. To correct it, check whether the request packet meets JSON specifications. |
| 90002 | The MsgBody in the JSON request packet does not meet message format requirements, or MsgBody is not set to the Array type. For more information, see the definition of the [TIMMsgElement Object](https://cloud.tencent.com/document/product/269/2720#.E6.B6.88.E6.81.AF.E5.85.83.E7.B4.A0-timmsgelement). |
| 90003 | The JSON request packet does not contain the To_Account field or To_Account does not exist. |
| 90005 | The JSON request packet does not contain the MsgRandom field or MsgRandom is not of the Integer type. |
| 90006 | The JSON request packet does not contain the MsgTimeStamp field or MsgTimeStamp is not of the Integer type. |
| 90007 | The MsgBody in the JSON request packet is not set to the Array type. To correct it, change the type to Array. |
| 90008 | The JSON request packet does not contain the From_Account field or From_Account does not exist. |
| 90009 | The request requires app admin permissions. |
| 90010 | The JSON request packet does not meet message format requirements. For more information, see the definition of the [TIMMsgElement Object](https://cloud.tencent.com/document/product/269/2720#.E6.B6.88.E6.81.AF.E5.85.83.E7.B4.A0-timmsgelement). |
| 90011 | The number of target accounts to which messages will be sent exceeds 500. To correct it, reduce the number of target accounts in To_Account. |
| 90012 | To_Account is not registered or does not exist. To correct it, check whether To_Account has been imported into IM or is misspelled. |
| 90026 | The retention period of offline messages is invalid. The period cannot exceed 7 days. |
| 90031 | The SyncOtherMachine field in the JSON request packet is not of the Integer type. |
| 90044 | The MsgLifeTime field in the JSON request packet is not of the Integer type. |
| 90048 | The requested user account does not exist. |
| 90054 | The MsgKey in the recall request is invalid. |
| 90994 | An internal server error occurred. To correct it, try again. |
| 90995 | An internal server error occurred. To correct it, try again. |
| 91000 | An internal server error occurred. To correct it, try again. |
| 90992 | An internal server error occurred. To correct it, try again. If this error code is returned for all requests and the app has configured third-party callback, check whether the app server sends the callback result to the IM backend server normally. |
| 93000 | The JSON data packet exceeds the length limit of 8 KB. |
| 91101 | The instance is forced offline by long polling in the web app (the maximum number of concurrent online instances in the web app is reached.) |
| 120001 - 130000 | A custom error code returned by third-party callbacks for one-to-one chat messages. |

### Error codes for groups

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 10002 | An internal server error occurred. To correct it, try again. |
| 10003 | The API name in the request is incorrect. To correct it, check the API name and try again. |
| 10004 | A parameter is invalid. To correct it, check whether request parameters are correct based on the error description. |
| 10005 | The request packet carries too many accounts. |
| 10006 | The operation frequency limit was reached. To correct it, reduce the calling frequency. |
| 10007 | Operation permissions are insufficient. For example, an ordinary member in a public group attempts to remove a member from the group, but only the app admin has the permission to do so. |
| 10008 | The request is invalid. The reason may be that the signature information carried by the request failed the verification. To correct it, try again or [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=40&source=0&data_title=%E4%BA%91%E9%80%9A%E4%BF%A1%20%20IM&step=1) to contact our technical customer service. |
| 10009 | The group owner is not allowed to quit the group. |
| 10010 | The group does not exist or has been dismissed. |
| 10011 | Failed to parse the JSON packet. To correct it, check whether the packet meets JSON specifications. |
| 10012 | The UserID that initiated the operation is invalid. To correct it, check whether the UserID that initiated the operation is correct. |
| 10013 | The invitee is already a group member. |
| 10014 | The maximum number of group members was reached, and no more applicants can be added. To correct it, reduce the number of users to be added for batch addition. |
| 10015 | The group ID is invalid. To correct it, check whether the group ID is correct. |
| 10016 | The app backend rejected this operation through a third-party callback. |
| 10017 | Failed to send the message due to muting. To correct it, check whether the sender is muted. |
| 10018 | The maximum response packet length of 1 MB was reached. To correct it, reduce the data volume requested at a time. |
| 10019 | The requested user account does not exist. |
| 10021 | The group ID is already in use. To correct it, choose another group ID. |
| 10023 | The frequency limit for sending messages was reached. To correct it, increase the message sending interval. |
| 10024 | This invitation or request has been processed. |
| 10025  | The group ID is already in use, and the operator is the group owner who can operate the group directly. |
| 10026 | The command word of this SDKAppID request has been disabled. To correct it, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=40&source=0&data_title=%E4%BA%91%E9%80%9A%E4%BF%A1%20%20IM&step=1) to contact our customer service. |
| 10030 | The message to be recalled does not exist. |
| 10031 | Failed to recall the message because it has exceeded the recallable period (2 minutes by default). |
| 10032 | The message to be recalled does not support recalling. |
| 10033 | The group type does not support recalling. |
| 10034 | The message type does not support deletion. |
| 10035 | AVChatRoom and BChatRoom groups do not support message deletion. |
| 10036 | The number of created AVChatRoom groups exceeded the limit. To correct it, see [Pricing](https://cloud.tencent.com/document/product/269/11673) and purchase the "IM AVChatRoom" prepaid package. |
| 10037 | The maximum number of groups that can be created and joined by a single user was reached. To correct it, see [Pricing](https://cloud.tencent.com/document/product/269/11673) and purchase or upgrade the prepaid package "Number of groups that can be created and joined by a single user". |
| 10038 | The maximum number of group members was reached. To correct it, see [Pricing](https://cloud.tencent.com/document/product/269/11673) and purchase or upgrade the prepaid package "Increase the maximum number of group members". |
| 10041 | This app (SDKAppID) was configured not to support group message recalling. |

## 3. Error Codes of IM SDK V3

| Error Code | Description |
| ------ | ------------------------------------------------------ |
| 6003 | The batch operation failed. |
| 6011 | The recipient is invalid. |
| 6012 | The request timed out. |
| 6018 | The INIT CORE module failed. |
| 6020 | SessionNode is null. |
| 6023 | Logout occurred before login is completed (this error code is returned during login.) |
| 6024 | The TLS SDK has not been initialized. |
| 6025 | The TLS SDK failed to find the corresponding user information. |
| 6100 | The BIND of QALSDK failed for an unknown reason. |
| 6101 | The SSO ticket was missing. |
| 6102 | The BIND operation was repeated. |
| 6103 | TinyId is empty. |
| 6104 | GUID is empty. |
| 6105 | Failed to parse the registration packet. |
| 6106 | Registration timed out. |
| 6107 | The BIND operation is in progress. |
| 6120 | An unknown error occurred during packet sending. |
| 6121 | No network connection when sending the request packet. |
| 6122 | No network connection when sending the response packet. |
| 6123 | No permission to send the request packet. |
| 6124 | An SSO error occurred. |
| 6125 | Request timed out. |
| 6126 | The response timed out. |
| 6127 | Failed to resend. |
| 6128 | Failed to resend the packet. |
| 6129 | The storage operation was blocked. |
| 6130 | The sending was overloaded. |
| 6131 | The data logic is incorrect. |
| 6150 | proxy_manager did not finish server data synchronization. |
| 6151 | proxy_manager is synchronizing server data. |
| 6152 | proxy_manager synchronization failed. |
| 6153 | proxy_manager request parameters failed to pass the local check. |
| 6160 | Group assistant request fields contain non-preset fields. |
| 6161 | Local storage is disabled for group assistant group profiles. |
| 6162 | Failed to load the group profile. |
| 6200 | No network connection when sending the request. |
| 6201 | No network connection when sending the response. |
| 6205 | The QALSDK service is not ready. |
| 6207 | Account authentication failed (TinyId conversion failed.) |
| 6209 | Network connection was not initiated after the app was started. |
| 6210 | QALSDK execution failed. |
| 6211 | The request is invalid. Specifically, toMsgService is invalid. |
| 6212 | The request queue is full. |
| 6213 | The account was forced offline by another device. |
| 6214 | The service has been suspended. |
| 6215 | The SSO signature is incorrect. |
| 6216 | The SSO cookie is invalid. |
| 6217 | The packet length was detected incorrect by the response packet verification of TLS SDK during login. |
| 6218 | Reporting the state to OPENMSG by OPENSTATSVC timed out during login. |
| 6219 | Failed to parse the response packet when OPENSTATSVC reported the state to OPENMSG during login. |
| 6220 | TLS SDK decryption failed during login. |
| 6221 | Wi-Fi authentication is required. |
| 6222 | The operation was canceled by the user. |
| 6223 | Failed to recall the message because it has exceeded the recallable period (2 minutes by default). |
| 6224 | The UGC extension package was missing. |
| 6226 | Auto login failed because the local ticket had expired. To correct it, log in manually with UserSig. |
| 6300 | No SSO non-persistent connection is available. |
| 80101 | Message content failed security filtering. |
| 70101 | Login failed because the ticket had expired. |
| 90101 | The IM SDK has been initialized and no further initialization is required. |
| 115000 | The error code for OpenBDH. |
| 6250 | No network connection when sending the request. To correct it, try again after the network restores to normal. |
| 6251 | No network connection when sending the response. To correct it, try again after the network restores to normal. |
| 6252 | QALSDK execution failed. |
| 6253 | The request is invalid. Specifically, toMsgService is invalid. |
| 6254 | The request queue is full. |
| 6255 | The account was forced offline by another device. |
| 6256 | The service has been suspended. |
| 6257 | The SSO signature is incorrect. |
| 6258 | The SSO cookie is invalid. |
