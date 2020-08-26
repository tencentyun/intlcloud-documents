## Client Return Code


| Code   | Description                         | Debugging Method                                            |
| ------ | :--------------------------- | :--------------------------------------------------- |
| -10000 | The client stopped the TPNS service | It may be because that other actions are performed after the `Stop` API is called and before registration is performed again |
| -10001 | Error with the required parameters in SDK start function | Check whether the parameters in the `Start` API are entered correctly |
| -10002 | The token has already been bound or unbound | Call the ID querying API to view the token status |
| -10003 | Not connected to the internet | Check the device's network connection status |
| -10004 | SDK failed to get device token | Check the device's network connection, enable debugging, and check the token printout status |
| -101 | MD5 value error | Check whether the start parameters are entered correctly |
| -102 | Account is empty | Check whether the ID parameter in the binding API is empty |
| -201 | TPNS registration failed | Check the device's network connection status |
| -202 | Tagging operation failed | Check the device's network connection status |
| -203 | Message statistics reporting failed | Check the device's network connection status and check whether there is an `xg` field in the message body |
| -204 | TPNS unregistration failed | Check the device's network connection status |
| -205 | Badge reporting failed | Check the device's network connection status |
| -301 | An internal SDK error occurred while registering for TPNS | Update the SDK to the latest version |
| -302 | An internal SDK error occurred while tagging | Update the SDK to the latest version |
| -303 | An internal SDK error occurred while reporting message statistics | Update the SDK to the latest version |
| -304 | An internal SDK error occurred while unregistering the TPNS service | Update the SDK to the latest version |
| -305 | An internal SDK error occurred while reporting the badge | Update the SDK to the latest version |


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
| 1008021 | p12 certificate format verification failed |
| 1008022 | Incorrect p12 certificate password |
| 1008025 | Application creation failed. Application already exists under the product |
| 1008026 | Batch operation partially failed |
| 1008027 | Batch operation entirely failed |
| 1008028  | Frequency limit exceeded |
| 1008029  | Token verification invalid |
| 1008030  | App unpaid |
| 1008031  | App resources destroyed |
| 10110008 | Account of the Token queried does not exist |
| 10010005 | Push target does not exist |
| 10010018 | Duplicate push|
| 10030002 | AccessID and AccessKey do not match |
