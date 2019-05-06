
This document describes the Super Player for Tencent Cloud Web Video-on-Demand (VOD) service.  You can integrate the Super Player with your web applications through Tencent Cloud API to process video playback. This document is written for developers who have at least basic JavaScript knowledge.

## Features
The VOD Super Player performs video playback via the HTML5 `<video>` tag and Flash, enabling DRM-encrypted playback on a wide range of applications, including browsers that do not support video playback natively, with many other added functions such as hotlink protection.

### Supported Video Formats 

| Output Formats | Browsers for PC  | Mobile Browsers |
|------------|-----------------------------------|---------------------------------------|
| HLS (m3u8) | IE 11/10/9/8 (Flash enabled) | Android 4+ and iOS (native support) |
| MP4   	 | IE 8 (Flash enabled) | Android 4.4+ and iOS (native support) |

### Supported Browsers 
- **Desktop**: The latest versions of browsers such as Chrome, Firefox, Safari, Edge, and QQ Browser as well as IE 11/10/9/8 (Flash needs to be enabled; IE 8 is supported only on Windows 7) are supported.
- **Mobile**: Browsers compatible with the HTML5 `<video>` standard is supported, such as Android Chrome, iOS Safari, WeChat, Mobile QQ, and Mobile QQ Browser.

With this player, the same snippet of code can automatically switch between desktop browser and mobile browser in an adaptive manner. The player can automatically distinguish the platform and use the optimal playback scheme. For example, it will use the Flash player in IE 11/10/9/8 to enable the browser to play HLS videos through HTML5, preferably use the HTML5 technology in modern browsers such as Chrome for video playback, and directly use the HTML5 technology in mobile browsers.

### Video Transcoding Service
Since MP4 and HLS (m3u8) are currently the most widely supported formats in desktop and mobile browsers,  Tencent Cloud VOD converts the video format into MP4 or HLS (m3u8).

## Preparations
### Step 1. Activating the Service
Register your Tencent Cloud account at [Tencent Cloud's official website](https://cloud.tencent.com/) and then activate the **VOD** service.
### Step 2. Uploading a File
After the VOD service is being activated, you can upload a new video file at [VOD Video Management](https://console.cloud.tencent.com/video/videomanage). Please ensure that your VOD service is activated to upload a new file.
### Step 3. Getting FileID and APPID
1. Get the FileID.
On the "VOD video management" page, find the video for which you need to get the ID, click **Manage** in the "Action" column and you will see the ID in the **Basic Info** tab as shown below:
![](https://main.qcloudimg.com/raw/28e0da3aaea156ec0eecb840f2da5350.png)
2. Get the APPID 
You can find it in **Tencent Cloud Console** > **[Account Information](https://console.cloud.tencent.com/developer)**.


## Initializing the Web Player
After done with the preparation, you are ready to add a video player to your webpage in the following three steps.
### Step 1. Importing Files into the Page
Import the player style and script files:
```
 <link href="//imgcache.qq.com/open/qcloud/video/tcplayer/tcplayer.css" rel="stylesheet">
 <script src="//imgcache.qq.com/open/qcloud/video/tcplayer/tcplayer.min.js"></script>
```

>! If you want to play HLS and Dash videos via HTML5 in a cross-platform browser such as Chrome and Firefox, you need to import hls.js and dash.js before importing tcplayer.min.js.
```
 <script src="//imgcache.qq.com/open/qcloud/video/tcplayer/libs/hls.min.0.12.4.js"></script>
 <script src="//imgcache.qq.com/open/qcloud/video/tcplayer/libs/dash.all.min.2.9.3.js"></script>
```

### Step 2. Placing the Player Container
Place the player container at the desired place on the page. For example, add the following code to index.html (the container ID, width, and height can be customized).
```
<video id="player-container-id" width="414" height="270" preload="auto" playsinline webkit-playsinline>
</video>
```

>?
>- The player container must be a `<video>` tag.
>- The `player-container-id` in the sample is a customizable ID of the player container.
- It is more flexible to set the size of the player container zone through CSS  than through the attribute to have better display effects such as full-screen mode and container adaption.
>- In this sample,  `preload` specifies whether to load the video after the page is loaded. This attribute is usually set to `auto` for faster playback initialization. Other options include `meta` (loads only metadata after the page is loaded) and `none` (does not load the video after the page is loaded). Due to system restrictions, videos will not be automatically loaded on mobile devices.
>- The `playsinline` and `webkit-playsinline` are used to process inline playback when video playback is not supported in the official mobile browser.  This sample is for your reference only.
>- If  `x5-playsinline`  is set, the X5 UI player will be used in the TBS kernel.

### Step 3. Initializing the Code
Add the following initialization script to the page initialization code to pass in the fileID and appID obtained in the preparations.
```
var player = TCPlayer('player-container-id', { // player-container-id is the player container ID, which must be the same as that in HTML
    fileID: '4564972818956091133', // Pass in the fileID of the video to be played, which is required
    appID: '1253668508' // Pass in the appID of the VOD account, which is required
  });
```

>! The video to be played needs to be transcoded by Tencent Cloud as it cannot be guaranteed that the original video can be played normally in the browser.

## Complete Sample Page
[Sample code link](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-base.html)
## How to Use
Some of the features of the player are described in detail below, including best practices and precautions.
### Setting the Player Dimensions
Here are a few ways to set the dimensions of the player:

* The width and height attributes can be set for the `<video>` tag. They should be in px (for example, width = "100px" or width = 100) but not percentage.
* 	The dimensions can be set through CSS which supports values in px and percentage (for example, width:"100px" or width:"100%").

>?
>- If you do not set the width and height, the player will set its display dimensions to the resolution of the video after obtaining the resolution. If the viewable area of the browser is smaller than the video resolution, the player will not fit within the browser's viewable area; therefore, this is generally not recommended. The best practice is to set the player size through CSS.
>- Skilled use of CSS can achieve effects such as fit to full screen and container adaption.

Sample:
[Set size through CSS](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-size.html)
[Fit to the viewable area of the webpage](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-size-full-viewport.html)
[Proportional adaption](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-size-adaptive.html)

### Playing in Multiple Definitions
1. Upload a video and transcode it.
	1. Log in to [VOD Console](https://console.cloud.tencent.com/video).
	2. Click **Web Upload** > **Add a video** > **Select a file** to select a video file.
	3. Click **Next**, select **Process video while uploading** > **Manually select a transcoding template for transcoding** and configure the transcoding template as shown below:
	![](https://main.qcloudimg.com/raw/19221cb0a6f1ac92215218084d787d5f.png)
	4. Click **OK** to upload the video.
	
2. View the video file address. After the video is transcoded, files for multiple definitions will be generated.
 1. Click **Video Management** to go to the video list page.
 2. Locate the uploaded video and click <img src="https://main.qcloudimg.com/raw/6c5fae0c4c2a6b91dd575e605362ccf4.png"  style="margin:0;"> under its ID to view the video address as shown below.
![](https://main.qcloudimg.com/raw/0595704870303eafc6437b117548748d.png)
3. Use the FileID and APPID to play the video in the Tencent Cloud VOD player. The definition selection effect is as shown in the figure below:
![](https://mc.qcloudimg.com/static/img/d35731fae08327c66602ee3b7be77c2c/image.png)

>! This feature is unavailable for browser-hijacking playback. Generally, a mobile browser would hijack the playback and play the video using its own player.

Sample:
[Multiple definitions](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-base.html)

### Specifying a Playback Definition
There are two cases here: specifying a playback definition or letting the player play videos in a specific definition by default.

#### Specifying a Playback Definition
A definition can be specified for playback through the player's definition parameter.

| Option | Description |
|-------|----------|
| 10 | Mobile MP4 |
| 20 | MP4 SD |
| 30 | MP4 HD |
| 40 | MP4 UHD |
| 210 | Mobile HLS |
| 220 | HLS SD |
| 230 | HLS HD |
| 240 | HLS UHD |

In the sample below, the mobile MP4 definition is specified for playback:
[Specify a playback definition](http://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-definition.html)
>!
>- If you specify a playback definition in this way, the player will not display the definition switching menu. If you want to specify a definition and display the definition switching menu at the same time, please use the following method to specify the player to play videos in a specific definition by default.
>- This feature is unavailable when adaptive bitrate videos are played.

#### Specifying the Player to Play Videos in a Specific Definition by Default
1. Log in to the [VOD console](https://console.cloud.tencent.com/video).
2. Click **Distribution and Playback** > **Web Player**, select the player, and set the default definition as shown below.
![](https://main.qcloudimg.com/raw/c2a9ba8be1500d0332ed7bab0f113980.png)
3. Click **Video Management**, find the video with which you want to associate the player, and click **Manage** > **Web player code generation** in its operation column.
4. Click **Modify** to associate the video with the player configuration as shown in the figure below.
![](https://main.qcloudimg.com/raw/22efefd6323f11825fbef967009efabb.png)
5. When this video is played with the Tencent Cloud player, the associated player configuration will be used.

>?
>- If the video file in the default definition does not exist, the first file in the video's definition list will be obtained for playback. For example, if the player is configured to play the video in UHD by default, but the video has only SD and HD files, the video will be played in SD.
>- After the player is configured in the console, it may take up to 10 minutes for the configuration to take effect on all CDN nodes.
>- This feature is unavailable when adaptive bitrate videos are played.
>- This feature is unavailable for browser-hijacking playback.

### Playback Resuming Feature
The prerequisite for enabling playback resuming is that the video is played through fileID. Only with a unique fileID can the player record the playback time point of the video. If the page is closed before the video is completely played, the playback can be resumed from where it left off when the page is opened again in the same browser. Playback resuming can be enabled with the following parameters:

```
var player = TCPlayer('player-container-id', {
    fileID: '', // Pass in the fileID of the video to be played, which is required
    appID: '', // Pass in the appID of the VOD account, which is required
    plugins:{
        ContinuePlay: { // Turn on playback resuming
          // auto: true, // [Optional] Whether to resume automatically after the video is played
          // text: 'You left off at', // [Optional] prompt text
          // btnText: 'Resume' // [Optional] button text
        },
      }
  });
```
See the figure below for an example of the feature in use:
![](https://mc.qcloudimg.com/static/img/e155be329a6fec959e1ad6b361add390/image.png)

Sample:
[Resume playback](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-continue-play.html)

>!
> - This feature is available only for videos that are transcoded by Tencent Cloud and played through the fileID and appID.
> - This feature stores the playback time point in localStorage, which must be supported by the browser.
>- This feature is unavailable for browser-hijacking playback.
> - This feature is not interoperable across platforms/browsers. For example, if the user left off in a PC browser, they cannot resume the playback in a mobile browser or a different PC browser. If you want to implement this, you need to develop additional APIs on your own.

### Setting the Player Logo
The VOD Super Player supports configuring the player logo. You can select a player configuration in **Distribution and Playback** > **Web Player** and click the "Appearance" column to set the logo information. After the logo information is set, when a video is played using this player configuration, the logo will be displayed at the specified location.

Sample:
[Display a logo](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-logo.html)

>!
>- After the player is configured in the console, it may take up to 10 minutes for the configuration to take effect on all CDN nodes.
>- The set logo cannot be displayed for browser-hijacking playback.

### Roll Image Feature
The VOD Super Player supports configuring pre-, mid-, and post-roll images where hyperlinks can be added. You can select a player configuration in **Distribution and Playback** > **Web player management** and click the "Roll Image" column to set the roll image information.

- The default roll image display style is horizontally and vertically centered. If the image is larger than the player's display zone, it will be scaled down proportionally according to the width of the player and then horizontally centered. The excessive part of the image will not be displayed.
- You can customize the display style of the roll image through CSS.
```
.tcp-image-patch-start{} /* Pre-roll image style class */
.tcp-image-patch-pause{} /* Mid-roll image style class */
.tcp-image-patch-ended{} /* Post-roll image style class */
```

Sample:
[Roll image](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-image-patch.html)

>!
>- To avoid the video initialization speed being affected by a large roll image, we recommend using an image with a size of up to 50 KB and dimensions that do not exceed the display zone of the player.
>- After the player is configured in the console, it may take up to 10 minutes for the configuration to take effect on all CDN nodes.
>- The set roll image cannot be displayed for browser-hijacking playback.

### Thumbnail Preview
The VOD Super Player supports thumbnail preview. There are two ways to enable this feature:
1. Generate the thumbnail and VTT file of the video using the server API. For more information, see [Video Screenshot Overview - Sprite](https://cloud.tencent.com/document/product/266/11702).
2. Generate the thumbnail file and VTT file on your own and pass the URLs of the two files to the player. For more information, see the sample named "Thumbnail preview - Pass in thumbnail and VTT files"

The effect after this feature is successfully enabled is as shown in the figure below:
![](https://main.qcloudimg.com/raw/cf668bbf1a991c347fbeacb6555831c1.png)

Sample:
[Thumbnail preview - Generation on the server](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-vtt-thumbnail.html)
[Thumbnail preview - Pass in thumbnail and VTT files] (https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-vtt-thumbnail-src.html)
>!
>- This feature is only available for desktop browsers.
>- This feature is unavailable for browser-hijacking playback.
>- The more the generated thumbnails, the more accurate the progress bar preview, but the slower the loading. You need to find the desired balance.

### Changing a FileID for Playback
The video can be changed for playback by instantiating the object's loadVideoByID(args) method. The parameters supported by this method are as follows:
```
player.loadVideoByID({
  fileID: '', // Pass in the fileID of the video to be played, which is required
  appID: '', // Pass in the appID of the VOD account, which is required
  t: '', // See the description of key-based hotlink protection
  us: '', // See the description of key-based hotlink protection
  sign:'', // See the description of key-based hotlink protection
  exper:'' // See the description of preview
});
```

Sample:
[Change a fileID for playback] (http://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-change-file.html)

### Mirroring Feature
You can activate the mirroring feature to flip over the video screen as shown below:
![](https://main.qcloudimg.com/raw/d5886d7d550be72b608077f341299610.png)

Display the mirroring option in the right click menu:
```
var player = TCPlayer('player-container-id', {
  fileID: '', // Pass in the fileID of the video to be played, which is required
  appID: '', // Pass in the appID of the VOD account, which is required
  plugins: {
    ContextMenu: {
      mirror: true
    }
  }
});
```

Sample:
[Mirroring feature](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-mirror.html)

>! This feature is unavailable for browser-hijacking playback.

### Progress Bar Marking
You can enable progress bar marking in the player by [adding timestamps](https://cloud.tencent.com/document/product/266/14190) through the server API as shown below:
![](https://main.qcloudimg.com/raw/70d880065adce22cb64270f4999558f8.png)

How to enable in the player:
```
var player = TCPlayer('player-container-id', {
  fileID: '', // Pass in the fileID of the video to be played, which is required
  appID: '', // Pass in the appID of the VOD account, which is required
  plugins: {
    ProgressMarker: true
  }
});
```

Sample:
[Progress bar marking](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-progress-marker.html)

>!
>- This feature is only available for desktop browsers.
>- This feature is unavailable for browser-hijacking playback.

### HLS Adaptive Bitrate Playback
- The Master Playlist of the HLS specification can be played at an adaptive bitrate according to the network speed. During video download, if the network speed is high enough to download a ts multipart with a high bitrate, the player will play the ts multipart; otherwise, it will play a ts multipart with a low bitrate. This feature is supported by most mobile and desktop browsers.
- To use the HLS Master Playlist, you need to transcode the video through the server API, and this feature can be enabled only if the HLS Master Playlist is generated after the video is transcoded. For more information, see [Video Transcoding Overview](https://cloud.tencent.com/document/product/266/11701).
- When the HLS Master Playlist is played, the player's definition selection feature will become selecting a specified bitrate or automatic selection based on the network speed. See the figure below:
![](https://main.qcloudimg.com/raw/339d7dfb3a4d247deb70460edac35a0e.png)

>!
>- As mobile browsers don't have the corresponding API, manual selection of a specified bitrate is unavailable for mobile browsers.
>- Manual selection of a specified bitrate is not supported in Flash playback mode.
>- If the HLS Master Playlist is outputted during video transcoding, the player will preferably play the video using the HLS Master Playlist.

Sample:
[HLS Master Playlist](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-hls-masterplaylist.html)

### Referer Hotlink Protection
For detailed steps to enable this feature, see [Referer Hotlink Protection](https://cloud.tencent.com/document/product/266/14046).

The following parameters should be added to the player initialization:
```
var player = TCPlayer('player-container-id', {
     fileID: '', // Pass in the fileID of the video to be played, which is required
     appID: '', // Pass in the appID of the VOD account, which is required
     flash:{
         swf: '//[Tencent Cloud's isolated domain name]/vod-player/[appID]/[fileID]/tcplayer/player.swf' // Address of the .swf file, which is required
     }
   });
```
The swf URL needs to be passed in. If the browser uses Flash for playback, the Flash player will be obtained from this address. When the Flash player initiates a video request, the request's referer will bring this URL or the URL of the page.

>?
>- The referer of the video request initiated by the player in Flash mode will bring the swf URL in IE and Firefox or the page URL in Chrome.
>- You can also download the player.swf file to your CDN server and pass in the swf parameter pointing to the path of your CDN server.
>- The isolated domain name provided by Tencent Cloud is a domain name exclusive to each user. One appID corresponds to one domain name, which is usually in the format of [appID].vod2.myqcloud.com.
>- You need to add the domain name of the player.swf URL to the whitelist before videos for which referer hotlink protection is enabled can be played in Flash mode.
>- The Flash swf file of the player is stored under the imgcache.qq.com domain name by default. If you need to deploy it to your own server, you can download it [here](https://imgcache.qq.com/open/qcloud/video/tcplayer/player.swf) and deploy it by yourself.
>- If iframe is embedded into the player page, the referer of the video request will bring the iframe src.

### Key Hotlink Protection
For detailed steps to enable this feature, see [Key Hotlink Protection](https://cloud.tencent.com/document/product/266/14047).

The following parameters should be added to the player initialization:
```
var player = TCPlayer('player-container-id', {
     fileID: '', // Pass in the fileID of the video to be played, which is required
     appID: '', // Pass in the appID of the VOD account, which is required
     t: '',
     us: '',
     sign:''
   });
```
For the specific meanings of the t, us, and sign parameters, see [Key Hotlink Protection](https://cloud.tencent.com/document/product/266/14047).

>!
>- sign is calculated in the method of sign = md5(KEY+appId+fileId+t+us), which is slightly different from that in the [Key Hotlink Protection](https://cloud.tencent.com/document/product/266/14047). The remaining parameters are the same.
>- If referer hotlink protection is also enabled, simply add the parameters to the sample code of the referer hotlink protection configuration.
>- If the feature of playing DRM content is enabled, the calculation method of sign is: sign = md5(KEY+appId+fileId+playDefinition+t+us). For more information, see [DRM Hotlink Protection Description](https://cloud.tencent.com/document/product/266/34101).

### Preview
To use the preview feature, you need to enable key hotlink protection as instructed in [Key Hotlink Protection](https://cloud.tencent.com/document/product/266/14047). The following parameters should be added to the player initialization:
```
var player = TCPlayer('player-container-id', {
     fileID: '', // Pass in the fileID of the video to be played, which is required
     appID: '', // Pass in the appID of the VOD account, which is required
     t: '',
     us: '',
     sign:'',
     exper:''
   });
```
For the specific meanings of the t, us, sign, and exper parameters, see [Key Hotlink Protection](https://cloud.tencent.com/document/product/266/14047).

>!
>- Currently, this feature does not support commercial DRM playback solutions.
>- sign with preview is calculated in the method of sign = md5(KEY+appId+fileId+t+exper+us), which is slightly different from that in [Key Hotlink Protection](https://cloud.tencent.com/document/product/266/14047). The remaining parameters are the same.
>- The duration of video playback in the player is the length specified by the exper parameter. Unlike other preview features that control the playback duration on the playback side, the player does not get the complete video.
>- The player will still display the original video duration after the preview feature is enabled (the preview duration will be displayed for HSL videos in Chrome and Firefox).

### Encrypted HLS Playback
For detailed steps to enable this feature, see the [Video Encryption Document](https://cloud.tencent.com/document/product/266/9638).

>!
>- If the URL of the playback page or Flash swf is different from the domain name of the decryption key server, the key server needs to deploy corssdomain.xml and cross-origin resource sharing (CORS) to allow Flash and JavaScript to obtain the decryption key across origins.
>- The domain name of swf URL is configured in crossdomain.xml which must be placed in the root directory of the key server.
>- The Flash swf file of the player is stored under the imgcache.qq.com domain name by default. If you need to deploy it to your own server, you can download it [here](https://imgcache.qq.com/open/qcloud/video/tcplayer/player.swf) and deploy it by yourself.
>- Videos can be encrypted only once. Please strictly follow the steps in the Video Encryption Document.
>- The correct length of a decryption key is 16 bytes, and there cannot be blank characters at the beginning and the end.
>- Currently, this feature can be replaced with a commercial DRM solution.

### Playing DRM Content
The VOD Super Player integrates the feature of playing [DRM](https://cloud.tencent.com/document/product/266/34105#.E5.95.86.E4.B8.9A.E7.BA.A7-drm) content and supports the following DRM schemes:

- DASH scheme based on Widevine commercial encryption
- HLS scheme based on FairPlay commercial encryption
- HLS scheme based on SimpleAES basic encryption

For more information about DRM, see [How to Protect the Copyright of Content](<https://cloud.tencent.com/document/product/266/34105#.E5.95.86.E4.B8.9A.E7.BA.A7-drm>).

#### Support Conditions by Browser
The support for DRM by each browser is as follows.

| Browser | Widevine | FairPlay | SimpleAES | Dash (unencrypted) | HLS (unencrypted) |
|-------|----------|----------|-----------|------|------|
| Chrome (PC and Mac)  | ✔   |✖         | ✔        | ✔    |✔      |
| Firefox (PC and Mac) | ✔   |✖         | ✔        | ✔    |✔      |
| Edge            | ✖   |✖         | ✔        | ✔    |✔      |
| Mac Safari      | ✖   |✔         | ✔        | ✔    |✔      |
| iOS Safari      | ✖   |✔         | ✔        | ✔    |✔      |
| iOS Chrome      | ✖   |✖         | ✔        | ✖    |✔      |
| iOS WeChat and QQ     | ✖   |✖         | ✔        | ✖    |✔      |
| Android Chrome  | ✔   |✖         | ✔        | ✔    |✔      |
| Android WeChat and QQ | ✖   |✖         | ✔        | ✔    |✔      |
| IE 8, 9, 10, and 11     | ✖   |✖         | ✔        | ✖    |✔     |

>! IE uses Flash for playback.

#### How to Use

First, the app needs to get the token from your **business backend**. For more information about how to generate a token, see [here](<https://cloud.tencent.com/document/product/266/34102#token-.E7.94.9F.E6.88.90>).

If you need to play FairPlay-encrypted content, follow the [ASK and FPS Certificate Guidelines](https://cloud.tencent.com/document/product/266/34102#ask-.E5.92.8C-fps-.E8.AF.81.E4.B9.A6) to generate an FPS certificate and deploy it on your server. The URI of the certificate download address is marked as `certificateUri`.

Then, play the video through FileID + Token with the following playback code:

```
var player = TCPlayer('player-container-id', {
  appID:  '', // Pass in the appID of the VOD account, which is required
  fileID: '', // Pass in the fileID of the video to be played, which is required
  playDefinition: '' // Pass in the playback template, which is required for playing DRM content
  plugins: {
    DRM: {
      token: '', // Pass in the token issued by your backend service, which is required for playing DRM content
      certificateUri: '', // Pass in the download address of the FairPlay certificate, which is required for playing FairPlay-encrypted content
    }
  }``
});
```
The player will select an appropriate playback scheme based on the priority according to the [playback template](https://cloud.tencent.com/document/product/266/34101#.E6.92.AD.E6.94.BE.E6.A8.A1.E6.9D.BF) ID passed in and the support condition of the current browser. The priority order for DRM scheme selection is Widevine > FairPlay > SimpleAES, for example:
- If the `playDefinition` passed in is 20, the player selects the encrypted outputs of Widevine, FairPlay, or SimpleAES for playback.
- If the `playDefinition` passed in is 12, the player selects the encrypted outputs of Widevine or FairPlay for playback.
- If the `playDefinition` passed in is 10, the player selects unencrypted outputs of HLS or DASH for playback.

Sample:
[DRM auto recognition playback](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-drm-token-auto.html)

>!
>- [Playback Template Description Document](https://cloud.tencent.com/document/product/266/34101#.E6.92.AD.E6.94.BE.E6.A8.A1.E6.9D.BF).
>- [Token Generation Guide](https://cloud.tencent.com/document/product/266/34102#token-.E7.94.9F.E6.88.90).
>- [FairPlay Certificate Generation Guide](https://cloud.tencent.com/document/product/266/34102#ask-.E5.92.8C-fps-.E8.AF.81.E4.B9.A6).
>- Commercial DRM content can only be played on pages using the HTTPS protocol.
>- Currently, DRM content only supports adaptive bitrate.
