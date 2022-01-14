## Client Return Codes


| Error Code | Description |
|---|---|
| 0 | The call is successful. |
| 2 | Incorrect parameter. For example, a single-character alias is bound, or the length of the iOS token, which should have 64 characters, is incorrect. |
| -1 | SDK internal error. Please save the log and [contact us](https://intl.cloud.tencent.com/support). |
| -2 | Request timeout. |
| -3 | The resource has been terminated. To fix this error, you need to purchase the service again and upgrade the application to a later version. |
| -4 | The number of connections exceeds the package limit, and connections will be refused randomly. To fix this error, you need to upgrade the service. |
| -5 | An error occurred while getting `Guid`. Please check whether the network, `AccessId` and `AccessKey` are correct and whether the resource has been purchased. |
 |-7 | An error occurred while sending the request packet. Please check the network connectively. Alternatively, you can save the log and [contact us](https://intl.cloud.tencent.com/support). |
| -11 | Failed to connect to the MQTT server. Please check the network connectivity. |
| -101 | Certain content in the SDK is in an incorrect JSON format. Please save the log and [contact us](https://intl.cloud.tencent.com/support). |
| -102 | Unable to get the token. Please check the network connectivity and application configuration. |
| -502  | An error occurred while getting `Guid`. Check whether the network and the domain name configured for the service access point are correct. For more information, see [SDK Integration](https://intl.cloud.tencent.com/document/product/1024/30713).  |
| -701 | A network exception occurred while sending the request packet. |
| -702 | Sending the request packet timed out. |
| -1101 | A network exception occurred while connecting to the MQTT server. Please check the network connectivity. |
| -1102 | A network exception occurred while connecting to the MQTT server. Please check the network or [contact us](https://intl.cloud.tencent.com/support). |
| -1103 | The connection to the MQTT server timed out. Please check the network connectivity. |
| -10005 | AIDL configuration error. |
| 20 | Authentication error. `AccessID` or `AccessKey` is incorrectly configured. |
| 10000 | Start error. |
| 10001 | Operation type error code. For example, this error will occur when the parameter is incorrect. |
| 10002 | If a registration operation is requested while the previous registration is ongoing, this error code will be returned in the callback API. |
| 10003 | Incorrect permission configuration or lack of required permissions. |
| 10004 | The so library has not been imported correctly. (In Android Studio, you can create the `jniLibs` folder in the `main` directory, and add the 7 so library folders under Other-Platform-SO in the SDK documentation to this directory). |
| 10005 | The XGRemoteService node of the AndroidManifest file was not configured, or the action package name of the node was incorrectly configured |
| 10008 | The ContentProvider was incorrectly configured. Please check the AndroidManifest file. |
| 10009 | The jce JAR is incorrect or missing (check whether the wup package has been compiled into it. If this error occurs after obfuscated packaging, please check the obfuscation code). |
| 10101 | Failed to create the linkage (switch to another network and try again). |
| 10102 | The linkage is closed during request processing (switch to another network and try again). |
| 10103 | The server has closed the linkage during request processing (switch to another network and try again). |
| 10104 | An exception occurs during request processing (switch to another network and try again). |
| 10105 | Sending or receiving packets timed out during request processing (switch to another network and try again). |
| 10106 | Failed to send a request due to timeout (switch to another network and try again). |
| 10107 | Failed to receive a request due to timeout (switch to another network and try again). |
| 10108 | The server returns an exception message. |
| 10109 | Unknown exception. Please switch to another network or restart the device. |
| 10110 | The handler for creating the linkage was null. |
| Other | Unknown error. Please save the log and [contact us](https://intl.cloud.tencent.com/support). |
| 10006 | Incorrect AccessKey or AccessID. |
| 10007 | An error occurred while initializing the TPNS service. |
| 10008 | Incorrect AccessKey or AccessID. |
| 10110 | Signature authentication error. |
| 10115 | Repeated registration in a short amount of time. |
| 10300 | Marathon policy return code |
| 10400 | Incorrect SDK parameters. |
| 20002 | No valid network connection available. Please check whether the application has made the payment. |
|10030009  |The app does not exist. During SDK integration, you need to configure the domain name based on your service access point. For more information, see [SDK Integration](https://intl.cloud.tencent.com/document/product/1024/30713). |



## Server Return Codes


| Error Code | Description |
| ----- | --------------------- |
| 1010001 | No resources are deployed. Please check whether the application has purchased push resources. |
| 1008001 | Parameter parsing error. |
| 1008002 | The required parameter is missing. |
| 1008003 | Authentication failed. |
| 1008004 | Service call failed. |
| 1008006 | Invalid token. Please check whether the device token has been successfully registered. |
| 1008007 | Parameter verification failed. |
| 1008011 | File upload failed. |
| 1008012 | The uploaded file is empty. |
| 1008013 | Certificate parsing error. |
| 1008015 | The push task ID does not exist. |
| 1008016 | Incorrect date and time parameter format. |
| 1008019 | Failed to pass the content security review. |
| 1008020 | Certificate package name verification failed. |
| 1008021 | Failed to pass the p12 certificate verification. |
| 1008022 | Incorrect p12 certificate password. |
| 1008025 | Application creation failed. The application already exists under the product. |
| 1008026 | Batch operation partially failed. |
| 1008027 | Batch operation fully failed. |
| 1008028 | Frequency limit exceeded. |
| 1008029 | Invalid token. |
| 1008030 | Unpaid application. |
| 1008031 | The application resource has been terminated. |
| 10110008 | The queried token and account do not exist. |
| 10010005 | The push target does not exist. |
| 10010012 | Invalid push time. Please change the push time.<br>For a scheduled push, if `send_time` passed in is earlier than the current time, specific rules are as follows:<li>If `send_time` is 10 minutes or less earlier than the current time, the push task is created, and the API schedules the task immediately when receiving it.</li><li>If `send_time` is over 10 minutes earlier than the current time, the push task is rejected, and the API returns a failure message.</li> |
| 10010018 | Repeated push. |
| 10030002 | `AccessID` and `AccessKey` do not match. |

