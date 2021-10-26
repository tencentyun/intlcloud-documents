[](id:structure)
## Project Structure

Download the source code for the UGSV demo app and open the project with Android Studio. You will see a directory structure as shown below.
![](https://main.qcloudimg.com/raw/56990c09cfb83517988f721a0f694530.png)

| File/Directory | Description |
| ------------ | ------------------------------------------------------------ |
| common | Common components, including tools and custom UIs (beauty filter and player controls) |
| login | Account module, including login and registration |
| mainui | Main UI of the UGSV demo app, including main activities and the video list |
| play | Playback module |
| userinfo | User profile module |
| videochoose | Video file selection module |
| videoeditor | Video editing module |
| videojoiner | Video splicing module |
| videopublish | Video publishing module |
| videorecord | Video shooting module |
| jniLibs | Tencent’s SDKs underlying the UGSV demo app, mainly BuglySDK, plus the libraries used for file uploading and LiteAVSDK |

[](id:effect)
## Animated Stickers

The source code for the UGSV demo app uses LiveAV_UGC by default, which does not offer animated stickers. To use animated stickers, please download the Enterprise Edition [here](https://intl.cloud.tencent.com/document/product/1069/37914).

[](id:function)
## Module Introduction

The UGSV demo app’s functional modules include account, main UI, playback, and UGSV (editing, splicing, shooting, and publishing), which correspond to different codes. Below is a description of these modules plus their implementation methods.

[](id:account)
### Account

#### Description

- The account module handles the logics of user login/registration and login data caching.
- You can replace this module with your own account system if you already have one.
- The account module registers usernames and passwords with the backend of the UGSV demo app by calling `register` of `TCUserMgr`, handles logins by calling `login` of `TCUserMgr`, caches login data locally in Sharepreference, and clears the cached data after logout.

#### Code

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
### Main UI and list management

#### Description

- The main UI offers access to three primary features of the app: video list, video shooting/editing, and user profile.
- By default, users log in to the video list page. When they click **+**, a dialog box pops up asking them to select whether to shoot new videos or edit local videos. They can also click the user profile button to go to the user information page.
- The list management module pulls and displays the video list.

#### Code

| Class                                                         | Description                                    |
| -------------------------- | -------------------------------------------------------- |
| TCSplashActivity.java | Splash screen |
| TCMainActivity.java | Main view, which includes the video list, video recording/editing and user profile pages |
| TCLiveListMgr.java | List management class, which provides APIs to get local videos and update the video list from the server |
| TCLiveListFragment.java | List view, which displays video information |
| TCLiveListAdapter.java | Video list adapter |
| TCUGCVideoListAdapter.java | Video list adapter |
| TCVideoInfo | Video data |

[](id:record)
### Video shooting

#### Description

With the UGSV demo app, users can shoot [UGSV](https://intl.cloud.tencent.com/document/product/1069/37911) not longer than 1 minute, but the SDK does not show video length.

#### Code

| Class                                                         | Description                                    |
| -------------------------- | -------------------- |
| TCVideoRecordActivity.java | Video shooting view |
| RecordProgressView | View for pressing and holding to shoot videos |
| ComposeRecordBtn | Progress bar for multi-segment shooting |

[](id:file)
### File selection

#### Description

This module lists all the MP4 files stored locally on phones for users to choose from.

#### Code

| Class                                                         | Description                                    |
| ----------------------------- | ---------------------------------------------------- |
| TCVideoChooseActivity.java | Local MP4 file selecting view|
| TCVideoEditerListAdapter.java | Local MP4 file list adapter |
| TCVideoEditerMgr.java | MP4 file management class, which provides an API to get the MP4 files stored on phones |
| TCVideoFileInfo.java | Local video data |

[](id:edit)
### Video editing

#### Description

The [video editing](https://intl.cloud.tencent.com/document/product/1069/38024) module offers features including video clipping, slow motion, filters, music mixing, stickers and subtitling.

#### Code

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
<td>If users select multiple files to edit, the SDK will splice the videos.</td>
</tr>
</tbody></table>
- **videoeditor/cutter/directory**: video clipping
- **videoeditor/time/ directory**: speed adjustment, including slow motion, loop and rewind.
- **videoeditor/bgm/ directory**: background music
- **videoeditor/paster/ directory**: stickers, including animated and static stickers
- **videoeditor/motion/ directory**: four animated filters. You cannot add your own filters. To use more filters, please contact us by submitting a ticket.
- **videoditor/bubble/ directory**: bubble subtitles
- **videoeditor/utils/ directory**: video editing tools
- **videoeditor/common/directory**: common video editing components
- **videojoiner/directory**: video splicing


[](id:pod)
### Video publishing

#### Description

This module allows users to publish videos to Tencent Cloud’s video distribution platform (VOD system).

#### Code

| Class                                                         | Description                                    |
| ----------------------------- | -------------- |
| TCVideoPublisherActivity.java | Video publishing view|

[](id:play)
### Playback

#### Description

 This module allows users to swipe up and down to play videos that have been published to the VOD system.

#### Code

| Class                                                         | Description                                    |
| ------------------------- | -------------- |
| TCVodPlayerActivity.java | UGSV playback view |





