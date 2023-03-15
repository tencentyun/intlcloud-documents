## Prerequisites
1. Activate [VOD](https://intl.cloud.tencent.com/product/vod). If you don’t have an account yet, [sign up](https://intl.cloud.tencent.com/login) first.
2. Download and install Xcode from App Store.
3. Download and install CocoaPods as instructed at the [CocoaPods website](https://cocoapods.org/).

## This Document Describes
* How to integrate the Player SDK for iOS.
* How to use the Player SDK for VOD playback.
* How to use the underlying capabilities of the Player SDK to implement more features.

## SDK Integration
[](id:step1)

### Step 1. Download the SDK ZIP file
<dx-tabs>
::: Integrate via CocoaPods[](id:cocoapods)
Directly integrate `TXLiteAVSDK_Player` as a Pod:
```objective-c
 pod 'TXLiteAVSDK_Player'
```
To specify a version, you can add the following dependency to the `podfile` file:
```objective-c
 pod 'TXLiteAVSDK_Player', '~> 10.3.11513'
```

:::
::: Manually download the SDK[](id:manual)

1. Download the package of the SDK and demo on the latest version [here](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Player_iOS_latest.zip).
2. Add `SDK/TXLiteAVSDK_Player.framework` to the project to be integrated and select **Do Not Embed**.
3. You need to configure `-ObjC` of the project target; otherwise, the SDK will crash as the SDK category cannot be loaded.
```objective-c
Open Xcode, select the target, select the **Build Settings** tab, search for "Other Link Flag", and enter "-ObjC".
```
2. Add library files (in the SDK directory)
 **TXFFmpeg.xcframework**: Add the .xcframework file to the project, set it to **Embed & Sign** in **General** > **Frameworks, Libraries, and Embedded Content**, and check whether **Code Sign On Copy** is selected in **Build Phases** > **Embed Frameworks** in your **project settings** as shown below:
    **TXSoundTouch.xcframework**: Add the .xcframework file to the project, set it to **Embed & Sign** in **General** > **Frameworks, Libraries, and Embedded Content**, and check whether **Code Sign On Copy** is selected in **Build Phases** > **Embed Frameworks** in your **project settings** as shown below:<br>
    <img style="width:400px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/b226decc76c33eff8c3f5b4cc4246bea.png" />
 <br>
 Then, select **Build Settings** > **Search Paths** in Xcode and add the path of the above frameworks in **Framework Search Paths**.

<b>MetalKit.framework</b>: Open Xcode, go to your **project settings**, select **Build Phases** > **Link Binary With Libraries**, click **+** in the bottom-left corner, and enter "MetalKit" to add it to the project as shown below:<br>
<img style="width:400px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/8ab7576dcc8bbe7b36396955ca06b186.png" />
<br>
<img style="width:400px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/8480798e5ba897077ed3cef8ebc12f2e.png" />
<br>

<b>ReplayKit.framework</b>: Open Xcode, go to your **project settings**, select **Build Phases** > **Link Binary With Libraries**, click **+** in the bottom-left corner, and enter "ReplayKit" to add it to the project as shown below:<br>
<img style="width:400px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/aa07f3d4963ee703505a14a743f61a68.png" />
<img style="width:400px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/12491d4a64aa6df44e6a966e80ca54de.png" />
<br>

Add the following system libraries in the same way:

<br><b>System frameworks</b>: SystemConfiguration, CoreTelephony, VideoToolbox, CoreGraphics, AVFoundation, Accelerate, and MobileCoreServices<br>
<b>System libraries:</b> libz, libresolv, libiconv, libc++, and libsqlite3

<h4>Picture-in-Picture (PiP) feature</h4>

To use the PiP feature, configure as shown below. If you don’t need the PiP feature, skip this part.
<br>
1. To use the PiP feature of iOS, upgrade the SDK to 10.3 or later.
<br>
2. To use the PiP feature, you need to enable the background mode. In Xcode, select the target, click **Signing & Capabilities** > **Background Modes**, and select **Audio, AirPlay, and Picture in Picture** as shown below:
<br>
<img style="width:400px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/116e1e741f80d810502221fd143d8434.png" />
<br>
:::
</dx-tabs>

[](id:step2)

### Step 2. Set the SDK connection environment

In order to help you conduct business with higher quality and security in compliance with applicable laws and regulations in different countries and regions, Tencent Cloud provides two SDK connection environments. If you serve global users, we recommend you use the following API to configure the global connection environment.

```objective-c
// If you serve global users, configure the global SDK connection environment.
[TXLiveBase setGlobalEnv:"GDPR"]
```

[](id:step3)

### Step 3. Configure the license

If you have the required license, you need to get the license URL and key in the [RT-Cube console](https://console.cloud.tencent.com/vcube).
If you don't have the required license, you need to get it as instructed in [Video Playback License](https://cloud.tencent.com/document/product/881/74588).

After obtaining the license information, before calling relevant APIs of the SDK, initialize the license through the following API. We recommend you set the following in `- [AppDelegate application:didFinishLaunchingWithOptions:]`:

```objective-c
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    NSString * const licenceURL = @"<The license URL obtained>";
    NSString * const licenceKey = @"<The key obtained>";

    //TXLiveBase can be found in the "TXLiveBase.h" header file
    [TXLiveBase setLicenceURL:licenceURL key:licenceKey]; 
    NSLog(@"SDK Version = %@", [TXLiveBase getSDKVersionStr]);
}
```

[](id:step4)

### Step 4. Create a player object

The `TXVodPlayer` module of the Player SDK is used to implement the VOD feature.

```objectivec
TXVodPlayer *_txVodPlayer = [[TXVodPlayer alloc] init];
[_txVodPlayer setupVideoWidget:_myView insertIndex:0]
```

[](id:step5)

### Step 5. Create a rendering view

In iOS, a view is used as the basic UI rendering unit. Therefore, you need to configure a view, whose size and position you can adjust, for the player to display video images on.

```objectivec
[_txVodPlayer setupVideoWidget:_myView insertIndex:0]
```

Technically, the player does not render video images directly on the view (`_myView` in the sample code) you provide. Instead, it creates a subview for OpenGL rendering over the view.

You can adjust the size of video images by changing the size and position of the view. The SDK will make changes to the video images accordingly.

![](https://qcloudimg.tencent-cloud.cn/raw/235b2e8e6fc3eb328ba05a4c5d251da7.jpg)

**How to make an animation**
 You are allowed great flexibility in view animation, but note that you need to modify the `transform` rather than `frame` attribute of the view.

```objectivec
[UIView animateWithDuration:0.5 animations:^{
     _myView.transform = CGAffineTransformMakeScale(0.3, 0.3); // Shrink by 1/3
 }];
```

[](id:step6)

### Step 6. Start playback

`TXVodPlayer` supports two playback modes for you to choose as needed:

<dx-tabs>
::: Through URL
  `TXVodPlayer` will internally recognize the playback protocol automatically. You only need to pass in your playback URL to the `startPlay` function.
```objectivec
NSString* url = @"http://1252463788.vod2.myqcloud.com/xxxxx/v.f20.mp4";
[_txVodPlayer startPlay:url];
```
:::
::: Through `fileId`
```objectivec
TXPlayerAuthParams *p = [TXPlayerAuthParams new];
p.appId = 1252463788;
p.fileId = @"4564972819220421305";
[_txVodPlayer startPlayWithParams:p];
```
You can go to [Media Assets](https://console.cloud.tencent.com/vod/media) and find it. After clicking it, you can view its `fileId` in the video details on the right.
Play back the video through the `fileId`, and the player will request the backend for the real playback URL. If the network is abnormal or the `fileId` doesn't exist, the `PLAY_ERR_GET_PLAYINFO_FAIL` event will be received; otherwise, `PLAY_EVT_GET_PLAYINFO_SUCC` will be received, indicating that the request succeeded.
:::
</dx-tabs>

### Step 7. Stop playback

Remember to use **removeVideoWidget** to terminate the view control before exiting the current UI when stopping playback. This can prevent memory leak and screen flashing issues.

```objectivec
// Stop playback
[_txVodPlayer stopPlay];
[_txVodPlayer removeVideoWidget]; // Remember to terminate the view control
```

## Basic Feature Usage
### 1. Playback control

#### Starting playback

```objective-c
// Start playback
[_txVodPlayer startPlay:url];
```

#### Pausing playback

```objective-c
// Pause the video
[_txVodPlayer pause];
```

#### Resuming playback

```objective-c
// Resume the video
[_txVodPlayer resume];
```

#### Stopping playback

```objective-c
// Stop the video
[_txVodPlayer stopPlay];
```

#### Adjusting playback progress (seek)

When the user drags the progress bar, `seek` can be called to start playback at the specified position. The Player SDK supports accurate seek.

```objective-c
int time = 600; // In seconds if the value is of `int` type
// Adjust the playback progress
[_txVodPlayer seek:time];
```

#### Specifying playback start time

You can specify the playback start time before calling `startPlay` for the first time.

```objective-c
float startTimeInSecond = 60; // Unit: Second
[_txVodPlayer setStartTime:startTimeInSecond];  // Set the playback start time
[_txVodPlayer startPlay:url];
```


### 2. Image adjustment
- **view: size and position**
You can modify the size and position of the view by adjusting the size and position of the parameter `view` of setupVideoWidget. The SDK will automatically adjust the size and position of the view based on your configuration.
- **setRenderMode: Aspect fill or aspect fit**
<table>
<tr><th>Value</th><th>Description</th></tr>
<tr>
<td>RENDER_MODE_FILL_SCREEN</td>
<td>Images are scaled to fill the entire screen, and the excess parts are cropped. There are no black bars in this mode, but images may not be displayed in whole.</td>
</tr><tr>
<td>RENDER_MODE_FILL_EDGE</td>
<td>Images are scaled as large as the longer side can go. Neither side exceeds the screen after scaling. Images are centered, and there may be black bars.</td>
</tr></table>
- **setRenderRotation: Image rotation**
<table>
<tr><th>Value</th><th>Description</th></tr>
<tr>
<td>HOME_ORIENTATION_RIGHT</td>
<td>The Home button is on the right of the video image</td>
</tr><tr>
<td>HOME_ORIENTATION_DOWN</td>
<td>The Home button is below the video image</td>
</tr><tr>
<td>HOME_ORIENTATION_LEFT</td>
<td>The Home button is on the left of the video image</td>
</tr><tr>
<td>HOME_ORIENTATION_UP</td>
<td>The Home button is above the video image</td>
</tr></table>

### 3. Adjustable-Speed playback
The VOD player supports adjustable-speed playback. You can use the `setRate` API to set the VOD playback speed, such as 0.5X, 1.0X, 1.2X, and 2X.


 ```objectivec
// Set playback at 1.2X rate
[_txVodPlayer setRate:1.2]; 
// ...
// Start playback
[_txVodPlayer startPlay:url];
 ```

### 4. Playback loop

```objective-c
// Set playback loop
[_txVodPlayer setLoop:true];
// Get the current playback loop status
[_txVodPlayer loop];
```

### 5. Muting/Unmuting

```objective-c
// Mute or unmute the player. true: Mute; false: Unmute
[_txVodPlayer setMute:true];
```

### 6. Screencapturing

Call **snapshot** to take a screenshot of the current video frame. This method captures only the video frame. To capture the UI, use the corresponding API of the iOS system.


### 7. Roll image ad
The Player SDK allows you to add roll images on the UI for advertising as follows:
* If `autoPlay` is set to `NO`, the player will load the video normally but will not immediately start playing it back.
* Users can see the roll image ad on the player UI after the player is loaded and before the video playback starts.
* When the ad display stop conditions are met, the `resume` API will be called to start video playback.

### 8. HTTP-REF
`headers` in `TXVodPlayConfig` can be used to set HTTP request headers, such as the `Referer` field commonly used to prevent the URL from being copied arbitrarily (Tencent Cloud provides a more secure signature-based hotlink protection solution) and the `Cookie` field for client authentication
### 9. Hardware acceleration
It is extremely difficult to play back videos of the Blu-ray (1080p) or higher image quality smoothly if only software decoding is used. Therefore, if your main scenario is game live streaming, we recommend you use hardware acceleration.

Before switching between software and hardware decoding, you need to call **stopPlay** first. After the switch, you need to call **startPlay**; otherwise, severe blurring will occur.

```objectivec
[_txVodPlayer stopPlay];
_txVodPlayer.enableHWAcceleration = YES;
[_txVodPlayer startPlay:_flvUrl type:_type];
```

### 10. Definition settings
The SDK supports the multi-bitrate format of HLS, so users can switch between streams at different bitrates. After receiving the `PLAY_EVT_PLAY_BEGIN` event, you can get the array of multiple bitrates as follows:
```objectivec
NSArray *bitrates = [_txVodPlayer supportedBitrates]; // Get the array of multiple bitrates
```

During playback, you can call `-[TXVodPlayer setBitrateIndex:]` at any time to switch the bitrate. During switch, the data of another stream will be pulled. The SDK is optimized for Tencent Cloud multi-bitrate files to implement smooth switch.
### 11. Adaptive bitrate streaming
The SDK supports adaptive bitrate streaming of HLS. After this capability is enabled, the player can dynamically select the most appropriate bitrate for playback based on the current bandwidth. After receiving the `PLAY_EVT_PLAY_BEGIN` event, you can enable adaptive bitrate streaming as follows:
```objectivec
[_txVodPlayer setBitrateIndex:-1]; // Pass in `-1` for the `index` parameter
```
During playback, you can call `-[TXVodPlayer setBitrateIndex:]` at any time to switch to another bitrate. After the switch, adaptive bitrate streaming will be disabled.

### 12. Playback progress listening

There are two metrics for the VOD progress: **loading progress** and **playback progress**. Currently, the SDK notifies the two progress metrics in real time through event notifications. For more information on the event notification content, see [Event Listening](#listening).


```objective-c
-(void) onPlayEvent:(TXVodPlayer *)player event:(int)EvtID withParam:(NSDictionary*)param {
    if (EvtID == PLAY_EVT_PLAY_PROGRESS) {
            // Loading progress in seconds. The decimal part is in ms.
            float playable = [param[EVT_PLAYABLE_DURATION] floatValue];
                [_loadProgressBar setValue:playable];
                
            // Playback progress in seconds. The decimal part is in ms.
            float progress = [param[EVT_PLAY_PROGRESS] floatValue];
                [_seekProgressBar setValue:progress];
                
            // Total video duration in seconds. The decimal part is in ms.
            float duration = [param[EVT_PLAY_DURATION] floatValue];
            // It can be used to set duration display, etc.
    }
}
```


### 13. Playback network speed listening

You can display the current network speed when the video is lagging by [listening on events](#listening).

* You can use the `NET_SPEED` of `onNetStatus` to get the current network speed. For detailed directions, see [Playback status feedback (onNetStatus)](#status).
* After the `PLAY_EVT_PLAY_LOADING` event is detected, the current network speed will be displayed.
* After the `PLAY_EVT_VOD_LOADING_END` event is received, the view showing the current network speed will be hidden.

### 14. Video resolution acquisition

The Player SDK plays back a video through a URL string. The URL doesn't contain the video information, and you need to access the cloud server to load such information. Therefore, the SDK can only send the video information to your application as event notifications. For more information, see [Event Listening](#listening).

**Resolution information**
<dx-tabs>
::: Method 1
Use the `VIDEO_WIDTH` and `VIDEO_HEIGHT` of `onNetStatus` to get the video width and height. For detailed directions, see [Status feedback (onNetStatus)](#status).
:::
::: Method 2
Directly call `-[TXVodPlayer width]` and `-[TXVodPlayer height]` to get the current video width and height.
:::
</dx-tabs>

### 15. Player buffer size

During normal video playback, you can control the maximum size of the data buffered from the network in advance. If the maximum buffer size is not configured, the player will use the default buffer policy to guarantee a smooth playback experience.

```java
TXVodPlayConfig *_config = [[TXVodPlayConfig alloc]init];
[_config setMaxBufferSize:10];  // Maximum buffer size during playback in MB
[_txVodPlayer setConfig:_config];  // Pass in `config` to `_txVodPlayer`
```

### 16. Local video cache[](id:cache)
In short video playback scenarios, the local video file cache is required, so that general users don't need to consume traffic again to reload an already watched video.

- **Supported format:** The SDK supports caching videos in two common VOD formats: HLS (M3U8) and MP4.
- **Enablement time:** The SDK doesn't enable the caching feature by default. We recommend you do not enable it for scenarios in which most videos are watched only once.
- **Enablement method:** To enable it, you need to configure two parameters: local cache directory and cache size.
```objectivec
// Set the global cache directory of the playback engine
NSArray *paths = NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES);
NSString *documentsDirectory = [paths objectAtIndex:0];
NSString *preloadDataPath = [documentsDirectory stringByAppendingPathComponent:@"/preload"];
if (![[NSFileManager defaultManager] fileExistsAtPath:preloadDataPath]) {
     [[NSFileManager defaultManager] createDirectoryAtPath:preloadDataPath
                               withIntermediateDirectories:NO
                                                attributes:nil
                                                     error:&error];
[TXPlayerGlobalSetting setCacheFolderPath:preloadDataPath];
// Set the playback engine cache size
[TXPlayerGlobalSetting setMaxCacheSize:200];
// ...
// Start playback
[_txVodPlayer startPlay:playUrl];                            
```

>? The `TXVodPlayConfig#setMaxCacheItems` API used for configuration on earlier versions has been deprecated and is not recommended.

## Using Advanced Features

### 1. Video preloading

#### Step 1. Use video preloading

In UGSV playback scenarios, the preloading feature contributes to a smoother viewing experience: While watching a video, you can load the URL of the next video to be played back on the backend. When the next video is switched to, it will be preloaded and can be played back immediately.

Video preloading can deliver an instant playback effect but has certain performance overheads. If your business needs to preload many videos, we recommend you use this feature together with [video predownloading](#download).

This is how seamless switch works in video playback. You can use `isAutoPlay` in `TXVodPlayer` to implement the feature as follows:
<img src="https://qcloudimg.tencent-cloud.cn/raw/b2bd645f29af403bf2740156aee44092.jpg" width=850px>

```objectivec
// Play back video A: If `isAutoPlay` is set to `true`, the video will be immediately loaded and played back when `startPlay` is called
NSString* url_A = @"http://1252463788.vod2.myqcloud.com/xxxxx/v.f10.mp4";
_player_A.isAutoPlay = YES;
[_player_A startPlay:url_A];

// To preload video B when playing back video A, set `isAutoPlay` to `NO`
NSString* url_B = @"http://1252463788.vod2.myqcloud.com/xxxxx/v.f20.mp4";
_player_B.isAutoPlay = NO;
[_player_B startPlay:url_B];
```

After video A ends and video B is automatically or manually switched to, you can call the `resume` function to immediately play back video B.

>! After `autoPlay` is set to `false`, make sure that video B has been prepared before calling `resume`, that is, you should call it only after the `PLAY_EVT_VOD_PLAY_PREPARED` event of video B (2013: the player has been prepared, and the video can be played back) is detected.

```objectivec
-(void) onPlayEvent:(TXVodPlayer *)player event:(int)EvtID withParam:(NSDictionary*)param
{
    // When video A ends, directly start playing back video B for seamless switch
    if (EvtID == PLAY_EVT_PLAY_END) {
            [_player_A stopPlay];
            [_player_B setupVideoWidget:mVideoContainer insertIndex:0];
            [_player_B resume];
        }
}
```

#### Step 2. Configure the video preloading buffer

- You can set a large buffer to play back videos more smoothly under unstable network conditions.

- You can set a smaller buffer to reduce the traffic consumption. 

##### Preloading buffer size

This API is used to control the maximum buffer size before the playback starts in preloading scenarios (that is, `AutoPlay` of the player is set to `false` before video playback starts).

```objective-c
TXVodPlayConfig *_config = [[TXVodPlayConfig alloc]init];
[_config setMaxPreloadSize:(2)];;  // Maximum preloading buffer size in MB. Set it based on your business conditions to reduce the traffic consumption
[_txVodPlayer setConfig:_config];  // Pass in `config` to `_txVodPlayer`
```

##### Playback buffer size 

During normal video playback, you can control the maximum size of the data buffered from the network in advance. If the maximum buffer size is not configured, the player will use the default buffer policy to guarantee a smooth playback experience.

```objective-c
TXVodPlayConfig *_config = [[TXVodPlayConfig alloc]init];
[_config setMaxBufferSize:10];  // Maximum buffer size during playback in MB
[_txVodPlayer setConfig:_config];  // Pass in `config` to `_txVodPlayer`
```

### 2. Video predownloading[](id:download)
You can download part of the video content in advance without creating a player instance, so as to start playing back the video faster when using the player. This helps deliver a better playback experience.

Before using the playback service, make sure that [video cache](#cache) has been set.
>?
>- `TXPlayerGlobalSetting` is the global cache setting API, and the original `TXVodConfig` API has been deprecated.
>- The global cache directory and size settings have a higher priority than those configured in `TXVodConfig` of the player.

Sample:

```objective-c
// Set the global cache directory of the playback engine
NSArray *paths = NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES);
NSString *documentsDirectory = [paths objectAtIndex:0];
NSString *preloadDataPath = [documentsDirectory stringByAppendingPathComponent:@"/preload"];
if (![[NSFileManager defaultManager] fileExistsAtPath:preloadDataPath]) {
     [[NSFileManager defaultManager] createDirectoryAtPath:preloadDataPath 
      												 withIntermediateDirectories:NO 
      																					attributes:nil 
      																							 error:&error]; //Create folder
}
[TXPlayerGlobalSetting setCacheFolderPath:preloadDataPath];

// Set the playback engine cache size
[TXPlayerGlobalSetting setMaxCacheSize:200];
NSString *m3u8url = "http://****";
int taskID = [[TXVodPreloadManager sharedManager] startPreload:m3u8url 
 																									 preloadSize:10 
 																					 preferredResolution:1920*1080 
 																											delegate:self];


// Cancel predownloading
[[TXVodPreloadManager sharedManager] stopPreload:taskID];
```

### 3. Video download
Video download allows users to download online videos and watch them offline. In addition, the Player SDK provides the local encryption feature, so that downloaded local files are still encrypted and can be decrypted and played back only in the specified player. This feature can effectively prevent downloaded videos from being distributed without authorization and protect the video security.

As HLS streaming media cannot be directly saved locally, you cannot download them and play back them as local files. You can use the video download scheme based on `TXVodDownloadManager` to implement offline HLS playback.

> ! 
> - Currently, `TXVodDownloadManager` can cache only HLS files but not MP4 and FLV files.
>- The Player SDK already supports playing back local MP4 and FLV files.

[](id:offline1)
#### Step 1. Make preparations

`TXVodDownloadManager` is designed as a singleton; therefore, you cannot create multiple download objects. It is used as follows:

```objective-c
TXVodDownloadManager *downloader = [TXVodDownloadManager shareInstance];
[downloader setDownloadPath:"<Specify your download directory>"];
```

[](id:offline2)
#### Step 2. Start the download
You can start the download by URL or `fileid`.
<dx-tabs>
::: Through URL
You only need to pass in the download URL.
```objective-c
[downloader startDownloadUrl:@"http://1253131631.vod2.myqcloud.com/26f327f9vodgzp1253131631/f4bdff799031868222924043041/playlist.m3u8"]
```
:::
::: Through `fileid`
You need to pass in `appId` and `fileId` at least for download by `fileid`.
```objective-c
TXPlayerAuthParams *auth = [TXPlayerAuthParams new];
auth.appId = 1252463788;
auth.fileId = @"4564972819220421305";
TXVodDownloadDataSource *dataSource = [TXVodDownloadDataSource new];
dataSource.auth = auth;
[downloader startDownload:dataSource];
```
:::
</dx-tabs>


[](id:offline3)
#### Step 3. Receive the task information 

Before receiving the task information, you need to set the callback delegate first.

```objective-c
downloader.delegate = self;
```

You may receive the following task callbacks:
<table><thead>
<tr><th width="55%">Callback Message</th><th>Description</th></tr>
</thead>
<tbody><tr>
<td>-[TXVodDownloadDelegate onDownloadStart:]</td>
<td>The task started, that is, the SDK started the download.</td>
</tr>
<tr>
<td>-[TXVodDownloadDelegate onDownloadProgress:]</td>
<td>Task progress. During download, the SDK will frequently call back this API. You can update the displayed progress here.</td>
</tr>
<tr>
<td>-[TXVodDownloadDelegate onDownloadStop:]</td>
<td>The task stopped. When you call <code>stopDownload</code> to stop the download, if this message is received, the download is stopped successfully.</td>
</tr>
<tr>
<td>-[TXVodDownloadDelegate onDownloadFinish:]</td>
<td>Download was completed. If this callback is received, the entire file has been downloaded, and the downloaded file can be played back by `TXVodPlayer`.</td>
</tr>
<tr>
<td>-[TXVodDownloadDelegate onDownloadError:errorMsg:]</td>
<td> Download error. If the network is disconnected during download, this API will be called back and the download task will stop. For all error codes, see <code>TXDownloadError</code>.</td>
</tr>
</tbody></table>

As the downloader can download multiple files at a time, the callback API carries the `TXVodDownloadMediaInfo` object. You can access the URL or `dataSource` to determine the download source and get other information such as download progress and file size.

[](id:offline4)
#### Step 4. Stop the download

You can call the `-[TXVodDownloadManager stopDownload:]` method to stop the download. The parameter is the object returned by `-[TXVodDownloadManager sartDownloadUrl:]`. **The SDK supports checkpoint restart.** If the download directory is not changed, when you resume downloading a file, the download will start from the point where stopped.

If you don't need to resume the download, call the `-[TXVodDownloadManager deleteDownloadFile:]` method to delete the file to release the storage space.

### 4. Encrypted playback

The video encryption solution is used in scenarios where the video copyright needs to be protected, such as online education. To encrypt your video resources, you need to alter the player and encrypt and transcode video sources. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/266/38131).

### 5. Player configuration 

Before calling `statPlay`, you can call `setConfig` to configure the player parameters, such as player connection timeout period, progress callback interval, and maximum number of cached files. `TXVodPlayConfig` allows you to configure detailed parameters. For more information, see [Basic Configuration API](https://intl.cloud.tencent.com/document/product/266/47844). Below is the configuration sample code:

```java
TXVodPlayConfig *_config = [[TXVodPlayConfig alloc]init];
[_config setEnableAccurateSeek:true];  // Set whether to enable accurate seek. Default value: true
[_config setMaxCacheItems:5];  // Set the maximum number of cached files to 5
[_config setProgressInterval:200];  // Set the progress callback interval in ms
[_config setMaxBufferSize:50];  // Set the maximum preloading buffer size in MB
[_txVodPlayer setConfig:_config];  // Pass in `config` to `_txVodPlayer`
```

##### Specifying resolution when playback starts

 When playing back an HLS multi-bitrate video source, if you know the video stream resolution information in advance, you can specify the preferred resolution before playback starts, and the player will select and play back the stream at or below the preferred resolution. In this way, after playback starts, you don't need to call `setBitrateIndex` to switch to the required bitstream.

```java
TXVodPlayConfig *_config = [[TXVodPlayConfig alloc]init];
// The parameter passed in is the product of the video width and height. You can pass in a custom value.
[_config setPreferredResolution:720*1280];
[_txVodPlayer setConfig:_config];  // Pass in `config` to `_txVodPlayer`
```

##### Setting playback progress callback interval

```objective-c
TXVodPlayConfig *_config = [[TXVodPlayConfig alloc]init];
[_config setProgressInterval:200];  // Set the progress callback interval in ms
[_txVodPlayer setConfig:_config];  // Pass in `config` to `_txVodPlayer`
```

[](id:listening)

## Player Event Listening
You can bind a `TXVodPlayListener` listener to the `TXVodPlayer` object to use `onPlayEvent` (event notification) and `onNetStatus` (status feedback) to sync information to your application.

### Event notification (onPlayEvent)

#### Playback events
| Event ID | Code | Description |
| :-------------------  |:-------- |  :------------------------ |
|PLAY_EVT_PLAY_BEGIN    |  2004|  Video playback started. |
|PLAY_EVT_PLAY_PROGRESS |  2005|  Video playback progress. The current playback progress, loading progress, and total video duration will be notified of.      |
|PLAY_EVT_PLAY_LOADING|  2007|  The video is being loaded. The `LOADING_END` event will be reported if video playback resumes. |
|PLAY_EVT_VOD_LOADING_END   |  2014|  Video loading ended, and video playback resumed.                        |
| VOD_PLAY_EVT_SEEK_COMPLETE | 2019 | Seeking was completed. The seeking feature is supported by v10.3 or later. |

#### Stop events
| Event ID | Code | Description |
| :-------------------  |:-------- |  :------------------------ |
|PLAY_EVT_PLAY_END      |  2006|  Video playback ended.      |
|PLAY_ERR_NET_DISCONNECT |  -2301  | The network was disconnected and could not be reconnected after multiple retries. You can restart the player to perform more connection retries. |
|PLAY_ERR_HLS_KEY       | -2305 | Failed to get the HLS decryption key.                                  |

#### Warning events
You can ignore the following events, which are only used to notify you of some internal events of the SDK.

| Event ID | Code | Description |
| :-------------------  |:-------- |  :------------------------ |
| PLAY_WARNING_VIDEO_DECODE_FAIL   |  2101  | Failed to decode the current video frame.  |
| PLAY_WARNING_AUDIO_DECODE_FAIL   |  2102  | Failed to decode the current audio frame.  |
| PLAY_WARNING_RECONNECT           |  2103  | The network was disconnected, and automatic reconnection was performed (the `PLAY_ERR_NET_DISCONNECT` event will be thrown after three failed attempts). |
| PLAY_WARNING_HW_ACCELERATION_FAIL|  2106  | Failed to start the hardware decoder, and the software decoder was used instead.   |


#### Connection events
The following server connection events are mainly used to measure and collect the server connection time:

| Event ID | Code | Description |
| :-----------------------  |:-------- |  :------------------------ |
| PLAY_EVT_VOD_PLAY_PREPARED | 2013 | The player has been prepared and can start playback. If `autoPlay` is set to `false`, you need to call `resume` after receiving this event to start playback. |
| PLAY_EVT_RCV_FIRST_I_FRAME|  2003    | The network received the first renderable video data packet (IDR).  |

#### Image quality events
The following events are used to get image change information:

| Event ID | Code | Description |
| :-----------------------  |:-------- |  :------------------------ |
| PLAY_EVT_CHANGE_RESOLUTION|  2009    | The video resolution changed.               |
| PLAY_EVT_CHANGE_ROATION   |  2011    | The MP4 video was rotated. |


#### Video information events
| Event ID | Code | Description |
| :-----------------------  |:-------- |  :------------------------ |
|PLAY_EVT_GET_PLAYINFO_SUCC   | 2010 | Obtained the information of the file played back successfully. |

If you play back a video through `fileId` and the playback request succeeds, the SDK will notify the upper layer of some request information, and you can parse `param` to get the video information after receiving the `PLAY_EVT_GET_PLAYINFO_SUCC` event.

| Video Information | Description |
| :------------------------  |  :------------------------ |
| EVT_PLAY_COVER_URL     | Video thumbnail URL |
| EVT_PLAY_URL  | Video playback URL |
| EVT_PLAY_DURATION | Video duration |

```objective-c
-(void) onPlayEvent:(TXVodPlayer *)player event:(int)EvtID withParam:(NSDictionary*)param
{
    if (EvtID == PLAY_EVT_VOD_PLAY_PREPARED) {
        // The player preparation completion event is received, and you can call the `pause`, `resume`, `getWidth`, and `getSupportedBitrates` APIs.
    } else if (EvtID == PLAY_EVT_PLAY_BEGIN) {
        // The playback start event is received
    } else if (EvtID == PLAY_EVT_PLAY_END) {
        // The playback end event is received
    }
}
```

[](id:status)

### Status feedback (onNetStatus)
The status feedback is triggered once every 0.5 seconds to provide real-time feedback on the current status of the pusher. It can act as a dashboard to inform you of what is happening inside the SDK so you can better understand the current video playback status.
<table>
<tr><th>Parameter</th><th>Description</th></tr><tr>
<td>CPU_USAGE</td><td>Current instantaneous CPU utilization</td>
</tr><tr>
<td>VIDEO_WIDTH</td><td>Video resolution - width</td>
</tr><tr>
<td>VIDEO_HEIGHT</td><td>Video resolution - height</td>
</tr><tr>
<td>NET_SPEED</td><td>Current network data reception speed</td>
</tr><tr>
<td>VIDEO_FPS</td><td>Current video frame rate of streaming media</td>
</tr><tr>
<td>VIDEO_BITRATE</td><td>Current video bitrate in Kbps of streaming media</td>
</tr><tr>
<td>AUDIO_BITRATE</td><td>Current audio bitrate in Kbps of streaming media</td>
</tr><tr>
<td>V_SUM_CACHE_SIZE</td><td>Buffer (`jitterbuffer`) size. If the current buffer length is 0, lag will occur soon.</td>
</tr><tr>
<td>SERVER_IP</td><td>Connected server IP</td>
</tr></table>
Below is the sample code of using `onNetStatus` to get the video playback information:
```objective-c
- (void)onNetStatus:(TXVodPlayer *)player withParam:(NSDictionary *)param {
    // Get the current CPU utilization
    float cpuUsage = [[param objectForKey:@"CPU_USAGE"] floatValue];
    // Get the video width
    int videoWidth = [[param objectForKey:@"VIDEO_WIDTH"] intValue];
    // Get the video height
    int videoHeight = [[param objectForKey:@"VIDEO_HEIGHT"] intValue];
    // Get the real-time speed
    int  speed = [[param objectForKey:@"NET_SPEED"] intValue];
    // Get the current video frame rate of streaming media
    int fps = [[param objectForKey:@"VIDEO_FPS"] intValue];
    // Get the current video bitrate in Kbps of streaming media
    int videoBitRate = [[param objectForKey:@"VIDEO_BITRATE"] intValue];
    // Get the current audio bitrate in Kbps of streaming media
    int audioBitRate = [[param objectForKey:@"AUDIO_BITRATE"] intValue];
    // Get the buffer (`jitterbuffer`) size. If the current buffer length is 0, lag will occur soon.
    int jitterbuffer = [[param objectForKey:@"V_SUM_CACHE_SIZE"] intValue];
    // Get the connected server IP
    NSString *ip = [param objectForKey:@"SERVER_IP"];
}
```

## Scenario-Specific Features

### 1. SDK-based demo component

Based on the Player SDK, Tencent Cloud has developed a [player component](https://intl.cloud.tencent.com/document/product/266/33976). It integrates quality monitoring, video encryption, TESHD, definition switch, and small window playback and is suitable for all VOD and live playback scenarios. It encapsulates complete features and provides upper-layer UIs to help you quickly create a playback program comparable to popular video apps.

### 2. Open-source GitHub projects

Based on the Player SDK, Tencent Cloud has developed immersive video player, video feed stream, and multi-layer reuse components and will provide more user scenario-based components on future versions. You can download the [Player for iOS](https://github.com/LiteAVSDK/Player_iOS) to try out the components.
