[](id:structure)
## 1. Project Structure
![](https://main.qcloudimg.com/raw/6dece0a7e9535e3fdb138975ff69452c.png)
A UGSV application mainly integrates `UGCKit` as the core feature library, which is used for playback and shoot. For the integration method, please see [UGCKit](https://github.com/tencentyun/UGSVSDK/tree/master/iOS).
The UGSV application implements the beauty filter feature mainly by integrating `BeautySettingkit`. For the integration method, please see [iOS](https://intl.cloud.tencent.com/document/product/1069/38028),[Eye Enlarging, Face Slimming, and Pendants (iOS)](https://intl.cloud.tencent.com/document/product/1069/38030) . The relevant code is in the `BeautySettingKit` directory.

[](id:function)
## 2. Module Overview
UGSV features are divided into seven modules, including:
- Account, list management, release, and profile modules, which are in the UGSV application's directory.
- Playback, shoot, and editing modules, which are managed by `UGCKit`.

[](id:accounts)
### Account module
- The account module is used to process user login/signup and login caching logic.
- If you have your own account system, you can directly replace this module with your system.
- The UI logic of the account module includes `XiaoShiPin/AppViewControllers/Account` and `XiaoShiPin/AppViewControllers/AccountInfo`. The former is related to the login UI module, and the latter the profile processing UI module used after login.
- The business logic of the account module can be viewed in `XiaoShiPin/Model`.

[](id:board)
### Homepage and list management
#### Module overview
- The homepage module is mainly used to switch between three level-1 features: VOD list, shoot, and profile.
- After the application is opened, the list page will be displayed by default. If you click "Shoot" but have not logged in, you will be redirected to the login page first; if you have logged in, you will be redirected to the push page. If you click "Profile", you will be redirected to the profile page.
- List management includes list pull and display.

#### Relevant code
- Model:
	- TCLiveListModel(`XiaoShiPin/AppViewControllers/mainList`): VOD list's definition at the data layer and serialization/deserialization implementation.
- UI:
	- TCNavigationController: custom navigation bar, which is mainly used to set the navigation bar background color.
	- TCMainViewController: homepage tab bar control, which is used to switch between the list, shoot, and profile tabs.
	- TCVideoListCell: VOD list's cell class, which is mainly used to display the covers, titles, and nicknames.
	- TCLiveListViewController: VOD list's `TableViewController`, which is used to display the VOD list. If it is clicked, the playback page will be displayed.

[](id:play)
### Playback module
#### Module overview
The playback module mainly provides features such as short video preload, playback, caching, and sharing.

#### Relevant code
The `/XiaoShiPin/AppViewControllers/VideoPlayer` directory mainly contains the business logic and UIs for playback.

[](id:record)
### Shoot module
#### Module overview
The shoot module mainly provides features such as multi-segment short video shoot, multi-segment deletion, multi-resolution shoot, and adjustable-speed shoot.

#### Relevant code
The `UGCKit/Source/Record` directory contains all the shoot-related logic.

[](id:edit)
### Editing module
#### Module overview
The editing module mainly provides features such as short video clipping, background music, filters, special effects, animated stickers, and static stickers.

#### Relevant code
The `UGCKit/Source/Edit` directory contains all the editing-related logic.

[](id:pod)
### Release module
#### Module overview
The release module mainly provides features such as short video release.

#### Relevant code
The `XiaoShiPin/AppViewController/Publish` directory contains all the release-related logic.

[](id:file)
### Profile module
#### Module overview
- The profile module is mainly used to display, store, and modify the user profile and sync such operations to the server.
- The user profile mainly includes user profile photo, nickname, gender, live stream cover, location, etc. The profile module is provided by the IMSDK, which allows you to add custom fields to enrich the user profile.
- The profile module syncs the latest user profile from the server to the application, and the user can view their own profile information such as photo, nickname, and gender through the profile module.
- The user can modify their own profile through the profile module, which will sync the modification to the server.
- The user profile can also be obtained and modified in other modules through the profile module.
	
#### Relevant code
The `XiaoShiPin/AppViewController/AccountInfo` directory contains all the user profile-related logic.




