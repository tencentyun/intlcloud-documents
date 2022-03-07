[](id:structure)
## 1. Project Structure
![](https://qcloudimg.tencent-cloud.cn/raw/d58cd35e0289a415d8bd7b1a0c3d84c1.png)
UGCKit, ,which is used for video shooting and playback, is the main feature library of the UGSV App. For how to integrate it, see [UGCKit](https://github.com/tencentyun/UGSVSDK/tree/master/iOS).
The beauty filters of the UGSV App are based on `BeautySettingkit`. For how to integrate it, see [TikTok-like Special Effects](https://intl.cloud.tencent.com/document/product/1069/38028). You can find the code in the `BeautySettingKit` directory.

[](id:function)
## 2. Modules
The UGSV App has seven modules:
- The account, list management, publishing, and profile modules are under the `XiaoshiPinApp` directory.
- The video playback, shooting, and editing modules are parts of UGCKit.

[](id:accounts)
### Account
- The account module handles the logics of user login/registration and login data caching.
- You can replace this module with your own account system if you already have one.
- The UI of the account module is implemented by `XiaoShiPin/AppViewControllers/Account` and `XiaoShiPin/AppViewControllers/AccountInfo`. The former is responsible for login, and the latter is responsible for profile processing.
- You can view the business logic of the account module in `XiaoShiPin/Model`.

[](id:board)
### Main view and list management
#### Description
- The main view offers access to three primary features of the app: video list, video shooting, and user profile.
- By default, users log in to the video list page. When they tap the shooting tab, they will be directed to the login page if they are not logged in and the publishing page if they are. If they tap the profile tab, the user profile page will be displayed.
- The list management module pulls and displays the video list.

#### Code
- Model:
	- TCLiveListModel(`XiaoShiPin/AppViewControllers/mainList`): data-level definition and pickling/unpickling of the video list
- UI:
	- TCNavigationController: controller for the navigation bar, used to customize the background color of the navigation bar
	- TCMainViewController: controller for the tab bar of the main view, used to switch among the video list, shooting and user profile pages
	- TCVideoListCell: cell class of the VOD list, which displays the thumbnail, title, and username
	- TCLiveListViewController: TableViewController for the video list, which displays videos and directs users to the playback page when they tap a video

[](id:play)
### Playback
#### Description
The playback module offers features including video preloading, playback, caching, sharing, etc.

#### Code
You can find the code in `/XiaoShiPin/AppViewControllers/VideoPlayer`, which includes the UI logic and business logic for playback.

[](id:record)
### Shooting
#### Description
The shooting module offers features including segment-based shooting and deletion, multi-resolution shooting, and shooting speed changing, etc.

#### Code
You can find the logic for shooting in `UGCKit/Source/Record`.

[](id:edit)
### Video editing
#### Description
The video editing module offers features including video trimming, background music adding, filters, special effects, animated and static stickers, etc.

#### Code
You can find the logic for video editing in `UGCKit/Source/Edit`.

[](id:pod)
### Publishing
#### Description
The publishing module offers the video publishing feature.

#### Code
You can find the logic for publishing in `XiaoShiPin/AppViewController/Publish`.

[](id:file)
### User profile
#### Description
- The user profile module is responsible for displaying, saving, and modifying user profiles and syncing the data to the server.
- User profiles include users’ profile photos, aliases, gender, live streaming thumbnails, regions, etc. The user profile module is provided by the IM SDK, which allows you to use custom fields to include more information in user profiles.
- The user profile module syncs the latest user profile data from the server to your app. It allows users to view their profiles, including photos, names, and gender.
- Users can modify their profiles. The changes will be synced to the server.
- Other modules can obtain and modify user profiles from this module.
	
#### Code
You can find the logic for user profiles in `XiaoShiPin/AppViewController/AccountInfo`.




