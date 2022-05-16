
### Where can I download GME demos and SDKs?

See [SDK Download Guide](https://intl.cloud.tencent.com/document/product/607/18521). GME provides demos for Unity, Cocos2d, Android (native) and iOS (native).

### Which version of Visual Studio is supported for Windows Demo?
VS2015 is recommended. If you want to use VS2010, you need to downgrade the project on your own.

### How can I use my own account in the Demo?

- Go to the [GME Console](https://console.cloud.tencent.com/gamegme/detail/1400391524) and get the AppID and key in **Service Management**.
- Modify the key for voice chat in GetAuthBuffer in AVChatViewController.

### Does GME allow using only one openid across multiple devices?

An OpenId is the unique ID of a user. If you use the same OpenId on multiple devices, such as for multi-device login, it may cause login failure. 

### How can I experience the effect if I am the only person in the room?

Use the demo on another device to enter the same room.

### What should I do if I receive the error message "errinfo=priv map info error" when using the Demo?

If an error occurs for room access parameters, check whether your SDKAppID and access key have been replaced as instructed.

### How do I use a downloaded demo?

- See [Usage Documentation](https://intl.cloud.tencent.com/document/product/607/39154).
- For Unity Demo users, see [Using Unity Demo](https://intl.cloud.tencent.com/document/product/607/38535).

### Why is the Unity exported demo muted when using?
`OnApplicationFocus` is configured in Unity Demo. When the program loses focus, the sound is paused. If you need to play sound in the backgroud, remove the codes that calling the Pause API.

### How do I get logs?

For troubleshooting, provide the log and the occurrence time
Logs are all named in the format of QAVSDK_date.log, and can be found in the following directories:

| OS | Path |
| ------- | ------------------------------------------------------------ |
| Windows | `%appdata%\Tencent\GMEGLOBAL\ProcessName`                            |
| iOS     | `Application/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/Documents`   |
| Android | `/sdcard/Android/data/xxx.xxx.xxx/files`                       |
| Mac     | `/Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents` |

If you are using the Unity engine and developing on PC, try to find the log under the `%appdata%\Tencent\GME\Unity.exe`.

On an iOS device, logs can be obtained through application supporting file sharing as follows:
1. Add the UIFileSharingEnabled key to the application's `Info.plist` file, and set the key value to "YES".
2. Place the files to be shared in the Documents directory of your application.
3. Once the device is connected with the user's computer, iTunes displays a File Sharing area in the Apps tab of the selected device.
4. User can add files to the directory or drag files to the desktop computer.

>? For GME SDK 2.8.4 and older versions, logs of Windows devices are stored under `%appdata%\Tencent\GME\ProcessName`.

**Log output level**

It is recommended to restore the default log output level if you have called the SetLogLevel when providing logs.
