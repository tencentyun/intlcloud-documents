# Error Codes



| Code | Description | Debugging method |
| ------ | :--------------------------- | :--------------------------------------------------- |
| -10000 | The client has stopped the TPNS service | It may be because that other actions are performed after the stop API is called and before registration is performed again |
| -10001 | Error in the required parameters in SDK start function | Check whether the parameters in the start API are entered correctly |
| -10002 | The token has already been bound or unbound | Call the token querying API to view the token status |
| -10003 | Not connected to the internet | Check the device's network connection status |
| -10004 | SDK fails to get device token | Check the device's network connection, enable debugging, and check the token printout status |
| -101 | MD5 value error | Check whether the start parameters are entered correctly |
| -102 | Account is empty | Check whether the token parameter in the binding API is empty |
| -201 | TPNS registration fails | Check the device's network connection status |
| -202 | Tagging operation fails | Check the device's network connection status |
| -203 | Message statistics reporting fails | Check the device's network connection status and check whether there is a xg field in the message body |
| -204 | TPNS service unregistration fails | Check the device's network connection status |
| -205 | Badge reporting fails | Check the device's network connection status |
| -301 | Internal SDK error when registering for TPNS | Update the SDK to the latest version |
| -302 | Internal SDK error when tagging | Update the SDK to the latest version |
| -303 | Internal SDK error when reporting message statistics | Update the SDK to the latest version |
| -304 | Internal SDK error when unregistering the TPNS service | Update the SDK to the latest version |
| -305 | Internal SDK error when reporting the badge | Update the SDK to the latest version |

For other error codes, see error code overview in REST API.
