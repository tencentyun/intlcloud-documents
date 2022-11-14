[](id:structure)

## Project Structure

The project contains four modules: [app](#app), [ugckit](#ugckit), [xmagickit](#xmagickit), and [beautysettingkit](#beautysettingkit).

## app[](id:app)
### Directory overview
<img src="https://qcloudimg.tencent-cloud.cn/raw/94254bf5017089b5cfe0a2de144dd419.png" width=500>

| File/Directory | Description |
| ------------ | ------------------------------------------------------------ |
| common | Common components, including tools and custom UIs (beauty filter and player controls) |
| login | The account module, including login and registration |
| logoff | The account cancellation UI |
| mainui | The main UI of the UGSV demo app, including main activities and the video list |
| manager | The permission processing module |
| play | The VOD playback module |
| userinfo | The profile module |
| videochoose | The video file selection module |
| videoeditor | The video editing module |
| videojoiner | The video composition module |
| videopublish | The video publishing module |
| videorecord | The video shooting module |
| webview | The module for loading HTML5 mobile web pages |

[](id:function)
### Module overview
The UGSV demo app's functional modules include account, main UI, playback, and UGSV (editing, composition, shooting, and publishing), which correspond to different codes. Below is a description of these modules plus their implementation methods.
[](id:account)
#### Account module
- The account module handles the logics of user login/registration and login data caching.
- You can replace this module with your own account system if you already have one.
- The account module registers usernames and passwords with the backend of the UGSV demo app by calling `register` of `TCUserMgr`, handles logins by calling `login` of `TCUserMgr`, caches login data locally in Sharepreference, and clears the cached data after logout.

**Code:**

| Class                                                         | Description                                    |
| ----------------------- | ------------------------------------------------------------ |
| TCApplication.java | SDK initialization class |
| TCLoginActivity.java | User login view |
| TCRegisterActivity.java | User registration view |
| TCUserMgr | User login/registration management class |
| ProgressFragmentUtil       | Control for displaying the progress bar                                        |
| TCUserInfoFragment.java | User profile view |
| TCAboutActivity | "About" view of the UGSV demo app |

[](id:board)
#### Main UI and list management
- The main UI offers access to three primary features of the app: video list, video shooting/editing, and user profile.
- By default, users log in to the video list page. When they click **+**, a dialog box pops up asking them to select whether to shoot new videos or edit local videos. They can also click the user profile button to go to the user information page.
- The list management module pulls and displays the video list.

**Code:**

| Class                                                         | Description                                    |
| -------------------------- | -------------------------------------------------------- |
| TCSplashActivity.java | Splash screen |
| TCMainActivity.java | The main UI, which includes the video list, video recording/editing and user profile pages |
| TCLiveListMgr.java | List management class, which provides APIs to get local videos and update the video list from the server |
| TCLiveListFragment.java | List view, which displays video information |
| TCLiveListAdapter.java | Video list adapter |
| TCUGCVideoListAdapter.java | Video list adapter |
| TCVideoInfo | Video data |

[](id:record)
#### Short video shooting module
With the UGSV demo app, users can shoot [UGSV](https://intl.cloud.tencent.com/document/product/1069/37911) not longer than one minute, but the SDK does not show video length.
**Code:**

| Class                                                         | Description                                    |
| -------------------------- | -------------------- |
| TCVideoRecordActivity.java | Video shooting view |
| RecordProgressView | View for pressing and holding to shoot videos |
| ComposeRecordBtn | Progress bar for multi-segment shooting |

[](id:file)
#### File selection module
This module lists all the MP4 files stored locally on phones for users to choose from.
**Code:**

| Class                                                         | Description                                    |
| ----------------------------- | ---------------------------------------------------- |
| TCVideoChooseActivity.java | Local MP4 file selecting view|
| TCVideoEditerListAdapter.java | Local MP4 file list adapter |
| TCVideoEditerMgr.java | MP4 file management class, which provides an API to get the MP4 files stored on mobile phones |
| TCVideoFileInfo.java | Local video data |

[](id:edit)
#### Editing module
The [video editing](https://intl.cloud.tencent.com/document/product/1069/38024) module offers features including video clipping, slow motion, filters, music mixing, stickers and subtitling.

**Code:**
- **videoeditor/ directory: **
<table>
<thead><tr><th>Class</th><th>Description</th></tr></thead>
<tbody><tr>
<td>TCVideoPreprocessActivity.java</td>
<td>Video pre-processing view, which is displayed when users start editing a video after shooting</td>
</tr><tr>
<td>TCVideoCutterActivity.java</td>
<td>Video clipping view</td>
</tr><tr>
<td>TCVideoEditerActivity.java</td>
<td>The editing view displayed after video clipping, with options including music, filters, speed adjustment, tone, stickers and subtitles at the bottom</td>
</tr><tr>
<td>TCVideoEffectActivity.java</td>
<td>The special effect adding view, which shows when users click the button at the bottom</td>
</tr><tr>
<td>BaseEditFragment.java</td>
<td>Parent class of the special effect fragment, which controls the playback of special effects on multiple views</td>
</tr><tr>
<td>TCVideoJoinerActivity.java</td>
<td>If users select multiple files to edit, the SDK will compose the videos.</td>
</tr>
</tbody></table>
- **videoeditor/cutter/directory**: Video clipping
- **videoeditor/time/ directory**: Speed adjustment, including slow motion, loop and rewind.
- **videoeditor/bgm/ directory**: Background music
- **videoeditor/paster/ directory**: Stickers, including animated and static stickers
- **videoeditor/motion/ directory**: Four animated filters. You cannot add your own filters. To use more filters, contact us by submitting a ticket.
- **videoditor/bubble/ directory**: Bubble subtitles
- **videoeditor/utils/ directory**: Video editing tools
- **videoeditor/common/directory**: Common video editing components
- **videojoiner/directory**: Video composition


[](id:pod)
#### Short video publishing module
This module allows users to publish videos to Tencent Cloud's video distribution platform (VOD system).
**Code:**

| Class                                                         | Description                                    |
| ----------------------------- | -------------- |
| TCVideoPublisherActivity.java | Video publishing view|

[](id:play)
#### Short video playback
This module allows users to swipe up and down to play videos that have been published to the VOD system.

**Code:**

| Class                                                         | Description                                    |
| ------------------------- | -------------- |
| TCVodPlayerActivity.java | UGSV playback view |

## ugckit[](id:ugckit)
<img src="https://qcloudimg.tencent-cloud.cn/raw/be809606cec3c56ed629a05736c292aa.png" width=500>

This module is the advanced encapsulation (with the UI) of the UGSV SDK to facilitate quick integration.
### Directory overview

| File/Directory | Description |
| ---------------------------- | ------------------------------------------------------------ |
| base | General APIs |
| component | Components used on the UI |
| module | Encapsulated modules such as clipping, editing, special effects, composition, shooting, multi-screen shooting, upload, and video selection to be used by the corresponding views |
| utils | The tool module |
| PermissionIntroductionDialog | The permission pop-up window |
| UGCKit | The UGSV initialization class |
| UGCKitConstants | Constant configuration information |
| UGCKitPicturePicker | The view of the image selection module |
| UGCKitVideoCut | The view of the short video clipping module |
| UGCKitVideoEdit |The view of the short video editing module |
| UGCKitVideoEffect | The view of the short video special effect setting module |
| UGCKitVideoJoin | The view of the short video composition module |
| UGCKitVideoMixRecord | The view of the multi-screen shooting module |
| UGCKitVideoPicker | The view of the video selection module |
| UGCKitVideoPublish | The view of the video upload module |
| UGCKitVideoRecord | The view of the short video recording module |

## xmagickit[](id:xmagickit)
<img src="https://qcloudimg.tencent-cloud.cn/raw/5142c8534c29f9af2b43a8d2aa68d12a.png" width=500>

This module encapsulates Tencent Effect so that it can quickly integrated.

| File/Directory | Description |
| ---------- | ------------------------------------------------------------ |
| config | The configuration information for parsing animated effect resources downloaded dynamically in the demo project |
| download | The module for downloading animated effect resources |
| module | The class for creating and encapsulating Tencent Effect beauty filter attributes |
| panel | The beauty filter panel module |
| utils | The tool class |
| widget | The custom view |
| XMagicImpl | The basic encapsulation of beauty filter objects for easier use |

## beautysettingkit[](id:beautysettingkit)

<img src="https://qcloudimg.tencent-cloud.cn/raw/7b3306355b0354522f0ae11f432b2184.png" width=500>

This module is the basic beauty filter module of UGSV. To use basic beauty filters, you can use this module for quick integration.

| File/Directory | Description |
| ------------ | ------------------ |
| adapter | The UI adapter of the beauty filter panel |
| constant | The beauty filter constant definitions |
| download | The beauty filter download module |
| model | The encapsulated module of beauty filter attributes |
| utils | The tool class |
| view | The beauty filter panel |
| BeautyImpl | The encapsulation class for using beauty filters |
| BeautyParams | The encapsulation class of beauty filter parameters |

