### Where can the GME Demo and SDK be downloaded?

Please go to the [Download Guide](https://intl.cloud.tencent.com/document/product/607/18521). Currently, there are demos for Unity, Cocos2D, Android native development and iOS native development.

### Can the account in the downloaded GME Demo be changed to my own account?
- Yes, you need to get the sdkappid and permission key.
- To use your own appid, you need to modify the Key of Voice Chat in GetAuthBuffer in AVChatViewController.

### An error occurred when using the Demo: errinfo=priv map info error. How to fix this error?
There is an error in the relevant room entering parameters. Please check whether the sdkappid and permission key have been replaced.



### How to get logs?
QAVSDK_date.log is the log file. The directory is as follows:

| OS | Path |
| ------- | ------------------------------------------------------------ |
| Windows | %appdata%\Tencent\GME\ProcessName                            |
| iOS     | Application/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/Documents   |
| Android | /sdcard/Android/data/xxx.xxx.xxx/files                       |
| Mac     | /Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents |

### What are the main reasons for sound lagging?
- **Poor sound source:** For example, the host uses an external device to play music and collects the sound using a mobile phone for audio broadcasting (lag is inevitable in this case, and it is recommended that the host use a headphone).
- **Poor network connection:** The audience will hear lagged sound if the uplink packet loss rate is too high or the uplink latency fluctuates greatly.
