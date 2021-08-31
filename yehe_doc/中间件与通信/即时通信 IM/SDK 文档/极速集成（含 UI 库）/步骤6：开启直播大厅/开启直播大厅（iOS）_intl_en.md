TUIKit 5.0.10 and later versions support the live room feature and interconnection between the iOS and Android platforms. To implement the live room feature, you need to [integrate the TUIKitLive component](#step2) as well.

[](id:step1)
## Step 1: Activate the TRTC Service

1. Log in to the [IM console](https://console.cloud.tencent.com/im) and click the target app card to go to the basic configuration page of the app.
2. Click **Activate** under **Activate Tencent Real-Time Communication (TRTC)**.
3. Click **Confirm** in the pop-up dialog box.

   >? A TRTC app with the same SDKAppID as the IM app will be created in the [TRTC console](https://console.cloud.tencent.com/trtc). You can use the same account and authentication information for IM and TRTC.

[](id:step2)
## Step 2: Integrate TUIKitLive

1. Add the following content to the podfile file.
 ```
pod 'TXIMSDK_TUIKit_live_iOS'                // By default, the audio and video library of the TXLiteAVSDK_TRTC version is integrated.
// pod 'TXIMSDK_TUIKit_live_iOS_Professional' // By default, the audio and video library of the TXLiteAVSDK_Professional version is integrated.
 ```
Do not integrate different Tencent Cloud [audio and video libraries](https://intl.cloud.tencent.com/document/product/647/34615) at the same time to avoid symbol conflicts. If you use a library not of the [TRTC](https://intl.cloud.tencent.com/document/product/647/34615#TRTC) version, we recommend that you remove it and integrate the `TXIMSDK_TUIKit_iOS_Professional` version. The audio and video library of the [LiteAV_Professional](https://intl.cloud.tencent.com/document/product/647/34615#.E4.B8.93.E4.B8.9A.E7.89.88.EF.BC.88professional.EF.BC.89) version contains all basic audio and video capabilities.

[](id:step3)
## Step 3: Initialize and Log In to TUIKit

Pass in the SDKAppID generated in [Step 1](#step1) to initialize TUIKit and call `login` to log in to TUIKit. For more information on how to generate UserSig, see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166).

```
[[TUIKit sharedInstance] setupWithAppId:SDKAppID];
[[TUIKit sharedInstance] login:@"userID" userSig:@"userSig" succ:^{
     NSLog(@"-----> login succeeds");
} fail:^(int code, NSString *msg) {
     NSLog(@"-----> login fails");
}];
```

[](id:step4)
## Step 4: Start Live Streaming at the Anchor End

Create an anchor. To start live streaming at the anchor end, create `TUILiveRoomAnchorViewController` and set a unique `roomId`.

```objectivec
#import "TUIKitLive.h"
/// roomId: 123456. A viewer needs to set the same `roomId` as that at the anchor end to view the anchor's live streams. The `roomId` used here is only an example. The actual value must be unique.
TUILiveRoomAnchorViewController *anchorVC = 
[[TUILiveRoomAnchorViewController alloc] initWithRoomId:123456];
/// Receive the callback for successful anchor creation/exit.
anchorVC.delegate =  self ; 
[anchorVC eanblePK: NO];
/// `push/present` displays `viewController` on the anchor page.
[self.navigationController pushViewController:anchorVC animated: YES];
```

[](id:step5)
## Step 5: View Live Streams at the Viewer End

Create a viewer. To view an anchor's live streams, create `TUILiveRoomAudienceViewController` and set the same `roomId` as that at the anchor end.

```objectivec
#import "TUIKitLive.h"
/// Initialize the viewer page and set the same `roomId` as that at the anchor end to view the anchor's live streams.
/// Set `useCDN` to `NO`. If you need CDN for playback, refer to the following section.
/// `anchorId` is the `userId` of the anchor in the live room. It is optional. However, we recommend that you set it.
/// `cdnUrl` is the CDN playback address, for example, http://[playback domain]/live/[sdkappid]_[roomId]_[userID]_main.flv.
TUILiveRoomAudienceViewController *audienceVC =
[[TUILiveRoomAudienceViewController alloc] initWithRoomId:123456
						 anchorId:nil
						   useCdn:NO
						   cdnUrl:@""];
/// `push/present` displays `viewController` on the viewer page based on project requirements.
[self.navigationController pushViewController:anchorVC animated: YES];
```

[](id:step6)
## Step 6: Implement Live Rooms

After you create an anchor and a viewer, a live room list is required to associate them.
- After the anchor creates a room, record the room ID to the backend.
- After the anchor terminates the room, the backend also terminates the room ID.
- The viewer gets the room ID list from the backend and clicks a room ID to enter the corresponding room.

Room lists can vary, and we do not provide an example of how to build a room list at the backend. You can see [`TUILiveRoomManager`](https://github.com/tencentyun/TIMSDK/blob/master/iOS/TUIKitDemo/TUIKitDemo/Scenes/Data/TUILiveRoomManager.m) in the demo to implement the logic by which the client reports the room list.

1. After the anchor is created, live streaming started or stopped information is reported in the callback function at the anchor end.

```objectivec
#pragma mark  - TUILiveRoomAnchorDelegate**
/// Callback for successful room creation
- (void)onRoomCreate:(TRTCLiveRoomInfo *roomInfo) {
    NSSTring *roomId = roomInfo.roomId;
	/// Report successful live room creation.
	[TUILiveRoomManager.sharedManager createRoom:sdkAppId 
						type:@"liveRoom" 
					     success:nil
					      failed:nil];
}

/// Callback for exiting/stopping live streaming
- (void)onRoomDestroy:(TRTCLiveRoomInfo *roomInfo) {
    NSSTring *roomId = roomInfo.roomId;
	/// Report live room termination.
  [TUILiveRoomManager.sharedManager destroyRoom:sdkAppId 
   					   type:@"liveRoom"
					success:nil 
					 failed:nil];
}
```

2. Create the live room page UI.
   The live room page displays the live stream list. For more information on the implementation, see `TUILiveRoomListViewController` implementation in the demo.
3. Click a room to view.
   Click a room on the live room page. Create a viewer by referring to [Step 4: View Live Streams at the Viewer End](#step4) to view live streams.

[](id:step7)
## Step 7: Use LVB CDN to View Live Streams

When `TUILiveRoomAudienceViewController` is created at the viewer end, TRTC is used to view live streams by default if `useCdn` is set to `NO`, and CDN is used to view live streams if `useCdn` is set to `YES` and `cdnUrl` is set.

TRTC uses UDP to transmit audio and video data, and LVB CDN uses RTMP, HLS, FLV, or other protocols to transmit data. TRTC provides a shorter delay and smoother microphone on/off experience than LVB CDN. However, TRTC is more expensive than LVB CDN.

If you do not have high delay requirements, use CDN to view live streams to reduce costs.

#### Prerequisites
  You have activated Tencent Cloud [CSS](https://console.cloud.tencent.com/live). You need to configure a playback domain for live playback according to the requirements of applicable authorities. For detailed directions, please see [Adding Domain Name](https://intl.cloud.tencent.com/document/product/267/35970).

#### Enabling relayed push
1. Log in to the [TRTC console](https://console.cloud.tencent.com/trtc).
2. Select **Application Management** on the left sidebar and click **Feature Configuration** on the row of the target app.
3. In **Relayed Push Configuration**, click ![](https://main.qcloudimg.com/raw/5f58afe211aa033037e5c0b793023b49.png) next to **Enable Relayed Push**, and click **Enable Relayed Push** in the dialog box that pops up.

#### Configuring a playback domain
  1. Log in to the [CSS console](https://console.cloud.tencent.com/live/).
  2. Click **Add Domain**, enter a playback domain for which you have already obtained the ICP filing, select **Playback Domain** as its type, select an acceleration region (which is **Chinese mainland** by default), and click **Confirm**.

#### Entering the playback URL when a viewer enters the room
After you enable relayed push, the anchor end automatically pushes live streams to the cloud. When a viewer views the live streams, you need to enter the URL from LVB CDN.
```
/// For example, if you configure a playback domain and set the domain to `my.com` in CNAME, the default playback URL is http://[playback domain name]/live/[sdkAppId]_[roomId]_[userId]_main.flv.
/// 
TUILiveRoomAudienceViewController *audienceVC = 
[[TUILiveRoomAudienceViewController alloc] initWithRoomId:123456 
						 anchorId:nil 
						   useCdn:YES 
						   cdnUrl:@"http://[playback domain name]/live/[sdkAppId]_[roomId]_[userId]_main.flv"];
```

>! For more information on TRTC relayed live streaming, see [CDN Relayed Live streaming](https://intl.cloud.tencent.com/document/product/647/35242) and [On-Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618).


## FAQs

### What can I do if no image is displayed after the anchor enables live streaming?

Live streaming requires a camera and microphone. You need to apply for camera and microphone use permissions from users.
Use Xcode to open your project. Click the project file, select the target, click the **Info** tab, and add `NSCameraUsageDescription` and `NSMicrophoneUsageDescription`.
![](https://main.qcloudimg.com/raw/3314513111612f40463882b8eea2e9d6.png)
After the project runs on your mobile phone, choose **Settings** -> **Privacy** -> **Camera and Microphone** and assign permissions to the app.

### How can I customize gifts?

The TUIKit_live SDK allows users to customize gifts. To modify the gift content or source, modify the server request address or logic in the `TUILiveDefaultGiftAdapterImp.m` file of TUIKit_live. Ensure that the returned data has the same format as the existing data.

```objectivec
// eg data format. Complete reference link: https://liteav-test-1252463788.cos.ap-guangzhou.myqcloud.com/gift_data.json. The JSON string content is as follows:
{
  "giftList": [
    {
      "giftId": "1", // Gift ID. Each gift has a unique ID.
      "giftImageUrl": "https://8.url.cn/huayang/resource/now/new_gift/1590482989_25.png", // Image displayed on the gift panel
      "lottieUrl": "https://assets5.lottiefiles.com/packages/lf20_t9v3tO.json", // Large gift animation file
      "price": 2989, // Price of a virtual gift
      "title": "rocket", // Gift title
      "type": 1 // Gift type. `1`: large gift, displayed in full screen mode. `2`: small gift, dynamically displayed on the top of the message list.
    },
    {
      "giftId": "2",
      "giftImageUrl": "https://8.url.cn/huayang/resource/now/new_gift/1507876726_3",
      "lottieUrl": "",
      "price": 298,
      "title": "egg",
      "type": 0
    }
}
```

### How do I implement PK?

To implement the PK feature, perform the following steps:

1. Enable PK when creating `TUILiveRoomAnchorViewController` at the anchor end.

```objectivec 
TUILiveRoomAnchorViewController *anchorVC = 
[[TUILiveRoomAnchorViewController alloc] initWithRoomId:123456];
anchorVC.delegate = self;
/// Enable PK.
[anchorVC eanblePK: YES];
```

2. Set PK list data in the `getPKRoomIDList:` callback of `TUILiveRoomAnchorViewController` at the anchor end.

```objectivec
- (void)getPKRoomIDList:(TUILiveOnRoomListCallback)callback {
	/// If the rooms you create require the PK feature, return the anchor's room ID array that supports PK through callback in this callback.
   	callback(@[@"12345", @"123456"]);
}
```





