## Prerequisites
1. To try out complete player features, we recommend you activate [VOD](https://intl.cloud.tencent.com/product/vod). If you haven't registered an account, [sign up](https://intl.cloud.tencent.com/login) first. If you don't use the VOD service, you can skip this step; however, you will be able to use only basic player features after integration.
2. Download and install [Android Studio](https://developer.android.com/studio). If you have already done so, skip this step.

## This Document Describes
* How to integrate the Player SDK for Android.
* How to use the Player SDK for VOD playback.
* How to use the underlying capabilities of the Player SDK to implement more features.

## SDK Integration
[](id:stepone)

### Step 1. Download the SDK ZIP file[](id:step1)
[Download](https://vcube.cloud.tencent.com/home.html) the SDK ZIP file and integrate the SDK into your application as instructed in the SDK integration document.

### Step 2. Set the SDK connection environment

In order to help you conduct business with higher quality and security in compliance with applicable laws and regulations in different countries and regions, Tencent Cloud provides two SDK connection environments. If you serve global users, we recommend you use the following API to configure the global connection environment.

```java
// If you serve global users, configure the global SDK connection environment.
TXLiveBase.setGlobalEnv("GDPR");
```

### Step 3. Configure the license

If you have the required license, you need to get the license URL and key in the [RT-Cube console](https://console.cloud.tencent.com/vcube).

If you don't have the required license, you need to get it as instructed in Video Playback License

After obtaining the license information, before calling relevant APIs of the SDK, initialize the license through the following API. We recommend you set the following in the `Application` class:

```java
public class MApplication extends Application {

    @Override
    public void onCreate() {
        super.onCreate();
        String licenceURL = ""; // The license URL obtained
        String licenceKey = ""; // The license key obtained
        TXLiveBase.getInstance().setLicence(this, licenceURL, licenceKey);
        TXLiveBase.setListener(new TXLiveBaseListener() {
            @Override
            public void onLicenceLoaded(int result, String reason) {
                Log.i(TAG, "onLicenceLoaded: result:" + result + ", reason:" + reason);
            }
        });
    }
}
```

### Step 4. Add a view

The SDK provides `TXCloudVideoView` for video rendering by default. First, add the following code to the layout XML file:
```xml
<com.tencent.rtmp.ui.TXCloudVideoView
            android:id="@+id/video_view"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:layout_centerInParent="true"
            android:visibility="gone"/>
```

[](id:step3)

### Step 5. Create a player object

Create the **TXVodPlayer** object and use the `setPlayerView` API to associate the object with the **video_view** control just added to the UI.

```java
// `mPlayerView` is the video rendering view added in step 2
TXCloudVideoView mPlayerView = findViewById(R.id.video_view);
// Create a player object
TXVodPlayer mVodPlayer = new TXVodPlayer(getActivity());
// Associate the player object with the video rendering view
mVodPlayer.setPlayerView(mPlayerView);
```

[](id:step4)

### Step 6. Start playback

`TXVodPlayer` supports two playback modes for you to choose as needed:

<dx-tabs>
::: Through URL
  `TXVodPlayer` will internally recognize the playback protocol automatically. You only need to pass in your playback URL to the `startPlay` function.

```java
// Play back a video resource at a URL
String url = "http://1252463788.vod2.myqcloud.com/xxxxx/v.f20.mp4";
mVodPlayer.startPlay(url); 


// Play back a local video resource
String localFile = "/sdcard/video.mp4";
mVodPlayer.startPlay(localFile); 
```
:::
::: Through `FileId`
```objectivec
// We recommend you use the following new API:
TXPlayInfoParams playInfoParam = new TXPlayInfoParams(1252463788, // `appId` of the Tencent Cloud account
    "4564972819220421305", // `fileId` of the video
    "psignxxxxxxx"); // This parameter must be specified for an encrypted video.
mVodPlayer.startPlay(playInfoParam);

// Legacy API, which is not recommended
TXPlayerAuthBuilder authBuilder = new TXPlayerAuthBuilder();
authBuilder.setAppId(1252463788);
authBuilder.setFileId("4564972819220421305");
mVodPlayer.startPlay(authBuilder); 
```
Find the target video file in [Media Assets](https://console.cloud.tencent.com/vod/media), and you can view the `FileId` below the filename.

Play back the video through the `FileId`, and the player will request the backend for the real playback URL. If the network is abnormal or the `FileId` doesn't exist, the `TXLiveConstants.PLAY_ERR_GET_PLAYINFO_FAIL` event will be received; otherwise, `TXLiveConstants.PLAY_EVT_GET_PLAYINFO_SUCC` will be received, indicating that the request succeeded.
:::
</dx-tabs>


[](id:5)

### Step 7. Stop playback

**Remember to terminate the view control** when stopping the playback, especially before the next call of `startPlay`. This can prevent memory leak and screen flashing issues.

In addition, when exiting the playback UI, you need to call the `onDestroy()` function for the rendering view. This can prevent memory leak and "Receiver not registered" alarms.

```java
@Override
public void onDestroy() {
    super.onDestroy();
    mVodPlayer.stopPlay(true); // `true` indicates to clear the last-frame image
    mPlayerView.onDestroy(); 
}
```
>?The boolean parameter of `stopPlay` indicates whether to clear the last-frame image. Early versions of the live player of the RTMP SDK don't have an official pause feature; therefore, this boolean value is used to clear the last-frame image.

If you want to retain the last-frame image after VOD stops, simply do nothing after receiving the playback stop event; playback will stop at the last frame by default.

## Basic Feature Usage
### 1. Playback control

#### Starting playback

```java
// Start playback
mVodPlayer.startPlay(url)
```

#### Pausing playback

```java
// Pause the video
mVodPlayer.pause();
```

#### Resuming playback

```java
// Resume the video
mVodPlayer.resume();
```

#### Stopping playback

```java
// Stop the video
mVodPlayer.stopPlay(true);
```

#### Adjusting playback progress (seek)

When the user drags the progress bar, `seek` can be called to start playback at the specified position. The Player SDK supports accurate seek.

```java
int time = 600; // In seconds if the value is of `int` type
// float time = 600; // In seconds if the value is of `float` type
// Adjust the playback progress
mVodPlayer.seek(time);
```

#### Specifying playback start time

You can specify the playback start time before calling `startPlay` for the first time.

```java
float startTimeInSecond = 60; // Unit: Second
mVodPlayer.setStartTime(startTimeInSecond);   // Set the playback start time
mVodPlayer.startPlay(url);
```

### 2. Image adjustment

- **view: size and position**
You can modify the size and position of video images by adjusting the size and position of the `video_view` control added in the [Add a view](#addview) step during SDK integration.
- **setRenderMode: Aspect fill or aspect fit**
<table>
<thead>
<tr>
<th>Value</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>RENDER_MODE_FULL_FILL_SCREEN</td>
<td>Images are scaled to fill the entire screen, and the excess parts are cropped. There are no black bars in this mode, but images may not be displayed entirely.</td>
</tr>
<tr>
<td>RENDER_MODE_ADJUST_RESOLUTION</td>
<td>Images are scaled as so that the long side of the video fits the screen. Neither side exceeds the screen after scaling. Images are centered, and there may be black bars.</td>
</tr>
</tbody></table>
- **setRenderRotation: Image rotation**
<table>
<thead>
<tr>
<th>Value</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>RENDER_ROTATION_PORTRAIT</td>
<td>Normal playback (the Home button is below the video image)</td>
</tr>
<tr>
<td>RENDER_ROTATION_LANDSCAPE</td>
<td>Clockwise rotation of the image by 270 degrees (the Home button is on the left of the video image)</td>
</tr>
</tbody></table>
```java
 // Fill the screen at the original aspect ratio
mVodPlayer.setRenderMode(TXLiveConstants.RENDER_MODE_FULL_FILL_SCREEN);
// Normal playback (the Home button is below the video image)
mVodPlayer.setRenderRotation(TXLiveConstants.RENDER_ROTATION_PORTRAIT);
```



### 3. Adjustable-Speed playback
The VOD player supports adjustable-speed playback. You can use the `setRate` API to set the VOD playback speed, such as 0.5X, 1.0X, 1.2X, and 2X.


```java
// Set playback at 1.2X rate
mVodPlayer.setRate(1.2); 
```

### 4. Playback loop

```java
// Set playback loop
mVodPlayer.setLoop(true);
// Get the current playback loop status
mVodPlayer.isLoop(); 
```

### 5. Muting/Unmuting

```java
// Mute or unmute the player. true: Mute; false: Unmute
mVodPlayer.setMute(true);
```

### 6. Screencapturing

Call **snapshot** to take a screenshot of the current video frame. This method captures only the video frame. To capture the UI, use the corresponding API of the Android system.



```java
// Take a screenshot
mVodPlayer.snapshot(new ITXSnapshotListener() {
    @Override
    public void onSnapshot(Bitmap bmp) {
        if (null != bmp) {
           // Get the screenshot bitmap
        }
    }
});
```


### 7. Roll image ad
The Player SDK allows you to add roll images on the UI for advertising as follows:
* If `autoPlay` is set to `NO`, the player will load the video normally but will not immediately start playing it back.
* Users can see the roll image ad on the player UI after the player is loaded and before the video playback starts.
* When the ad display stop conditions are met, the `resume` API will be called to start video playback.

```java
mVodPlayer.setAutoPlay(false);  // Set manual playback
mVodPlayer.startPlay(url);    // The video will be loaded after `startPlay` is called and won't be played back automatically after being loaded successfully
// ......
// Display the ad on the player UI
// ......  
mVodPlayer.resume();  // Call `resume` to start playing back the video after the ad display ends
```

### 8. HTTP-REF
`headers` in `TXVodPlayConfig` can be used to set HTTP request headers, such as the `Referer` field commonly used to prevent the URL from being copied arbitrarily (Tencent Cloud provides a more secure signature-based hotlink protection solution) and the `Cookie` field for client authentication
### 9. Hardware acceleration
It is extremely difficult to play back videos of the Blu-ray (1080p) or higher image quality smoothly if only software decoding is used. Therefore, if your main scenario is game live streaming, we recommend you use hardware acceleration.

Before switching between software and hardware decoding, you need to call **stopPlay** first. After the switch, you need to call **startPlay**; otherwise, severe blurring will occur.

```java
 mVodPlayer.stopPlay(true);
 mVodPlayer.enableHardwareDecode(true);
 mVodPlayer.startPlay(flvUrl, type);
```
### 10. Definition settings
The SDK supports the multi-bitrate format of HLS, so users can switch between streams at different bitrates to switch the video definition. After receiving the `PLAY_EVT_PLAY_BEGIN` event, you can set the definition as follows:

```java
ArrayList<TXBitrateItem> bitrates = mVodPlayer.getSupportedBitrates(); // Get the array of multiple bitrates
int index = bitrates.get(i).index;  // Specify the subscript of the bitrate of the stream to be played back
mVodPlayer.setBitrateIndex(index);  // Switch to the stream at the target bitrate and definition
```

During playback, you can call `mVodPlayer.setBitrateIndex(int)` at any time to switch the bitrate. During the switch, the data of another stream will be pulled. The SDK is optimized for Tencent Cloud multi-bitrate files to implement smooth switching.
### 11. Adaptive bitrate streaming
The SDK supports adaptive bitrate streaming of HLS. After this capability is enabled, the player can dynamically select the most appropriate bitrate for playback based on the current bandwidth. After receiving the `PLAY_EVT_PLAY_BEGIN` event, you can enable adaptive bitrate streaming as follows:
```java
mVodPlayer.setBitrateIndex(-1); // Pass in `-1` for the `index` parameter
```
During playback, you can call `mVodPlayer.setBitrateIndex(int)` at any time to switch to another bitrate. After the switch, adaptive bitrate streaming will be disabled.

### 12. Playback progress listening

There are two metrics for the VOD progress: **loading progress** and **playback progress**. Currently, the SDK notifies the two progress metrics in real time through event notifications. For more information on the event notification content, see [Event Listening](#listening).

You can bind a **TXVodPlayerListener** listener to the `TXVodPlayer` object, and the progress notification will be called back to your application through the **PLAY_EVT_PLAY_PROGRESS** event. The event information contains the above two progress metrics.




```java
mVodPlayer.setVodListener(new ITXVodPlayListener() {
    @Override
    public void onPlayEvent(TXVodPlayer player, int event, Bundle param) {
        if (event == TXLiveConstants.PLAY_EVT_PLAY_PROGRESS) {
            // Loading progress in ms
            int playable_duration_ms = param.getInt(TXLiveConstants.EVT_PLAYABLE_DURATION_MS);
            mLoadBar.setProgress(playable_duration_ms); // Set the loading progress bar

            // Playback progress in ms
            int progress_ms = param.getInt(TXLiveConstants.EVT_PLAY_PROGRESS_MS);
            mSeekBar.setProgress(progress_ms);  // Set the playback progress bar

            // Total video duration in ms
            int duration_ms = param.getInt(TXLiveConstants.EVT_PLAY_DURATION_MS);
            // It can be used to set duration display, etc.
        }
    }

    @Override
    public void onNetStatus(TXVodPlayer player, Bundle bundle) {
    }
});
```


### 13. Playback network speed listening

You can display the current network speed when the video is lagging by [listening on events](#listening).

* You can use the `NET_STATUS_NET_SPEED` of `onNetStatus` to get the current network speed. For detailed directions, see [Playback status feedback (onNetStatus)](#status).
* After the `PLAY_EVT_PLAY_LOADING` event is detected, the current network speed will be displayed.
* After the `PLAY_EVT_VOD_LOADING_END` event is received, the view showing the current network speed will be hidden.

```java
mVodPlayer.setVodListener(new ITXVodPlayListener() {
    @Override
    public void onPlayEvent(TXVodPlayer player, int event, Bundle param) {
        if (event == TXLiveConstants.PLAY_EVT_PLAY_LOADING) {
            // Show the current network speed

        } else if (event == TXLiveConstants.PLAY_EVT_VOD_LOADING_END) {
            // Hide the view showing the current network speed
        }
    }

    @Override
    public void onNetStatus(TXVodPlayer player, Bundle bundle) {
        // Get the real-time speed in Kbps
        int speed = bundle.getInt(TXLiveConstants.NET_STATUS_NET_SPEED);
    }
});
```

### 14. Video resolution acquisition

The Player SDK plays back a video through a URL string. The URL doesn't contain the video information, and you need to access the cloud server to load such information. Therefore, the SDK can only send the video information to your application as event notifications. For more information, see [Event Listening](#listening).

**You can get the resolution information in the following two methods:**

Method 1: Use the `NET_STATUS_VIDEO_WIDTH` and `NET_STATUS_VIDEO_HEIGHT` of `onNetStatus` to get the video width and height. For detailed directions, see [Playback status feedback (onNetStatus)](#status).

Method 2: Directly call `TXVodPlayer.getWidth()` and `TXVodPlayer.getHeight()` to get the current video width and height after receiving the `PLAY_EVT_VOD_PLAY_PREPARED` event callback from the player.

```java
mVodPlayer.setVodListener(new ITXVodPlayListener() {
    @Override
    public void onPlayEvent(TXVodPlayer player, int event, Bundle param) {
    }

    @Override
    public void onNetStatus(TXVodPlayer player, Bundle bundle) {
        // Get the video width
        int videoWidth = bundle.getInt(TXLiveConstants.NET_STATUS_VIDEO_WIDTH);
        // Get the video height
        int videoHeight = bundle.getInt(TXLiveConstants.NET_STATUS_VIDEO_HEIGHT);
    }
});

// Get the video width and height. The values can be returned only after the `PLAY_EVT_VOD_PLAY_PREPARED` event callback is received from the player
mVodPlayer.getWidth();
mVodPlayer.getHeight();
```

### 15. Player buffer size

During normal video playback, you can control the maximum size of the data buffered from the network in advance. If the maximum buffer size is not configured, the player will use the default buffer policy to guarantee a smooth playback experience.

```java
TXVodPlayConfig config = new TXVodPlayConfig();
config.setMaxBufferSize(10);  // Maximum buffer size during playback in MB
mVodPlayer.setConfig(config);  // Pass in `config` to `mVodPlayer`
```

### 16. Local video cache[](id:cache)

In short video playback scenarios, the local video file cache is required, so that general users don't need to consume traffic again to reload an already watched video.

- **Supported format:** The SDK supports caching videos in two common VOD formats: HLS (M3U8) and MP4.
- **Enablement time:** The SDK doesn't enable the caching feature by default. We recommend you do not enable it for scenarios in which most videos are watched only once.
- **Enablement method:** This feature can be enabled in the player and takes effect globally. To enable it, you need to configure two parameters: local cache directory and cache size.

```java
File sdcardDir = getApplicationContext().getExternalFilesDir(null);
if (sdcardDir != null) {
    // Set the global cache directory of the playback engine
   TXPlayerGlobalSetting.setCacheFolderPath(sdcardDir.getPath() + "/txcache");
    // Set the global cache directory and cache size in MB of the playback engine
    TXPlayerGlobalSetting.setMaxCacheSize(200); 
}

// Use the player
```

>?The `TXVodPlayConfig#setMaxCacheItems` API used for configuration on earlier versions has been deprecated and is not recommended.

## Using Advanced Features

### 1. Video preloading

#### Step 1. Use video preloading

In UGSV playback scenarios, the preloading feature contributes to a smooth viewing experience: When a video is being played, you can load the next video to be played back on the backend. When a user switches to the next video, it will already be loaded and can be played back immediately.

Video preloading can deliver an instant playback effect but has certain performance overheads. If your business needs to preload many videos, we recommend you use this feature together with [video predownloading](#download).

This is how seamless switch works in video playback. You can use `setAutoPlay` in `TXVodPlayer` to implement the feature as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/b2bd645f29af403bf2740156aee44092.jpg)

```java
// Play back video A: If `autoPlay` is set to `true`, the video will be immediately loaded and played back when `startPlay` is called
String urlA = "http://1252463788.vod2.myqcloud.com/xxxxx/v.f10.mp4";
playerA.setAutoPlay(true);
playerA.startPlay(urlA);

// To preload video B when playing back video A, set `setAutoPlay` to `false`
String urlB = @"http://1252463788.vod2.myqcloud.com/xxxxx/v.f20.mp4";
playerB.setAutoPlay(false);
playerB.startPlay(urlB); // The video won't be played back immediately but will start to be loaded
```

After video A ends and video B is automatically or manually switched to, you can call the `resume` function to immediately play back video B.

>! After `autoPlay` is set to `false`, make sure that video B has been prepared before calling `resume`, that is, you should call it only after the `PLAY_EVT_VOD_PLAY_PREPARED` event of video B (2013: the player has been prepared, and the video can be played back) is detected.


```java
public void onPlayEvent(TXVodPlayer player, int event, Bundle param) {
    // When video A ends, directly start playing back video B for seamless switch
    if (event == PLAY_EVT_PLAY_END) {
           playerA.stop();
           playerB.setPlayerView(mPlayerView);
           playerB.resume();
        }
}
```

#### Step 2. Configure the video preloading buffer

- You can set a large buffer to play back videos more smoothly under unstable network conditions.
- You can set a smaller buffer to reduce the traffic consumption. 

##### Preloading buffer size

This API is used to control the maximum buffer size before the playback starts in preloading scenarios (that is, `AutoPlay` of the player is set to `false` before video playback starts).

```java
TXVodPlayConfig config = new TXVodPlayConfig();
config.setMaxPreloadSize(2);  // Maximum preloading buffer size in MB. Set it based on your business conditions to reduce the traffic consumption
mVodPlayer.setConfig(config);  // Pass in `config` to `mVodPlayer`
```

##### Playback buffer size 

During normal video playback, you can control the maximum size of the data buffered from the network in advance. If the maximum buffer size is not configured, the player will use the default buffer policy to guarantee a smooth playback experience.

```java
TXVodPlayConfig config = new TXVodPlayConfig();
config.setMaxBufferSize(10);  // Maximum buffer size during playback in MB
mVodPlayer.setConfig(config);  // Pass in `config` to `mVodPlayer`
```

[](id:download)
### 2. Video predownloading

You can download part of the video content in advance without creating a player instance, so as to start playing back the video faster when using the player. This helps deliver a better playback experience.

Before using the playback service, make sure that [video cache](#cache) has been set.

>? 
> 1. `TXPlayerGlobalSetting` is the global cache setting API, and the original `TXVodConfig` API has been deprecated.
> 2. The global cache directory and size settings have a higher priority than those configured in `TXVodConfig` of the player.

Sample:

```java
// Set the global cache directory and cache size of the playback engine
File sdcardDir = getApplicationContext().getExternalFilesDir(null);
// Set the global cache directory and cache size of the playback engine
if (sdcardDir != null) {
    TXPlayerGlobalSetting.setCacheFolderPath(sdcardDir.getPath() + "/PlayerCache");
    TXPlayerGlobalSetting.setMaxCacheSize(200); // Unit: MB
}

String palyrl = "http://****";
// Start predownloading
final TXVodPreloadManager downloadManager = TXVodPreloadManager.getInstance(getApplicationContext());
final int taskID = downloadManager.startPreload(playUrl, 3, 1920*1080, new ITXVodPreloadListener() {
    @Override
    public void onComplete(int taskID, String url) {
        Log.d(TAG, "preload: onComplete: url: " + url);
    }

    @Override
    public void onError(int taskID, String url, int code, String msg) {
        Log.d(TAG, "preload: onError: url: " + url + ", code: " + code + ", msg: " + msg);
    }

});

// Cancel predownloading
downloadManager.stopPreload(taskID);
```

### 3. Video download
Video download allows users to download online videos and watch them offline. In addition, the Player SDK provides the local encryption feature, so that downloaded local files are still encrypted and can be decrypted and played back only in the specified player. This feature can effectively prevent downloaded videos from being distributed without authorization and protect the video security.

As HLS streaming media cannot be directly saved locally, you cannot download them and play back them as local files. You can use the video download scheme based on `TXVodDownloadManager` to implement offline HLS playback.

> !
> -  Currently, `TXVodDownloadManager` can cache only non-nested HLS files but not MP4 and FLV files.
> - The Player SDK already supports playing back local MP4 and FLV files.

[](id:offline1)
#### Step 1. Make preparations

`TXVodDownloadManager` is designed as a singleton; therefore, you cannot create multiple download objects. It is used as follows:

```java
TXVodDownloadManager downloader = TXVodDownloadManager.getInstance();
downloader.setDownloadPath("<Specify your download directory>");
```

[](id:offline2)
#### Step 2. Start the download
You can start the download through [URL](#url) or [Fileid](#fileid) as follows:
<dx-tabs>
::: Through URL[](id:url)
You need to pass in the download URL at least. Only the non-nested HLS format is supported. If no specific value is passed in to `userName`, it will be `default` by default.
```java
downloader.startDownloadUrl("http://1500005830.vod2.myqcloud.com/43843ec0vodtranscq1500005830/00eb06a88602268011437356984/video_10_0.m3u8", "");
```
:::
::: Through Fileid[](id:fileid)
For download through `Fileid`, you need to pass in `AppID`, `Fileid`, and `qualityId` at least. For signed videos, you also need to pass in `pSign`. If no specific value is passed in to `userName`, it will be `default` by default.
```java
//  QUALITYOD // Original resolution
// QUALITYFLU // LD
// QUALITYSD  // SD
// QUALITYHD  // HD
TXVodDownloadDataSource source = new TXVodDownloadDataSource(1252463788, "4564972819220421305", QUALITYHD, "", "");
downloader.startDownload(source);
```
:::
</dx-tabs>


[](id:offline3)
#### Step 3. Receive the task information 
Before receiving the task information, you need to set the callback listener first.

```java
downloader.setListener(this);
```

You may receive the following task callbacks:

| Callback Message | Description |
|---------|---------|
| void onDownloadStart(TXVodDownloadMediaInfo mediaInfo)       | The task started, that is, the SDK started the download.                              |
| void onDownloadProgress(TXVodDownloadMediaInfo mediaInfo)    | Task progress. During download, the SDK will frequently call back this API. You can use `mediaInfo.getProgress()` to get the current progress. |
| void onDownloadStop(TXVodDownloadMediaInfo mediaInfo)        | The task stopped. When you call `stopDownload` to stop the download, if this message is received, the download is stopped successfully. |
| void onDownloadFinish(TXVodDownloadMediaInfo mediaInfo)      | Download was completed. If this callback is received, the entire file has been downloaded, and the downloaded file can be played back by `TXVodPlayer`. |
| void onDownloadError(TXVodDownloadMediaInfo mediaInfo, int error, String reason) | Download error. If the network is disconnected during download, this API will be called back and the download task will stop. The error code is in `TXVodDownloadManager`.  |


As the downloader can download multiple files at a time, the callback API carries the `TXVodDownloadMediaInfo` object. You can access the URL or `dataSource` to determine the download source and get other information such as download progress and file size.

[](id:offline4)

#### Step 4. Stop the download
You can call the `downloader.stopDownload()` method to stop the download. The parameter is the object returned by `downloader.startDownload()`. **The SDK supports checkpoint restart.** If the download directory is not changed, when you resume downloading a file, the download will start from the point where stopped.

#### Step 5. Manage downloads
You can get the download lists of all accounts or the specified account.
```java
// Get the download lists of all users
// You can distinguish between the download lists of different users by `userName` in the download information
List<TXVodDownloadMediaInfo> downloadList = downloader.getDownloadMediaInfoList(); 
if (downloadInfoList == null || downloadInfoList.size() <= 0) return;
// Get the download list of the `default` user
List<TXVodDownloadMediaInfo> defaultUserDownloadList = new ArrayList<>();
for(TXVodDownloadMediaInfo downloadMediaInfo : downloadInfoList) {
  if ("default".equals(downloadMediaInfo.getUserName())) {
  	defaultUserDownloadList.add(downloadMediaInfo);
  }
}
```

To get the download information of a `Fileid`, such as the current download status and progress, you need to pass in `AppID`, `Fileid`, and `qualityId`.
```java
// Get the download information of a `fileId`
TXVodDownloadMediaInfo downloadInfo = downloader.getDownloadMediaInfo(1252463788, "4564972819220421305", QUALITYHD);
int duration = downloadInfo.getDuration();	// Get the total duration
int playableDuration = downloadInfo.getPlayableDuration(); // Get the playable duration of the downloaded video
float progress = downloadInfo.getProgress();	// Get the download progress
String playPath = downloadInfo.getPlayPath(); // Get the offline playback path, which can be passed in to the player to start offline playback.
int downloadState = downloadInfo.getDownloadState(); // Get the download status. For more information, see the `STATE_xxx` constant.
boolean isDownloadFinished = downloadInfo.isDownloadFinished(); // If `true` is returned, the download is completed.
```

To get the download information of a URL, you need to pass in the URL information.
```java
// Get the download information of a URL
TXVodDownloadMediaInfo downloadInfo = downloader.getDownloadMediaInfo("http://1253131631.vod2.myqcloud.com/26f327f9vodgzp1253131631/f4bdff799031868222924043041/playlist.m3u8");
```

To delete the download information and relevant file, you need to pass in the `TXVodDownloadMediaInfo` parameter.
```java
// Delete the download information
boolean deleteRst = downloader.deleteDownloadMediaInfo(downloadInfo);
```


### 4. Encrypted playback

The video encryption solution is used in scenarios where the video copyright needs to be protected, such as online education. To encrypt your video resources, you need to alter the player and encrypt and transcode video sources. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/266/38131).

### 5. Player configuration 

Before calling `statPlay`, you can call `setConfig` to configure the player parameters, such as player connection timeout period, progress callback interval, and maximum number of cached files. `TXVodPlayConfig` allows you to configure detailed parameters. For more information, see [Basic Configuration API](https://intl.cloud.tencent.com/document/product/266/47841). Below is the configuration sample code:

```java
TXVodPlayConfig config = new TXVodPlayConfig();
config.setEnableAccurateSeek(true);  // Set whether to enable accurate seek. Default value: true
config.setMaxCacheItems(5);  // Set the maximum number of cached files to 5
config.setProgressInterval(200);  // Set the progress callback interval in ms
config.setMaxBufferSize(50);  // Set the maximum preloading buffer size in MB
mVodPlayer.setConfig(config);  // Pass in `config` to `mVodPlayer`
```

##### Specifying resolution when playback starts

When playing back an HLS multi-bitrate video source, if you know the video stream resolution information in advance, you can specify the preferred resolution before playback starts, and the player will select and play back the stream at or below the preferred resolution. In this way, after playback starts, you don't need to call `setBitrateIndex` to switch to the required bitstream.

```java
TXVodPlayConfig config = new TXVodPlayConfig();
// The parameter passed in is the product of the video width and height. You can pass in a custom value.
config.setPreferredResolution(TXLiveConstants.VIDEO_RESOLUTION_720X1280); 
mVodPlayer.setConfig(config);  // Pass in `config` to `mVodPlayer`
```

##### Setting playback progress callback interval

```
TXVodPlayConfig config = new TXVodPlayConfig();
config.setProgressInterval(200);  // Set the progress callback interval in ms
mVodPlayer.setConfig(config);  // Pass in `config` to `mVodPlayer`
```

[](id:listening)

## Player Event Listening
You can bind a `TXVodPlayListener` listener to the `TXVodPlayer` object to use `onPlayEvent` (event notification) and `onNetStatus` (status feedback) to sync information to your application.

### Playback event notifications (onPlayEvent)


| Event ID | Code | Description |
| ----------------------------------------- | ---- | ---------------------------------------------------------- |
| PLAY\_EVT\_PLAY\_BEGIN       | 2004 | Video playback started.                                               |
| PLAY\_EVT\_PLAY\_PROGRESS    | 2005 | Video playback progress (including the current playback progress, loading progress, and total video duration).      |
| PLAY\_EVT\_PLAY\_LOADING     | 2007 | The video is being loaded. The `LOADING_END` event will be reported if video playback resumes. |
| PLAY\_EVT\_VOD\_LOADING\_END | 2014 | Video loading ended, and video playback resumed.                        |
| TXVodConstants.VOD_PLAY_EVT_SEEK_COMPLETE | 2019 | Seeking was completed. The seeking feature is supported by v10.3 or later. |

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
| ----------------------------- | ---- | ---------- |
| PLAY\_EVT\_CHANGE\_RESOLUTION | 2009 | The video resolution changed.    |
| PLAY\_EVT\_CHANGE\_ROTATION   | 2011 | The MP4 video was rotated. |

#### Video information events
| Event ID | Code | Description |
| :-----------------------  |:-------- |  :------------------------ |
|TXLiveConstants.PLAY_EVT_GET_PLAYINFO_SUCC   | 2010 | Obtained the information of the file played back successfully. |

If you play back a video through `fileId` and the playback request succeeds (called API: startPlay(TXPlayerAuthBuilder authBuilder)), the SDK will notify the upper layer of some request information, and you can parse `param` to get the video information after receiving the `TXLiveConstants.PLAY_EVT_GET_PLAYINFO_SUCC` event.

| Video Information | Description |
| ------------------------------------------- | ---------------------------------------------- |
| EVT\_PLAY\_COVER\_URL | Video thumbnail URL |
| EVT\_PLAY\_URL | Video playback address |
| EVT\_PLAY\_DURATION | Video duration |
| EVT_TIME | Event occurrence time |
| EVT_UTC_TIME | UTC time |
| EVT_DESCRIPTION | Event description |
| EVT_PLAY_NAME  | Video name |
| TXVodConstants.EVT_IMAGESPRIT_WEBVTTURL | Download URL of the image sprite WebVTT file, which is supported by v10.2 or later |
| TXVodConstants.EVT_IMAGESPRIT_IMAGEURL_LIST | Download URL of the image sprite image, which is supported by v10.2 or later |
| TXVodConstants.EVT_DRM_TYPE | Encryption type, which is supported by v10.2 or later |


Below is the sample code of using `onPlayEvent` to get the video playback information:

```java
mVodPlayer.setVodListener(new ITXVodPlayListener() {
    @Override
    public void onPlayEvent(TXVodPlayer player, int event, Bundle param) {
        if (event == TXLiveConstants.PLAY_EVT_VOD_PLAY_PREPARED) {
            // The player preparation completion event is received, and you can call the `pause`, `resume`, `getWidth`, and `getSupportedBitrates` APIs.
        } else if (event == TXLiveConstants.PLAY_EVT_PLAY_BEGIN) {
            // The playback start event is received
        } else if (event == TXLiveConstants.PLAY_EVT_PLAY_END) {
            // The playback end event is received
        }
    }

    @Override
    public void onNetStatus(TXVodPlayer player, Bundle bundle) {
    }
});
```

[](id:status)

### Playback status feedback (onNetStatus)
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

```java
mVodPlayer.setVodListener(new ITXVodPlayListener() {
    @Override
    public void onPlayEvent(TXVodPlayer player, int event, Bundle param) {
    }

    @Override
    public void onNetStatus(TXVodPlayer player, Bundle bundle) {
        // Get the current CPU utilization
        CharSequence cpuUsage = bundle.getCharSequence(TXLiveConstants.NET_STATUS_CPU_USAGE);
        // Get the video width
        int videoWidth = bundle.getInt(TXLiveConstants.NET_STATUS_VIDEO_WIDTH);
        // Get the video height
        int videoHeight = bundle.getInt(TXLiveConstants.NET_STATUS_VIDEO_HEIGHT);
        // Get the real-time rate in Kbps
        int speed = bundle.getInt(TXLiveConstants.NET_STATUS_NET_SPEED);
        // Get the current video frame rate of streaming media
        int fps = bundle.getInt(TXLiveConstants.NET_STATUS_VIDEO_FPS);
        // Get the current video bitrate in Kbps of streaming media
        int videoBitRate = bundle.getInt(TXLiveConstants.NET_STATUS_VIDEO_BITRATE);
        // Get the current audio bitrate in Kbps of streaming media
        int audioBitRate = bundle.getInt(TXLiveConstants.NET_STATUS_AUDIO_BITRATE);
        // Get the buffer (`jitterbuffer`) size. If the current buffer length is 0, lag will occur soon.
        int jitterbuffer = bundle.getInt(TXLiveConstants.NET_STATUS_VIDEO_CACHE);
        // Get the connected server IP
        String ip = bundle.getString(TXLiveConstants.NET_STATUS_SERVER_IP);
    }
});
```

## Scenario-Specific Features

### 1. SDK-based demo component

Based on the Player SDK, Tencent Cloud has developed a [player component](https://intl.cloud.tencent.com/document/product/266/33975). It integrates quality monitoring, video encryption, TESHD, definition switch, and small window playback and is suitable for all VOD and live playback scenarios. It encapsulates complete features and provides upper-layer UIs to help you quickly create a playback program comparable to popular video apps.

### 2. Open-source GitHub projects

Based on the Player SDK, Tencent Cloud has developed immersive video player, video feed stream, and multi-layer reuse components and will provide more user scenario-based components on future versions. You can download [Player for Android](https://github.com/LiteAVSDK/Player_Android) to try them out.
