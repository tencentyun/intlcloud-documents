[//]: # (chinagitpath:XXXXX)

## Preparations
- Developers need to complete the following steps when integrating the security SDK:
 1. Copy the SDK dynamic library to the specified project directory associated with the game platform and the CPU architecture.
 2. Call the SDK API based on the game_id and user's login information.
 3. Verify whether the SDK is integrated correctly.

- The following files are required for the integration of the security SDK to Android OS written in C/C++:
```
tp2.jar
libtersafe2.so
```
- Permissions required:
```
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.GET_TASKS" />
<uses-permission android:name="android.permission.INTERNET" />
```
- SDK API functions:
```
Initialization API: initEx
User login API: onUserLogin
API for switching from foreground to background: onAppPause
API for switching from background to foreground: onAppPause
```

## Adding SDK Files to the Project
### Add files
1. Copy the tp2.jar file from the sdk/android/c directory to the libs directory in the android project directory.
2. Copy the folder (containing the libtersafe2.so file) named after the CPU architecture from the sdk/android/java/lib directory to the libs directory of the android project directory. Do not copy unsupported CPU architectures.
![](https://mc.qcloudimg.com/static/img/eab83b3ae6d2a13b8f6a8479137a5e07/image.png)

### Setting of project attributes
Select the game project on the left "Project Explorer" pane in Eclipse, right-click and select "Properties" in the pop-up menu, then select "Java Build Path" on the left of the "Properties" window, and click "Add JARs" in "Libraries" to add tp2.jar.
![](https://mc.qcloudimg.com/static/img/2b038746f019e439ef5bbdb473ab16b2/image.png)
 Select tp2.jar that has been copied to the project directory.
 ![](https://mc.qcloudimg.com/static/img/b48aeb6b30b9c689ca5e56357a0c72b3/image.png)
 After adding tp2.jar, select it in "Order and Export".
 ![](https://mc.qcloudimg.com/static/img/e19cbe55f0997e7bdb68eeef275a1fb4/image.png)
Clean and rebuild the project.

## Calling SDK API
Import the packet.
```
import com.tencent.tersafe2.TP2Sdk;
```

### Initialization function
**Function signature**
```
public static int initEx(int gameId, String appKey);
```

**Parameter description**

| Parameter | Required | Description |
|---------|---------|---------|
| gameId | Yes | The game_id assigned by Tencent Cloud |
| appKey | Yes | The game_key assigned by Tencent Cloud, which corresponds to the game_id. |

- Both gameID and appKey are automatically generated after a new game has been registered on the Tencent Cloud official website (xxxxxxxxxxxx).
- **Return value**: 0 indicates a successful call.

### User login API
**Function signature**
```
public static native int onUserLogin(int accountType, int worldId, String openId, String roleId);
```

**Parameter description**

| Parameter | Title 2 |
|---------|---------|
| account_type | Account type associated to the operating platform. Refer to TssSdkEntryId below. |
| worldId | Information on the server where user's game role is created |
| openId | User's unique ID, which can be a custom string. This is required for penalties purposes. |
| roleId | Identifies the varying roles created by a user |

For the account_type, 1 indicates QQ (default), 2 indicates WeChat, and 99 indicates other platforms. Chinese and international mainstream platforms, please refer to the following values.
```
enum TssSdkEntryId
{
ENTRY_ID_QZONE = 1, // QQ
ENTRY_ID_MM = 2, // WeChat
ENTRT_ID_FACEBOOK = 3, // facebook
ENTRY_ID_TWITTER = 4, // twitter
ENTRY_ID_LINE = 5, // line
ENTRY_ID_WHATSAPP = 6, // whatsapp
ENTRY_ID_OTHERS = 99, // Other platforms
};
```
- world_id is defined by the game. Enter 0 if the game has only one server.
- role_id is used to identify different roles of an account under one server. Enter "" if there is only one role.
- open_id is assigned by the specific operating platform to uniquely identify users.
**Return value**: 0 indicates a successful call.

### API for switching from foreground to background
**Function signature**
```
int onAppPause ();
```
If the App switches from foreground to background, the game is inactive.
**Return value**: 0 indicates a successful call.

### API for switching from background to foreground
**Function signature**
If the App switches from background to foreground, the game is active.
**Return value**: 0 indicates a successful call.

### When to call the function
1. Call TP2Sdk.initEx immediately after the game is launched. Parameters are gameID and appKey. Calling the security API function earlier can better protect the game process.
2. TP2Sdk.onUserLogin is called after the game is authorized by the user to access its login information. If the game has set world_id and role_id, then call the TP2Sdk.onUserLogin function after obtaining both world_id and role_id. During gameplay, if you need to retrieve the user's login information in situations like when the network is disconnected or the user logged out and needs to re-login, you will need to call the function again. The parameter to be passed is the user's account information, which can be customized.
3. TP2Sdk.onAppPause is called when the game switches from foreground to background.
4. TP2Sdk.onAppResume is called when the game switches from background to foreground.

### Sample Code
```
public void onCreate()
 {
//Called immediately after the game is launched.
TP2Sdk. initEx(9000, "d5ab8dc7ef67ca92e41d730982c5c602");
int accountType = ENTRYID.ENTRY_ID_QZONE; /* Account type */
int worldId = 1; /* Server id*/
String openId = "B73B36366565F9E02C752"; /* Platform-specific user ID */
String roleId = "paladin"; /* Role id*/
// Called when the user logs in the game
TP2Sdk.onUserLogin(accountType, worldId, openId, roleId);
}
// Game switches from foreground to background
public void onPause()
 {
super.onResume();
TP2Sdk.onPause();
}
// Game switches from background to foreground
public void onResume()
{
super.onResume();
TP2Sdk.onResume();
}
```

## Verifying Whether the SDK is Integrated Correctly
1. Connect your Android phone to a Windows PC via a USB cable. After the connection is successful, log in to the Android ADB console using Windows CMD, as shown below:
![](https://mc.qcloudimg.com/static/img/091f2d44b4862e843748fdd9655e9914/image.png)
2. Type cd /sdcard, press enter, then type mkdir sdk, and press enter, to create the /sdcard/sdk directory. If the directory already exists, a prompt indicating "mkdir failed for /sdcard/sdk. File exists" will appear, and you can proceed to the next step:
![](https://mc.qcloudimg.com/static/img/748c74c2ef3f5bec2a650f3d8eb0bdc6/image.png)
3. Type cd /sdcard/sdk to enter the directory, and type echo>enable.log to create an empty file enable.log.
![](https://mc.qcloudimg.com/static/img/26aa6733a77a4c2625d131cddba47b89/image.png)
Files under the directory created by the shell may not be accessed on some models. In this case, change the /sdcard/sdk directory with root user or use another mobile phone.
![](https://mc.qcloudimg.com/static/img/91cd8bb85e88eede943d47570a792c35/image.png)
4. Start and log in to the game, check whether tp2.log and tlog.log are generated in the /data/data/log directory, as shown below:
![](https://mc.qcloudimg.com/static/img/3ce91cbdb15cdb72998fbfcc2bdf074e/image.png)
If no log is generated, check whether you have the read/write permission to /sdcard/sdk and enable.log. This directory cannot be read/written on a small number of models. Use another model for testing or change /sdcard/sdk to /data/data/log with root user.
>**Note:** enable.log is only used for testing purposes.
5. Open the tp2.log file, and check whether it contains the information of three native APIs **tp2_sdk_init_ex, tp2_setuserinfo and setgamestatus** as well as the jar packet's version number **jar_ver**. Only when all the above conditions are met, can the security SDK run properly. setgamestatus:1 indicates that the current process is running in the foreground, and setgamestatus:2 indicates that the current process is running in the background.
Verify whether the API is correctly called by switching the App between foreground and background, and also check whether the userinfo is entered correctly.
![](https://mc.qcloudimg.com/static/img/75eef4a35cf89e8e1d02be304403377b/image.png)
6. Open tlog.log to view the data sent by the security SDK, as shown below:
![](https://mc.qcloudimg.com/static/img/50526870e79bb4d21d5b5bb0c333f86f/image.png)
In addition to reporting some basic process information during initialization, the security SDK also sends data according to the results of periodic security scanning, such as the incorrect signature of the App certificate, modification of memory data, a running add-on process, etc. The tlog.log records the data (only generated during testing) sent by the SDK. Generally, the data size per hour is about 20 KB. You can check the size of tlog.log to calculate the volume of data sent by the security SDK.

