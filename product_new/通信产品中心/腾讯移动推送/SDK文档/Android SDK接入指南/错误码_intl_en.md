## Client Return Code


| Error Code | Cause and Solution |
|---|---|
| 0 | Call is successful |
| 2 | Parameter error. For example, a single-character alias is bound, or the length of iOS token is incorrect, which should have 64 characters |
|-1 | Internal SDK error. Please keep the log and contact TPNS technical support |
| -2| Waiting for server return packet timed out |
| -3 | The resource has been terminated. To fix this error, you need to purchase the service again and upgrade the application version (that is, the application version number needs to be higher than the previous version number) |
| -4 | The number of connections exceeds the package limit, and connections will be refused randomly. To fix this error, you need to upgrade the service |
| -5 | An error occurred while getting `Guid`. Please check whether the network, `AccessId`, and `AccessKey` are correct and whether the resource has been purchased |
| -7| An error occurred while sending the request packet. Please check the network or keep the log and contact TPNS technical support |
| -11 | Failed to connect to the MQTT server. Please check the network |
|-101 | Certain content in the SDK is in incorrect JSON format. Please keep the log and contact TPNS technical support |
| -102 | Unable to get the token. Please check the network and application configuration |
| -701 | A network exception occurred while sending the request packet |
| -702 | Sending request packet timed out |
| -1101 | A network exception occurred while connecting to the MQTT server. Please check the network |
| -1102 | An error occurred while connecting to the MQTT server. Please check the network or contact TPNS technical support |
| -1103 | Connection to the MQTT server timed out. Please check the network |
| -10005 | AIDL configuration error |
| 20 | Authentication error. `Access ID` or `Access Key` is incorrectly configured |
| 10000 | Start error |
| 10001 | Operation type error code. For example, this error will occur if the parameter is incorrect |
| 10002 | When a registration operation is being performed, if another registration operation comes in, this error code will be called back |
| 10003 | Permission configuration error or missing required permissions |
| 10004 | The .so files were not imported correctly (In Android Studio, you can add a folder named jniLibs in the main directory, and add the 7 .so file folders under Other-Platform-SO in SDK documentation to this directory) |
| 10005 |The `XGRemoteService` node of the AndroidManifest file was not configured, or the action package name of the node was configured incorrectly |
| 10008 | The `ContentProvider` was not correctly configured. Please check the AndroidManifest file |
| 10009 | jce JAR error or missing jce JAR (check whether the wup package has been compiled into it; if this error occurs after obfuscated packaging, please check the obfuscated code) |
| 10101 | Fail to create the linkage (switch to another network and retry) |
| 10102 | The linkage is closed during request processing (switch to another network and retry) |
| 10103 | The server has closed the linkage during request processing (switch to another network and retry) |
| 10104 | An exception occurs during request processing (switch to another network and retry) |
| 10105 | Message delivery or reception has timed out during request processing (switch to another network and retry) |
| 10106 | The wait to send the request has timed out during request processing (switch to another network and retry) |
| 10107 | The wait to receive the request has timed out during request processing (switch to another network and retry) |
| 10108 | The server returns an exception message |
| 10109 | Unknown exception. Please switch to another network or restart the device |
| 10110 | The handler for creating the linkage was null |
| Other | If other unknown errors occur, please keep the error log and contact us |
|10006| Incorrect `AccessKey` or `AccessID`|
| 10007 | TPNS Service initialization error |
|10008| Incorrect `AccessKey` or `AccessID`|
| 10110 | Verification processing error |
| 10115 | Repeated registration in a short time |
| 10300 | Marathon policy return code |
| 10400 | SDK parameters error |
| 20002 | No valid network connection available. Please check whether the application has made the payment |


## Server Return Code


| Error Code | Description |
| ----- | --------------------- |
| 1010001 | Resources not deployed. Please check whether the application has purchased push resources |
| 1008001 | Parameter parsing error |
| 1008002 | Required parameter missing |
| 1008003 | Verification failed |
| 1008004 | Service call failed |
| 1008006 | Invalid token. Please check whether the device token has been successfully registered |
| 1008007 | Parameter verification failed |
| 1008011| File upload failed. | 
| 1008012 | Uploaded file is empty |
| 1008013 | Certificate parsing error |
|1008015  | The push task ID does not exist |
| 1008016 | Incorrect date and time parameter format |
| 1008019 | Fail to pass the content security review |
| 1008020 | Certificate package name verification failed |
| 10080021 | p12 certificate format verification failed |
| 1008022 | Incorrect p12 certificate password |
| 1008025 | Application creation failed. Application already exists under the product |
| 10010005 | Push target does not exist |
|10030002 | `AccessID` does not match `AccessKey` |
