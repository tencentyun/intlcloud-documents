>? TUIKit 5.0.10 and later versions provide the TUIKit_live UI component, which supports the livestreaming feature based on Tencent Real-Time Communication (TRTC).

After importing TUIKit to your project, you can quickly enable the livestreaming feature in several simple steps. If you have not imported TUIKit, import `tuikit` and `tuiki-live` using the method in [Step 2: Import TUIKit](#step2).



<span id="step1"></span>
## Step 1: Enable the TRTC Service

1. Log in to the [IM console](https://console.cloud.tencent.com/im) and click the target application card to go to the basic configuration page of the application.
2. Click **Activate** under **Activate Tencent Real-Time Communication (TRTC)**.
3. Click **Confirm** in the dialog box that appears.
   A TRTC application with the same SDKAppID as the IM application is created in the [TRTC console](https://console.cloud.tencent.com/trtc/app). You can use the same account and authentication information for IM and TRTC.
   	
<span id="step2"></span>
## Step 2: Configure Project Files

We recommend that you use source code to integrate `tuikit` and `tuikit-live`. In this way, you can modify the source code to meet your business needs.
Copy the `tuikit` and `tuikit-live` code to your project, add `tuikit` and `tuikit-live module` to `settings.gradle`, and import dependencies to your project.

```
implementation project(':tuikit')
implementation project(':tuikit-live')
```
<span id="step3"></span>
## Step 3: Initialize and Log In to TUIKit

Import the SDKAppID generated in [Step 1](#Step1) to initialize TUIKit and call the `login` API to log in to TUIKit. For more information on how to generate UserSig, see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166).

```
TUIKitConfigs config = new ConfigHelper().getConfigs();
TUIKit.init(this, SDKAPPID, config);
TUIKit.login(userID, userSig, new IUIKitCallBack() {
    @Override
    public void onError(String module, final int code, final String desc) {
        // Login failed
    }

    @Override
    public void onSuccess(Object data) {
        // Login successful
    }
});
```
<span id="step4"></span>
## Step 4: Start Livestreaming at the Anchor End

Create an anchor. To start livestreaming at the anchor end, create `TUILiveRoomAnchorLayout` and set a unique roomid.

```java
TUILiveRoomAnchorLayout layoutTuiLiverRomAnchor = findViewById(R.id.tui_liveroom_anchor_layout);
// Callback for receiving successful anchor creation/exit
layoutTuiLiverRomAnchor.setLiveRoomAnchorLayoutDelegate(this);
// roomId: 123456. A viewer needs to set the same roomid as that at the anchor end to view the anchor's livestream. The roomid used here is only an example. The actual value must be unique.
layoutTuiLiverRomAnchor.initWithRoomId(getSupportFragmentManager(), 12345);
```

<span id="step5"></span>
## Step 5: View Livestreams at the Viewer End

Create a viewer. To view an anchor's livestream, create `TUILiveRoomAudienceLayout` and set the same roomid as that at the anchor end.

```java
TUILiveRoomAudienceLayout roomAudienceLayout = findViewById(R.id.layout_room_audience);
// Initialize the viewer page and set the same roomId as that at the anchor end to view the anchor's livestream. anchorId is the anchor ID.
// Set useCDN to false. If you need CDN for playback, refer to the following section.
roomAudienceLayout.initWithRoomId(getSupportFragmentManager(), 12345, “1280”, false, “”);
```

<span id="step6"></span>
## Step 6: Generate a Live Room List

After you create an anchor and a viewer, a live room list is required to associate them.

- After the anchor creates a room, record the room ID to the server end.
- After the anchor terminates the room, the server also terminates the room ID.
- The viewer gets the room ID list from the server and clicks it to enter the corresponding room.

Room lists can vary, and we do not provide an example of how to build a room list at the server end. You can see [`RoomManager`](https://github.com/tencentyun/TIMSDK/blob/master/Android/app/src/main/java/com/tencent/qcloud/tim/demo/scenes/net/RoomManager.java) in the demo to implement the logic by which the client reports the room creation result.

1. After the anchor is created, livestream enabled or disabled information is reported in the callback function at the anchor end.
```java
// TUILiveRoomAnchorLayoutDelegate
// Callback for successful room creation
public void onRoomCreate(final TRTCLiveRoomDef.TRTCLiveRoomInfo roomInfo) {
    // Reports successful live room creation
    RoomManager.getInstance().createRoom(roomInfo.roomId, RoomManager.TYPE_LIVE_ROOM, null);
} 

 // Callback for exiting/stopping livestreaming
public void onRoomDestroy(TRTCLiveRoomDef.TRTCLiveRoomInfo roomInfo) {
    // Terminating a room
    RoomManager.getInstance().destroyRoom(roomInfo.roomId, RoomManager.TYPE_LIVE_ROOM, null);
}
```
2. Create the live room list page UI.
The live room list page displays livestreams. For more information on the implementation, see `LiveRoomFragment.java` implementation in the demo.
3. Click a room to view.
On the live room list page, click a room. Create a viewer by referring to [Step 5: View Livestreams at the Viewer End](#step5) to view livestreams.

<span id="step7"></span>
## Step 7: Use LVB CDN to View Livestreams 

When TUILiveRoomAudienceLayout is created at the viewer end, TRTC is used to view livestreams by default if useCdn is set to false, and CDN is used to view livestreams if useCdn is set to true.

TRTC uses UDP to transmit audio and video data, and standard LVB CDN uses RTMP, HLS, FLV, or other protocols to transmit data. TRTC provides a shorter delay and smoother microphone on/off experience than LVB CDN. However, TRTC is more expensive than LVB CDN.

If you do not have high delay requirements, use CDN to view livestreams to reduce costs.

#### Prerequisites

You have activated Tencent Cloud [LVB](https://console.cloud.tencent.com/live). You need to configure a playback domain name for livestream playback according to the requirements of applicable authorities. For more information, please see [Adding Domain Name](https://intl.cloud.tencent.com/document/product/267/35970).

#### Enabling relayed push

1. Log in to the [TRTC console](https://console.cloud.tencent.com/trtc).
2. Select **Application Management** on the left sidebar and click **Feature Configuration** in the row of the target application.
3. In **Relayed Push Configuration**, click ![](https://main.qcloudimg.com/raw/5f58afe211aa033037e5c0b793023b49.png) to the right of **Enable Relayed Push**. In the **Enable Relayed Push** dialog box that appears, click **Confirm** to enable the feature.

#### Configuring a playback domain name

1. Log in to the [LVB console](https://console.cloud.tencent.com/live).
2. Click **Add Domain Name**, enter a playback domain name, select **Playback domain name** as the domain name type, select an acceleration region (which is **Mainland China** by default), and click **OK**.
3. Enter the playback URL when a viewer enters the room.
   After you enable relayed push, the anchor end automatically pushes livestreams to the cloud. When a viewer views the livestreams, you need to enter the URL from LVB CDN.

```
// eg: If you configure a playback domain name and set the domain name to my.com in CNAME, the default playback URL is http://[playback domain name]/live/[sdkappid]_[roomId]_[userID]_main.flv.
TUILiveRoomAudienceLayout roomAudienceLayout = findViewById(R.id.layout_room_audience);
roomAudienceLayout.initWithRoomId(getSupportFragmentManager(), 12345, "12565", true, "http://[playback domain name]/live/[sdkappid]_[roomId]_[userID]_main.flv");
```

>! For more information on TRTC relayed livestreaming, see [CDN Relayed Livestreaming](https://intl.cloud.tencent.com/document/product/647/35242) and [On-Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618).


## FAQ

### How can I customize gifts?

The TUIKit_live SDK allows users to customize gifts. To modify the gift content or source, modify the server request address or logic in the `DefaultGiftAdapterImp.java` file of TUIKit_live. Ensure that the returned data has the same format as the existing data.

```java
//eg data format. Complete reference link: https://liteav-test-1252463788.cos.ap-guangzhou.myqcloud.com/gift_data.json. The JSON character string content is as follows:
{
  "giftList": [
    {
      "giftId": "1", // Gift ID. Each gift has a unique ID.
      "giftImageUrl": "https://8.url.cn/huayang/resource/now/new_gift/1590482989_25.png", // Image displayed on the gift panel
      "lottieUrl": "https://assets5.lottiefiles.com/packages/lf20_t9v3tO.json", // Large gift animation file
      "price": 2989, // Price of a virtual gift
      "title": "rocket", // Gift title
      "type": 1 // Gift type. 1: large gift, displayed in full screen mode. 2: small gift, dynamically displayed on the top of the message list
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

1. Enable PK when TUILiveRoomAnchorLayout is created at the anchor end.
```java 
TUILiveRoomAnchorLayout layoutTuiLiverRomAnchor = findViewById(R.id.tui_liveroom_anchor_layout);
mLayoutTuiLiverRomAnchor.initWithRoomId(getSupportFragmentManager(), 12345);
// Enable PK.
layoutTuiLiverRomAnchor.enablePK(true);
layoutTuiLiverRomAnchor.setLiveRoomAnchorLayoutDelegate(this);
```
2. Set PK list data in the getRoomPKList callback of UILiveRoomAnchorLayout at the anchor end.
```java
public void getRoomPKList(final TUILiveRoomAnchorLayout.OnRoomListCallback callback) {
    /// If your room requires the PK feature, return the anchor's room ID array that supports PK through callback in this callback function.
    RoomManager.getInstance().getRoomList(RoomManager.TYPE_LIVE_ROOM, new RoomManager.GetRoomListCallback() {
        @Override
        public void onSuccess(List<String> roomIdList) {
            if (callback != null) {
                callback.onSuccess(roomIdList);
            }
        }

        @Override
        public void onCallback(int code, String msg) {
        }
    });}
```
