## Client return code

<hr>

| Error code | Cause and solution |
|---|---|
| 0 | Call is successful |
| 2 | Parameter error. For example, a single-character alias is bound, or the length of iOS token is incorrect, which should have 64 characters |
| 20 | Authentication error; access id or access key is incorrectly configured |
| 10000 | Start error |
| 10001 | Operation type error code. For example, this error will occur if the parameter is incorrect |
| 10002 | If another registration operation comes in when performing a registration operation, this error code will be called back |
| 10003 | Permission configuration error or missing required permissions |
| 10004 | The .so files were not imported correctly (In Android Studio, you can add a folder named jniLibs in the main directory, and add the 7 .so file folders under Other-Platform-SO in SDK documentation to this directory) |
| -10005 | AIDL configuration error |
| 10006 | AccessKey or AccessID error |
| 10007 | TPNS Service initialization error |
| 10008 | AccessKey or AccessID error |
| 10009 | jce JAR error or missing jce JAR (check whether the wup package has been compiled into it; if this error occurs after obfuscated packaging, please check the obfuscated code) |
| 10101 | Fail to create the linkage (switch to another network and retry) |
| 10102 | The linkage is closed during request processing (switch to another network and retry) |
| 10103 | The server has closed the linkage during request processing (switch to another network and retry) |
| 10104 | An exception occurs during request processing (switch to another network and retry) |
| 10105 | Message delivery or reception has timed out during request processing (switch to another network and retry) |
| 10106 | The wait to send the request has timed out during request processing (switch to another network and retry) |
| 10107 | The wait to receive the request has timed out during request processing (switch to another network and retry) |
| 10108 | The server returns an exception message |
| 10109 | Unknown exception (switch to another network or restart the device) |
| 10110 | Verification processing error |
| 10115 | Repeated registration in a short time |
| 10300 | Marathon policy return code |
| 10400 | SDK parameters error |
| Other | If other unknown errors occur, please keep the error log and contact us |

## Server return code

<hr>

| Error code | Meaning |
| ----- | --------------------- |
| 1010001 | Resources not deployed, please confirm whether the app has purchased push resources |
| 1008001 | Parameter parsing error |
| 1008002 | Required parameter missing |
| 1008003 | Verification failure |
| 1008004 | Service call failure |
| 1008006 | Invalid token |
| 1008007 | Parameter verification failure |
| 1008011 | File upload failure | 
| 1008012 | Uploaded file is empty |
| 1008013 | Certificate parsing error |
| 1008015 | Push job ID does not exist |
| 1008016 | Incorrect date and time parameter format |
| 1008019 | Fail to pass the content security review |
| 1008020 | Certificate package name verification failure |
| 10080021 | p12 certificate format verification failure |
| 1008022 | Incorrect p12 certificate password |
| 1008025 | Application creation failure. Application already exists under the product |
| 10010005 | Push target does not exist |


