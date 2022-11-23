## `SuperPlayerPlugin` Class

### setGlobalLicense

**Description**

This API is used to set the license.

After you apply for and get a license, you can use the following API to initialize it. We recommend you call this API during application start. Video playback will fail if the license is not set.

**API**

```dart
static Future<void> setGlobalLicense(String licenceUrl, String licenceKey) async;
```

**Parameter description**

| Parameter | Type | Description |
| ---------- | ------ | -------------- |
| licenceUrl | String | The license URL |
| licenceKey | String | The license key |

**Return values**

Unlimited


### createVodPlayer

**Description**

This API is used to create a VOD player instance at the native layer. If you use `TXVodPlayerController`, as it already integrates an instance, you don't need to create another.

**API**

```dart
static Future<int?> createVodPlayer() async;
```

**Parameter description**

Unlimited

**Return values**

| Returned Value | Type | Description |
| ------ | ------ | ------------------ |
| playerId | int | The player ID |


### createLivePlayer

**Description**

This API is used to create a live player instance at the native layer. If you use `TXVodPlayerController`, as it already integrates an instance, you don't need to create another.

**API**

```dart
static Future<int?> createLivePlayer() async;
```

**Parameter description**

Unlimited

**Return values**

| Returned Value | Type | Description |
| ------ | ------ | ------------------ |
| playerId | int | The player ID |


### setConsoleEnabled

**Description**

This API is used to enable/disable player native log output.

**API**

```dart
static Future<int?> setConsoleEnabled() async;
```

**Parameter description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| enabled | bool | Enables/Disables player log |

**Return values**

Unlimited


### releasePlayer

**Description**

This API is used to release the player resources.

**API**

```dart
static Future<int?> releasePlayer(int? playerId) async;
```

**Parameter description**

Unlimited

**Return values**

Unlimited


### setGlobalMaxCacheSize

**Description**

This API is used to set the maximum cache size of the player engine. After setting, the backend will clear files in the cache directory automatically according to the set value.

**API**

```dart
static Future<void> setGlobalMaxCacheSize(int size) async;
```

**Parameter description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| size | int | The maximum cache size in MB |

**Return values**

Unlimited


### setGlobalCacheFolderPath

**Description**

This API is used to set the cache path, which is set to the application's sandbox directory by default. You only need to pass in the relative cache directory instead of the entire absolute path to the parameter.

**API**

```dart
static Future<bool> setGlobalCacheFolderPath(String postfixPath) async;
```

**Parameter description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| postfixPath | String | The cache path, which is set to the application's sandbox directory by default. You only need to pass in the relative cache directory instead of the entire absolute path to `postfixPath`. On Android, videos will be cached to the `Android/data/your-pkg-name/files/testCache` directory on the SD card. On iOS, videos will be cached to the `Documents/testCache` directory in the sandbox. |

**Return values**

Unlimited


### setLogLevel

**Description**

This API is used to set the log output level.

**API**

```dart
static Future<void> setLogLevel(int logLevel) async;
```

**Parameter description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| logLevel | int | `0`: Logs at all levels;</br> `1`: DEBUG, INFO, WARNING, ERROR, and FATAL logs;</br> `2`: INFO, WARNING, ERROR, and FATAL logs;</br> `3`: WARNING, ERROR, and FATAL logs;</br> `4`: ERROR and FATAL logs;</br> `5`: Only FATAL logs;</br> `6`: No SDK logs. |

**Return values**

Unlimited


### setBrightness

**Description**

This API is used to set the brightness. It is applicable only to the current application.

**API**

```dart
static Future<void> setBrightness(double brightness) async;
```

**Parameter description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| brightness | double | The brightness level. Value range: 0.0–1.0 |

**Return values**

Unlimited


### restorePageBrightness

**Description**

This API is used to reset the UI brightness. It is applicable only to the current application.

**API**

```dart
static Future<void> restorePageBrightness() async;
```

**Parameter description**

Unlimited

**Return values**

Unlimited


### getBrightness

**Description**

This API is used to get the brightness level of the current UI.

**API**

```dart
static Future<double> getBrightness() async;
```

**Parameter description**

Unlimited

**Return values**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| brightness | double | The brightness level. Value range: 0.0–1.0 |


### setSystemVolume

**Description**

This API is used to set the volume level of the current system.

**API**

```dart
static Future<void> setSystemVolume(double volume) async;
```

**Parameter description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| volume | double | The volume level. Value range: 0.0–1.0 |

**Return values**

Unlimited


### getSystemVolume

**Description**

This API is used to set the volume level of the current system.

**API**

```dart
static Future<double> getSystemVolume() async;
```

**Parameter description**

Unlimited

**Returned value description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| volume | double | The volume level. Value range: 0.0–1.0 |


### abandonAudioFocus

**Description**

This API is used to release the audio focus. It is applicable only to Android.

**API**

```dart
static Future<double> abandonAudioFocus() async;
```

**Parameter description**

Unlimited

**Return values**

Unlimited


### requestAudioFocus

**Description**

This API is used to request the audio focus. It is applicable only to Android.

**API**

```dart
static Future<void> requestAudioFocus() async ;
```

**Parameter description**

Unlimited

**Return values**

Unlimited


### isDeviceSupportPip

**Description**

This API is used to check whether the current device supports the picture-in-picture (PiP) mode.

**API**

```dart
static Future<int> isDeviceSupportPip() async;
```

**Parameter description**

Unlimited

**Returned value description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| isDeviceSupportPip | int | `0`: The PiP mode can be enabled;</br> `-101`: The Android version is too early; </br> `-102`: The PiP permission is disabled or the device doesn't support PiP; </br> `-103`: The current UI has been terminated. |


### getLiteAVSDKVersion

**Description**

This API is used to get the version number of the current native-layer player SDK.

**API**

```dart
static Future<String?> getLiteAVSDKVersion() async;
```

**Parameter description**

Unlimited

**Returned value description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| sdkVersion | String | The version of the current player SDK. |


### setGlobalEnv

**Description**

This API is used to set the `LiteAVSDK` connection environment.
Tencent Cloud's globally deployed environments need to be connected to access points in different regions according to the applicable laws and regulations in the region.

**Note**

If your users are in the Chinese mainland, do not call this API; if your users are from outside the Chinese mainland, contact us to learn how to configure `env_config` so as to ensure that your application complies with the General Data Protection Regulation (GDPR).

**API**

```dart
static Future<int> setGlobalEnv(String envConfig) async;
```

**Parameter description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| envConfig | String | The environment to be connected to. The SDK is connected to the Chinese mainland environment by default. |

**Returned value description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| result | int | Valid values: `1`: Set successfully; `2`: Failed to set. |



## `TXVodPlayerController` Class


### initialize

**Description**

This API is used to initialize the controller and request assignment of shared textures.

**API**

```dart
Future<void> initialize({bool? onlyAudio}) async;
```

**Parameter description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| onlyAudio | bool | Whether the player is an audio-only player. This parameter is optional. |

**Returned value description**

Unlimited


### startVodPlay

**Note**

Starting from v10.7, `startPlay` is replaced by `startVodPlay`, and playback will succeed only after you use `{@link SuperPlayerPlugin#setGlobalLicense}` to set the license; otherwise, playback will fail (black screen occurs). The license needs to be set only once globally. You can use the license for CSS, UGSV, or video playback. If you have no such licenses, you can [quickly apply for a trial license](https://www.tencentcloud.com/document/product/266/51098) or [purchase an official license](https://www.tencentcloud.com/document/product/266/51098#.E8.B4.AD.E4.B9.B0.E5.B9.B6.E6.96.B0.E5.BB.BA.E6.AD.A3.E5.BC.8F.E7.89.88-license).

**Description**

This API is used to play back a video via URL.

**API**

```dart
Future<bool> startVodPlay(String url) async;
```

**Parameter description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| url | String | The URL of the video to be played back. |

**Returned value description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| result | bool | Whether creation succeeded. |


### startVodPlayWithParams

**Note**

Starting from v10.7, `startPlay` is replaced by `startVodPlay`, and playback will succeed only after you use `{@link SuperPlayerPlugin#setGlobalLicense}` to set the license; otherwise, playback will fail (black screen occurs). The license needs to be set only once globally. You can use the license for CSS, UGSV, or video playback. If you have no such licenses, you can [quickly apply for a trial license](https://www.tencentcloud.com/document/product/266/51098) or [purchase an official license](https://www.tencentcloud.com/document/product/266/51098#.E8.B4.AD.E4.B9.B0.E5.B9.B6.E6.96.B0.E5.BB.BA.E6.AD.A3.E5.BC.8F.E7.89.88-license).

**Description**

This API is used to play back a video via `fileId`.

**API**

```dart
Future<void> startVodPlayWithParams(TXPlayInfoParams params) async;
```

**Parameter description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| appId | int | The application's `appId`, which is required. |
| fileId | String | The file ID, which is required. |
| timeout | String | Encrypted link timeout timestamp, which will be converted to a hexadecimal lowercase string. The CDN server will determine whether the link is valid based on the timestamp |
| exper | String | Preview duration in seconds. |
| us | String | A unique ID request, which increases the link uniqueness. |
| sign | String | The hotlink protection signature. For more information, see [Overview](https://www.tencentcloud.com/document/product/266/33984). |
| https | String | Whether to use HTTPS requests. Default value: `false`. |

**Returned value description**

Unlimited


### pause

**Description**

This API is used to pause a video during playback.

**API**

```dart
Future<void> pause() async;
```

**Parameter description**

Unlimited

**Returned value description**

Unlimited


### resume

**Description**

This API is used to resume the playback of a paused video.

**API**

```dart
Future<void> resume() async;
```

**Parameter description**

Unlimited

**Returned value description**

Unlimited


### stop

**Description**

This API is used to stop a video during played back.

**API**

```dart
Future<bool> stop({bool isNeedClear = false}) async;
```
**Parameter description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| isNeedClear | bool | Whether to clear the last-frame image. |

**Returned value description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| result | bool | Whether stop succeeded. |


### setIsAutoPlay

**Description**

This API is used to set whether to automatically play back the video after calling `startVodPlay` to load the video URL.

**API**

```dart
Future<void> setIsAutoPlay({bool? isAutoPlay}) async;
```

**Parameter description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| isAutoPlay | bool | Whether to play back the video automatically. |

**Returned value description**

Unlimited


### isPlaying

**Description**

This API is used to query whether the player is currently playing a video.

**API**

```dart
Future<bool> isPlaying() async;
```

**Parameter description**

Unlimited

**Returned value description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| isPlaying | bool | Whether playback is ongoing. |


### setMute

**Description**

This API is used to set whether to mute the current playback.

**API**

```dart
Future<void> setMute(bool mute) async;
```

**Parameter description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| mute | bool | Whether to mute the playback. |

**Returned value description**

Unlimited


### setLoop

**Description**

This API is used to specify whether to loop the video after the video playback ends.

**API**

```dart
Future<void> setLoop(bool loop) async;
```

**Parameter description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| loop | bool | Whether to loop the video. |

**Returned value description**

Unlimited


### seek

**Description**

This API is used to adjust the playback progress to the specified time.

**API**

```dart
_controller.seek(progress);
```

**Parameter description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| progress | double | Target playback time in seconds. |

**Returned value description**

Unlimited


### setRate

**Description**

This API is used to set the playback rate.

**API**

```dart
Future<void> setRate(double rate) async;
```

**Parameter description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| rate | double | Video playback rate. Default value: 1.0 |

**Returned value description**

Unlimited


### getSupportedBitrates

**Description**

This API is used to get the bitrates supported by the video being played back.

**API**

```dart
Future<List?> getSupportedBitrates() async;
```

**Parameter description**

Unlimited

**Returned value description**

| Returned Value | Type | Description |
| ------ | ------ | ------------------ |
| index | int | Bitrate number |
| width | int | The video width for the bitrate |
| height | int | Video height for the bitrate |
| bitrate | int | Bitrate value |

### getBitrateIndex

**Description**

This API is used to get the set bitrate number.

**API**

```dart
Future<int> getBitrateIndex() async;
```

**Parameter description**

Unlimited

**Returned value description**

| Returned Value | Type | Description |
| ------ | ------ | ------------------ |
| index | int | Bitrate number |


### setBitrateIndex

**Description**

This API is used to set the current bitrate by bitrate number.

**API**

```dart
Future<void> setBitrateIndex(int index) async;
```

**Parameter description**

| Returned Value | Type | Description |
| ------ | ------ | ------------------ |
| index | int | The bitrate number. `-1` indicates to enable adaptive bitrate streaming. |

**Returned value description**

Unlimited


### setStartTime

**Description**

This API is used to specify the playback start time.

**API**

```dart
Future<void> setStartTime(double startTime) async;
```

**Parameter description**

| Returned Value | Type | Description |
| ------ | ------ | ------------------ |
| startTime | double | The playback start time in seconds. |

**Returned value description**

Unlimited


### setAudioPlayoutVolume

**Description**

This API is used to set the video volume level.

**API**

```dart
Future<void> setAudioPlayoutVolume(int volume) async;
```

**Parameter description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| volume | int | Video volume level. Value range: 0–100 |

**Returned value description**

Unlimited


### setRequestAudioFocus

**Description**

This API is used to set the audio focus. It is applicable only to Android.

**API**

```dart
Future<bool> setRequestAudioFocus(bool focus) async;
```

**Parameter description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| focus | bool | Whether to set the audio focus. |

**Returned value description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| result | bool | Whether the focus is set successfully. |


### setConfig

**Description**

This API is used to configure the player.

**API**

```dart
Future<void> setConfig(FTXVodPlayConfig config) async ;
```

**Parameter description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| config | FTXVodPlayConfig | For more information, see the `FTXVodPlayConfig` class. |


**Returned value description**

Unlimited


### getCurrentPlaybackTime

**Description**

This API is used to get the current playback time in seconds.

**API**

```dart
Future<double> getCurrentPlaybackTime() async;
```

**Parameter description**

Unlimited

**Returned value description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| playbackTime | double | The current playback time in seconds. |


### getBufferDuration

**Description**

This API is used to get the currently buffered video duration in seconds.

**API**

```dart
 Future<double> getBufferDuration();
```

**Parameter description**

Unlimited

**Returned value description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| playbackTime | double | The currently buffered video duration in seconds. |


### getPlayableDuration

**Description**

This API is used to get the playable duration of the video being played back in seconds.

**API**

```dart
 Future<double> getPlayableDuration() async;
```

**Parameter description**

Unlimited

**Returned value description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| playableDuration | double | The currently playable video duration in seconds. |


### getWidth

**Description**

This API is used to get the width of the video being played back.

**API**

```dart
Future<int> getWidth() async;
```

**Parameter description**

Unlimited

**Returned value description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| width | int | The current video width |


### getHeight

**Description**

This API is used to get the height of the video being played back.

**API**

```dart
Future<int> getHeight() async;
```

**Parameter description**

Unlimited

**Returned value description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| height | int | The current video height. |


### setToken

**Description**

This API is used to set the token for HLS encryption. After the token is set, the player will automatically add `voddrm.token` before the filename in the URL.

**API**

```dart
Future<void> setToken(String? token) async;
```

**Parameter description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| token | String | The token for video playback. |

**Returned value description**

Unlimited


### isLoop

**Description**

This API is used to get the current playback loop status of the player.

**API**

```dart
Future<bool> isLoop() async;
```

**Parameter description**

Unlimited

**Returned value description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| isLoop | bool | Whether the player is in loop status. |


### enableHardwareDecode

**Description**

This API is used to enable/disable playback based on hardware decoding. After the value is set, it will not take effect until the video playback is restarted.

**API**

```dart
Future<bool> enableHardwareDecode(bool enable);
```

**Parameter description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| enable | bool | Whether to enable hardware decoding. |

**Returned value description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| result | bool | The hardware/software decoding setting result. |


### dispose

**Description**

This API is used to terminate the controller. After it is called, all notification events will be terminated, and the player will be released.

**API**

```dart
void dispose() async;
```

**Parameter description**

Unlimited

**Returned value description**

Unlimited


### getDuration

**Description**

This API is used to get the total video duration.

**API**

```dart
Future<double> getDuration() async;
```

**Parameter description**

Unlimited

**Returned value description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| duration | double | The total video duration in seconds. |


### enterPictureInPictureMode

**Description**

This API is used to enter the PiP mode.

**API**

```dart
Future<int> enterPictureInPictureMode({String? backIconForAndroid, String? playIconForAndroid, String? pauseIconForAndroid, String? forwardIconForAndroid}) async;
```

**Parameter description**

The parameters are applicable only to Android.

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| backIcon | String | The seek backward icon, which can be up to 1 MB in size as limited by Android. It is optional, and if it is not set, the system icon will be used. |
| playIcon | String | The playback icon, which can be up to 1 MB in size as limited by Android. It is optional, and if it is not set, the system icon will be used. |
| pauseIcon | String | The pause icon, which can be up to 1 MB in size as limited by Android. It is optional, and if it is not set, the system icon will be used. |
| forwardIcon | String | The fast forward icon, which can be up to 1 MB in size as limited by Android. It is optional, and if it is not set, the system icon will be used. |

**Returned value description**

| Parameter | Code | Description |
| ------ | ------ | ------------------ |
| NO_ERROR | 0 | Started successfully with no errors. |
| ERROR_PIP_LOWER_VERSION | -101 | The Android version is too early and doesn't support the PiP mode. |
| ERROR_PIP_DENIED_PERMISSION | -102 | The PiP mode permission wasn't enabled, or the current device doesn't support PiP. |
| ERROR_PIP_ACTIVITY_DESTROYED | -103 | The current UI was terminated. |
| ERROR_IOS_PIP_DEVICE_NOT_SUPPORT | -104 | The device model or system version doesn't support PiP (only supported on iPadOS 9+ and iOS 14+). This error is applicable only to iOS. |
| ERROR_IOS_PIP_PLAYER_NOT_SUPPORT | -105 | The player doesn't support PiP. This error is applicable only to iOS. |
| ERROR_IOS_PIP_VIDEO_NOT_SUPPORT | -106 | The video doesn't support PiP. This error is applicable only to iOS. |
| ERROR_IOS_PIP_IS_NOT_POSSIBLE | -107 | The PiP controller was unavailable. This error is applicable only to iOS. |
| ERROR_IOS_PIP_FROM_SYSTEM | -108 | The PiP controller reported an error. This error is applicable only to iOS. |
| ERROR_IOS_PIP_PLAYER_NOT_EXIST | -109 | The player object doesn’t exist. This error is applicable only to iOS. |
| ERROR_IOS_PIP_IS_RUNNING | -110 | The PiP feature was running. This error is applicable only to iOS. |
| ERROR_IOS_PIP_NOT_RUNNING | -111 | The PiP feature didn't start. This error is applicable only to iOS. |



## `FTXVodPlayConfig` Class

#### Attribute configuration description


| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| connectRetryCount | int | The number of player reconnections. If the SDK is disconnected from the server due to an exception, the SDK will attempt to reconnect to the server. |
| connectRetryInterval | int | The interval between two player reconnections. If the SDK is disconnected from the server due to an exception, the SDK will attempt to reconnect to the server. |
| timeout | int | Player connection timeout period |
| playerType | int | Player type. Valid values: 0: VOD; 1: live streaming; 2: live stream replay. |
| headers | Map | Custom HTTP headers |
| enableAccurateSeek | bool | Whether to enable accurate seek. Default value: `true`. |
| autoRotate | bool | If it is set to `true`, the MP4 file will be automatically rotated according to the rotation angle set in the file, which can be obtained from the `PLAY_EVT_CHANGE_ROTATION` event. Default value: `true`. |
| smoothSwitchBitrate | bool | Whether to enable smooth multi-bitrate HLS stream switch. If it is set to `false` (default), multi-bitrate URLs are opened faster. If it is set to `true`, the bitrate can be switched smoothly when IDR frames are aligned. |
| cacheMp4ExtName | String | The cached MP4 filename extension. Default value: `mp4`. |
| progressInterval | int | The progress callback interval in milliseconds. If it is not set, the SDK will call back the progress once every 0.5 seconds. |
| maxBufferSize | int | The maximum size of playback buffer in MB. The setting will affect `playableDuration`. The greater the value, the more the data that is buffered in advance. |
| maxPreloadSize | int | Maximum preload buffer size in MB |
| firstStartPlayBufferTime | int | Duration of the video data that needs to be loaded during the first buffering in ms. Default value: 100 ms |
| nextStartPlayBufferTime | int | Minimum buffered data size to stop buffering (secondary buffering for insufficient buffered data or progress bar drag buffering caused by `seek`) in ms. Default value: 250 ms |
| overlayKey | String | The HLS security enhancement encryption and decryption key |
| overlayIv | String | The HLS security enhancement encryption and decryption IV |
| extInfoMap | Map | Some special configuration items |
| enableRenderProcess | bool | Whether to allow the postrendering and postproduction feature, which is enabled by default. If the super-resolution plugin exists after it is enabled, the plugin will be loaded by default |
| preferredResolution | int | Resolution of the video used for playback preferably. `preferredResolution` = `width` * `height` |


## `TXLivePlayerController` Class


### initialize

**Description**

This API is used to initialize the controller and request assignment of shared textures.

**API**

```dart
Future<void> initialize({bool? onlyAudio}) async;
```

**Parameter description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| onlyAudio | bool | Whether the player is an audio-only player. This parameter is optional. |

**Returned value description**

Unlimited


### startLivePlay

**Note**

Starting from v10.7, `startPlay` is replaced by `startLivePlay`, and playback will succeed only after you use `{@link SuperPlayerPlugin#setGlobalLicense}` to set the license; otherwise, playback will fail (black screen occurs). The license needs to be set only once globally. You can use the license for CSS, UGSV, or video playback. If you have no such licenses, you can quickly [apply for a trial license](https://www.tencentcloud.com/document/product/266/51098) or [purchase an official license](https://www.tencentcloud.com/zh/document/product/266/51098).

**Description**

This API is used to play back a video via URL.

**API**

```dart
Future<bool> play(String url, {int? playType}) async;
```

**Parameter description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| url | String | The URL of the video to be played back. |
| playType | int | The supported playback type, which is optional. RTMP live streaming is used by default. Valid values: `LIVE_RTMP`, `LIVE_FLV`, `LIVE_RTMP_ACC`, and `VOD_HLS`. For more information, see `TXPlayType`. |

**Returned value description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| result | bool | Whether creation succeeded. |


### pause

**Description**

This API is used to pause a video during playback.

**API**

```dart
Future<void> pause() async;
```

**Parameter description**

Unlimited

**Returned value description**

Unlimited


### resume

**Description**

This API is used to resume the playback of a paused video.


**API**

```dart
Future<void> resume() async;
```

**Parameter description**

Unlimited

**Returned value description**

Unlimited


### stop

**Description**

This API is used to stop a video during played back.

**API**

```dart
Future<bool> stop({bool isNeedClear = false}) async;
```
**Parameter description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| isNeedClear | bool | Whether to clear the last-frame image. |

**Returned value description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| result | bool | Whether stop succeeded. |


### setIsAutoPlay

**Description**

This API is used to set whether to automatically play back the video after calling `startVodPlay` to load the video URL.

**API**

```dart
Future<void> setIsAutoPlay({bool? isAutoPlay}) async;
```

**Parameter description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| isAutoPlay | bool | Whether to play back the video automatically. |

**Returned value description**

Unlimited


### isPlaying

**Description**

This API is used to query whether the player is currently playing a video.

**API**

```dart
Future<bool> isPlaying() async;
```

**Parameter description**

Unlimited

**Returned value description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| isPlaying | bool | Whether playback is ongoing. |


### setMute

**Description**

This API is used to set whether to mute the current playback.

**API**

```dart
Future<void> setMute(bool mute) async;
```

**Parameter description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| mute | bool | Whether to mute the playback. |

**Returned value description**

Unlimited


### setVolume

**Description**

This API is used to set the video volume level.

**API**

```dart
 Future<void> setVolume(int volume);
```

**Parameter description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| volume | int | Video volume level. Value range: 0–100 |

**Returned value description**

Unlimited


### setLiveMode

**Description**

This API is used to set the live streaming mode.

**API**

```dart
Future<void> setLiveMode(TXPlayerLiveMode mode) async;
```

**Parameter description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| mode | int | Live streaming mode, which can be set to auto, expedited, or smooth mode. |

**Returned value description**

Unlimited


### setAppID

**Description**

This API is used to set the `appID` for cloud-based control.

**API**

```dart
Future<void> setAppID(int appId) async;
```

**Parameter description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| appId | int | The application ID. |

**Returned value description**

Unlimited


### resumeLive

**Description**

This API is used to resume live playback from time-shifting playback.

**API**

```dart
Future<int> resumeLive() async;
```

**Parameter description**

Unlimited

**Returned value description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| result | int | Valid values: `1`: Success; `0`: Failure. |


### setConfig

**Description**

This API is used to configure the player.

**API**

```dart
Future<void> setConfig(FTXLivePlayConfig config) async;
```

**Parameter description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| config | FTXLivePlayConfig | For more information, see the `FTXLivePlayConfig` class. |

**Returned value description**

Unlimited


### enableHardwareDecode

**Description**

This API is used to enable/disable playback based on hardware decoding. After the value is set, it will not take effect until the video playback is restarted.

**API**

```dart
Future<bool> enableHardwareDecode(bool enable);
```

**Parameter description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| enable | bool | Whether to enable hardware decoding. |

**Returned value description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| result | bool | The hardware/software decoding setting result. |


### enterPictureInPictureMode

**Description**

This API is used to enter the PiP mode. It is applicable only to Android. Currently, live streaming on iOS doesn't support the PiP mode.

**API**

```dart
Future<int> enterPictureInPictureMode({String? backIconForAndroid, String? playIconForAndroid, String? pauseIconForAndroid, String? forwardIconForAndroid}) async;
```

**Parameter description**

The parameters are applicable only to Android.

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| backIcon | String | The seek backward icon, which can be up to 1 MB in size as limited by Android. It is optional, and if it is not set, the system icon will be used. |
| playIcon | String | The playback icon, which can be up to 1 MB in size as limited by Android. It is optional, and if it is not set, the system icon will be used. |
| pauseIcon | String | The pause icon, which can be up to 1 MB in size as limited by Android. It is optional, and if it is not set, the system icon will be used. |
| forwardIcon | String | The fast forward icon, which can be up to 1 MB in size as limited by Android. It is optional, and if it is not set, the system icon will be used. |

**Returned value description**

| Parameter | Code | Description |
| ------ | ------ | ------------------ |
| NO_ERROR | 0 | Started successfully with no errors. |
| ERROR_PIP_LOWER_VERSION | -101 | The Android version is too early and doesn't support the PiP mode. |
| ERROR_PIP_DENIED_PERMISSION | -102 | The PiP mode permission wasn't enabled, or the current device doesn't support PiP. |
| ERROR_PIP_ACTIVITY_DESTROYED | -103 | The current UI was terminated. |
| ERROR_IOS_PIP_DEVICE_NOT_SUPPORT | -104 | The device model or system version doesn't support PiP (only supported on iPadOS 9+ and iOS 14+). This error is applicable only to iOS. |
| ERROR_IOS_PIP_PLAYER_NOT_SUPPORT | -105 | The player doesn't support PiP. This error is applicable only to iOS. |
| ERROR_IOS_PIP_VIDEO_NOT_SUPPORT | -106 | The video doesn't support PiP. This error is applicable only to iOS. |
| ERROR_IOS_PIP_IS_NOT_POSSIBLE | -107 | The PiP controller was unavailable. This error is applicable only to iOS. |
| ERROR_IOS_PIP_FROM_SYSTEM | -108 | The PiP controller reported an error. This error is applicable only to iOS. |
| ERROR_IOS_PIP_PLAYER_NOT_EXIST | -109 | The player object doesn’t exist. This error is applicable only to iOS. |
| ERROR_IOS_PIP_IS_RUNNING | -110 | The PiP feature was running. This error is applicable only to iOS. |
| ERROR_IOS_PIP_NOT_RUNNING | -111 | The PiP feature didn't start. This error is applicable only to iOS. |


### dispose

**Description**

This API is used to terminate the controller. After it is called, all notification events will be terminated, and the player will be released.

**API**

```dart
void dispose() async;
```

**Parameter description**

Unlimited

**Returned value description**

Unlimited



### switchStream

**Description**

This API is used to switch the stream played back.

**API**

```dart
Future<int> switchStream(String url) async;
```

**Parameter description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| url | String | The video source to be switched to. |

**Returned value description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| result | int | The switch result. |


## `FTXLivePlayConfig` Class

#### Attribute configuration description

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| cacheTime | double | The player cache time in seconds. The value must be greater than `0`. Default value: `5`. |
| maxAutoAdjustCacheTime | double | The maximum time for automatic cache time adjustment in seconds. The value must be greater than `0`. Default value: `5`. |
| minAutoAdjustCacheTime | double | The minimum time for automatic cache time adjustment in seconds. The value must be greater than `0`. Default value: `1`. |
| videoBlockThreshold | int | The alarm threshold for player video lag in milliseconds. Only when the rendering interval exceeds this threshold, will the `PLAY_WARNING_VIDEO_PLAY_LAG` notification be sent. |
| connectRetryCount | int | The default number of times the SDK tries reconnecting when the player is disconnected. Value range: 1–10. Default value: `3` |
| connectRetryInterval | int | The interval between network reconnections in seconds. Value range: 3–30. Default value: `3` |
| autoAdjustCacheTime | bool | Whether to automatically adjust the player cache time. Default value: `true`. Valid values: `true`: Enable automatic adjustment. You can use `maxCacheTime` and `minCacheTime` to specify the maximum and minimum cache time respectively; `false`: Disable automatic adjustment and use the default cache time (1s). You can use `cacheTime` to change the cache time. |
| enableAec | bool | Whether to enable acoustic echo cancellation (AEC). Default value: `false`. |
| enableMessage | bool | Whether to enable the message channel. Default value: `true`. |
| enableMetaData | bool | Whether to enable the `MetaData` callback. Default value: `false`. Valid values: `true`: The SDK throws the `MetaData` of the video stream through the `EVT_PLAY_GET_METADATA` message; `false`: The SDK doesn't throw the `MetaData` of the video stream. |
| flvSessionKey | String | Whether to enable HTTP header information callback. Default value: `""` |
