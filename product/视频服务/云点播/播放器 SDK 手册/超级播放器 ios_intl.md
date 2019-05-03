## Overview

The Super Player SDK for iOS is an open-source Tencent Cloud player component, and it provides powerful playback capabilities similar to Tencent Video - it allows users to convert portrait video to landscape or vice versa, to select the video quality, to enable gesture recognition and small window for the video playback, as well as to cache video, switch between software/hardware decoding and adjust playback speed. It is compatible with more video formats and more powerful than the system-default player. It also enables many other advanced functions such as instant playback on the splash screen and video thumbnails.

## SDK Download

The VOD Super Player SDK for iOS can be downloaded [here](https://github.com/tencentyun/SuperPlayer_iOS).

## Target Audience

This document describes Tencent Cloud's proprietary capabilities. Please make sure that you have activated the relevant [Tencent Cloud](https://cloud.tencent.com/) services. If you haven't registered an account, please [sign up](https://cloud.tencent.com/login).

## Quick Integration

### Preparations for Access

#### Scheme 1. Official CocoaPods

Add the following code to your Podfile:
```
pod 'SuperPlayer'
```

#### Scheme 2. Local CocoaPods

[Download the SDK](https://github.com/tencentyun/SuperPlayer_iOS) and zip it in your local system. After that, you can see the extracted files.

![](https://mc.qcloudimg.com/static/img/5ef04a5e101beea834813e58fc5115ec/androidzippkg.png)

The player code is in `Demo/SuperPlayer` and the SDK library is in the SDK directory.
In your Podfile, add the following code:

```
pod 'SuperPlayer', :path => '<unzipped folder path>/Demo/SuperPlayer/SuperPlayer.podspec', :subspecs => ['Player']
# subspecs varies by the downloaded SDK. If you download the Pro edition, you need to change Player to Professional, and so on.
```
Enter `pod install` or `pod update` on the command line to perform the installation.

### Using the Player

The main class of the player is `SuperPlayerView`, and videos can be played after it is created.
```objective-c
// Import the header file
#import <SuperPlayer/SuperPlayer.h>
_playerView = [[SuperPlayerView alloc] init];
// Set the delegate to accept events
_playerView.delegate = self;
// Set the parent View; _playerView will be automatically added under holderView
_playerView.fatherView = self.holderView;
SuperPlayerModel *playerModel = [[SuperPlayerModel alloc] init];
// Set the playback information
playerModel.appId = 1252463788;  // AppId
playerModel.fileId = @"4564972819219071679";  // Video FileId
// Start playback
[_playerView playWithModel:self.playerModel];
```
Run the code and you can see that the video is played on the phone and most of the features in the interface are available.
![](https://main.qcloudimg.com/raw/128c45edfc77b319475868c21caec2de.png)

### Selecting a FileId

A video FileId is usually returned by the server after the video is uploaded:
1. After the video is released to the client, the server will return a [fileId](https://cloud.tencent.com/document/product/584/9367#8..E5.8F.91.E5.B8.83.E7.BB.93.E6.9E.9C) to the client.
2. When the video is uploaded to the server, the corresponding fileId is included in the notification of the [upload confirmation](https://cloud.tencent.com/document/product/266/9757).

If the file already exists in Tencent Cloud, you can go to [Video Management](https://console.cloud.tencent.com/video/videolist), find the corresponding file, and view its fileId. The ID as shown in the figure below is the fileId:
![Video Management](https://main.qcloudimg.com/raw/15c5d181b9037b58db5cf192fe831f1b.png)

## Thumbnails and Timestamps

When long videos are played, thumbnails (image sprite) and timestamps can help viewers find the points of interest easily. You can use TencentCloud API to quickly process videos.
- [Create a sprite by screencapturing](https://cloud.tencent.com/document/product/266/8101)
- [Add a timestamp](https://cloud.tencent.com/document/product/266/14190)

After the task is successfully executed, new elements will be displayed in the player interface.

![](https://main.qcloudimg.com/raw/55ebce6d0c703dafa1ac131e1852e025.png)

## Playing a DRM-encrypted Video

Digital Rights Management (DRM) encrypts copyrighted works through technical means and controls their use, modification, and distribution to protect their security. It is applicable to copyrighted multimedia content such as music and movies.

The iOS player can play the outputs of two encryption methods:

1. Encrypted HLS format based on FairPlay
2. Encrypted HLS format based on SimpleAES

For more information about DRM, see [How to Protect the Copyright of Content](<https://cloud.tencent.com/document/product/266/34105#.E5.95.86.E4.B8.9A.E7.BA.A7-drm>).

### How to Use

First, the app needs to get the token from your **business backend**. For more information about how to generate a token, see [here](<https://cloud.tencent.com/document/product/266/34102#token-.E7.94.9F.E6.88.90>).

If you need to play FairPlay-encrypted content, follow the [ASK and FPS Certificate Guidelines](https://cloud.tencent.com/document/product/266/34102#ask-.E5.92.8C-fps-.E8.AF.81.E4.B9.A6) to generate an FPS certificate whose content is indicated by `fairplay_cer`.

Then, play the video through FileId + Token with the following playback code:

```
SuperPlayerModel *model = [[SuperPlayerModel alloc] init];
SuperPlayerVideoId *video = [[SuperPlayerVideoId alloc] init];
video.appId = 1253039488;
video.fileId = @"15517827183850370616";
video.playDefinition = @"20";
video.version = FileIdV3; // The V3 protocol is required for DRM
model.videoId = video;
model.token = token; // Token issued by the server
model.certificate = fairplay_cer; // FairPlay's certificate which is read from the local file
```

`playDefinition` in the code is the ID of the [playback template](https://cloud.tencent.com/document/product/266/34101#.E6.92.AD.E6.94.BE.E6.A8.A1.E6.9D.BF). The player will play the video as specified by the playback template. For example, if the template ID is 20, the player will first try to play the output of commercial encryption, and if it cannot play, downgrade and play the output of SimpleAES encryption.

## Small Window Playback

A small window is a player that floats over the main window within the app. Small window playback is very simple. You just need to call the following code in the appropriate location:
```objective-c
SuperPlayerWindowShared.superPlayer = _playerView; // Set the player for small window playback
SuperPlayerWindowShared.backController = self;  // Set the returned view controller
[SuperPlayerWindowShared show]; // Floating display
```
![](https://main.qcloudimg.com/raw/e2ee64230af1b9c3a79cad935afa8b6a.jpeg)

## Exiting Playback

When the player is no longer needed, please call resetPlayer to clear the internal state of the player and free up the memory.
```objective-c
[_playerView resetPlayer];
```

## More Features

To experience the complete features, scan the QR code to download the Tencent Video Cloud toolkit or run the project demo directly.
![Download QR code for iOS](https://main.qcloudimg.com/raw/b670e99ddb3f0d828798520e19f40fa7.png)
