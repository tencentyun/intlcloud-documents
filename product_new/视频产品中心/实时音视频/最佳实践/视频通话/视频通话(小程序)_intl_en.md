This document describes how to use the most basic features of the Tencent Cloud TRTC SDK and helps you get started with the SDK.

## Preparations
Before using the basic features, please make sure that you have completed the following steps. For more information, please see [Demo Quick Start for WeChat Mini Program](https://intl.cloud.tencent.com/document/product/647/35123/35087) and [SDK Quick Integration for WeChat Mini Program](https://intl.cloud.tencent.com/document/product/647/35123/35098).
- Create a TRTC application, purchase a corresponding package, and get the `SDKAppid`.
- Get the private key file.
- Enable the category and push/pull tag permissions for WeChat Mini Program.
- Configure the domain name for the WeChat Mini Program server.
- Integrate the &lt;webrtc-room&gt; component into your WeChat Mini Program project.


## Deploying Signature Service
You need a signature service to distribute `userSig` when the component is initialized. For more information, please see [How to Generate UserSig](https://intl.cloud.tencent.com/document/product/647/35166).

## Integrating the &lt;webrtc-room&gt; Component
Follow the steps in [SDK Quick Integration for WeChat Mini Program](https://intl.cloud.tencent.com/document/product/647/35123/35096) to import the &lt;webrtc-room&gt; component into your WeChat Mini Program project. After that, you can manipulate the basic audio/video features in the following steps.

## Assembling Parameters
To use the &lt;webrtc-room&gt; component, you must prepare the following parameters:

- **sdkAppID**
Log in to the [TRTC Console](https://console.cloud.tencent.com/rav) and create an application to get the `SDKAPPID`:
![](https://main.qcloudimg.com/raw/92d980b7ed3b1b4eebd02019e8a48243.png)
>!`SDKAPPID` is a unique identifier used by the Tencent Cloud backend to distinguish between different TRTC applications, which is needed in the subsequent development process.


- **userID**
It can be specified arbitrarily. As it is of string type, it can be directly in line with your existing account system or be the `openid` of WeChat Mini Program; however, please note that **there should not be identical `userIDs` in the same audio/video room**.

- **userSig**
`userSig` can be calculated based on `sdkAppID` and `userID`. For the calculation method, please see [How to Generate UserSig](https://intl.cloud.tencent.com/document/product/647/35166).

- **roomID**
The room number is of numeric type and can be specified arbitrarily; however, please note that **different audio/video rooms in the same application cannot have the same `roomID`**.

- **template**
This identifies the UI template used by the component. The component has three built-in layouts: `bigsmall`, `float` (default value), and `grid`.

- **bindRoomEvent**
This listens on events returned by the &lt;webrtc-room&gt; component for easy troubleshooting.

With the above parameters ready, you can create (or enter) an audio/video room.

## Entering (or Creating) Room
After setting the attributes of the &lt;webrtc-room&gt; component, get the object instance of the &lt;webrtc-room&gt; component and call the `start()` method of the object instance to complete initialization and enter the room.

```
Page({
    // ...
    joinRoom: function (res) {
        this.setData({
            userID: res.data.userID, // [Required] user ID, which can be specified by your service or use `openid` of WeChat Mini Program
            sdkAppID: res.data.sdkAppID, // [Required] `sdkAppID` that will be assigned to a created application after TRTC is activated
            roomID: res.data.roomID, // [Required] room number, which can be specified by your service
            userSig: res.data.userSig, // [Required] identity signature, which needs to be obtained from a self-built signature service
            privateMapKey: '' // Generally optional
        }, function() {
            var webrtcroomCom = this.selectComponent('#webrtcroom');
            if (webrtcroomCom) {
                webrtcroomCom.start();
            }
            
        })
    },
    // ...
})
```

## Enabling (or Disabling) Local Sound Capture
Modify the component attribute `muted` to enable/disable local sound capture.
```
Page({
    // ...
    changeMute: function (isMuteMute) {
        this.data.muted = isMuteMute; // true or false
        this.setData({
            muted: this.data.muted
        });
    },
    // ...
})
```

## Enabling (or Disabling) Local Video Capture
Modify the component attribute `enableCamera` to enable/disable local video capture.
```
Page({
    // ...
    enableCamera: function (isEnableCamera) {
        this.data.enableCamera = isEnableCamera; // true or false
        this.setData({
            enableCamera: this.data.enableCamera
        });
    },
    // ...
})
```

## Switching Cameras
Call the component instance method `switchCamera()` to switch cameras.
```
Page({
    // ...
    changeCamera: function () {
        this.data.webrtcroomComponent.switchCamera();
    },
    // ...
})
```

## Exiting Room
Call the component instance method `stop()` to exit the room.
```
Page({
    // ...
    exitRoom: function () {
        this.data.webrtcroomComponent.stop();
    },
    // ...
})
```

## UI Customization
The &lt;webrtc-room&gt; component supports customizing the placement layout of multiple video images. If the existing template does not meet your needs, please follow the steps below for customization.

- Step 1. Create the `/pages/templates/mytemplate` folder and create `mytemplate.wxml` and `mytemplate.wxss` files.
- Step 2. Write `mytemplate.wxml` and `mytemplate.wxss` files.

```
//mytemplate.wxml
<template name='mytemplate'>
    <view class='videoview'>
        <view class="pusher-box">
            <live-pusher
                id="rtcpusher"
                autopush
                mode="RTC"
                url="{{pushURL}}"
                aspect="{{aspect}}"
                min-bitrate="{{minBitrate}}"
                max-bitrate="{{maxBitrate}}"
                audio-quality="high"
                beauty="{{beauty}}"
                muted="{{muted}}"
                waiting-image="https://mc.qcloudimg.com/static/img/daeed8616ac5df256c0591c22a65c4d3/pause_publish.jpg"
                background-mute="{{true}}"
                debug="{{debug}}"
                bindstatechange="onPush"
                binderror="onError">
                <cover-image  class='character' src="/pages/Resources/mask.png"></cover-image>
                <cover-view class='character' style='padding: 0 5px;'>Me</cover-view>
            </live-pusher>
        </view>
        <view class="player-box" wx:for="{{members}}" wx:key="userID">
            <view class='poster'>
                <cover-image class='set' src="https://miniprogram-1252463788.file.myqcloud.com/roomset_{{index + 2}}.png">
                </cover-image>
            </view>
            <live-player
                id="{{item.userID}}"
                autoplay
                mode="RTC"
                wx:if="{{item.accelerateURL}}"
                object-fit="fillCrop"
                min-cache="0.1"
                max-cache="0.3"
                src="{{item.accelerateURL}}"
                debug="{{debug}}"
                background-mute="{{true}}"
                bindstatechange="onPlay">
                <cover-view class='loading' wx:if="{{item.loading}}">
                    <cover-image src="/pages/Resources/loading_image0.png"></cover-image>
                </cover-view>
                <cover-image  class='character' src="/pages/Resources/mask.png"></cover-image>
                <cover-view class='character' style='padding: 0 5px;'>{{item.userName}}</cover-view>
            </live-player>
        </view>
    </view>
</template>
```  

```
//mytemplate.wxss
.videoview {
    background-repeat:no-repeat;
    background-size: cover;
    width: 100%;
    height: 100%;
}
```

- Step 3. Import the template into the &lt;webrtc-room&gt; component.

```
// Add a custom template to the `webrtcroom.wxml` file of the <webrtc-room> component
<import src='/pages/templates/mytemplate/mytemplate.wxml'/>
<view class='conponent-box'>
    <view styles="width:100%;height=100%;" wx:if="{{template=='1v3'}}">
        <template is='mytemplate' data="{{pushURL, aspect,
                      minBitrate, maxBitrate, beauty, muted, debug, members}}"/>
    </view>
</view>

// Add a custom style to the webrtcroom.wxss file in the `<webrtc-room>` component
@import "../templates/mytemplate/mytemplate.wxss";
```

>! In the current version, the compatibility of the &lt;live-pusher&gt; and &lt;live-player&gt; tags with WeChat Mini Program's view rendering system is not perfect, and there are still quite a lot of bugs in the `zOrder` control. We are working with the WeChat team to fix them.
