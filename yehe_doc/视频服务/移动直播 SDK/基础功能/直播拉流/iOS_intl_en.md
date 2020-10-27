## Basics

This document introduces the livestream playback function of Video Cloud SDK.

#### Livestreaming

- The **livestreaming** video source is pushed by the host in real time. When the host stops pushing, the video view on the player stops. In addition, the video is broadcast in real time, and no progress bar is displayed when the player is playing the livestreaming URL.

#### Supported protocols

Common livestreaming protocols are listed below. We recommend that you use an FLV-based livestreaming URL that starts with "http" and ends with ".flv" on apps.

| Livestreaming Protocol | Advantage | Disadvantage | Playback Delay |
| ----------- | ---------------------- | -------------------- | --------- |
| FLV | High maturity, high concurrency, and no pressure | The video can be played only after the SDK is integrated. | 2s - 3s |
| RTMP | Lowest theoretical delay when using high-quality lines | The performance is poor in the case of high concurrency. | 1s - 3s |

## Notes

- **Are there any restrictions?**
  The Tencent Video Cloud SDK **does not** impose any limits on the source of the playback URL, which means it is available for both Tencent Cloud and non-Tencent Cloud playback URLs. However, the player in the Tencent Video Cloud SDK only supports livestreaming URLs in FLV and RTMP formats.

## Interfacing

#### Step 1: create a player

The V2TXLivePlayer module in the Tencent Video Cloud SDK implements the livestream playback feature.

```objective-c
V2TXLivePlayer *txLivePlayer = [[V2TXLivePlayer alloc] init];
```

#### Step 2: render a view

Find a place to display the video images in the player. In the iOS system, a view is used as the basic rendering unit. Therefore, you simply need to prepare a view and configure the layout.

```objective-c
[txLivePlayer setRenderView:_myView];
```

Technically, the player does not directly render the video image to the view (_myView in the sample code) you provide. Instead, it creates a subView used for OpenGL rendering on top of the view.

You can adjust the size of the rendered image simply by adjusting the size and position of the view. The SDK will automatically adapt the video images to the size and position of the view.

**How can I make animations?**
You can add animation effects for a view as desired. But note that you must modify the `transform` attribute of the view, instead of the `frame` attribute.

```objective-c
[UIView animateWithDuration:0.5 animations:^{
    _myView.transform = CGAffineTransformMakeScale(0.3, 0.3); // Shrink by 1/3
}];
```

#### Step 3: start livestream playback

```objective-c
NSString* flvUrl = @"http://2157.liveplay.myqcloud.com/live/2157_xxxx.flv";
[txLivePlayer startPlay:flvUrl];
```
#### Step 4: adjust the view

* **view: size and position**
  You can modify the size and position of the view by adjusting the size and position of the parameter `view` of setupVideoWidget. The SDK will automatically adjust the size and position of the view based on your configuration.

* **setRenderFillMode: Fill or Fit**


| Option                | Description                                                  |
| -------------------   | ------------------------------------------------------------ |
| V2TXLiveFillMode_Fill | Fill the image on the screen without leaving any black edges. If the aspect ratio of the view is different from that of the screen, part of the view content will be cropped. |
| V2TXLiveFillMode_Fit  | Make the view fit the screen without cropping. If the aspect ratio of the view is different from that of the screen, black edges will appear. |

* **setRenderRotation: view rotation**


| Option | Description |
| ------------------ | --------------- |
| V2TXLiveRotation_0 | Do not rotate the view. |
| V2TXLiveRotation_90 | Rotate 90 degrees clockwise. |
| V2TXLiveRotation_180 | Rotate 180 degrees clockwise. |
| V2TXLiveRotation_270 | Rotate 270 degrees clockwise. |

#### Step 5: pause playback

Strictly speaking, you cannot pause livestream playback. Here, pausing livestream playback actually means **freezing the image** and **turning off the sound**, but the video source keeps updating on the cloud. When you resume the playback, the video is resumed from the latest time. This is the biggest difference between livestreaming and VOD. In the VOD service, the video is paused and resumed in the same way as a local video file.

```objective-c
// Pause the audio.
[txLivePlayer pauseAudio];
// Resume the audio.
[txLivePlayer resumeAudio];

// Pause the video.
[txLivePlayer pauseVideo];
// Resume the video.
[txLivePlayer resumeVideo];
```

#### Step 6: stop livestream playback

Call **stopPlay** to stop livestream playback.

```objective-c
// Stop playback.
[txLivePlayer stopPlay];
```

#### Step 7: take snapshots

You can capture the current image as a frame by calling **snapshot**. This feature can only capture frames from the current livestreaming video. To capture the entire UI, you must call the API of the iOS system.

```objective-c
// Callback notification of the Tencent Cloud video call feature
- (V2TXLiveCode)snapshot:(id<V2TXLiveSnapshotObserver>)observer;

// Snapshot callback
@protocol V2TXLiveSnapshotObserver <NSObject>
@optional
- (void)onSnapshotComplete:(TXImage *)image;
@end
```

## Delay Adjustment

The LVB feature of the Tencent Cloud SDK, equipped with the self-developed playback engine, is not developed based on ffmpeg. Compared with open-source players, LVB delivers better performance in delay control. We provide three delay adjustment modes for live show, game, and hybrid scenarios, respectively.

* **Performance comparison among the three modes**


| Control Mode | Lag Rate | Average Delay | Applicable Scenario | Principle |
| :------- | :--------- | :------- | :------------------- | :--------------------------------------------------------- |
| Speedy mode | High (relatively smooth) | 2s - 3s | Live show (online quiz) | It has an advantage in delay control and is suitable for delay-sensitive scenarios. |
| Smooth mode | Lowest | >= 5s | Livestreaming game (Penguin e-Sports) | It is suitable for ultra-high-bitrate livestreaming games, such as PlayerUnknown's Battlegrounds. |
| Auto mode | Network adaption | 2s - 8s | Hybrid scenario | The better the audience's network condition, the shorter the delay, and vice versa. |

* **Interfacing codes of the three modes**

  ```objective-c
  #define CACHE_TIME_FAST             1.0f
  #define CACHE_TIME_SMOOTH           5.0f
  
  // Speedy mode
  [_player setCacheParams:CACHE_TIME_FAST maxTime:CACHE_TIME_FAST];
  
  // Smooth mode
  [_player setCacheParams:CACHE_TIME_SMOOTH maxTime:CACHE_TIME_SMOOTH];
  
  // Auto mode
  [_player setCacheParams:CACHE_TIME_FAST maxTime:CACHE_TIME_SMOOTH];
  ```

## Listening to SDK Events

You can bind a **V2TXLivePlayerObserver** to the V2TXLivePlayer object. After that, you will be notified of SDK internal status information through **onPlayBegin**, **onLoading**, **onConnectionBroken** and **onStatisticsUpdate**.

#### Connection status update callback

```objective-c
/**
 * @brief Callback notification for the start of playback by the live player.
 */
- (void)onPlayBegin:(id<V2TXLivePlayer>)player;

/**
 * @brief Callback notification for the loading of the live player.
 */
- (void)onLoading:(id<V2TXLivePlayer>)player;

/**
 * @brief Callback notification for the disconnected live player.
 *
 * @param player Player object that calls back this notification
 * @param reason Disconnection reason. 0: normal disconnection
 */
- (void)onConnectionBroken:(id<V2TXLivePlayer>)player
                    reason:(NSInteger)reason;
```

#### Warning event callback

```objective-c
- (void)onWarning:(id<V2TXLivePlayer>)player
             code:(V2TXLiveCode)code
          message:(NSString *)msg
        extraInfo:(NSDictionary *)extraInfo;
```

#### Warning codes

| Warning Code ID | Value | Description |
| ----------------------------------------- | -------| -------------------------------- |
| V2TXLIVE_WARNING_NETWORK_BUSY             | 1101   | Data upload was jammed because the upstream bandwidth was too low. |
| V2TXLIVE_WARNING_VIDEO_BLOCK              | 2105   | Lagging occurred during video playback.                 |

#### Error event callback

```objective-c
- (void)onError:(id<V2TXLivePlayer>)player
           code:(V2TXLiveCode)code
        message:(NSString *)msg
      extraInfo:(NSDictionary *)extraInfo;
```

#### Error codes

| Error Code ID | Value | Description |
| ------------------------------   | ---- | -------- |
| V2TXLIVE_ERROR_FAILED            | -1   | Unclassified error.|
| V2TXLIVE_ERROR_INVALID_PARAMETER | -2   | An invalid parameter was input during the API call.|
| V2TXLIVE_ERROR_REFUSED           | -3   | The API call was rejected.       |
| V2TXLIVE_ERROR_NOT_SUPPORTED     | -4   | The current API cannot be called.|
| V2TXLIVE_ERROR_INVALID_LICENSE   | -5   | Failed to call the API because the license was invalid.|

## Obtaining the video resolution

Through the onVideoResolutionChanged callback, you can obtain the aspect ratio of the current video. This is the quickest way to obtain the video resolution, which takes about 100 ms to 200 ms after playback starts.

```objective-c
- (void)onVideoResolutionChanged:(id<V2TXLivePlayer>)player
                           width:(NSInteger)width
                          height:(NSInteger)height;
```

| Parameter  | Description | Value |
| :----- | :------- | :----------------- |
| width  | Video width | Resolution value, such as 1920 |
| height | Video height | Resolution value, such as 1080 |

## Periodically Triggered Status Notification

The **onStatisticsUpdate** notification is triggered every second to provide real-time feedback on the current status of the pusher. Like a car dashboard, it can inform you of what is happening inside the SDK so that you can see the current network conditions and video information.

```objective-c
- (void)onStatisticsUpdate:(id<V2TXLivePlayer>)player
                statistics:(V2TXLivePlayerStatistics *)statistics;
```

| Evaluation Parameter | Description |
| ------------ | ---------------------------- |
| appCpu | CPU utilization of the current app as a percentage (%) |
| systemCpu | int | CPU utilization of the current system as a percentage (%) |
| width | Video width |
| height | Video height |
| fps | Frame rate in fps |
| videoBitrate | Video bitrate in Kbps |
| audioBitrate | Audio bitrate in Kbps |

