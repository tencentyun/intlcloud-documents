The UGSV player plugin for WeChat Mini Program is a solution provided by VOD for playing back UGSV content in WeChat Mini Program. This plugin contains a qualification certificate of the License for Publication of Audiovisual Programs Through Information Network and can also help you integrate with video capabilities for easy and smooth playback of your videos in WeChat Mini Program. It makes it easy for you to produce, edit, and integrate audiovisual programs and make them available to the public over the internet.

Relying on the sophisticated one-stop service platform of VOD, the UGSV player plugin for WeChat Mini Program has a rich set of features such as upload, processing, distribution, AI analysis, and content protection of videos, effectively improving your video service quality. 

## Preparations
#### Signing up for a Tencent Cloud account
1. [Sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and [verify your organizational identity](https://intl.cloud.tencent.com/document/product/378/3629).
2. Log in to the [VOD Console](https://console.cloud.tencent.com/vod) and get the [VOD APPID](https://console.cloud.tencent.com/developer) for connection to the UGSV player plugin for WeChat Mini Program.
3. Purchase the [UGSV player plugin for WeChat Mini Program](https://buy.cloud.tencent.com/vod).


#### Signing up a WeChat Mini Program
Sign up for and log in to a WeChat Mini Program on the [WeChat Official Accounts Platform](https://mp.weixin.qq.com/). Please select the category of your WeChat Official Accounts Platform according to your actual business type.
>The UGSV player plugin for WeChat Mini Program is only available to WeChat Mini Programs operated by organizational users.

#### Adding the plugin
Before using the plugin, you must first add it to your WeChat Mini Program Console in the following ways:
+ Select **Settings** > **Third-party Services** > **Add Plugin** in the WeChat Mini Program Console, search for "VOD UGSV player" in the pop-up window, select the plugin, and add it.
+ Search for the `APPID` of VOD UGSV player: `wx116d0dd5e6a39ac7`, select the plugin, and add it.

After adding the plugin, you can use it in your WeChat Mini Program.

#### Installing the WeChat Mini Program Developer Tool
+ Download and install the latest version of [WeChat Developer Tool](https://developers.weixin.qq.com/miniprogram/dev/devtools/download.html).
+ Before using the WeChat Mini Program, please read the [plugin usage documentation](https://mp.weixin.qq.com/debug/wxadoc/dev/framework/plugin/using.html) to understand the use scopes and limits of plugins.

## Using a Plugin

### Uploading video to console
1. Upload a video to the VOD Console. For detailed directions, please see [Video Upload](https://intl.cloud.tencent.com/document/product/266/33890#.E5.B7.B2.E4.B8.8A.E4.BC.A0).
2. Transcode the video to a format that can be played back in WeChat Mini Program. Currently, only videos in MP4, 3GP, and M3U8 formats are supported in this scenario. For detailed directions, please see [Video Processing](https://intl.cloud.tencent.com/document/product/266/33892).
3. After the video is successfully transcoded, it will be displayed in the list of [published videos](https://intl.cloud.tencent.com/document/product/266/33896#video-release-steps).
![](https://main.qcloudimg.com/raw/234d040ceaa88fa231e7d3f8a9ad711a.png)


### Applying for video release in WeChat Mini Program
- You can publish a video in **Media Assets** > **Videos** > **[Video Release in WeChat Mini Program](https://intl.cloud.tencent.com/document/product/266/33896#video-release-steps).
- Due to the video upload requirements of WeChat Mini Program, you can only publish videos in MP4, 3GP, and M3U8 formats. The VOD platform will audit the videos to confirm whether they can be approved for playback.
- Query release status
VOD displays the release status of an audited video to identify whether it is approved for release:
	+ If the release status is "approved", the video `fileId` has obtained the playback qualification from VOD, and the video under it can be played back in WeChat Mini Program.
	+ If the release status is "rejected", the video may be suspected of violations, and you need to manually check whether this is the case. If you believe that the video content does not involve violations, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
![](https://main.qcloudimg.com/raw/1f451438a09881a2cc8266856ed12c5d.png)

### Adding plugin code
Import the plugin code into your WeChat Mini Program. For more information, please see the [plugin usage documentation](https://developers.weixin.qq.com/miniprogram/dev/framework/plugin/using.html). The following code needs to be inserted before the plugin can be used:
```
// Insert in wxml
<my-player appid="xxxxx" fileid="xxxxxxxx" playerid="myPlayerId"></my-player>
// Declare the plugin used and its version in app.json
"plugins": {
    "myPlugin": {
      "version": "1.0.0",
      "provider": "wx116d0dd5e6a39ac7"
    }
  }
// Declare in xxxx.json of the page
"usingComponents": {
    "my-player": "plugin://myPlugin/player"
  }
```
+ appid: this parameter is required and can be viewed in **[Account Info](https://console.cloud.tencent.com/developer)** in the console.
+ fileid: this parameter is required and indicates the unique ID of a video file. After a video is uploaded, its `fileid` can be viewed in [Media Assets](https://intl.cloud.tencent.com/document/product/266/33895).
+ playerid: this parameter is required and indicates the unique ID of a video container. In your WeChat Mini Program, you need to get the specific `video context` through this ID to control the video.



## Feature List
The table below lists the features provided by the UGSV player plugin for WeChat Mini Program. You can also refer to the official [video documentation](https://developers.weixin.qq.com/miniprogram/dev/component/video.html) of WeChat Mini Program to stay informed of feature updates.

| Parameter Name | Type | Default Value | Required | Description |
|--|--|--|--|--|
|appid|string|-| Yes | Please view in your Tencent Cloud account information |
|fileid|string| -| Yes | Video file ID, which can be viewed in the media asset management information after a video is uploaded to the VOD Console |
|playerid|string|- | Yes | Unique ID of a video container, which can be customized on your own |
|controls|boolean|true| No | Whether to display the default playback controls (play/pause buttons, playback progress, and time) |
|danmu-list|Array.&lt;object&gt;|- | No | On-screen comment list |
| danmu-btn | boolean | false | No | Whether to display the on-screen comment button, which is only valid during initialization and cannot be changed dynamically |
| enable-danmu | boolean | false | No | Whether to display on-screen comments, which is only valid during initialization and cannot be changed dynamically |
| autoplay | boolean | false | No | Whether to play automatically |
| loop | boolean | false | No | Whether to loop the video |
| muted | boolean | false | No | Whether to mute the video |
| initial-time | number | 0 | No | Specifies the initial playback position of the video |
| direction | number |  -| No | Sets the video direction in full screen mode. If this parameter is not specified, it will be determined automatically based on the aspect ratio |
| show-progress | boolean | true | No | If this parameter is not set, it will be displayed only if the width is greater than 240 |
| show-fullscreen-btn | boolean | true | No | Whether to display the full screen mode button	 |
| show-play-btn | boolean | true | No | Whether to display the play button in the control bar at the bottom of the video |
| show-center-play-btn | boolean | true | No | Whether to display the play button in the middle of the video |
| enable-progress-gesture | boolean | true | No | Whether to enable the progress control gesture |
| object-fit | string | contain | No | The presentation style of the video when the video dimensions do not match the dimensions of the video container |
| poster | string | - | No | Web resource address or Tencent Cloud file ID (2.3.0) of the video cover image. If the `controls` attribute value is `false`, `poster` will not take effect |
| show-mute-btn | boolean | false | No | Whether to display the mute button |
| title | string | - | No | Video title, which will be displayed on top when in full screen mode |
| play-btn-position | string | bottom | No | Position of the play button |
| enable-play-gesture | boolean | false | No | Whether to enable playback gesture, i.e., double-tap for play/pause |
| auto-pause-if-navigate | boolean | true | No | Whether to automatically pause the video on the current page when another WeChat Mini Program page is redirected to |
| auto-pause-if-open-native | boolean | true | No | Whether to automatically pause the video on the current page when another WeChat page is redirected to |
| vslide-gesture | boolean | false | No | Whether to enable gestures for brightness and volume adjustment in non-full screen mode (same as `page-gesture`) |
| vslide-gesture-in-fullscreen | boolean | true | No | Whether to enable gestures for brightness and volume adjustment in full screen mode |
| bindplay | eventhandle |  -| No | Triggers a `play` event when playback is started/resumed |
| bindpause | eventhandle | - | No | Triggers a `pause` event when playback is paused |
| bindended | eventhandle | - | No | Triggers an `end` event when playback reaches the end |
| bindtimeupdate | eventhandle | - | No | Triggered when the playback progress changes; event.detail = {currentTime, duration}; trigger frequency: once every 250 ms |
| bindfullscreenchange | eventhandle | - | No | Triggered when the video enters/exits full screen mode; event.detail = {fullScreen, direction}; valid values of `direction`: vertical, horizontal |
| bindwaiting | eventhandle |-  | No | Triggered when the video buffers |
| binderror | eventhandle |  -| No | Triggered when an error occurs during video playback |
| bindprogress | eventhandle |-  | No | Triggered when the loading progress changes. Only one-stage loading is supported; event.detail = {buffered}; this parameter is a percentage value |

## UGSV Player Demo
VOD provides a sample demo of importing UGSV player into WeChat Mini Program. For more information, please see [Demo Source Code](https://github.com/tencentyun/mp-vod-player).
Scan the QR code below to try out the UGSV player plugin for WeChat Mini Program.
<img src="https://main.qcloudimg.com/raw/85e45f082433f47c2d17ffe59c4dcf5c.png" width="250">

 
## Instructions
+ The plugin service takes effect immediately after purchase. In addition to the purchase charge, the UGSV player plugin for WeChat Mini Program is also billed based on the number of video playbacks and VOD usage. <!--doc For more information, please see [Purchase Guide](https://intl.cloud.tencent.com/document/product/266/2838).-->
+ One Tencent Cloud account provides only one APPID; therefore, you can purchase only one plugin under your Tencent Cloud account.

