### Where can I download GME demos and SDKs?

Please download GME demos and SDKs as instructed in the [SDK Download Guide](https://intl.cloud.tencent.com/document/product/607/18521). Currently, the demos are available for Unity, Cocos2d, Android (native), and iOS (native).

### Which version of Visual Studio should be used to run the GME demo for Windows?
Please use VS2015 to directly run it or use VS2010 to run it after manually degrading the program.

### After downloading the GME demo, how to use my own `AppID`?

- Please go to the [GME console](https://console.cloud.tencent.com/gamegme/detail/1400391524) and get the `AppID` and access key on the **Service Management** page.
- To use your own `AppID`, you need to modify the key for voice chat in `GetAuthBuffer` of `AVChatViewController`.

### Does GME allow one `OpenId` to be used across multiple devices?

No. `OpenId` is a unique identifier of a user, which is required in initializing the GME engine. If an `OpenId` is used for login via multiple devices at the same time, there will be an account exception and GME features will be unavailable.

### How can I experience the demo locally if I am the only member in the room?

Please use the demo on another device to enter the same room.

### What should I do if I receive the error message `errinfo=priv map info error` when using the demo?

For any room access parameter errors, please check whether the `AppID` of the SDK and access key have been replaced as instructed.

### How do I use a downloaded demo?

- See [Using Demo](https://intl.cloud.tencent.com/document/product/607/36419).
- For Unity users, see [Using Unity Demo](https://intl.cloud.tencent.com/document/product/607/38535).

### Why is there always no sound in the demo exported from Unity?
It is because that the `OnApplicationFocus` is set in the Unity demo. If the program loses the focus, the audio will be paused. To achieve playback in the background, please remove the code of `Pause` API calls.

### How to get logs?

**When providing logs, you should also specify the time point when the problem occurred.**
Logs are all named in the format of `QAVSDK_date.log`, and can be found in the following directories:

| OS    | Path                                                         |
| ------- | ------------------------------------------------------------ |
| Windows | %appdata%\Tencent\GME\ProcessName                            |
| iOS     | Application/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/Documents   |
| Android | /sdcard/Android/data/xxx.xxx.xxx/files                       |
| Mac     | /Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents |

If you are using the Unity engine and developing it on PC, you can try this path to find logs: `%appdata%\Tencent\GME\Unity.exe`.

For operations on an iOS device, you can follow the steps below to get logs by sharing files through an app:
1. In the `Info.plist` file of the app, add the key `UIFileSharingEnabled` and set the key value to `YES`.
2. Save the file to be shared in the `Documents` directory of the app.
3. Once the device is connected to a computer, iTunes will display a "File Sharing" area in the "Apps" tag of the selected device.
4. Then, users can add files to the directory or move the file to a PC.

**Log levels**

If you have called the log level set through the `SetLogLevel` API when providing logs, we recommend setting the level to its default value.
