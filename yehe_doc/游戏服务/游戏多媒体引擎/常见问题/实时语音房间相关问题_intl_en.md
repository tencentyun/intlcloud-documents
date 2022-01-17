### What gaming scenarios does the voice chat service support?
There are mainly three types of applicable scenarios:
- **Mic sequence mode:** this mode allows players to mic on in turn with high and smooth sound quality, which is suitable for voice chat-enabled games such as werewolf.
- **Free audio call mode:** this mode allows multiple players to speak at the same time with ultra low latency, which is suitable for competitive games such as multi-player team battles.
- **Command mode:** this mode is suitable for commander games such as one-to-many command battles and audio interaction with host.
Voice chat features provided by Tencent Cloud SDK can meet the needs of the above-mentioned scenarios. However, the specific mode (such as mic sequence) is something that should be implemented in your own product's application layer through a delivery protocol, for example.

### What are the requirements for the value of `openid`?
Only a 64-bit unsigned integer can be an `openid`. Convert it to a string before passing it to the SDK.

### Can one single `openid` enter multiple rooms at the same time?
No. One `openid` can only exist in one room at a time.

### When should the `Poll` function in the GME SDK be invoked?
Please start invoking the `Poll` function periodically after initializing the SDK.

### The trigger event needs to periodically invoke the `Poll` function. Is it okay to start a new thread, wake it up periodically, and then invoke the function?
Theoretically, all TencentCloud APIs need to be called in the same thread. If you choose to call them in child threads, be sure to call them in the same child thread, especially for `Init` and `Poll`.


### How often should I invoke the `Poll` function?
If there are no special requirements, please invoke the function as instructed in the sample code of the demo.

### Is there a limit on the number of voice chat rooms or members in GME?
There is no limit on the number of voice chat rooms or the number of members.

### How many users can be in a room? How many users can speak at the same time?
GME has no limit on the number of users in a room, but only up to 6 users can speak at the same time.

### What are the requirements for room ID?
A room ID can contain up to 127 characters (for the voice messaging and speech-to-text feature, `null` must be entered).

### Why room entry fails even if 0 is returned when the `EnterRoom` API is called?
A callback will be returned after the `EnterRoom` API is called, which, instead of the API returned value, should be used to determine whether room entry succeeds.

### How do I troubleshoot failures such as 10001 returned for room entry?
The troubleshooting steps are as follows:
1. View and confirm the validity of the parameters in the room entry API, such as `Appid`, `UIN`, and `AuthBuffer` (please see the API documentation for the corresponding platform).
2. Check whether the relevant parameters in the console match the local ones.
3. Check whether your account is overdue in the console.
4. Check whether your testing devices are in the private network or public network. If they are in the private network, please troubleshoot as instructed in [Dealing with Corporate Firewall Restrictions](https://intl.cloud.tencent.com/document/product/607/35232).

### What should I do if the callback returns the error code 1101 when the `EnterRoom` API is called for room entry after the `Init` method is called?
Please make sure that all APIs are called in the same thread and the `Poll` API is called periodically.

### Why is "HTTP Invalid id" returned when I enter a room in an application?
If your account mapped by the `OpenId` parameter when you call the `EnterRoom` API starts from 0, you are recommended to add 10000 to it. For example, if your account is 999, 10999 should be entered as your `OpenId`.

### What should I do if the error code 7004 indicating a network error is returned during room entry?
1. View and confirm the validity of the parameters in the room entry API, such as `Appid`, `UIN`, and `AuthBuffer` (please see the API documentation for the corresponding platform).
2. Check whether your testing devices are in the private network or public network. If they are in the private network, please troubleshoot as instructed in [Dealing with Corporate Firewall Restrictions](https://intl.cloud.tencent.com/document/product/607/35232).
3. Troubleshoot network problems as instructed below.



### How do I troubleshoot network problems?
**Network diagnosis**:
- [Click here to check the domain name tcloud.tim.qq.com](https://ping.huatuo.qq.com/tcloud.tim.qq.com) or directly copy the following link: https://ping.huatuo.qq.com/tcloud.tim.qq.com
- [Click here to check the domain name gmeconf.qcloud.com](https://ping.huatuo.qq.com/gmeconf.qcloud.com) or directly copy the following link: https://ping.huatuo.qq.com/gmeconf.qcloud.com
- [Click here to check the domain name yun.tim.qq.com](https://ping.huatuo.qq.com/yun.tim.qq.com) or directly copy the following link: https://ping.huatuo.qq.com/yun.tim.qq.com

Use a browser on the device with network problems to open the three links above, wait for the check to be completed (it may take 5–10 seconds), click **Copy Result URL for Sharing** to copy the result, and provide it to Tencent Cloud technical support for assistance.

![](https://main.qcloudimg.com/raw/0b540f4bf6222c6b9548b148496a15bb.png)

**SSO diagnosis**:
On the device with network problems, [click here to check the domain name tcloud.tim.qq.com](https://tcloud.tim.qq.com), view the displayed content, copy or take a screenshot of the content, and provide it to Tencent Cloud technical support for assistance.
Sample: {"ActionStatus":"FAIL","ErrorCode":60002,"ErrorInfo":"HTTP parse Error"}

### After I enter the voice chat room, will I exit the room automatically if I switch my mobile phone to the background?
 You will automatically exit the room after 90 s of no heartbeat reported to the server.

### What should I do if a client is disconnected from a voice chat room?
If the network connection is interrupted, the client will try reconnecting to the room in 60 minutes. `ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT` will be called back after 60 minutes. After the reconnection, the mic and speaker status do not need to be set.


### Is there an API for room ID recycling?
No. After the last member exits the room, the room will be automatically terminated.

### How should be APIs called when room entry is performed immediately after room exit?
If there is a scenario in the application where room entry is performed immediately after room exit, you don't need to wait for the `RoomExitComplete` callback notification from the `ExitRoom` API during API call; instead, you can directly call the API.


### Are room entry and exit operations async? Can the two APIs be called at the same time?
You need to call `exitroom` first and then call `enterroom` after receiving a callback for successful room exit. If there is a scenario in the application where room entry is performed immediately after room exit, you don't need to wait for the `RoomExitComplete` callback notification from the `ExitRoom` API during API call; instead, you can directly call the API.



### When is the member status synced? Will a user receive a notification when entering the room for the first time?
Notifications for audio events are subject to a threshold, and the notification "A member sends an audio packet" will be sent only when this threshold is exceeded. If a member in the room does not speak for two seconds, the notification "A member stops sending audio packets" will be sent. There will be a notification when a user enters the room for the first time.



### Will a blocked user stay in the blocklist after exiting the room?
No. After voice room exit, the blocklist becomes invalid.

### I can normally use the range voice but there is no attenuation. I set the 3D sound effect file but the return value is still 0. Why did this happen?
Confirm if you enable the 3D sound effect API `EnableSpatializer`, and use [UpdateSelfPosition and UpdateAudioRecvRange](https://intl.cloud.tencent.com/document/product/607/18218) to update your position.
