`TUIKit` `5.0.10` and later versions support the live room feature and interconnection between the iOS and Android platforms. To implement the live room feature, you need to integrate the `TUIKitLive` component as well by referring to [Step 2](#step2).


## Step 1: Activate the TRTC Service[](id:step1)

1. Log in to the [IM console](https://console.cloud.tencent.com/im) and click the target app card to go to the basic configuration page of the app.
2. Click **Activate** under **Activate Tencent Real-Time Communication (TRTC)**.
3. Click **Confirm** in the pop-up dialog box.
>?A TRTC app with the same SDKAppID as the IM app will be created in the [TRTC console](https://console.cloud.tencent.com/trtc). You can use the same account and authentication information for IM and TRTC.


## Step 2: Configure Project Files[](id:step2)

You are advised to use the source code to integrate `tuikit` and `tuikit-live`. In this way, you can modify the source code to meet your business needs.
Copy the `tuikit` and `tuikit-live` code to your project, add `tuikit` and `tuikit-live module` to `settings.gradle`, and import dependencies to your project.

```groovy
implementation project(':tuikit')
implementation project(':tuikit-live')
```

## Step 3: Initialize and Log In to TUIKit[](id:step3)

Pass in the SDKAppID generated in [Step 1](#Step1) to initialize `TUIKit` and call `login` to log in to TUIKit. For more information on how to generate UserSig, see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166).

```java
TUIKitConfigs config = new ConfigHelper().getConfigs();
TUIKit.init(this, SDKAPPID, config);
TUIKit.login(userID, userSig, new IUIKitCallBack() {
    @Override
    public void onError(String module, final int code, final String desc) {
        // Login failed
    }

    @Override
    public void onSuccess(Object data) {
        // Login succeeded
    }
});
```

## Step 4: Start Live Streaming at the Anchor End[](id:step4)

Create an anchor. To start live streaming at the anchor end, create `TUILiveRoomAnchorLayout` and set a unique `roomId`.

```java
TUILiveRoomAnchorLayout layoutTuiLiverRomAnchor = findViewById(R.id.tui_liveroom_anchor_layout);
// Receive the callback for successful anchor creation/exit.
layoutTuiLiverRomAnchor.setLiveRoomAnchorLayoutDelegate(this);
// `roomId`: 123456. A viewer needs to set the same `roomId` as that at the anchor end to view the anchor's live streams. The `roomId` used here is only an example. The actual value must be unique.
layoutTuiLiverRomAnchor.initWithRoomId(getSupportFragmentManager(), 12345);
```

## Step 5: View Live Streams at the Viewer End[](id:step5)

Create a viewer. To view an anchor's live streams, create `TUILiveRoomAudienceLayout` and set the same `roomId` as that at the anchor end.

```java
TUILiveRoomAudienceLayout roomAudienceLayout = findViewById(R.id.layout_room_audience);
// Initialize the viewer page and set the same `roomId` as that at the anchor end to view the anchor's live streams. `anchorId` is the anchor ID.
// Set `useCDN` to `false`. If you need CDN for playback, refer to the following section.
roomAudienceLayout.initWithRoomId(getSupportFragmentManager(), 12345, "1280", false, "");
```

## Step 6: Implement Live Rooms[](id:step6)

After you create an anchor and a viewer, a live room list is required to associate them.

- After the anchor creates a room, record the room ID to the server end.
- After the anchor terminates the room, the server also terminates the room ID.
- The viewer gets the room ID list from the server and clicks a room ID to enter the corresponding room.

Room lists can vary, and we do not provide an example of how to build a room list at the server end. You can see [`RoomManager`](https://github.com/tencentyun/TIMSDK/blob/master/Android/Demo/app/src/main/java/com/tencent/qcloud/tim/demo/scenes/net/RoomManager.java) in the demo to implement the logic by which the client reports the room list.

1. After the anchor is created, live streaming started or stopped information is reported in the callback function at the anchor end.
```java
// TUILiveRoomAnchorLayoutDelegate
// Callback for successful room creation
public void onRoomCreate(final TRTCLiveRoomDef.TRTCLiveRoomInfo roomInfo) {
    // Report successful live room creation.
    RoomManager.getInstance().createRoom(roomInfo.roomId, RoomManager.TYPE_LIVE_ROOM, null);
} 

 // Callback for exiting/stopping live streaming
public void onRoomDestroy(TRTCLiveRoomDef.TRTCLiveRoomInfo roomInfo) {
    // Terminate a room.
    RoomManager.getInstance().destroyRoom(roomInfo.roomId, RoomManager.TYPE_LIVE_ROOM, null);
}
```
2. Create the live room page UI.
The live room page displays the live stream list. For more information on the implementation, see `LiveRoomFragment.java` implementation in the demo.
3. Click a room to view.
Click a room on the live room page. Create a viewer by referring to [Step 5. View Live Streams at the Viewer End](#step5) to view live streams.

## Step 7: Use LVB CDN to View Live Streams[](id:step7)

When `TUILiveRoomAudienceLayout` is created at the viewer end, TRTC is used to view live streams by default if `useCdn` is set to `false`, and CDN is used to view live streams if `useCdn` is set to `true` and `cdnDomain` is set.

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
3. Enter the playback URL when a viewer enters the room.
   After you enable relayed push, the anchor end automatically pushes live streams to the cloud. When a viewer views the live streams, you need to enter the URL from LVB CDN.

```
// For example, if you configure a playback domain and set the domain to `my.com` in CNAME, the default playback URL is http://[playback domain name]/live/[sdkappid]_[roomId]_[userID]_main.flv.
TUILiveRoomAudienceLayout roomAudienceLayout = findViewById(R.id.layout_room_audience);
roomAudienceLayout.initWithRoomId(getSupportFragmentManager(), 12345, "12565", true, "http://[playback domain]/live/[sdkappid]_[roomId]_[userID]_main.flv");
```

>! For more information on TRTC relayed live streaming, see [CDN Relayed Live Streaming](https://intl.cloud.tencent.com/document/product/647/35242) and [On-Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618).


## FAQs

### How can I customize gifts?

The TUIKit_live SDK allows users to customize gifts. To modify the gift content or source, modify the server request address or logic in the `DefaultGiftAdapterImp.java` file of TUIKit_live. Ensure that the returned data has the same format as the existing data.

```java
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

1. Enable PK when creating `TUILiveRoomAnchorLayout` at the anchor end.
```java 
TUILiveRoomAnchorLayout layoutTuiLiverRomAnchor = findViewById(R.id.tui_liveroom_anchor_layout);
mLayoutTuiLiverRomAnchor.initWithRoomId(getSupportFragmentManager(), 12345);
// Enable PK.
layoutTuiLiverRomAnchor.enablePK(true);
layoutTuiLiverRomAnchor.setLiveRoomAnchorLayoutDelegate(this);
```
2. Set PK list data in the `getRoomPKList` callback of `UILiveRoomAnchorLayout` at the anchor end.
```java
public void getRoomPKList(final TUILiveRoomAnchorLayout.OnRoomListCallback callback) {
    /// If the rooms you create require the PK feature, return the anchor's room ID array that supports PK through callback in this callback.
    RoomManager.getInstance().getRoomList(RoomManager.TYPE_LIVE_ROOM, new RoomManager.GetRoomListCallback() {
        @Override
        public void onSuccess(List<String> roomIdList) {
            if (callback != null) {
                callback.onSuccess(roomIdList);
            }
        }

        @Override
        public void onFailed(int code, String msg) {
        }
    });}
```
