## Intended Audience

This document describes some of the proprietary capabilities of Tencent Cloud. Make sure that you have activated the relevant [Tencent Cloud](https://intl.cloud.tencent.com) services before reading this document. If you don't have an account yet, [sign up for free trial](https://intl.cloud.tencent.com/login) first.

## This Document Describes
* How to integrate the Tencent Cloud RT-Cube Player SDK for Flutter.
* How to use the Player SDK for VOD playback.
* How to use the underlying capabilities of the Player SDK to implement more features.

## Basics
This document describes the VOD playback feature of the Player SDK. You can start by understanding the following basics:

- **Live streaming and video on demand**
  In live streaming, the video source is pushed by the host in real time. When the host stops pushing the stream, the player will also stop playing the video. Because the live stream is played back in real time, no progress bar will be displayed in the player during the playback.

In video on demand (VOD), the video source is a video file in the cloud, which can be played back at any time as long as it is not deleted from the cloud. A progress bar is displayed for controlling the playback progress. Typical VOD scenarios including viewing videos on video websites such as Tencent Video and Youku Tudou.

- **Supported protocols**
  Common VOD protocols are as listed below. Currently, VOD URLs in HLS format (starting with `http` and ending with `.m3u8`) are popular.
  ![](https://mc.qcloudimg.com/static/img/4b42a00bb7ce2f58f362f35397734177/image.jpg)

## Notes
The Player SDK **does not impose any limits on the sources of playback URLs**, which means that you can use it to play back videos from both Tencent Cloud and non-Tencent Cloud URLs. However, players in the SDK support only live streaming URLs in FLV, RTMP, and HLS (M3U8) formats, as well as VOD URLs in MP4, HLS (M3U8), and FLV formats.

## SDK Integration[](id:stepone)

### Step 1. Integrate the SDK ZIP file[](id:step1)

Download and integrate the SDK ZIP file.

### Step 2. Create a controller[](id:step2)

```dart
TXVodPlayerController _controller = TXVodPlayerController();
```

### Step 3. Configure event listening[](id:step3)

```dart
// Listen for the video width and height change and set an appropriate aspect ratio. You can also customize the aspect ratio, and the video texture will be stretched proportionally
_controller.onPlayerNetStatusBroadcast.listen((event) async {
  double w = (event["VIDEO_WIDTH"]).toDouble();
  double h = (event["VIDEO_HEIGHT"]).toDouble();

  if (w > 0 && h > 0) {
    setState(() {
      _aspectRatio = 1.0 * w / h;
    });
  }
});
```

### Step 4. Add a layout[](id:step4)
```dart
@override
Widget build(BuildContext context) {
return Container(
  decoration: BoxDecoration(
      image: DecorationImage(
        image: AssetImage("images/ic_new_vod_bg.png"),
        fit: BoxFit.cover,
      )),
  child: Scaffold(
      backgroundColor: Colors.transparent,
      appBar: AppBar(
        backgroundColor: Colors.transparent,
        title: const Text('VOD'),
      ),
      body: SafeArea(
          child: Container(
            height: 150,
            color: Colors.black,
            child: Center(
              child: _aspectRatio > 0
                  ? AspectRatio(
                aspectRatio: _aspectRatio,
                child: TXPlayerVideo(controller: _controller),
              ) : Container(),
            ),
          ))));
}
```

### Step 5. Initialize the player[](id:step5)

```dart
// Initialize the player and assign the shared texture
await _controller.initialize();
```

### Step 6. Start the playback[](id:step6)
<dx-tabs>
::: Through the URL
`TXVodPlayerController` will internally recognize the playback protocol automatically. You only need to pass in your playback URL to the `startVodPlay` function.
```dart
// Play back the video resource
String _url =
    "http://1400329073.vod2.myqcloud.com/d62d88a7vodtranscq1400329073/59c68fe75285890800381567412/adp.10.m3u8";
await _controller.startVodPlay(_url);
```
:::
::: Through `fileId`
```dart
// `psign` is a player signature. For more information on the signature and how to generate it, visit: https://intl.cloud.tencent.com/document/product/266/38099
TXPlayInfoParams params = TXPlayInfoParams(appId: 1252463788,
        fileId: "4564972819220421305", psign: "psignxxxxxxx");
await _controller.startVodPlayWithParams(params);
```
Find the target video file in [Media Assets](https://console.cloud.tencent.com/vod/media), and you can view the `FileId` below the filename.

Play back the video through the `FileId`, and the player will request the backend for the real playback URL. If the network is abnormal or the `FileId` doesn't exist, the `TXLiveConstants.PLAY_ERR_GET_PLAYINFO_FAIL` event will be received; otherwise, `TXLiveConstants.PLAY_EVT_GET_PLAYINFO_SUCC` will be received, indicating that the request succeeded.
:::
</dx-tabs>


### Step 7. Stop the playback[](id:step7)
**Remember to call the controller termination method** when stopping the playback, especially before the next call of `startVodPlay`. This can prevent memory leak and screen flashing issues.
```dart
@override
void dispose() {
  _controller.dispose();
  super.dispose();
}
```

## Basic Feature Usage

### 1. Playback control

#### Starting playback

```dart
// Start playback
_controller.startVodPlay(url)
```

#### Pausing playback

```dart
// Pause the video
_controller.pause();
```

#### Resuming playback

```dart
// Resume the video
_controller.resume();
```

#### Stopping playback

```dart
// Stop the video
_controller.stopPlay(true);
```

#### Stopping the player

```dart
// Release the controller
_controller.dispose();
```

#### Adjusting playback progress (seek)

When the user drags the progress bar, `seek` can be called to start playback at the specified position. The Player SDK supports accurate seek.

```dart
double time = 600; // The value is of `double` type and is in seconds.
// Adjust the playback progress
_controller.seek(time);
```

#### Specifying playback start time

You can specify the playback start time before calling `startVodPlay` for the first time.

```dart
double startTimeInSecond = 60; // Unit: Second.
_controller.setStartTime(startTimeInSecond);   // Set the playback start time
_controller.startVodPlay(url);
```

### 2. Adjustable-Speed playback

The VOD player supports adjustable-speed playback. You can use the `setRate` API to set the VOD playback speed, such as 0.5x, 1.0x, 1.2x, and 2x speed.

```dart
// Set playback at 1.2X rate
_controller.setRate(1.2); 
```

### 3. Playback loop

```dart
// Set playback loop
_controller.setLoop(true);
// Get the current playback loop status
_controller.isLoop(); 
```

### 4. Muting/Unmuting

```dart
// Mute or unmute the player. true: Mute; false: Unmute
_controller.setMute(true);
```

### 5. Roll image ad

The Player SDK allows you to add roll images on the UI for advertising as follows:

* If `autoPlay` is set to `NO`, the player will load the video normally but will not immediately start playing it back.
* Users can see the roll image ad on the player UI after the player is loaded and before the video playback starts.
* When the ad display stop conditions are met, the `resume` API will be called to start video playback.
```dart
_controller.setAutoPlay(false);  // Set manual playback
_controller.startVodPlay(url);    // The video will be loaded after `startVodPlay` is called and won't be played back automatically after being loaded successfully.
// ......
// Display the ad on the player UI
// ......  
_controller.resume();  // Call `resume` to start playing back the video after the ad display ends
```

### 8. HTTP-REF

`headers` in `TXVodPlayConfig` can be used to set HTTP request headers, such as the `Referer` field commonly used to prevent the URL from being copied arbitrarily (Tencent Cloud provides a more secure signature-based hotlink protection solution) and the `Cookie` field for client authentication

```dart
FTXVodPlayConfig playConfig = FTXVodPlayConfig();
Map<String, String> httpHeaders = {'Referer': 'Referer Content'};
playConfig.headers = httpHeaders;
_controller.setConfig(playConfig);
```

### 9. Hardware acceleration

It is extremely difficult to play back videos of the Blu-ray (1080p) or higher image quality smoothly if only software decoding is used. Therefore, if your main scenario is game live streaming, we recommend you use hardware acceleration.

Before switching between software and hardware decoding, you need to call **stopPlay** first. After the switch, you need to call **startVodPlay**; otherwise, severe blurs will occur.

```dart
 _controller.stopPlay(true);
 _controller.enableHardwareDecode(true); 
 _controller.startVodPlay(url);
```

### 10. Definition settings

The SDK supports the multi-bitrate format of HLS, so users can switch between streams at different bitrates to switch the video definition. After receiving the `PLAY_EVT_PLAY_BEGIN` event, you can set the definition as follows:

```dart
List _supportedBitrates = (await _controller.getSupportedBitrates())!;; // Get the array of multiple bitrates
int index = _supportedBitrates[i];  // Specify the subscript of the bitrate of the stream to be played back
_controller.setBitrateIndex(index);  // Switch to the stream at the target bitrate and definition
```

During playback, you can call `_controller.setBitrateIndex(int)` at any time to switch the bitrate. During switch, the data of another stream will be pulled. The SDK is optimized for Tencent Cloud multi-bitrate files to implement smooth switch.

### 11. Adaptive bitrate streaming

The SDK supports adaptive bitrate streaming of HLS. After this capability is enabled, the player can dynamically select the most appropriate bitrate for playback based on the current bandwidth. After receiving the `PLAY_EVT_PLAY_BEGIN` event, you can enable adaptive bitrate streaming as follows:

```dart
_controller.setBitrateIndex(-1); // Pass in `-1` for the `index` parameter
```

During playback, you can call `_controller.setBitrateIndex(int)` at any time to switch to another bitrate. After the switch, adaptive bitrate streaming will be disabled.

### 12. Enabling smooth bitrate switch

Before starting playback, you can enable smooth bitrate switch to seamlessly switch between different definitions (bitrates) during playback. If smooth bitrate switch is enabled, the transition between different bitrates will be smoother but will be more time-consuming. Therefore, this feature can be configured as needed.

```dart
FTXVodPlayConfig playConfig = FTXVodPlayConfig();
/// If it is set to `true`, the bitrate can be switched smoothly. If it is set to `false`, multi-bitrate URLs are opened faster.
playConfig.smoothSwitchBitrate = true;
_controller.setConfig(playConfig);
```

### 13. Playback progress listening

There are two metrics for the VOD progress: **loading progress** and **playback progress**. Currently, the SDK notifies the two progress metrics in real time through event notifications.

You can use the `onPlayerEventBroadcast` API to listen on player events, and the progress notification will be called back to your application through the **PLAY_EVT_PLAY_PROGRESS** event.

```dart
_controller.onPlayerEventBroadcast.listen((event) async {
  if(event["event"] == TXVodPlayEvent.PLAY_EVT_PLAY_PROGRESS) {// For more information, see the native SDK status codes of iOS or Android.
    // Playable duration, i.e., loading progress, in milliseconds
    double playableDuration = event[TXVodPlayEvent.EVT_PLAYABLE_DURATION_MS].toDouble();
    // Playback progress in seconds
    int progress = event[TXVodPlayEvent.EVT_PLAY_PROGRESS].toInt();
    // Total video duration in seconds
    int duration = event[TXVodPlayEvent.EVT_PLAY_DURATION].toInt();
  }
});
```

### 14. Playback network speed listening

You can use the `onPlayerNetStatusBroadcast` API to listen on the player network status such as `NET_STATUS_NET_SPEED`.

```dart
_controller.onPlayerNetStatusBroadcast.listen((event) {
	(event[TXVodNetEvent.NET_STATUS_NET_SPEED]).toDouble();
});
```

### 15. Video resolution acquisition

The Player SDK plays back a video through a URL string. The URL doesn't contain the video information, and you need to access the cloud server to load such information. Therefore, the SDK can only send the video information to your application as event notifications.

**You can get the resolution information in the following two methods:**

Method 1: Use the `NET_STATUS_VIDEO_WIDTH` and `NET_STATUS_VIDEO_HEIGHT` of `onPlayerNetStatusBroadcast` to get the video width and height.

Method 2: Directly call `getWidth()` and `getHeight()` to get the current video width and height after receiving the `PLAY_EVT_VOD_PLAY_PREPARED` event callback from the player.

```dart
 _controller.onPlayerNetStatusBroadcast.listen((event) {
  double w = (event[TXVodNetEvent.NET_STATUS_VIDEO_WIDTH]).toDouble();
  double h = (event[TXVodNetEvent.NET_STATUS_VIDEO_HEIGHT]).toDouble();
});

// Get the video width and height. The values can be returned only after the `PLAY_EVT_VOD_PLAY_PREPARED` event callback is received from the player
_controller.getWidth();
_controller.getHeight();
```

### 16. Player buffer size

During normal video playback, you can control the maximum size of the data buffered from the network in advance. If the maximum buffer size is not configured, the player will use the default buffer policy to guarantee a smooth playback experience.

```dart
FTXVodPlayConfig playConfig = FTXVodPlayConfig();
playConfig.maxBufferSize = 10;  ///  The maximum buffer size during playback in MB
_controller.setConfig(playConfig);
```

### 17. Local video cache[](id:cache)

In short video playback scenarios, the local video file cache is required, so that general users don't need to consume traffic again to reload an already watched video.

- **Supported format:** The SDK supports caching videos in two common VOD formats: HLS (M3U8) and MP4.
- **Enablement time:** The SDK doesn't enable the caching feature by default. We recommend you do not enable it for scenarios in which most videos are watched only once.
- **Enablement method:** This feature can be enabled in the player and takes effect globally. To enable it, you need to configure two parameters: local cache directory and cache size.

```dart
// Set the global cache directory and cache size in MB of the playback engine
SuperPlayerPlugin.setGlobalMaxCacheSize(200);
// Set the global cache directory of the playback engine
SuperPlayerPlugin.setGlobalCacheFolderPath("postfixPath");
```

## Using Advanced Features

### 1. Video preloading

#### Step 1. Use video preloading

In UGSV playback scenarios, the preloading feature contributes to a smooth viewing experience: When a video is being played, you can load the next video to be played back on the backend. When a user switches to the next video, it will already be loaded and can be played back immediately.

Video preloading can deliver an instant playback effect but has certain performance overheads. If your business needs to preload many videos, we recommend you use this feature together with [video predownloading](#download).

This is how seamless switch works in video playback. You can use `setAutoPlay` in `TXVodPlayerController` to implement the feature as follows:
<img src="https://qcloudimg.tencent-cloud.cn/raw/b2bd645f29af403bf2740156aee44092.jpg" width=700px>

```dart
// Play back video A: If `autoPlay` is set to `true`, the video will be immediately loaded and played back when `startVodPlay` is called
String urlA = "http://1252463788.vod2.myqcloud.com/xxxxx/v.f10.mp4";
controller.setAutoPlay(isAutoPlay: true);
controller.startVodPlay(urlA);

// To preload video B when playing back video A, set `setAutoPlay` to `false`
String urlB = "http://1252463788.vod2.myqcloud.com/xxxxx/v.f20.mp4";
controller.setAutoPlay(isAutoPlay: false);
controller.startVodPlay(urlB); // The video won't be played back immediately but will start to be loaded.
```

After video A ends and video B is automatically or manually switched to, you can call the `resume` function to immediately play back video B.

>! After `autoPlay` is set to `false`, make sure that video B has been prepared before calling `resume`, that is, you should call it only after the `PLAY_EVT_VOD_PLAY_PREPARED` event of video B (2013: the player has been prepared, and the video can be played back) is detected.


```dart
controller.onPlayerEventBroadcast.listen((event) async {// Subscribe to status change
  if(event["event"] == TXVodPlayEvent.PLAY_EVT_PLAY_END) {
    await _controller_A.stop();
    await _controller_B.resume();
  }
});
```

#### Step 2. Configure the video preloading buffer

- You can set a large buffer to play back videos more smoothly under unstable network conditions.
- You can set a smaller buffer to reduce the traffic consumption. 

##### Preloading buffer size

This API is used to control the maximum buffer size before the playback starts in preloading scenarios (that is, `AutoPlay` of the player is set to `false` before video playback starts).

```dart
TXVodPlayConfig config = new TXVodPlayConfig();
config.setMaxPreloadSize(2);  // Maximum preloading buffer size in MB. Set it based on your business conditions to reduce the traffic consumption
mVodPlayer.setConfig(config);  // Pass in `config` to `mVodPlayer`
```

##### Playback buffer size 

During normal video playback, you can control the maximum size of the data buffered from the network in advance. If the maximum buffer size is not configured, the player will use the default buffer policy to guarantee a smooth playback experience.

```dart
FTXVodPlayConfig config = FTXVodPlayConfig();
config.maxBufferSize = 10; // The maximum buffer size during playback in MB
_controller.setPlayConfig(config); // Pass in `config` to `controller`
```

[](id:download)

### 2. Video predownloading

You can download part of the video content in advance without creating a player instance, so as to start playing back the video faster when using the player. This helps deliver a better playback experience.

Before using the playback service, make sure that [video cache](#cache) has been set.

Sample:

```dart
// Set the global cache directory and cache size of the playback engine
SuperPlayerPlugin.setGlobalMaxCacheSize(200);
// The cache path is set to the application's sandbox directory by default. You only need to pass in the relative cache directory instead of the entire absolute path to `postfixPath`.
// On Android, videos will be cached to the `Android/data/your-pkg-name/files/testCache` directory on the SD card. 
// On iOS, videos will be cached to the `Documents/testCache` directory in the sandbox.
SuperPlayerPlugin.setGlobalCacheFolderPath("postfixPath");

String palyrl = "http://****";
// Start predownloading
int taskId = await TXVodDownloadController.instance.startPreLoad(palyrl, 3, 1920*1080,
  onCompleteListener:(int taskId,String url) {
    print('taskID=${taskId} ,url=${url}');
  }, onErrorListener: (int taskId, String url, int code, String msg) {
    print('taskID=${taskId} ,url=${url}, code=${code} , msg=${msg}');
  } 
);

// Cancel predownloading
TXVodDownloadController.instance.stopPreLoad(taskId);
```

### 3. Video download

Video download allows users to download online videos and watch them offline. In addition, the Player SDK provides the local encryption feature, so that downloaded local files are still encrypted and can be decrypted and played back only in the specified player. This feature can effectively prevent downloaded videos from being distributed without authorization and protect the video security.

As HLS streaming media cannot be directly saved locally, you cannot download them and play back them as local files. You can use the video download scheme based on `TXVodDownloadController` to implement offline HLS playback.
>?
> -  Currently, `TXVodDownloadController` can cache only non-nested HLS files but not MP4 and FLV files.
> -  The Player SDK already supports playing back local MP4 and FLV files.

[](id:offline1)

#### Step 1. Make preparations

`TXVodDownloadController` is designed as a singleton; therefore, you cannot create multiple download objects. It is used as follows:

```dart
// The cache path is set to the application's sandbox directory by default. You only need to pass in the relative cache directory instead of the entire absolute path to `postfixPath`.
// On Android, videos will be cached to the `Android/data/your-pkg-name/files/testCache` directory on the SD card. 
// On iOS, videos will be cached to the `Documents/testCache` directory in the sandbox.
SuperPlayerPlugin.setGlobalCacheFolderPath("postfixPath");
```

[](id:offline2)

#### Step 2. Start the download

You can start the download through [Fileid](#fileid) or [URL](#url) as follows:
<dx-tabs>

::: Through `Fileid`[](id:fileid)
For download through `Fileid`, you need to pass in `AppID`, `Fileid`, and `qualityId` at least. For signed videos, you also need to pass in `pSign`. If no specific value is passed in to `userName`, it will be `default` by default.

>!You can download encrypted videos only through `Fileid` and must enter the `psign` parameter.

```dart
// QUALITY_OD // Original resolution
// QUALITY_FLU // LD
// QUALITY_SD  // SD
// QUALITY_HD  // HD

TXVodDownloadMedialnfo medialnfo = TXVodDownloadMedialnfo();
TXVodDownloadDataSource dataSource = TXVodDownloadDataSource();
dataSource.appId = 1252463788;
dataSource.fileId = "4564972819220421305";
dataSource.quality = DownloadQuality.QUALITY_HD;
dataSource.pSign = "pSignxxxx";
medialnfo.dataSource = dataSource;
TXVodDownloadController.instance.startDonwload(medialnfo);
```
:::

::: Through URL[](id:url)
You need to pass in the download URL at least. Only the non-nested HLS, i.e., single-bitstream HLS, is supported. If no specific value is passed in to `userName`, it will be `default` by default.

```dart
TXVodDownloadMedialnfo medialnfo = TXVodDownloadMedialnfo();
medialnfo.url = "http://1500005830.vod2.myqcloud.com/43843ec0vodtranscq1500005830/00eb06a88602268011437356984/video_10_0.m3u8";
TXVodDownloadController.instance.startDonwload(medialnfo);
```

:::

</dx-tabs>


[](id:offline3)

#### Step 3. Receive the task information 

Before receiving the task information, you need to set the callback listener first.

```dart
TXVodDownloadController.instance.setDownloadObserver((event, info) {

}, (errorCode, errorMsg, info) {

});
```

You may receive the following task events:

| Event | Description |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| EVENT_DOWNLOAD_START       | The task started, that is, the SDK started the download.                               |
| EVENT_DOWNLOAD_PROGRESS    | The task progress. During download, the SDK will frequently call back this API. You can use `mediaInfo.getProgress()` to get the current progress. |
| EVENT_DOWNLOAD_STOP        | The task stopped. When you call `stopDownload` to stop the download, if this message is received, the download is stopped successfully. |
| EVENT_DOWNLOAD_FINISH      | Download was completed. If this callback is received, the entire file has been downloaded, and the downloaded file can be played back by `TXVodPlayer`. |


If the `downlodOnErrorListener` method is called back, a download error occurred. If the network is disconnected during download, this API will be called back and the download task will stop.

As the downloader can download multiple files at a time, the callback API carries the `TXVodDownloadMedialnfo` object. You can access the URL or `dataSource` to determine the download source and get other information such as download progress and file size.

[](id:offline4)

#### Step 4. Stop the download

You can call the `TXVodDownloadController.instance.stopDownload()` method to stop the download. The parameter is the `TXVodDownloadMedialnfo` object passed in when download starts. **The SDK supports checkpoint restart.** If the download directory is not changed, when you resume downloading a file, the download will start from the point where it stopped.

#### Step 5. Manage downloads

You can get the download lists of all accounts or the specified account.

```dart
// Get the download lists of all users
// You can distinguish between the download lists of different users by `userName` in the download information
List<TXVodDownloadMedialnfo> downloadInfoList = await TXVodDownloadController.instance.getDownloadList();
```

To get the download information of a `Fileid`, such as the current download status and progress, you need to pass in `AppID`, `Fileid`, and `qualityId`.

```dart
// Get the download information of a video
TXVodDownloadMedialnfo downloadInfo = await TXVodDownloadController.instance.getDownloadInfo(medialnfo);
int? duration = downloadInfo.duration;	// Get the total duration
int? playableDuration = downloadInfo.playableDuration; // Get the playable duration of the downloaded video
double? progress = downloadInfo.progress;	// Get the download progress
String? playPath = downloadInfo.playPath; // Get the offline playback path, which can be passed in to the player to start offline playback.
int? downloadState = downloadInfo.downloadState; // Get the download status. For more information, see the `STATE_xxx` constant.
```

```dart
// Delete the download information
bool result = await TXVodDownloadController.instance.deleteDownloadMediaInfo(medialnfo);
```

### 4. Encrypted playback

The video encryption solution is used in scenarios where the video copyright needs to be protected, such as online education. To encrypt your video resources, you need to alter the player and encrypt and transcode video sources. For more information, see [Media Encryption and Copyright Protection Overview](https://www.tencentcloud.com/document/product/266/38131).

After you get the `appId` as well as the encrypted video's `fileId` and `psign` in the Tencent Cloud console, you can play back the video as follows:

```dart
// `psign` is a player signature. For more information on the signature and how to generate it, visit: https://intl.cloud.tencent.com/document/product/266/38099
TXPlayInfoParams params = TXPlayInfoParams(appId: 1252463788,
        fileId: "4564972819220421305", psign: "psignxxxxxxx");
_controller.startVodPlayWithParams(params);
```

### 5. Player configuration 

Before calling `startVodPlay`, you can call `setConfig` to configure the player parameters, such as player connection timeout period, progress callback interval, and maximum number of cached files. `TXVodPlayConfig` allows you to configure detailed parameters. For more information, see [TXVodPlayConfig](https://www.tencentcloud.com/document/product/266/47844#txvodplayconfig). Below is the configuration sample code:

```dart
FTXVodPlayConfig config = FTXVodPlayConfig();
// If `preferredResolution` is not configured, the 720x1280 resolution stream will be played back preferably during multi-bitrate video playback
config.preferredResolution = 720 * 1280;
config.enableAccurateSeek = true;  // Set whether to enable accurate seek. Default value: `true`.
config.progressInterval = 200;  // Set the progress callback interval in milliseconds
config.maxBufferSize = 50;  //  Set the maximum preloading buffer size in MB
_controller.setPlayConfig(config);
```

##### Specifying resolution when playback starts

When playing back an HLS multi-bitrate video source, if you know the video stream resolution information in advance, you can specify the preferred resolution before playback starts, and the player will select and play back the stream at or below the preferred resolution. In this way, after playback starts, you don't need to call `setBitrateIndex` to switch to the required bitstream.

```dart
FTXVodPlayConfig config = FTXVodPlayConfig();
//  The parameter passed in is the product of the video width and height. You can pass in a custom value. Default value: `720 * 1280`.
config.preferredResolution = 720 * 1280;
_controller.setPlayConfig(config);
```

##### Setting playback progress callback interval

```dart
FTXVodPlayConfig config = FTXVodPlayConfig();
config.progressInterval = 200;  // Set the progress callback interval in milliseconds
_controller.setPlayConfig(config);
```

[](id:listening)

## Player Event Listening

You can listen on the player's playback events through `onPlayerEventBroadcast` of `TXVodPlayerController` to sync information to your application.

### Playback event notifications (`onPlayerEventBroadcast`)


| Event ID | Code | Description |
| ----------------------------------------- | ---- | ---------------------------------------------------------- |
| PLAY\_EVT\_PLAY\_BEGIN       | 2004 | Video playback started.                                               |
| PLAY\_EVT\_PLAY\_PROGRESS    | 2005 | The video playback progress (including the current playback progress, loading progress, and total video duration).      |
| PLAY\_EVT\_PLAY\_LOADING     | 2007 | The video is being loaded. The `LOADING_END` event will be reported if video playback resumes. |
| PLAY\_EVT\_VOD\_LOADING\_END | 2014 | Video loading ended, and video playback resumed.                        |
| VOD_PLAY_EVT_SEEK_COMPLETE | 2019 | Seeking was completed. The seeking feature is supported by v10.3 or later. |

#### Stop events

| Event ID | Code | Description |
| :---------------------- | :---- | :----------------------------------------------------- |
| PLAY_EVT_PLAY_END       | 2006  | Video playback ended.                                           |
| PLAY_ERR_NET_DISCONNECT | -2301 | The network was disconnected and could not be reconnected after multiple retries. You can restart the player to perform more connection retries. |
| PLAY_ERR_HLS_KEY        | -2305 | Failed to get the HLS decryption key.                                  |

#### Warning events

You can ignore the following events, which are only used to notify you of some internal events of the SDK.

| Event ID | Code | Description |
| :-------------------------------- | :--- | :----------------------------------------------------------- |
| PLAY_WARNING_VIDEO_DECODE_FAIL   |  2101  | Failed to decode the current video frame.  |
| PLAY_WARNING_AUDIO_DECODE_FAIL   |  2102  | Failed to decode the current audio frame.  |
| PLAY_WARNING_RECONNECT           |  2103  | The network was disconnected, and automatic reconnection was performed (the `PLAY_ERR_NET_DISCONNECT` event will be thrown after three failed attempts). |
| PLAY_WARNING_HW_ACCELERATION_FAIL | 2106 | Failed to start the hardware decoder, and the software decoder was used instead.   |

#### Connection events

The following server connection events are mainly used to measure and collect the server connection time:

| Event ID | Code | Description |
| :------------------------- | :--- | :----------------------------------------------------------- |
| PLAY_EVT_VOD_PLAY_PREPARED | 2013 | The player has been prepared and can start playback. If `autoPlay` is set to `false`, you need to call `resume` after receiving this event to start playback. |
| PLAY_EVT_RCV_FIRST_I_FRAME | 2003 | The network received the first renderable video data packet (IDR). |


#### Image quality events

The following events are used to get image change information:

| Event ID | Code | Description |
| ----------------------------- | ---- | ---------------- |
| PLAY\_EVT\_CHANGE\_RESOLUTION | 2009 | The video resolution changed.   |
| PLAY\_EVT\_CHANGE\_ROTATION   | 2011 | The MP4 video was rotated. |

#### Video information events

| Event ID | Code | Description |
| :----------------------------------------- | :--- | :------------------- |
| PLAY_EVT_GET_PLAYINFO_SUCC | 2010 | Obtained the information of the file played back successfully. |

If you play back a video through `fileId` and the playback request succeeds (called API: `startVodPlay(TXPlayerAuthBuilder authBuilder)`), the SDK will notify the upper layer of some request information, and you can parse `param` to get the video information after receiving the `TXLiveConstants.PLAY_EVT_GET_PLAYINFO_SUCC` event.

| Video Information | Description |
| ------------------------------------------- | ------------------------------------------------- |
| EVT\_PLAY\_COVER\_URL | Video thumbnail URL |
| EVT\_PLAY\_URL | Video playback address |
| EVT\_PLAY\_DURATION | Video duration |
| EVT_TIME | Event occurrence time |
| EVT_UTC_TIME | UTC time |
| EVT_DESCRIPTION | Event description |
| EVT_PLAY_NAME  | Video name |
| EVT_IMAGESPRIT_WEBVTTURL     |  The download URL of the image sprite WebVTT file, which is supported by v10.2 or later. |
| EVT_IMAGESPRIT_IMAGEURL_LIST | The download URL of the image sprite image, which is supported by v10.2 or later. |
| EVT_DRM_TYPE                 | The encryption type, which is supported by v10.2 or later. |


Below is the sample code for using `onPlayerEventBroadcast` to get the video playback information:

```dart
_controller.onPlayerEventBroadcast.listen((event) async {
  if (event["event"] == TXVodPlayEvent.PLAY_EVT_PLAY_BEGIN || event["event"] == TXVodPlayEvent.PLAY_EVT_RCV_FIRST_I_FRAME) {
  // code ...
  } else if (event["event"] == TXVodPlayEvent.PLAY_EVT_PLAY_PROGRESS) {
  // code ...
  }
});
```

[](id:status)

### Playback status feedback (`onPlayerNetStatusBroadcast`)

The status feedback is triggered once every 0.5 seconds to provide real-time feedback on the current status of the pusher. It can act as a dashboard to inform you of what is happening inside the SDK so you can better understand the current video playback status.

<table>
<tr><th>Parameter</th><th>Description</th></tr>
<tr>
<td>NET_STATUS_CPU_USAGE</td><td>Current instantaneous CPU utilization</td>
</tr><tr>
<td>NET_STATUS_VIDEO_WIDTH</td><td>Video resolution - width</td>
</tr><tr>
<td>NET_STATUS_VIDEO_HEIGHT</td><td>Video resolution - height</td>
</tr><tr>
<td>NET_STATUS_NET_SPEED</td><td>Current network data reception speed</td>
</tr><tr>
<td>NET_STATUS_VIDEO_FPS</td><td>Current video frame rate of streaming media</td>
</tr><tr>
<td>NET_STATUS_VIDEO_BITRATE</td><td>Current video bitrate in Kbps of streaming media</td>
</tr><tr>
<td>NET_STATUS_AUDIO_BITRATE</td><td>Current audio bitrate in Kbps of streaming media</td>
</tr><tr>
<td>NET_STATUS_VIDEO_CACHE</td><td>Buffer (`jitterbuffer`) size. If the current buffer length is 0, lag will occur soon.</td>
</tr><tr>
<td>NET_STATUS_SERVER_IP</td><td>Connected server IP</td>
</tr></table>

Below is the sample code of using `onNetStatus` to get the video playback information:

```dart
_controller.onPlayerNetStatusBroadcast.listen((event) async {
  int videoWidth = event[TXVodNetEvent.NET_STATUS_VIDEO_WIDTH];
});
```


### Video playback status feedback

The video playback status will be notified every time the playback status switches.

The enumeration class `TXPlayerState` is used to transfer the event.

| Status | Description |
| ------ | ------ |
| paused | The playback was paused |
| failed | The playback failed |
| buffering | Buffering |
| playing | Playing back |
| stopped | The playback was stopped |
| disposed | The control was released |


Below is the sample code for using `onPlayerState` to get the video playback status:

```dart
_controller.onPlayerState.listen((val) { });
```

### System volume level listening

To help you monitor the video playback volume level, the SDK encapsulates the volume level change notification into an event at the Flutter layer. You can directly use `SuperPlayerPlugin` to listen on the volume level change of the current device.

Below is the sample code for using `onEventBroadcast` to get the volume level status of the device:

```dart
SuperPlayerPlugin.instance.onEventBroadcast.listen((event) {
  int eventCode = event["event"];
});
```

The relevant events are as described below:

| Status | Code | Description   |
| ------ |------ | ------ |
| EVENT_VOLUME_CHANGED | 1 | The volume level changed. |
| EVENT_AUDIO_FOCUS_PAUSE | 2 | The volume level output and playback focus were lost. This event is applicable only to Android. |
| EVENT_AUDIO_FOCUS_PLAY | 3 | Obtained the volume level output focus successfully. This event is applicable only to Android. |

### PiP event listening

As PiP used by the SDK is based on the PiP capabilities of the system, after you enter the PiP mode, a series of notifications are provided to help you adjust the UI accordingly.

| Status | Code | Description   |
| ------ |------ | ------ |
| EVENT_PIP_MODE_ALREADY_ENTER | 1 | The player has entered the PiP mode. |
| EVENT_PIP_MODE_ALREADY_EXIT | 2 | The player has exited the PiP mode. |
| EVENT_PIP_MODE_REQUEST_START | 3 | The player requests to enter the PiP mode. |
| EVENT_PIP_MODE_UI_STATE_CHANGED | 4 | The PiP UI status changed. This event takes effect only on Android 31 or later. |
| EVENT_IOS_PIP_MODE_RESTORE_UI | 5 | The UI was reset. This event takes effect only on iOS. |
| EVENT_IOS_PIP_MODE_WILL_EXIT | 6 | The player will exit the PiP mode. This event takes effect only on iOS. |

Below is the sample code for using `onExtraEventBroadcast` to listen on PiP events:

```dart
SuperPlayerPlugin.instance.onExtraEventBroadcast.listen((event) {
  int eventCode = event["event"];
});
```
