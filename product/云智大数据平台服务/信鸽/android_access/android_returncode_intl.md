## Client Return Codes

<hr>

| Error code | Cause and solution |
|---|---|
| 0 | Call succeeded |
| 2 | Parameter error. For example, a single-character alias is bound, or the length of the iOS token is incorrect which should be 64 characters |
| 20 | Authentication error; access id or access key is incorrectly configured |
| 10000 | Start error |
| 10001 | Operation type error, for example, this error will occur when the parameter is wrong |
| 10002 | If another registration operation comes in when performing a registration operation, this error code will be called back |
| 10003 | Permission configuration error or missing required permissions |
| 10004 | The so libraries were not imported correctly (In Android Studio, you can add a folder named jniLibs in the main directory, and add the 7 so library folders under Other-Platform-SO in the SDK documentation to this folder) |
| 10005 |The XGRemoteService node of the AndroidManifest file was not configured, or the action package name of the node was configured incorrectly |
| 10008 | The ContentProvider was not correctly configured. Please check the AndroidManifest file |
| 10009 | jce JAR error or missing jce JAR (check whether the wup package has been compiled into it; if this error occurs after obfuscated packaging, please check the obfuscated code) |
| 10101 | Failed to create the linkage (switch to another network and retry) |
| 10102 | The linkage was actively closed during request processing (switch to another network and retry) |
| 10103 | The server closed the linkage during request processing (switch to another network and retry) |
| 10104 | An exception occurred during request processing (switch to another network and retry) |
| 10105 | Sending or receiving message timed out during request processing (switch to another network and retry) |
| 10106 | Waiting for the sending request timed out during request processing (switch to another network and retry) |
| 10107 | Waiting for the receiving request timed out during request processing (switch to another network and retry) |
| 10108 | The server returned an exceptional message |
| 10109 | Unknown exception (switch to another network or restart the device) |
| 10110 | The handler for creating the linkage was null |
| Other | If other unknown errors occurred, please keep the error log and contact us |
