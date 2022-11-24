This document describes how to solve GME issues encountered during development.

## FAQs
For common issues encountered during development, you can analyze their type and solve them as follows:

| Document | Solved Issues |
|---|----|
| [Features](https://intl.cloud.tencent.com/document/product/607/39520) | GME feature issues such as platform compatibility. |
| [Billing](https://intl.cloud.tencent.com/document/product/607/30255) | Questions about billing mode or billing time |
| [Demo](https://intl.cloud.tencent.com/document/product/607/39521) | Issues encountered when you use GME's `SampleProject` or demo |
|[Authentication](https://intl.cloud.tencent.com/document/product/607/39824)| Issues encountered during GME authentication |
|[Room Entering Failed](https://intl.cloud.tencent.com/document/product/607/39523), [Sound and Audio](https://intl.cloud.tencent.com/document/product/607/39524), and [Network](https://intl.cloud.tencent.com/document/product/607/39519) | Issues encountered when you use the GME voice chat feature |
|[Speech-to-text Conversion](https://intl.cloud.tencent.com/document/product/607/39716)| Issues encountered when you use the speech-to-text conversion feature |
| [Program Export](https://intl.cloud.tencent.com/document/product/607/39522) | Issues encountered when you export the application for each platform (to a real device)  |


## Development Issues

If a feature issue occurs during development, you can identify it based on the returned error code first. If you cannot troubleshoot the issue based on the error code, you can [submit a ticket](https://console.tencentcloud.com/workorder/category) for assistance.


### Error codes

For detailed error codes and their causes and solutions, see [Error Codes](https://intl.cloud.tencent.com/document/product/607/33223).


### How do I get logs?

When providing logs, you also need to specify the time point when the problem occurred as well as the logs of both the recipient (listener) and sender (speaker).

**Log path**
The file named `QAVSDK_date.log` is the log file, which is in the following directories:

| OS | Path |
| ------- | ------------------------------------------------------------ |
| Windows | `%appdata%\GMEGLOBAL\GME\processName`                            |
| iOS     | `Application/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/Documents`   |
| Android | `/sdcard/Android/data/xxx.xxx.xxx/files`                       |
| Mac     | `/Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents` |

If you are using the Unity engine and developing on PC, try to find the log under the `%appdata%\Tencent\GME\Unity.exe` path.

On iOS virtual machine, logs can be obtained through application supporting file sharing as follows:
1. Add the UIFileSharingEnabled key to the application's `Info.plist` file, and set the key value to "YES".
2. Place the files to be shared in the Documents directory of your application.
3. Once the device is plugged into the user's computer, iTunes displays a File Sharing area in the Apps tab of the selected device.
4. User can add files to the directory or drug files to the desk computer.

>? With GME version 2.8.4 or below, the Windows platform log location is: `%appdata%\Tencent\GME\ProcessName`.

**Log output level**

It is recommended to restore the default log output level if you have called the SetLogLevel when providing logs.


**Log encryption**

Currently, GME logs are encrypted by default. You can call the following API to disable log encryption. We recommend you disable log encryption during development and enable it before application release. This API must be called before `init`.

```
SetAdvanceParams("DisableEncryptLog", "1");
```

| Parameter | Description |
|--|--|
| Parameter 1 | Enter `DisableEncryptLog` to enable/disable log encryption. |
| Parameter 2 | Valid values: `1`: Disable log encryption; `0`: Enable log encryption. |


## Crash Issue


If a crash occurs, troubleshoot as instructed in [Program Export](https://intl.cloud.tencent.com/document/product/607/39522) first. If the issue persists, provide the stack to GME developers for assistance.
- If you have connected to a third-party exception reporting plugin, you can contact GME developers to share the link to the crashed stack.
- For iOS or Android, you can connect the device to a PC, use Xcode or Logcat in Android Studio to get the crashed stack, replicate it, and provide it to GME developers.
- For Windows, provide the dump file.
