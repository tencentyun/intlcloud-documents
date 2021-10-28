## Client Return Codes


| Error Code  |  Description                    |
| ------ | --------------------------- |
| 101    | Guid request timeout.          |
| 701    | SDK exception.  |
| 801    | Persistent connection timeout. |
| 901    | Persistent connection error.                   |
| 1001   | Unable to obtain the vendor token because `deviceToken` is empty.       |
| 1101   | Device network error.                    |
| 1102   | Not registered.                     |
| 1103   | App information or routing configuration error.               |
| 1104   |  Business API’s operation type pass-in error.                  |
| 1105   | Business API’s parameter pass-in error.             |
| 1106   | Business API’s parameters are empty.             |
| 1107   | Not supported by the system.                 |
| 1110   | Start failed.      |
| 1111   | Insufficient memory.      |
| 1501   | Failed to establish persistent connection.  |
| 1502   | Failed to establish persistent connection and the app was not running in the foreground.  |


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
|` 10010012 |Invalid push time. Please change the push time.<br>If `send_time` passed in is earlier than the current time, the rules are as follows:<ul><li>If `send_time` is 10 minutes or less earlier than the current time, the push task is created, and the API schedules the task immediately when receiving it.</li><li>If `send_time` is over 10 minutes earlier than the current time, the push task is rejected, and the API returns a failure message.</li></ul> |
| 10010018 | Repeated push. |
| 10030002 | `AccessID` and `AccessKey` do not match. |
