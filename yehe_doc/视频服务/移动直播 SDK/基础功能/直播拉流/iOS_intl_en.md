# iOS Live Pull Document
[Original document URL](https://github.com/tencentyun/qcloud-documents/blob/master/product/%E8%A7%86%E9%A2%91%E6%9C%8D%E5%8A%A1/%E7%A7%BB%E5%8A%A8%E7%9B%B4%E6%92%AD/%E5%9F%BA%E7%A1%80%E5%8A%9F%E8%83%BD/%E7%9B%B4%E6%92%AD%E6%8B%89%E6%B5%81/iOS.md)

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
| HLS (m3u8) | Good support by mobile browsers | There is a long delay. | 10s - 30s |

## Notes

- **Are there any restrictions?**
  The Tencent Video Cloud SDK **does not** impose any limits on the source of the playback URL, which means it is available for both Tencent Cloud and non-Tencent Cloud playback URLs. However, the player in the Tencent Video Cloud SDK only supports livestreaming URLs in FLV and RTMP formats.

## Interfacing

#### Step 1: create a player

The TXLivePlayer module in the Tencent Video Cloud SDK implements the livestream playback feature.

```objective-c
TXLivePlayerV2 *txLivePlayer = [[TXLivePlayerV2 alloc] init];
```

#### Step 2: render a view

Find a place to display the video images in the player. In the iOS system, a view is used as the basic rendering unit. Therefore, you simply need to prepare a view and configure the layout.

```objective-c
[txLivePlayer setRenderView:_myView];
```

Technically, the player does not directly render the video image to the view (_myView in the sample code) you provide. Instead, it creates a subView used for OpenGL rendering on top of the view.

You can adjust the size of the rendered image simply by adjusting the size and position of the view. The SDK will automatically adapt the video images to the size and position of the view.

![39a02a8525a20fd861c69c42d2b3ab14](https://main.qcloudimg.com/raw/7a067b6e006a5661670077f979826412.png)

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

  | Option | Description |
  | ------------------- | ------------------------------------------------------------ |
  | TXLiveFillMode_Fill | Fill the image on the screen without leaving any black edges. If the aspect ratio of the view is different from that of the screen, part of the view content will be cropped. |
  | TXLiveFillMode_Fit | Make the view fit the screen without cropping. If the aspect ratio of the view is different from that of the screen, black edges will appear. |

* **setRenderRotation: view rotation**

  | Option | Description |
  | ------------------ | --------------- |
  | TXLiveRotation_0 | Do not rotate the view. |
  | TXLiveRotation_90 | Rotate 90 degrees clockwise. |
  | TXLiveRotation_180 | Rotate 180 degrees clockwise. |
  | TXLiveRotation_270 | Rotate 270 degrees clockwise. |

  /// Upload the TODO image to the server on Monday.
  ![Snapshot 2020-08-06 10.55.49 AM](/Users/jj/Desktop/Snapshot 2020-08-06 10.55.49 AM.png)

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

#### Step 7: receive messages

This feature is used to deliver certain custom messages from the pusher to the audience through the audio/video lines. It is applicable to the following scenarios:

- Online quiz: the pusher delivers the **questions** to the audience. Perfect "sound-image-question" synchronization can be achieved.
- Live show: the pusher delivers **lyrics** to the audience. The lyrics can be displayed in real time on the player, without any effect from video encoding quality degradation.
- Online education: the pusher delivers **Laser pointer** and **Doodle pen** effects to the audience. Circles and lines can be drawn in real time on the player.

You can use this feature as follows:

* The TXLivePlayer monitors messages through **TXLivePlayerObserver**.

```objective-c
- (void)onRecvSEIMessage:(id<TXLivePlayerV2>)player message:(NSData *)msg {
    NSString *receiveMsg = [[NSString alloc] initWithData:msg encoding:NSUTF8StringEncoding];
    [self makeToastTip:receiveMsg];
}
```

#### Step 8: take snapshots

You can capture the current image as a frame by calling **snapshot**. This feature can only capture frames from the current livestreaming video. To capture the entire UI, you must call the API of the iOS system.

```objective-c
// Callback notification of the Tencent Cloud video call feature
- (TXLiveCode)snapshot:(id<TXLiveSnapshotObserver>)observer;

// Snapshot callback
@protocol TXLiveSnapshotObserver <NSObject>
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

You can bind a **TXLivePlayerObserver** to the TXLivePlayer object. After that, you will be notified of SDK internal status information through **onConnectionStateUpdate** and **onStatisticsUpdate**.

#### Connection status update callback

```objective-c
- (void)onConnectionStateUpdate:(id<TXLivePlayerV2>)player
                          state:(TXLivePlayerConnectionState)state
                        message:(NSString *)msg
                      extraInfo:(NSDictionary *)extraInfo;
```

#### Playback start event

| Event ID | Value | Description |
| -------------------------------------------------- | ---- | -------------- |
| TXLivePlayerConnectionState_StartConnectServer | 0 | Start connecting to the server |
| TXLivePlayerConnectionState_ConnectServerSuccess | 1 | Successfully connected to the server |
| TXLivePlayerConnectionState_StartReconnectServer | 2 | Start reconnecting to the server |
| TXLivePlayerConnectionState_StartLoading | 3 | Star loading |
| TXLivePlayerConnectionState_ReconnectServerSuccess | 5 | Successfully reconnected to the server |

#### Playback end event

| Event ID | Value | Description |
| -------------------------------------------- | ---- | ---------------- |
| TXLivePlayerConnectionState_LoadFinish | 4 | Finish loading |
| TXLivePlayerConnectionState_DisconnectServer | 6 | Disconnect from the server |

#### Warning event callback

```objective-c
- (void)onWarning:(id<TXLivePlayerV2>)player
             code:(TXLiveCode)code
          message:(NSString *)msg
        extraInfo:(NSDictionary *)extraInfo;
```

#### Warning codes

* Common warning codes (not belonging to the network, audio, or video module)

  Range: 7000000 to 7000999

  | Warning Code ID | Value | Description |
  | --------- | ---- | -------- |
  | TXLIVE_OK | 0 | Playback successful |

* Network module warning codes

  Range: 7001000 to 7001999

  | Warning Code ID | Value | Description |
  | --------------------------- | ------- | -------- |
  | TXLIVE_WARNING_NETWORK_BUSY | 7001000 | Network busy |

* Video module warning codes

  Range: 7002000 to 7002999

  | Warning Code ID | Value | Description |
  | -------------------------- | ------- | ------------ |
  | TXLIVE_WARNING_VIDEO_BLOCK | 7002000 | Failed to obtain the video |

#### Error event callback

```objective-c
- (void)onError:(id<TXLivePlayerV2>)player
           code:(TXLiveCode)code
        message:(NSString *)msg
      extraInfo:(NSDictionary *)extraInfo;
```

#### Error codes

### Common error codes

  Range: -7001000 to -7001999

| Error Code ID | Value | Description |
| ------------------------------ | -------- | -------- |
| TXLIVE_ERROR_NOT_SUPPORTED | -7001000 | Not supported |
| TXLIVE_ERROR_INVALID_PARAMETER | -7001001 | Invalid parameter |
| TXLIVE_ERROR_REFUSED | -7001002 | Refused |
| TXLIVE_ERROR_NOT_READY | -7001003 | Not ready |

* Camera error codes

  Range: -7002000 to -7002999

  | Error Code ID | Value | Description |
  | --------------------------------- | -------- | ------------------ |
  | TXLIVE_ERROR_CAMERA_START_FAILED  | -7002000 | Failed to start the camera |
  | TXLIVE_ERROR_CAMERA_OCCUPIED | -7002001 | Camera occupied |
  | TXLIVE_ERROR_CAMERA_NO_PERMISSION | -7002002 | Not authorized to access the camera |

* Microphone error codes

  Range: -7003000 to -7003999

  | Error Code ID | Value | Description |
  | ------------------------------------- | -------- | ------------------ |
  | TXLIVE_ERROR_MICROPHONE_START_FAILED | -7003000 | Failed to start the microphone |
  | TXLIVE_ERROR_MICROPHONE_OCCUPIED | -7003001 | Microphone occupied |
  | TXLIVE_ERROR_MICROPHONE_NO_PERMISSION | -7003002 | Not authorized to access the microphone |

### Screen capture error codes

  Range: -7004000 to -7004999

| Error Code ID | Value | Description |
| ----------------------------------------- | -------- | -------------- |
| TXLIVE_ERROR_SCREEN_CAPTURE_NOT_SUPPORTED | -7004000 | Screen capture not supported |
| TXLIVE_ERROR_SCREEN_CAPTURE_START_FAILED | -7004001 | Failed to capture screen |
| TXLIVE_ERROR_SCREEN_CAPTURE_INTERRUPTED | -7004002 | Screen capture interrupted |

* RTMP-specific error codes

  Range: -3000 to -3999

  | Error Code ID | Value | Description |
  | --------------------------------- | -------- | -------- |
  | TXLIVE_ERROR_INVALID_RTMP_LICENSE | -7005001 | Invalid RTMP license |

## Obtaining the video resolution

Through the onVideoResolutionChanged callback, you can obtain the aspect ratio of the current video. This is the quickest way to obtain the video resolution, which takes about 100 ms to 200 ms after playback starts.

```objective-c
- (void)onVideoResolutionChanged:(id<TXLivePlayerV2>)player
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
- (void)onStatisticsUpdate:(id<TXLivePlayerV2>)player
                statistics:(TXLivePlayerStatistics *)statistics;
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

