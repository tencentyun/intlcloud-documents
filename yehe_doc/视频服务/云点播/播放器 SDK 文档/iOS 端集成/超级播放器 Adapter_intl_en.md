## Overview

Tencent Cloud RT-Cube Superplayer Adapter for iOS is a player plugin provided by VOD for customers who want to use a third-party or proprietary player to connect to Tencent Cloud PaaS resources. It is generally used by customers who strongly need to customize player features.

[](id:sdkDownload)
## SDK Download

The Tencent Cloud RT-Cube Superplayer Adapter SDK and demo for iOS can be downloaded [here](https://mediacloud-76607.gzc.vod.tencent-cloud.com/TXCPlayerAdapter/Release/1.0.0/TXCPlayerAdapterSDK_1.0.0_iOS.zip). 

## Target Audience

This document describes Tencent Cloud's proprietary capabilities. Please make sure that you have activated the relevant [Tencent Cloud](https://intl.cloud.tencent.com) services before reading it. If you haven't registered an account, please [sign up for free trial](https://intl.cloud.tencent.com/login) first.

[](id:guide)
## Integration Guide

### Environment requirements

To configure the support for HTTP requests, you need to set `App Transport Security Settings->Allow Arbitrary Loads` to `YES` in the `info.plist` file of your project.

### Component dependency

Add the `GCDWebServer` component dependency.   

```objective-c
pod "GCDWebServer", "~> 3.0"
```

GCDWebServer is a lightweight HTTP server based on GCD and can be used for OS X and iOS. This library also implements extended features such as web-based file upload and WebDAV server.

### Using player

Declare the variables and then create an instance. The main class of the player is `TXCPlayerAdapter`, and videos can be played back after it is created.

A `fileId` is usually returned by the server after the video is uploaded:

1. After the video is published on the client, the server will return a `fileId` to the client.
2. When the video is uploaded to the server, the corresponding `fileId` will be included in the notification of upload confirmation.


If the file already exists in Tencent Cloud, you can go to [Media Assets](https://console.cloud.tencent.com/vod/media) and find it. After clicking it, you can view relevant parameters in the video details on the right.

```objective-c
NSInteger appId; //// `appid` can be applied for in Tencent Cloud VOD
NSString *fileId;
// `psign` is a signature for superplayer. For more information on the signature and how to generate it, please visit https://intl.cloud.tencent.com/document/product/266/38099
NSString *pSign = self.pSignTextView.text;
    
TXCPlayerAdapter *adapter = [TXCPlayerAdapter shareAdapterWithAppId:appId];
```

Request the video information and play back the video:

```objective-c
id<ITXCPlayerAssistorProtocol> assistor = [TXCPlayerAdapter createPlayerAssistorWithFileId:fileId pSign:pSign];
[assistor requestVideoInfo:^(id<ITXCPlayerAssistorProtocol> response, NSError *error) {
    if (error) {
        NSLog(@"create player assistor error : %@",error);
        [self.view makeToast:error.description duration:5.0 position:CSToastPositionBottom];
        return;
    }
    [weakSelf avplayerPlay:response]; // Play back the video
}];



- (void)avplayerPlay:(id<ITXCPlayerAssistorProtocol>)response
{
    AVPlayerViewController *playerVC = [[AVPlayerViewController alloc] init];
    self.playerVC = playerVC;
    TXCStreamingInfo *info = response.getStreamingInfo;
    AVPlayer *player = [[AVPlayer alloc] initWithURL:[NSURL URLWithString:info.playUrl]];
    playerVC.player = player;
    playerVC.title = response.getVideoBasicInfo.name;
    [self.navigationController pushViewController:playerVC animated:YES];
    
    [player addObserver:self forKeyPath:@"status" options:NSKeyValueObservingOptionNew context:nil];
}
```

Terminate the player after use:

```objective-c
[TXCPlayerAdapter destroy];
```



## SDK API Description

### Initializing Adapter
This API is used to initialize an Adapter singleton.

**API**

```
+ (instancetype)shareAdapterWithAppId:(NSUInteger)appId;
```

**Parameter description**

appId: enter the `appid` (if a subapplication is used, enter the `subappid`). |

### Terminating Adapter
This API is used to terminate Adapter. It can be called after the program exits.

**API**

```
+ (void)destroy;
```

### Creating the auxiliary class of player

An auxiliary class of the player can be used to get the playback `fileId` and process DRM encryption APIs.

**API**

```
+ (id<ITXCPlayerAssistorProtocol>)createPlayerAssistorWithFileId:(NSString *)fileId
                                                           pSign:(NSString *)pSign;
```

**Parameter description**

| Parameter | Type | Description |
| :----- | :----- | :----------------- |
| fileId    | String                | `fileId` of the video to be played back                               |
| pSign     | String                | Superplayer signature                                   |

### Requesting video playback information

This API is used to request the stream information of the video to be played back from the Tencent Cloud VOD server.

**API**

```objective-c
- (void)requestVideoInfo:(ITXCRequestVideoInfoCallback)completion;
```

**Parameter description**

| Parameter | Type | Description |
| :------------- | :--------------------------- | :----------- |
| completion | ITXCRequestVideoInfoCallback | Async callback function |



### Terminating the auxiliary class of player

This API is used to terminate an auxiliary class. You can call it when exiting the player or switching to the next video for playback.

**API**

```
+ (void)destroyPlayerAssistor:(id<ITXCPlayerAssistorProtocol>)assistor;
```



### Getting basic video information

This API is used to get the video information and will take effect only after `id<ITXCPlayerAssistorProtocol>.requestVideoInfo` is called back.

**API**

```
- (TXCVideoBasicInfo *)getVideoBasicInfo;
```

**Parameter description**

The parameters of `TXCVideoBasicInfo` are as follows:

| Parameter | Type | Description |
| :---------- | :----- | :------------------- |
| name | String | Video name |
| size | Int | Video size in bytes |
| duration | Float | Video duration in seconds |
| description | String | Video description |
| coverUrl | String | Video cover |



### Getting video stream information

This API is used to get the video stream information list and will take effect only after `id<ITXCPlayerAssistorProtocol>.requestVideoInfo` is called back.

**API**

```
- (TXCStreamingInfo *)getStreamingInfo;
```

**Parameter description**

The parameters of `TXCStreamingInfo` are as follows:

| Parameter | Type | Description |
| :--------- | :----- | :----------------------------------------------------------- |
| playUrl | String | Playback URL |
| subStreams | List | Adaptive bitstream substream information of the `[TXCSubStreamInfo]`(#TXCSubStreamInfo) type |

The parameters of `TXCSubStreamInfo` are as follows:[](id:TXCSubStreamInfo)

| Parameter | Type | Description |
| :------------- | :----- | :----------------------------------- |
| type | String | Substream type. Valid values: `video` |
| width | Int | Substream video width in px |
| height | Int | Substream video height in px |
| resolutionName | String | Specification name of the substream video displayed in the player |

### Getting keyframe timestamp information

This API is used to get the video keyframe timestamp information and will take effect only after `id<ITXCPlayerAssistorProtocol>.requestVideoInfo` is called back.

**API**

```
- (NSArray<TXCKeyFrameDescInfo *> *)getKeyFrameDescInfos;
```

**Parameter description**

The parameters of `TXCKeyFrameDescInfo` are as follows:

| Parameter | Type | Description |
| :--------- | :----- | :------------ |
| timeOffset | Float  | 1.1           |
| content    | String | "Beginning now..." |



### Getting thumbnail information

This API is used to get the thumbnail information and will take effect only after `id<ITXCPlayerAssistorProtocol>.requestVideoInfo` is called back.

**API**

```
- (TXCImageSpriteInfo *)getImageSpriteInfo;
```

**Parameter description**

The parameters of `TCXImageSpriteInfo` are as follows:

| Parameter | Type | Description |
| :-------- | :----- | :--------------------------------- |
| imageUrls | List | Array of thumbnail download URLs of `String` type |
| webVttUrl | String | Thumbnail VTT file download URL |
