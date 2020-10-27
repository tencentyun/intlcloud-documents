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

#### step1: setup a view
```
<com.tencent.rtmp.ui.TXCloudVideoView
	android:id="@+id/video_video"
	android:layout_width="match_parent"
	android:layout_height="match_parent" />
```

#### step2: create a player

The `V2TXLivePlayer` module in the Tencent Video Cloud SDK implements the livestream playback feature, and using `setRenderView` to bind view.

```
TXCloudVideoView videoView = (TXCloudVideoView) view.findViewById(R.id.video_view);
V2TXLivePlayer txLivePlayer = new V2TXLivePlayerImpl(mContext);
txLivePlayer.setRenderView(videoView);
```

#### step3: start livestream playback

```
String flvUrl = "http://2157.liveplay.myqcloud.com/live/2157_xxxx.flv";
txLivePlayer.startPlay(flvUrl); 
```

#### step4: adjust the view

* **setRenderFillMode: Fill or Fit**

| Option              | Description                                                         |
|  ----------------  | -----------------------------------------------------------  |
| V2TXLiveFillMode_Fill | Fill the image on the screen without leaving any black edges. If the aspect ratio of the view is different from that of the screen, part of the view content will be cropped. |
| V2TXLiveFillMode_Fit  | Make the view fit the screen without cropping. If the aspect ratio of the view is different from that of the screen, black edges will appear. |

* **setRenderRotation: view rotation**

| Option              | Description           |
| ------------------ | ------------- |
| V2TXLiveRotation_0   | Do not rotate the view.        |
| V2TXLiveRotation_90  | Rotate 90 degrees clockwise.  |
| V2TXLiveRotation_180 | Rotate 180 degrees clockwise. |
| V2TXLiveRotation_270 | Rotate 270 degrees clockwise. |

```
txLivePlayer.setRenderRotation(V2TXLiveDef.V2TXLiveRotation.V2TXLiveRotation_0);
txLivePlayer.setRenderFillMode(V2TXLiveDef.V2TXLiveFillMode.V2TXLiveFillMode_Fit);
```

 ![](https://main.qcloudimg.com/raw/d9ed5ecf515424bbbb53754a56a7c98f.png)

#### step5: pause playback

Strictly speaking, you cannot pause livestream playback. Here, pausing livestream playback actually means **freezing the image** and **turning off the sound**, but the video source keeps updating on the cloud. When you resume the playback, the video is resumed from the latest time. This is the biggest difference between livestreaming and VOD. In the VOD service, the video is paused and resumed in the same way as a local video file.

```
// Pause the audio.
txLivePlayer.pauseAudio();
// Resume the audio.
txLivePlayer.resumeAudio();

// Pause the video.
txLivePlayer.pauseVideo();
// Resume the video.
txLivePlayer.resumeVideo();
```

#### step6: stop livestream playback

Call **stopPlay** to stop livestream playback.

```
// Stop playback.
txLivePlayer.stopPlay();
```

#### step7: take snapshots

You can capture the current image as a frame by calling **snapshot**. This feature can only capture frames from the current livestreaming video. To capture the entire UI, you must call the API of the Android system.

```
txLivePlayer.snapshot(new V2TXLiveSnapshotObserver() {
	@Override
	public void onSnapshotComplete(Bitmap bitmap) {
		if (null != bitmap) {
			//doSomething
		}
	}
});
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

```
private float CACHE_TIME_FAST = 1.0f;
private float CACHE_TIME_SMOOTH = 5.0f;
  
// Speedy mode
txLivePlayer.setCacheParams(CACHE_TIME_FAST, CACHE_TIME_FAST);
// Smooth mode
txLivePlayer.setCacheParams(CACHE_TIME_SMOOTH, CACHE_TIME_SMOOTH);
// Auto mode
txLivePlayer.setCacheParams(CACHE_TIME_FAST, CACHE_TIME_SMOOTH);
```

## Listening to SDK Events

You can bind a `V2TXLivePlayerObserver` to the `V2TXLivePlayer` object. After that, you will be notified of SDK internal status information through `onConnectionStateUpdate` and `onStatisticsUpdate`.

#### Warning codes
| Warning Code ID  | Value | Description |
| :--------- | :---- | :-------- |
| V2TXLIVE_OK | 0    | Playback successful |
| V2TXLIVE_WARNING_NETWORK_BUSY | 1101 | Network busy |
| V2TXLIVE_WARNING_VIDEO_BLOCK | 2105 | Failed to obtain the video |


```
@Override
public void onWarning(V2TXLivePlayer player, int code, String msg, Bundle extraInfo) {
	// doSomething
}
```
#### Error codes
| Error Code ID                       | Value | Description       |
| :----------------------------- | :--- | :----------- |
| V2TXLIVE_ERROR_FAILED            | -1   | Unclassified error     |
| V2TXLIVE_ERROR_INVALID_PARAMETER | -2   | Invalid parameter |
| V2TXLIVE_ERROR_REFUSED           | -3   | Refused     |
| V2TXLIVE_ERROR_NOT_SUPPORTED     | -4   | Not supported |
| V2TXLIVE_ERROR_INVALID_LICENSE   | -5   | Invalid license |

```
@Override
public void onError(V2TXLivePlayer player, int code, String msg, Bundle extraInfo) {
	// doSomething
}
```
#### Obtaining the video resolution

Through the `onVideoResolutionChanged` callback, you can obtain the aspect ratio of the current video. This is the quickest way to obtain the video resolution, which takes about 100 ms to 200 ms after playback starts.

```
@Override
public void onVideoResolutionChanged(V2TXLivePlayer player, int width, int height) {
	// doSomething
}
```

| Parameter   | Description     | Value               |
| :----- | :------- | :----------------- |
| width  | Video width | Resolution value, such as 1920 |
| height | Video height | Resolution value, such as 1080 |

#### Periodically Triggered Status Notification

The `onStatisticsUpdate` notification is triggered every second to provide real-time feedback on the current status of the pusher. Like a car dashboard, it can inform you of what is happening inside the SDK so that you can see the current network conditions and video information.

```
@Override
public void onStatisticsUpdate(V2TXLivePlayer player, V2TXLiveDef.V2TXLivePlayerStatistics statistics) {
	// doSomething
}
```

| Parameter       | Description                      |
| ------------ | ---------------------------- |
| appCpu       | CPU utilization of the current app as a percentage (%)     |
| systemCpu    | CPU utilization of the current system as a percentage (%)  |
| width        | Video width                       |
| height       | Video height                      |
| fps          | Frame rate in fps                 |
| videoBitrate | Video bitrate in Kbps             |
| audioBitrate | Audio bitrate in Kbps             |

