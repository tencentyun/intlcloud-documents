This document describes how to quickly integrate the Tencent Cloud TRTC SDK for WeChat Mini Program into your project in the following steps.


## Preparations
Before integrating the SDK for WeChat Mini Program, please make sure that you have completed the following steps. For more information, please see [Running the Demo for WeChat Mini Program](https://intl.cloud.tencent.com/document/product/647/35123/35087).
- Create a TRTC application, purchase a corresponding package, and get the `SDKAppid`.
- Get the private key file.
- Enable the category and push/pull tag permissions for WeChat Mini Program.
- Configure the domain name for the WeChat Mini Program server.

## Development Environment Requirements
- The latest version of the WeChat Web Developer Tool.
- Minimum version of the WeChat Mini Program base library: 1.7.0.
- Minimum version of the WeChat app on iOS: 6.5.21.
- Minimum version of the WeChat app on Android: 6.5.19.

## Downloading Component Source Code
You can download the SDK source code package directly from [GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/WXMini) or through `git clone`:
```
$ cd YOUR_PATH
$ git clone https://github.com/tencentyun/TRTCSDK.git
```
The source code of the &lt;webrtc-room&gt; component is contained in the `TRTCSDK/WXMini/pages/components` directory. The &lt;webrtc-room&gt; tag is a WeChat Mini Program component for video call implemented based on &lt;live-pusher&gt; and &lt;live-player&gt;.

The file list of the &lt;webrtc-room&gt; component is as follows:

| Directory | Description | 
|:-------:|---------|
| bigsmalltemplate | 1v1 big/small image layout template | 
| floattemplate | Nested layout template | 
| gridtemplate | Grid layout template | 
| config.js | Constant configuration | 
| webim_wx.js | WEBIM SDK for WeChat Mini Program | 
| im_handler.js | WEBIM controller | 
| webrtc-room.js | webrtc-room component's main program file | 
| webrtc-room.json | webrtc-room component's declaration file | 
| webrtc-room.wxml | webrtc-room component's template file | 
| webrtc-room.wxss | webrtc-room component's style file | 

## Integrating Components
- Copy the `webrtc-room` folder to the `components` directory of your WeChat Mini Program project (create the `components` directory if it does not exist).
- Add the following code to the `Page.json` file. `usingComponents` is used to import the &lt;webrtc-room&gt; component.
```
// Page.json file
{
  "navigationBarTitleText": "Video call",
  "usingComponents": {
    "webrtc-room": "/pages/components/webrtc-room/webrtc-room"
  }
}
```
- Add the following code to the `Page.wxml` file, which is used to create a &lt;webrtc-room&gt; component named "myroom".
```
// Page.wxml file
<webrtc-room id="myroom"
    roomID="{{roomID}}"
    userID="{{userID}}"
    userSig="{{userSig}}"
    sdkAppID="{{sdkAppID}}"
    privateMapKey="{{privateMapKey}}"
    template="{{template}}"
    beauty="{{beauty}}"
    muted="{{muted}}"
    debug="{{debug}}"
    bindRoomEvent="onRoomEvent"
    enableIM="{{enableIM}}"
    bindIMEvent="onIMEvent">
</webrtc-room>
```
- Add the following code to the `Page.js` file, which is used to manipulate the &lt;webrtc-room&gt; component.
```
// Page.js file
Page({
    data: {
        //...
        roomID: '', // [Required] room number, which can be specified by your service
        userID: '', // [Required] user ID, which can be specified by your service or use `openid` of WeChat Mini Program
        userSig: '', // [Required] identity signature, which needs to be obtained from a self-built signature service
        sdkAppID: '', // [Required] `sdkAppID` that will be assigned to a created application after TRTC is activated
        template: 'float', // [Required] this identifies the UI template used by the component. The component has three built-in layouts: `bigsmall`, `float`, and `grid`
        privateMapKey: '', // Room permission key, which needs to be obtained from a self-built signature service
				           // If you have not enabled the permission key in **Console** > **TRTC** > **Application Name** > **Account Info**, this parameter can be left empty
        beauty: 3, // Effect level of the beauty filter. Value range: 0–9; the greater the value, the more obvious the effect
        muted: false, // true: muted; false: not muted
        debug: false, // true: prints the push debugging information; false: does not print the push debugging information
        enableIM: false // Whether to enable IM
        // For more information on other configuration parameters, please see the API documentation
    },
    // The tag returns internal events via `onRoomEvent`
    onRoomEvent: function(e){
        switch(e.detail.tag){
            case 'error': {
                // An error occurs
                var code = e.detail.code;
                var detail = e.detail.detail;
                break;
            }
        }
    },
    // IM message events are returned via `onIMEvent`; if `enableIM` is disabled, `onIMEvent` can be ignored
    onIMEvent: function(e){
        switch(e.detail.tag){
            case 'big_group_msg_notify': 
                // A group message is received
                console.debug( e.detail.detail )
                break;
            case 'login_event': 
                // Login event notification
                console.debug( e.detail.detail )
                break;
            case 'connection_event': 
                // Connection status event
                console.debug( e.detail.detail )
                break;
            case 'join_group_event': 
                // Group entry event notification
                console.debug( e.detail.detail )
                break;
        }
    },

    onLoad: function (options) {
        // Here, you need to call the signature service to get signature information such as `userSig`
 	   // `userSig` needs to be calculated on your business server; otherwise, your private key may be leaked, causing security risks
		// For the calculation method of `userSig`, please visit https://intl.cloud.tencent.com/document/product/647/35166
        let self = this;
        wx.request({
            url: '',  // Address of your `usersig` calculating server
            data: {}, // Parameter required to calculate `usersig`, which is left empty here. Generally, `userid` needs to be carried
				      // This is because `usersig` is essentially an ECDH signature on `userid` and some other information
            method: 'POST',
            success: function (res) {
                // Parse the HTTP return packet. The code here is just an example. Normally, information such as `userid` and `usersig` can be obtained
			   // With this information, the `start` method of the `webrtc-room` object instance can be called to start the component
                self.setData({
                    userID: res.data.userID,
                    sdkAppID: res.data.sdkAppID,
                    roomID: res.data.roomID,
                    userSig: res.data.userSig, 
                    privateMapKey: res.data.privateMapKey // Room permission key, which needs to be obtained from a self-built signature service
				  // If you have not enabled the permission key in **Console** > **TRTC** > **Application Name** > **Account Info**, this parameter can be left empty
                }, function() {
                    var webrtcroomCom = self.selectComponent('#myroom');
                    if (webrtcroomCom) {
                        webrtcroomCom.start();
                    }
                })
            },
            fail: function (res) {
                console.error('Request failed');
            }
        });     
    }
})
```

## FAQs

### 1. How do I troubleshoot errors during execution?
- Please check whether the enabled category of WeChat Mini Program is correct and whether the push/pull tag is enabled in the WeChat Mini Program Console.
- If the official demo can be executed properly, please deploy the SDK again.
- If the error persists, please submit a ticket or call the customer service at 95716.

### 2. What if I can't see the video image when running the WeChat Mini Program to enter an audio/video call?
- Please make sure that you are running it on a mobile phone. The simulator inside the WeChat Developer Tool does not currently support running the SDK directly.
- Please check the WeChat Mini Program base library version by using `wx.getSystemInfo`. Only versions above 1.7.0 support audio/video capabilities.
- Please check the category of the WeChat Mini Program. Due to regulatory requirements, not all categories of WeChat Mini Programs are enabled for the audio/video capabilities. For supported categories, please see the [official documentation of WeChat Mini Program](https://developers.weixin.qq.com/miniprogram/dev/component/live-player.html?search-key=%E5%AE%9E%E6%97%B6%E6%92%AD%E6%94%BE).
- If you have different needs or want to cooperate with us in depth, please submit a ticket or call the customer service at 95716.

### 3. What if an error occurs with the `live-pusher` or `live-player` tag?
- [live-pusher and Error Codes](https://mp.weixin.qq.com/debug/wxadoc/dev/component/live-pusher.html)
- [live-player and Error Codes](https://mp.weixin.qq.com/debug/wxadoc/dev/component/live-player.html)
- [livePusherContext](https://developers.weixin.qq.com/miniprogram/dev/api/media/live/LivePusherContext.html)
- [livePlayerContext](https://developers.weixin.qq.com/miniprogram/dev/api/media/live/LivePlayerContext.html)

### 4. What if I need to deploy the SDK in a production environment?
- Please apply for domain names and get ICP filing for them
- Please deploy the server code to the obtained server
- Please configure the domain names of the business server, WebRTC audio/video authentication service, push, and IM in the valid domain names of requests in the WeChat Mini Program Console:

| Domain Name | Description | 
|:-------:|---------|
|`https://official.opensso.tencent-cloud.com` | Domain name for the WebRTC audio/video authentication service | 
|`https://yun.tim.qq.com` | Domain name for the WebRTC audio/video authentication service | 
|`https://intl.cloud.tencent.com`| Push domain name | 
|`https://webim.tim.qq.com` | IM domain name | 
