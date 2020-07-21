
## Overview
Signaling APIs are a set of invitation process control APIs that are provided based on IM messages to implement various real-time scenarios, such as:
- Mic-on and mic-off management in live streaming chat rooms.
- Voice and video call feature in chat scenarios, similar to the voice and video call feature of WeChat.
- Process control for teachers to invite students to raise their hands and speak in turn in education scenarios.

## Features 
Signaling APIs support the following features:
### One-to-one chat invitation
While using the [Simple Message APIs](https://intl.cloud.tencent.com/document/product/1047/36360) or [Rich Media Message APIs](https://intl.cloud.tencent.com/document/product/1047/36360) for a one-to-one chat, you can use the [invite](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Signaling_08.html#a0c7b9134995c78f3e2b855acdf65ac12) signaling API to make a one-to-one call, and when receiving the invitation notification [onReceiveNewInvitation](http://doc.qcloudtrtc.com/im/protocolV2TIMSignalingListener-p.html#ae544e6c0e26c7f23cd2b544f66aab450), the other party can choose to accept or reject the call or wait until it times out.
### Group chat invitation
First, complete group management by using the APIs for [creating a group](https://intl.cloud.tencent.com/document/product/1047/34329), [joining a group](https://intl.cloud.tencent.com/document/product/1047/34329), [quitting a group](https://intl.cloud.tencent.com/document/product/1047/34329), [disbanding a group](https://intl.cloud.tencent.com/document/product/1047/34329), [group profile](https://intl.cloud.tencent.com/document/product/1047/34329) and [group members](https://intl.cloud.tencent.com/document/product/1047/34329). Listen for relevant event callback in the group via [V2TIMGroupListener](http://doc.qcloudtrtc.com/im/protocolV2TIMGroupListener-p.html). Then, group members can initiate a group call invitation [inviteInGroup](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Signaling_08.html#a1ea8dcc4ee2200bf5913a40efd76bf4e) in the group, and when receiving the invitation notification [onReceiveNewInvitation](http://doc.qcloudtrtc.com/im/protocolV2TIMSignalingListener-p.html#ae544e6c0e26c7f23cd2b544f66aab450), the invited group member can choose to accept or reject the call or wait until it times out.
### Canceling an invitation
Before an invitation times out or is processed by the callee, the caller can [cancel](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Signaling_08.html#acaac35e5db28db783420b5eb39d53e6f) the invitation. The invitee will receive the cancellation notification [onInvitationCancelled](http://doc.qcloudtrtc.com/im/protocolV2TIMSignalingListener-p.html#a36c345823e46c9fc732f95df2c77226b), and the invitation process ends.

![Canceling an invitation](https://main.qcloudimg.com/raw/f941775dedf2de6b50119df1df3e426d.png)

### Accepting an invitation
When receiving an invitation notification [onReceiveNewInvitation](http://doc.qcloudtrtc.com/im/protocolV2TIMSignalingListener-p.html#ae544e6c0e26c7f23cd2b544f66aab450), the callee can [accept](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Signaling_08.html#a1ffb6daba9deed8780f869205daf7771) the invitation before the invitation times out or is canceled by the caller. If the invitation is accepted, the caller will receive the invitation acceptance notification [onInviteeAccepted](http://doc.qcloudtrtc.com/im/protocolV2TIMSignalingListener-p.html#ac768c6b6214ca04277bc732bf71c61c0). After all callees finish processing the invitation (through acceptance, rejection, and timeout), the invitation process ends.

![Accepting/Rejecting an invitation](https://main.qcloudimg.com/raw/9d291afecc0283452115317ddae8ddd8.png)

### Rejecting an invitation
When receiving an invitation notification [onReceiveNewInvitation](http://doc.qcloudtrtc.com/im/protocolV2TIMSignalingListener-p.html#ae544e6c0e26c7f23cd2b544f66aab450), the callee can [reject](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Signaling_08.html#a39e685924aaa4d22daa88f2ec96aa827) the invitation before the invitation times out or is canceled by the caller. If the invitation is rejected, the caller will receive the invitation rejection notification [onInviteeRejected](http://doc.qcloudtrtc.com/im/protocolV2TIMSignalingListener-p.html#a69a44a16b45aad587854dccc2e8040be). After all callees finish processing the invitation (through acceptance, rejection, and timeout), the invitation process ends.
### Invitation timeout
If the timeout threshold of the invitation API is greater than 0 and the callee does not respond before the timeout threshold is reached, then the invitation times out, and both the caller and callee will receive the timeout notification [onInvitationTimeout](http://doc.qcloudtrtc.com/im/protocolV2TIMSignalingListener-p.html#a7dfc62abd16dfd864ce7d45d483bcfc6). After all callees finish processing the invitation (through acceptance, rejection, and timeout), the invitation process ends. If the timeout threshold is 0, there is no timeout notification.

![Invitation timeout](https://main.qcloudimg.com/raw/82ffceea500434dea5a9e409a08a9fbe.png)

## Application Scenarios Cases
### Voice and video calls
In the open-source project [TUIKit Demo](https://github.com/tencentyun/TIMSDK), we provide a solution for one-to-one and one-to-many voice and video call scenarios on the basis of the [TRTC component](https://intl.cloud.tencent.com/document/product/647/36066) with minor modifications. You can directly make modifications or adaptations based on our demo. In this document, we introduce the combined use of signaling APIs and the TRTC SDK by using a 1v1 video call scenario as an example.

**1v1 video call process:**
1. Based on the roomID generated by the service layer, the caller enters the TRTC room and calls the signaling invitation API [invite](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Signaling_08.html#a0c7b9134995c78f3e2b855acdf65ac12) to initiate a voice and video call request. The roomID is placed in the custom field of the invitation API.
2. The callee receives the signaling invitation notification [onReceiveNewInvitation](http://doc.qcloudtrtc.com/im/protocolV2TIMSignalingListener-p.html#ae544e6c0e26c7f23cd2b544f66aab450) and obtains the roomID from the custom data. The interface starts ringing.
3. The callee processes the invitation notification:
 - If the callee accepts the invitation, call the [accept](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Signaling_08.html#a1ffb6daba9deed8780f869205daf7771) signaling API. Then, the callee enters the TRTC room based on the roomID and calls the openCamera() function to activate the callee’s local camera. After both parties receive the `onRemoteUserEnterRoom` callback of the TRTC SDK, record the start time of this call.
 - If the callee rejects the invitation, call the [reject](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Signaling_08.html#a39e685924aaa4d22daa88f2ec96aa827) signaling API to end this call.
 - If the callee is in a call with another user, call the [reject](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Signaling_08.html#a39e685924aaa4d22daa88f2ec96aa827) signaling API to reject the invitation, and in the custom data, inform the caller that the invitation was rejected because the line was busy.
4. After the callee answers the call and a voice and video channel is established between the two parties, both parties will receive the `onUserVideoAvailable` event notification of the TRTC SDK, indicating that each party has obtained the video image of the other party. At this time, both parties can call the TRTC SDK API `startRemoteView` to display the video image from the other party. The voice from the other party is automatically played by default.
5. When either party hangs up, the call ends, and the user quits the TRTC room. After the other party receives the `onRemoteUserLeaveRoom` callback of the TRTC SDK, calculate the total call duration, and initiate an invitation again. The custom data in this invitation indicates the end of the call with the call duration attached to facilitate UI display.

**Timing diagram**
![Signaling combined with TRTC](https://main.qcloudimg.com/raw/0282df9543e2f5fe1b5097c9e9253da1.png)

### Teachers invite students to raise their hands and speak in turns in education scenarios
In this scenario, the teacher first asks students to raise their hands, and then choose one of the students to speak. The detailed process is as follows:
1. The teacher calls the [inviteInGroup](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Signaling_08.html#a1ea8dcc4ee2200bf5913a40efd76bf4e) API to invite students to raise their hands. In the custom `data` field, enter “raise hands”. Students receive the [onReceiveNewInvitation](http://doc.qcloudtrtc.com/im/protocolV2TIMSignalingListener-p.html#ae544e6c0e26c7f23cd2b544f66aab450) callback.
2. Based on the `inviteeList` and `data` fields in [onReceiveNewInvitation](http://doc.qcloudtrtc.com/im/protocolV2TIMSignalingListener-p.html#ae544e6c0e26c7f23cd2b544f66aab450), students know that they are invited to raise their hands. Therefore, call the [accept](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Signaling_08.html#a1ffb6daba9deed8780f869205daf7771) API to accept the invitation.
3. If one or more students raise their hands, all users receive the [onInviteeAccepted](http://doc.qcloudtrtc.com/im/protocolV2TIMSignalingListener-p.html#ac768c6b6214ca04277bc732bf71c61c0) callback. Detect “raise hands” in the `data` field, and display the list of students who raised their hands.
4. From the list of students who raised their hands, the teacher invites a student to speak. Call the [inviteInGroup](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Signaling_08.html#a1ea8dcc4ee2200bf5913a40efd76bf4e) API, and in the custom `data` field, enter “speak”. Students then receive the [onReceiveNewInvitation](http://doc.qcloudtrtc.com/im/protocolV2TIMSignalingListener-p.html#ae544e6c0e26c7f23cd2b544f66aab450) callback.
5. Based on the `inviteeList` and `data` fields in [onReceiveNewInvitation](http://doc.qcloudtrtc.com/im/protocolV2TIMSignalingListener-p.html#ae544e6c0e26c7f23cd2b544f66aab450), the student knows that he or she is invited to speak. Therefore, call the [accept](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Signaling_08.html#a1ffb6daba9deed8780f869205daf7771) API to accept the invitation.
6. If the student speaks, all users receive the [onInviteeAccepted](http://doc.qcloudtrtc.com/im/protocolV2TIMSignalingListener-p.html#ac768c6b6214ca04277bc732bf71c61c0) callback. Detect “speak” in the `data` field, and display the list of students who speak.
