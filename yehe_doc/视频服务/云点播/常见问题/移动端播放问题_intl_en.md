This document describes some common problems and their solutions for the Player SDKs for Android and iOS.

### What should I do when the "no v4 play info" error occurs?
- For playback through `FileId`, you need to first use the Adaptive-HLS(10) transcoding template to transcode the video or use the player signature `psign` to specify the video to be played back; otherwise, the video may fail to be played back.
- If you haven't enabled hotlink protection and a "no v4 play info" error occurs, transcode your video by using the Adaptive-HLS template (ID: 10) or get the playback URL of the video and play it by URL.

### How do I extract the Player logs to report an error?
The Player SDK outputs execution logs to local files. [Tencent Cloud technical support engineers](https://intl.cloud.tencent.com/document/product/266/19905) need them for problem analysis to help you locate the problem.

### How do I pull a Tencent Cloud media asset for playback?

For security considerations, there are currently no APIs for an application to directly pull a Tencent Cloud media asset. You need to pull a media asset in the following path: **application** > **application service backend** > **Tencent Cloud**. The backend service can call the [SearchMedia](https://intl.cloud.tencent.com/document/product/266/34179) API to get the media asset list.

## The SDK for Android

### What should I do if no images are displayed during playback?

Check whether `SurfaceView` or `TextureView` is bound to the `TXVodPlayer` object.

### How do I downsize the package?

- If you haven't used the [download cache feature](https://intl.cloud.tencent.com/document/product/266/47847) (an API in `TXVodDownloadManager`) of the SDK v9.4 or earlier and don't need to play back the downloaded files in the SDK v9.5 or later, you don't need to use the SO file of the feature, which helps reduce the size of the installation package. For example, if you have downloaded a cached file by using the `setDownloadPath` and `startDownloadUrl` functions of the `TXVodDownloadManager` class in the SDK v9.4 or earlier, and the `getPlayPath` path called back by `TXVodDownloadManager` is stored in the application for subsequent playback, you will need `libijkhlscache-master.so` to play back the file at the `getPlayPath` path; otherwise, you won't need it. You can add the following to `app/build.gradle`:
  ```xml
  packagingOptions{
      exclude "lib/armeabi/libijkhlscache-master.so"
      exclude "lib/armeabi-v7a/libijkhlscache-master.so"
      exclude "lib/arm64-v8a/libijkhlscache-master.so"
  }
  ```

- If your application is used only in the Chinese mainland, you can just package the SO files of the `armeabi-v7a` and `arm64-v8a` architectures or package only the JAR files and dynamically download the SO files after installation. For detailed directions, see [How to Downsize Installation Package](https://intl.cloud.tencent.com/document/product/647/35165).

### How do I make the console output fewer logs?

You can set `LogLevel` as follows to filter out unnecessary logs: TXLiveBase.setLogLevel(TXLiveConstants.LOG_LEVEL_DEBUG).

## The SDK for iOS

### What should I do if the playback control panel is not displayed?

The display of the playback control panel is controlled by `MPNowPlayingInfoCenter`. You can set the `nowPlayingInfo` attribute to update the title and image and set the volume level. For more information, see [LiteAVSDK/Player_iOS](https://github.com/LiteAVSDK/Player_ios).

### How do I make the console output fewer logs?

You can set `LogLevel` through the `setLogLevel` API in `TXLiveBase.h` as follows: [TXLiveBase setLogLevel:LOGLEVEL_DEBUG]. The greater the value, the fewer the output logs. The value ranges from 0 (output logs of all levels) to 6 (output no logs). For more information, see `TXLiveBase.h`.
