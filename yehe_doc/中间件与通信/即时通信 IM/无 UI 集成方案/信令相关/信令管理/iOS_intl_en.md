## Overview
Signaling APIs are a set of invitation process control APIs based on IM messages. They can be used to implement a variety of real-time features, including:
- Mic-on or mic-off management in audio-video chat rooms (TUILiveRoom)
- Audio/Video calls in chat scenarios
- Control of the process for teachers to invite students to "raise hands" and speak in education scenarios

## Features 
Signaling APIs support the following features:
### One-to-one chat invitation
When making a one-to-one chat via the [simple message sending or receiving API](https://intl.cloud.tencent.com/document/product/1047/36360) or [rich media message sending or receiving API](https://intl.cloud.tencent.com/document/product/1047/36360), you can use the [invite](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Signaling_08.html#a0d75713295f5f19c7d303a0eaeeaaacb) signaling API to initiate an end-to-end call invitation. When receiving the invitation notification [onReceiveNewInvitation](https://im.sdk.qcloud.com/doc/en/protocolV2TIMSignalingListener-p.html#ae544e6c0e26c7f23cd2b544f66aab450), the invitee can accept the invitation, reject the invitation, or wait until the invitation times out.
### Group chat invitation
First, you need to manage a group by using [group management APIs](https://intl.cloud.tencent.com/document/product/1047/34329) and listen for the group's event callbacks via [V2TIMGroupListener](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html). Then members of the group can initiate a group call invitation via [inviteInGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Signaling_08.html#ae7efa9137309a48c93fcd84a6d997506) within the group. When receiving the invitation notification [onReceiveNewInvitation](https://im.sdk.qcloud.com/doc/en/protocolV2TIMSignalingListener-p.html#ae544e6c0e26c7f23cd2b544f66aab450), an invitee can accept the invitation, reject the invitation, or wait until the invitation times out.
### Canceling an invitation
If an invitation has not timed out and has not been processed by an invitee, the inviter can cancel the invitation via [cancel](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Signaling_08.html#a09bc478d84e053d94004c7ec1bbddf58). After the inviter cancels the invitation, the invitee receives a cancellation notification [onInvitationCancelled](https://im.sdk.qcloud.com/doc/en/protocolV2TIMSignalingListener-p.html#a36c345823e46c9fc732f95df2c77226b), and the invitation process ends.

![Canceling an invitation](https://main.qcloudimg.com/raw/f482603761219a660d47098c8754ff5a.png)

### Accepting an invitation
When receiving an invitation notification [onReceiveNewInvitation](https://im.sdk.qcloud.com/doc/en/protocolV2TIMSignalingListener-p.html#ae544e6c0e26c7f23cd2b544f66aab450), an invitee can accept the invitation via [accept](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Signaling_08.html#a0f486191d6b1755a12de6e2fc42afc14) if the invitation has not timed out and has not been canceled by the inviter. If the invitee accepts the invitation, the inviter receives an invitation acceptance notification [onInviteeAccepted](https://im.sdk.qcloud.com/doc/en/protocolV2TIMSignalingListener-p.html#ac768c6b6214ca04277bc732bf71c61c0). After the processing (including invitation acceptance, rejection, and timeout) at the invitee side ends, the invitation process ends.

![Accepting/Rejecting an invitation](https://main.qcloudimg.com/raw/764eae198d01855a4e87f6611b056b28.png)

### Rejecting an invitation
When receiving an invitation notification [onReceiveNewInvitation](https://im.sdk.qcloud.com/doc/en/protocolV2TIMSignalingListener-p.html#ae544e6c0e26c7f23cd2b544f66aab450), the invitee can reject the invitation via [reject](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Signaling_08.html#aa945a73b34c98e5512ecdd77f2628b53) if the invitation has not timed out and has not been canceled by the inviter. If the invitee rejects the invitation, the inviter receives an invitation rejection notification [onInviteeRejected](https://im.sdk.qcloud.com/doc/en/protocolV2TIMSignalingListener-p.html#a69a44a16b45aad587854dccc2e8040be). After the processing (including invitation acceptance, rejection, and timeout) at the invitee side ends, the invitation process ends.
### Invitation timeout
If the timeout period of the invitation API is greater than 0 and the invitee does not respond within the timeout period, the invitation times out, and the inviter and invitee will receive a timeout notification [onInvitationTimeout](https://im.sdk.qcloud.com/doc/en/protocolV2TIMSignalingListener-p.html#a7dfc62abd16dfd864ce7d45d483bcfc6). After the processing (including invitation acceptance, rejection, and timeout) at the invitee side ends, the invitation process ends. If the timeout period of the invitation API is 0, there will be no timeout notification.

![Invitation timeout](https://main.qcloudimg.com/raw/293e604a66d65413be7b3b1e68b299c5.png)

## Use Cases
### Audio/Video call
In the open-source project [TUIKit Demo](https://github.com/tencentyun/TIMSDK), we developed a one-to-one and group audio/video call solution based on [the TRTC component TUICalling](https://intl.cloud.tencent.com/document/product/647/36066) for chat scenarios. You can directly modify the TUIKit demo for adaptation. The following takes the one-to-one video call process as an example to introduce how signaling APIs work with the TRTC SDK.

**One-to-one video call process:**
1. The inviter enters the TRTC room based on the room ID generated at the service layer and calls the signaling invitation API [invite](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Signaling_08.html#a0d75713295f5f19c7d303a0eaeeaaacb) to initiate an audio/video call request, with the room ID included in the custom field of the invitation API.
2. The invitee receives the signaling invitation notification [onReceiveNewInvitation](https://im.sdk.qcloud.com/doc/en/protocolV2TIMSignalingListener-p.html#ae544e6c0e26c7f23cd2b544f66aab450) and gets the room ID from the custom data. The invitee's phone begins to ring.
3. The invitee processes the invitation notification:
 - Accepting the invitation: The invitee calls the [accept](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Signaling_08.html#a0f486191d6b1755a12de6e2fc42afc14) signaling API, enters the TRTC room based on the room ID, and calls the `openCamera()` function to enable the local camera. The inviter and invitee receive the `onRemoteUserEnterRoom` callback from the TRTC SDK, and the systems of the two parties record the start time of the call.
 - Rejecting the invitation: The invitee calls the [reject](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Signaling_08.html#aa945a73b34c98e5512ecdd77f2628b53) signaling API to end the call.
 - If the invitee is on the phone with someone else, the invitee calls the [reject](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Signaling_08.html#aa945a73b34c98e5512ecdd77f2628b53) signaling API to reject the invitation and to specify the rejection reason (busy local line) in the custom data.
4. After the invitee answers the call and the audio/video channel between the inviter and invitee is established, both the inviter and invitee will receive the `onUserVideoAvailable` event notification from the TRTC SDK, which indicates that they have received each other's video image. At this point, they can call the `startRemoteView` API of the TRTC SDK to display the remote video image, and the remote audio will be automatically played back by default.
5. After the call ends (either the inviter or invitee hangs up), the party who hangs up exits the TRTC room. The other party receives the `onRemoteUserLeaveRoom` callback from the TRTC SDK, and its system calculates the total duration of the call and initiates an invitation again. The custom data in the invitation specifies the call end event and call duration to facilitate UI display.

**Flowchart**
![Signaling APIs working with TRTC SDK](https://main.qcloudimg.com/raw/868a811fe706f1cbb04014c1058c393d.png)

### Teacher inviting students to raise hands and speak
In this scenario, the teacher asks students to raise hands and then chooses one of the students to speak. The process is as follows:
1. The teacher calls the [inviteInGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Signaling_08.html#ae7efa9137309a48c93fcd84a6d997506) API to invite students to raise hands, specifying the hand raising operation in the custom field `data`. The students receive the [onReceiveNewInvitation](https://im.sdk.qcloud.com/doc/en/protocolV2TIMSignalingListener-p.html#ae544e6c0e26c7f23cd2b544f66aab450) callback.
2. Based on the `inviteeList` and `data` fields in [onReceiveNewInvitation](https://im.sdk.qcloud.com/doc/en/protocolV2TIMSignalingListener-p.html#ae544e6c0e26c7f23cd2b544f66aab450), a student determines that he/she is one of the invitees and the operation is hand raising. Then the student calls the [accept](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Signaling_08.html#a0f486191d6b1755a12de6e2fc42afc14) API to raise her/his hand.
3. If a student raises her/his hand, others can receive the [onInviteeAccepted](https://im.sdk.qcloud.com/doc/en/protocolV2TIMSignalingListener-p.html#ac768c6b6214ca04277bc732bf71c61c0) callback. The system determines that the `data` field specifies the hand raising operation and displays the list of students who raise hands.
4. The teacher calls the [inviteInGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Signaling_08.html#ae7efa9137309a48c93fcd84a6d997506) API to invite one of the students who raise their hands to speak. At this time, the system specifies the speaking operation in the custom field `data`. The students receive the [onReceiveNewInvitation](https://im.sdk.qcloud.com/doc/en/protocolV2TIMSignalingListener-p.html#ae544e6c0e26c7f23cd2b544f66aab450) callback.
5. Based on the `inviteeList` and `data` fields in the [onReceiveNewInvitation](https://im.sdk.qcloud.com/doc/en/protocolV2TIMSignalingListener-p.html#ae544e6c0e26c7f23cd2b544f66aab450) callback, a student determines that he/she is one of the invitees and the operation is speaking. Then the student calls the [accept](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Signaling_08.html#a0f486191d6b1755a12de6e2fc42afc14) API to speak.
6. If a student speaks, others can receive the [onInviteeAccepted](https://im.sdk.qcloud.com/doc/en/protocolV2TIMSignalingListener-p.html#ac768c6b6214ca04277bc732bf71c61c0) callback, and their systems determine that the `data` field specifies the speaking operation and display the list of students who speak.



## FAQs

### 1. Can a user be invited by two users at the same time?

The signaling APIs ([iOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Signaling_08.html) | [Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSignalingManager.html)) provided by the IM SDK does not limit the invitation logic. One user can receive multiple signaling invitations at the same time. For the audio/video call scenario, the component TUICalling provides a "busy" alert.

### 2. Can I send multiple signaling invitations at the same time?

Yes. The upper-layer semantics need to distinguish the required operations in the invitations based on the actual business requirements.

### 3. The IM SDK provides signaling APIs for initiating, rejecting/accepting, and canceling invitations only. How do I implement the hang-up operation?

* The invitation operation can be considered as a **connection request** by upper-layer semantics.
* The hang-up operation can be considered as a **hang-up request** by upper-layer semantics.

You can call the **invite** API of the IM SDK to initiate an invitation and specify the current invitation as a **connection or hang-up request** in the custom data of the API. Then, IM passes through the invitation to the peer for processing. 

### 4. What is the handling logic when a sent signaling invitation times out?

* If both the invitation sender and receiver are online, the timeout signaling is triggered by the receiver, and both the sender and receiver receive the `onInvitationTimeout` callback.
* If the receiver is offline, the timeout signaling is triggered by the sender, who receives the `onInvitationTimeout` callback.
* Timeout signaling is sent by the IM SDK.

### 5. If I go offline and then go online again, do I receive signaling messages that have not timed out?

If you cold start the app (kill the process and click the app icon again to start the app), there are two situations depending on the chat type:

* For a one-to-one chat, the IM SDK automatically synchronizes all signaling messages. If the signaling messages have not timed out, the IM SDK calls back `onReceiveNewInvitation`.
* For a group chat, the IM SDK automatically synchronizes signaling messages of the last 30 seconds. If some of the signaling messages have not timed out, the IM SDK calls back `onReceiveNewInvitation`.

If you hot start the app (click the app icon when the app runs in the background), the IM SDK synchronizes all signaling messages that have not timed out and calls back `onReceiveNewInvitation`, regardless of the current chat type (one-to-one or group chat).

### 6. Is the `inviteID` unique in signaling callbacks?

Yes. An `inviteID` is a unique identifier of a set of signaling messages (including invitation initiation, acceptance/rejection, and timeout messages).
