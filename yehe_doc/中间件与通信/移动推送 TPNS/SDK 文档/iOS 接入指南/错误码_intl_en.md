## Client Return Codes


| Error Code | Description | Call Method |
| ------ | :--------------------------- | :--------------------------------------------------- |
| -10000 | The client stopped the TPNS service. | The possible cause is that other actions are performed after the `Stop` API is called and before registration is performed again. |
| -10001 | Error with the required parameters in the SDK start function. | Check whether the parameters in the `Start` API are entered correctly. |
| -10002 | The token has already been bound or unbound. | Call the ID querying API to view the token status. |
| -10003 | Not connected to the internet. | Check the device's network connection status. |
| -10004 | SDK failed to get device token. | Check the device's network connection, enable debugging, and check the token printout status. |
| -101 | MD5 value error. | Check whether the start parameters are entered correctly. |
| -102 | Account is empty. | Check whether the ID parameter in the binding API is empty. |
| -201 | TPNS registration failed. | Check the device's network connection status. |
| -202 | Tagging operation failed. | Check the device's network connection status. |
| -203 | Message statistics reporting failed. | Check the device's network connection status and check whether there is an `xg` field in the message body. |
| -204 | TPNS unregistration failed. | Check the device's network connection status. |
| -205 | Badge reporting failed. | Check the device's network connection status. |
| -301   | An internal SDK error occurred while registering the TPNS service.      | Update the SDK to the latest version.                                      |
| -302 | An internal SDK error occurred while tagging. | Update the SDK to the latest version. |
| -303 | An internal SDK error occurred while reporting message statistics. | Update the SDK to the latest version. |
| -304 | An internal SDK error occurred while unregistering the TPNS service. | Update the SDK to the latest version. |
| -305 | An internal SDK error occurred while reporting badge statistics. | Update the SDK to the latest version. |


## Server Return Codes

| Error Code | Description |
| ----- | --------------------- |
| 1010001 | No resources are deployed. Please check whether the application has purchased push resources. |
| 1008001 | Parameter parsing error. |
| 1008002 | Parameter missing. |
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
| 10010012 | Invalid push time. Please change the push time.<br>If `send_time` passed in is earlier than the current time, the specific rules are as follows:<ul><li>If \|  `send_time` is 10 minutes or less earlier than \| the current time, the push task is created, and the API schedules the task immediately when receiving it.</li><li>If \|  `send_time` is over 10 minutes earlier than \| the current time, the push task is rejected, and the API returns a failure message.</li></ul> |
| 10010018 | Repeated push. |
| 10030002 | `AccessID` and `AccessKey` do not match. |

