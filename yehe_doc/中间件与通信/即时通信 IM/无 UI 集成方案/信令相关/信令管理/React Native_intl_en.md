1. ## Overview

   Signaling APIs are a set of invitation process control APIs based on IM messages. They can be used to implement a variety of real-time features, including:

   - Mic-on or mic-off management in audio-video chat rooms
   - Chatting: audio/video calls as those in WeChat
   - Control of the process for teachers to invite students to "raise hands" and speak in education scenarios

   ## Features

   Signaling APIs support the following features:

   ### One-to-one chat invitation

   When the [API for sending and receiving simple messages](https://intl.cloud.tencent.com/document/product/1047/36359#.E6.94.B6.E5.8F.91.E7.AE.80.E5.8D.95.E6.B6.88.E6.81.AF) or the [API for sending and receiving rich media messages](https://intl.cloud.tencent.com/document/product/1047/36359#.E6.94.B6.E5.8F.91.E5.AF.8C.E5.AA.92.E4.BD.93.E6.B6.88.E6.81.AF) is used for a one-to-one chat, the [invite](https://comm.qq.com/im/doc/RN/en/Api/V2TIMSignalingManager/invite.html) signaling API can be used to make a point-to-point call. After receiving the invitation [onReceiveNewInvitation](https://comm.qq.com/im/doc/RN/en/Callback/OnReceiveNewInvitation.html), the receiver can accept or reject the invitation, or wait for the invitation to time out.

   ### Group chat invitation

   First, you need to manage the group through APIs such as those for [creating a group](https://intl.cloud.tencent.com/document/product/1047/34328#.E5.88.9B.E5.BB.BA.E7.BE.A4.E7.BB.84), [joining a group](https://intl.cloud.tencent.com/document/product/1047/34328#.E5.8A.A0.E5.85.A5.E7.BE.A4.E7.BB.84), [leaving a group](https://intl.cloud.tencent.com/document/product/1047/34328#.E9.80.80.E5.87.BA.E7.BE.A4.E7.BB.84), and [disbanding a group](https://intl.cloud.tencent.com/document/product/1047/34328#.E8.A7.A3.E6.95.A3.E7.BE.A4.E7.BB.84), as well as [group profile](https://intl.cloud.tencent.com/document/product/1047/34328#.E7.BE.A4.E8.B5.84.E6.96.99.E5.92.8C.E7.BE.A4.E8.AE.BE.E7.BD.AE) and [group member](https://intl.cloud.tencent.com/document/product/1047/34328#.E7.BE.A4.E6.88.90.E5.91.98.E7.AE.A1.E7.90.86) APIs, and listen for relevant group callbacks through [V2TimGroupListener](https://comm.qq.com/im/doc/RN/en/Interface/Listener/V2TimGroupListener.html). Then group members can send a call invitation in the group through [inviteInGroup](https://comm.qq.com/im/doc/RN/en/Api/V2TIMSignalingManager/inviteInGroup.html). The invitee will receive the invitation [onReceiveNewInvitation](https://comm.qq.com/im/doc/RN/en/Callback/OnReceiveNewInvitation.html) and can accept or reject the invitation, or wait for the invitation to time out.

   ### Canceling an invitation

   An inviter can call [cancel](https://comm.qq.com/im/doc/RN/en/Api/V2TIMSignalingManager/cancel.html) to cancel the invitation, if it is not processed by the invitee before the timeout period. The invitee will receive the cancellation notification [onInvitationCancelled](https://comm.qq.com/im/doc/RN/en/Callback/OnInvitationCancelled.html), and the invitation process ends.

   ![](https://main.qcloudimg.com/raw/f482603761219a660d47098c8754ff5a.png)

   ### Accepting an invitation

   After receiving the invitation [onReceiveNewInvitation](https://comm.qq.com/im/doc/RN/en/Callback/OnReceiveNewInvitation.html), the invitee can call [accept](https://comm.qq.com/im/doc/RN/en/Api/V2TIMSignalingManager/accept.html) to accept the invitation, if it is not canceled by the inviter before the timeout period. The inviter will receive the acceptance notification [onInviteeAccepted](https://comm.qq.com/im/doc/RN/en/Callback/OnInviteeAccepted.html). After the invitation is processed by the invitee, for example, it is accepted or rejected, or times out, the invitation process ends.

   ![](https://main.qcloudimg.com/raw/764eae198d01855a4e87f6611b056b28.png)

   ### Rejecting an invitation

   After receiving the invitation [onReceiveNewInvitation](https://comm.qq.com/im/doc/RN/en/Callback/OnReceiveNewInvitation.html), the invitee can call [reject](https://comm.qq.com/im/doc/RN/en/Api/V2TIMSignalingManager/reject.html) to reject the invitation, if it is not canceled by the inviter before the timeout period. The inviter will receive the rejection notification [onInviteeRejected](https://comm.qq.com/im/doc/RN/en/Callback/OnInviteeRejected.html). After the invitation is processed by the invitee, for example, it is accepted or rejected, or times out, the invitation process ends.

   ### Invitation timeout

   If the timeout period of the invitation API is larger than 0, and the invitee doesn't respond to the invitation within the timeout period, the invitation times out, and both the inviter and the invitee will receive the timeout notification [onInvitationTimeout](https://comm.qq.com/im/doc/RN/en/Callback/OnInvitationTimeout.html). After the invitation is processed by the invitee, for example, it is accepted or rejected, or times out, the invitation process ends. If the timeout period of the invitation API is 0, there will be no timeout notification.

   ![](https://main.qcloudimg.com/raw/293e604a66d65413be7b3b1e68b299c5.png)

   ## Use Cases

   ### Audio/Video call

   In the open-source project [TRTCFlutterScenesDemo](https://github.com/tencentyun/TRTCFlutterScenesDemo), we developed an audio/video call solution suitable for one-to-one and multi-person chatting based on [TRTC](https://intl.cloud.tencent.com/document/product/647/41691). You can directly modify the demo for adaptation. The following takes the one-to-one video call process as an example to introduce how signaling APIs work with the TRTC SDK.

   **One-to-one video call process:**

   1. The inviter enters the TRTC room based on the room ID generated at the service layer and calls the signaling invitation API [invite](https://comm.qq.com/im/doc/RN/en/Api/V2TIMSignalingManager/invite.html) to initiate an audio/video call request, including the room ID in the custom field of the invitation API.
   2. The invitee receives the signaling invitation [onReceiveNewInvitation](https://comm.qq.com/im/doc/RN/en/Callback/OnReceiveNewInvitation.html) and gets the `roomID` through the custom data. The UI rings.
   3. The invitee processes the invitation notification:

   - To accept the invitation, the invitee needs to call the [accept](https://comm.qq.com/im/doc/RN/en/Api/V2TIMSignalingManager/accept.html) signaling API, enter the TRTC room based on the `roomID`, and call the `openCamera()` function to enable the local camera. The inviter and the invitee receive the `onRemoteUserEnterRoom` callback from the TRTC SDK, and their systems record the start time of the call.
   - To reject the invitation, the invitee needs to call the [reject](https://comm.qq.com/im/doc/RN/en/Api/V2TIMSignalingManager/reject.html) signaling API to end the call.
   - If the invitee is on the call, the invitee can call the [reject](https://comm.qq.com/im/doc/RN/en/Api/V2TIMSignalingManager/reject.html) signaling API to reject the invitation and notify the inviter through the custom data that the invitation is rejected due to the busy local line.

   4. After the invitee answers the call and the audio/video channel between the inviter and invitee is established, both the inviter and invitee will receive the `onUserVideoAvailable` event notification from the TRTC SDK, which indicates that they have received each other's video image. At this point, they can call the `startRemoteView` API of the TRTC SDK to display the remote video image, and the remote audio will be automatically played back by default.
   5. After the call ends (either the inviter or invitee hangs up), the party who hangs up exits the TRTC room. The other party receives the `onRemoteUserLeaveRoom` callback from the TRTC SDK, and its system calculates the total duration of the call and initiates an invitation again. The custom data in the invitation specifies the call end event and call duration to facilitate UI display.

   **Flowchart**
   ![](https://main.qcloudimg.com/raw/868a811fe706f1cbb04014c1058c393d.png)

   ### Teacher inviting students to raise their hand and speak

   In this scenario, the teacher asks students to raise hands and then chooses one of the students to speak. The process is as follows:

   1. The teacher calls the [inviteInGroup](https://comm.qq.com/im/doc/RN/en/Api/V2TIMSignalingManager/inviteInGroup.html) API to invite students to "raise hands", specifying the "hand raising" operation in the custom field `data`. The students receive the [onReceiveNewInvitation](https://comm.qq.com/im/doc/RN/en/Callback/OnReceiveNewInvitation.html) callback.
   2. The students check the `inviteeList` and `data` fields in [onReceiveNewInvitation](https://comm.qq.com/im/doc/RN/en/Callback/OnReceiveNewInvitation.html) to determine whether they are invited to raise their hand. Then they call the [accept](https://comm.qq.com/im/doc/RN/en/Api/V2TIMSignalingManager/accept.html) API to raise their hand.
   3. If a student raises her/his hand, others can receive the [onInviteeAccepted](https://comm.qq.com/im/doc/RN/en/Callback/OnInviteeAccepted.html) callback. The system determines that the `data` field is hand raising and displays the list of students who raise hands.
   4. The teacher invites one of the students raising their hand to speak and calls the [inviteInGroup](https://comm.qq.com/im/doc/RN/en/Api/V2TIMSignalingManager/inviteInGroup.html) API. Here, the custom field `data` is specified as "speaking". The students receive the [onReceiveNewInvitation](https://comm.qq.com/im/doc/RN/en/Callback/OnReceiveNewInvitation.html) callback.
   5. The students check the `inviteeList` and `data` fields in the [onReceiveNewInvitation](https://comm.qq.com/im/doc/RN/en/Callback/OnReceiveNewInvitation.html) callback to determine whether they are invited to speak. Then they call the [accept](https://comm.qq.com/im/doc/RN/en/Api/V2TIMSignalingManager/accept.html) API to speak.
   6. If one of the students speaks, all the students will receive the [onInviteeAccepted](https://comm.qq.com/im/doc/RN/en/Callback/OnInviteeAccepted.html) callback, which contains the `data` field specified as "speaking" and displays the list of speaking students.
