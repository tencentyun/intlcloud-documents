
### Where can I download the GME sample project and SDK?

For detailed directions on how to download the GME sample project and SDK, see [SDK Download Guide](https://intl.cloud.tencent.com/document/product/607/18521). Currently, sample projects for the Unity engine, Unreal Engine, Cocos2d engine, Android, iOS, Windows, macOS, and web are provided.

### Which version of Visual Studio should I use to open the GME sample project for Windows?
Please open with VS2015. Downgrade then project if you need VS2010.

### How do I replace the account with your own account after downloading the GME sample project?

- Get the `AppID` and permission key in [Service Management > Application Settings](https://console.cloud.tencent.com/gamegme) in the console.
- To use your own `AppID`, you need to change the key of voice chat in `GetAuthBuffer` in `AVChatViewController`.


### Is it OK for multiple users to use the same `OpenID` in GME?
`OpenID` is used to uniquely identify a user in the application during initialization of the GME engine. Sharing an `OpenID` across multiple devices, such as for multi-device login, may render your account unable to use GME properly.

### How can I experience the effect if I am the only person in the room?

Use the sample project on another device to enter the same room.

### What should I do if `errinfo=priv map info error` is displayed when I use the sample project?

There is an error in the relevant room entry parameters. Check whether the `SDKAppID` and permission key have been replaced.

### How do I use the downloaded sample project or demo?

- See [Running Demo](https://www.tencentcloud.com/document/product/607/39154).
- For Unity Demo users, see [Using Unity Demo](https://intl.cloud.tencent.com/document/product/607/50219).

### Why is the sample project exported from Unity often silent when used?
`OnApplicationFocus` is set in the Unity sample project. When the application loses focus, sound will be paused. To play back the sound on the backend, remove the code for calling the `Pause` API.

### How do I get logs?

**When providing logs, you also need to specify the time point when the problem occurred.**
The file named `QAVSDK_date.log` is the log file, which is in the following directories:

| OS | Path |
| ------- | ------------------------------------------------------------ |
| Windows | `%appdata%\Tencent\GMEGLOBAL\ProcessName`                            |
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


### Which Unity versions are supported by the GME SDK for Unity?
The GME SDK for Unity supports all Unity versions.



### Does GME's .so library on Android support ARMv8?
Yes. It is supported on v2.3.5 or later.


### Does the .so library on Android support x86-64?
No.
