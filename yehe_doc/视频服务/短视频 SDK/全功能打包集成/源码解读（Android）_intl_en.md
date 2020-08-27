## Project Structure

Download the UGSV application code, open the project in Android Studio, and you will see the following directory structure:
![](https://main.qcloudimg.com/raw/7e871288732522edc565944b3324a694.png)

| File/Directory | Description |
| ------------ | ------------------------------------------------------------ |
| common       | Common components, including various tool classes and custom pages (beauty filters and player controls)       |
| login        | Account module, including login and signup pages |
| mainui       | UGSV application homepage, including the main activity and video list |
| play         | VOD playback module |
| userinfo     | Profile module |
| videochoose | Short video file selection module |
| videoeditor  | Short video editing module |
| videojoiner  | Short video composition module |
| videopublish | Short video release module |
| videorecord  | Short video shoot module |
| jniLibs      | Tencent SDKs and libraries depended by the UGSV application, which are mainly BuglySDK, libraries used for file upload, and LiteAVSDK |

## Animated Sticker

The Basic Edition UGSV SDK rather than the Enterprise Edition is used in the UGSV application source code, which does not contain advanced features such as animated sticker. If you need such features, please download the Enterprise Edition [here](https://intl.cloud.tencent.com/document/product/1069/37914).

## Module Overview

The UGSV application's features can be divided into the account, homepage, playback, and short video (editing, composition, shoot, and release) modules, and so is the code. These modules and their implementations are detailed below:

### Account module

#### Module overview

- The account module is used to process user login/signup and login caching logic.
- If you have your own account system, you can directly replace this module with your system.
- The account module can call `register` of `TCUserMgr` to register the username and password on the business backend of the UGSV application, call the `login` method of `TCUserMgr` to log in and cache the login information in local `Sharepreference`, and log out and clear the local cache.

#### Relevant code

| Class | Description |
| ----------------------- | ------------------------------------------------------------ |
| TCApplication.java      | SDK initialization class |
| TCLoginActivity.java    | User login page |
| TCRegisterActivity.java | User signup page |
| TCUserMgr | User login and signup management class |
| OnProcessFragment       | Fragment displaying the progress bar                                         |
| TCUserInfoFragment.java     | User profile display page  |
| TCAboutActivity             | "About" page of UGSV application |

### Homepage and list management

#### Module overview

- The homepage module is mainly used to switch between three level-1 features: short video list, short video shoot/editing, and profile.
- After successful login, the list page will be displayed by default. If you click "+", a dialog box will pop up for you to select whether to shoot a short video or edit a local one. If you click "Profile", you will be redirected to the profile page.
- List management includes list pull and display.

#### Relevant code

| Class | Description |
| -------------------------- | -------------------------------------------------------- |
| TCSplashActivity.java      | Splash screen                                                 |
| TCMainActivity.java        | Homepage, which is used to display the short video list, short video shoot/editing information, and user information pages  |
| TCLiveListMgr.java         | List management class, which provides the APIs for getting the local memory list and updating the list from the server |
| TCLiveListFragment.java    | List display page, which is used to display the short video data |
| TCLiveListAdapter.java     | Short video list adaptation layer |
| TCUGCVideoListAdapter.java | Short video list adaptation layer |
| TCVideoInfo            | Video data |

### Short video shoot module

#### Module overview

The UGSV application provides the feature of shooting one-minute [short videos](https://intl.cloud.tencent.com/document/product/1069/37911), but the SDK itself does not display the shoot duration.

#### Relevant code

| Class | Description |
| -------------------------- | -------------------- |
| TCVideoRecordActivity.java | Short video shoot page |
| RecordProgressView         | View for short video shoot by pressing and holding the button |
| ComposeRecordBtn           | Multi-segment short video shoot progress bar |


### File selection module

#### Module overview

It provides the local file selection feature and lists all .mp4 video files in the phone.

#### Relevant code

| Class | Description |
| ----------------------------- | ---------------------------------------------------- |
| TCVideoChooseActivity.java    | Local .mp4 file selection page |
| TCVideoEditerListAdapter.java | Local .mp4 file list adapter |
| TCVideoEditerMgr.java         | .mp4 video file management class, which provides an API to get the .mp4 files stored in the phone |
| TCVideoFileInfo.java          | Local video data |

### Editing module

#### Module overview

[Video editing](https://intl.cloud.tencent.com/document/product/1069/38024) includes features such as video clipping, slow motion, filters, music mix, stickers, and subtitling.

#### Relevant code

- `videoeditor/` directory

| Class | Description |
| ------------------------------ | ------------------------------------------------------------ |
| TCVideoPreprocessActivity.java | Preprocessing class page for shot videos entering the editing process                         |
| TCVideoCutterActivity.java     | Short video clipping page                                               |
| TCVideoEditerActivity.java     | Page for short video editing after clipping, which provides features such as music, filters, speed adjustment, tone adjustment, stickers, and subtitles at the bottom |
| TCVideoEffectActivity.java     | Page for adding special effects to short video, which can be displayed with a click of the button at the bottom                         |
| BaseEditFragment.java          | Parent class of the special effect fragment, which is used to control the playback status of multiple special effects           |
| TCVideoJoinerActivity.java     | Page where multiple video files are composed into one file after they are selected for editing   |

- `videoeditor/cutter/` directory
  Contents related to video clipping.

- `videoeditor/time/` directory
  Contents related to time-based special effects, such as slow motion, loop, and video reverse.

- `videoeditor/bgm/` directory
  Contents related to background music.

- `videoeditor/paster/` directory
  Contents related to static and animated stickers.

- `videoeditor/motion/` directory
  Contents related to animated filters. Four animated filters are included **(currently, custom extensions are not supported; if you need more filters, please submit a ticket for assistance)**.

- `videoditor/bubble/` directory
  Contents related to bubble subtitles.

- `videoeditor/utils/` directory
  Contents related to short video editing tools.

- `videoeditor/common/` directory
  Common short video editing components.

- `videojoiner/` directory
  Contents related to short video composition.

### Short video release module

#### Module overview

This module is used to publish the shooting file to Tencent Cloud VOD.

#### Relevant code

| Class | Description |
| ----------------------------- | -------------- |
| TCVideoPublisherActivity.java | Short video release page |

### Short video playback

#### Module overview

 This module is used to play back the videos that have been published in the VOD system. You can swipe up/down on the short video list page to quickly switch to the previous/next video.

#### Relevant code

| Class | Description |
| ------------------------- | -------------- |
| TCVodPlayerActivity.java | Short video playback page |





