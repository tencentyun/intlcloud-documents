1. ## Overview
   Signaling APIs are a set of invitation process control APIs based on IM messages. They can be used to implement a variety of real-time features, including:
   - Audio-video chat rooms: mic on or mic off
   - Chatting: audio/video calls
   - Education: control of the process for teachers to invite students to "raise hands"

   ## Features 
   Signaling APIs support the following features:
   ### One-to-one chat invitation
   When making a one-to-one chat via the [simple message sending or receiving API](https://intl.cloud.tencent.com/document/product/1047/36359#.E6.94.B6.E5.8F.91.E7.AE.80.E5.8D.95.E6.B6.88.E6.81.AF) or [rich media message sending or receiving API](https://intl.cloud.tencent.com/document/product/1047/36359#.E6.94.B6.E5.8F.91.E5.AF.8C.E5.AA.92.E4.BD.93.E6.B6.88.E6.81.AF), you can use the [invite](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMSignalingManager/invite.html) signaling API to make an end-to-end call. When receiving the invitation notification [onReceiveNewInvitation](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnReceiveNewInvitationCallback.html), the invitee can choose to accept the invitation, reject the invitation, or wait until the invitation times out.

   ### Group chat invitation
   First, you need to manage a group by using [group management APIs](https://intl.cloud.tencent.com/document/product/1047/34328#.E5.88.9B.E5.BB.BA.E7.BE.A4.E7.BB.84) and listen for the group's event callbacks via [V2TimGroupListener](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Listener/V2TimGroupListener.html). Then members of the group can initiate a group call invitation via [inviteInGroup](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMSignalingManager/inviteInGroup.html) within the group. When receiving the invitation [onReceiveNewInvitation](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnReceiveNewInvitationCallback.html), an invitee can choose to accept the invitation, reject the invitation, or wait until the invitation times out.
   ### Canceling an invitation
   Before an invitation times out and the invitee processes the invitation, the inviter can cancel the invitation via [cancel](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMSignalingManager/cancel.html). After the inviter cancels the invitation, an invitee will receive a cancellation notification [onInvitationCancelled](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnInvitationCancelledCallback.html), and the invitation process ends.

   ![](https://main.qcloudimg.com/raw/f482603761219a660d47098c8754ff5a.png)

   ### Accepting an invitation
   When receiving an invitation [onReceiveNewInvitation](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnReceiveNewInvitationCallback.html), an invitee can accept the invitation via [accept](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMSignalingManager/accept.html) before the invitation times out and the inviter cancels the invitation. If the invitee accepts the invitation, the inviter will receive an invitation acceptance notification [onInviteeAccepted](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnInviteeAcceptedCallback.html). After the processing (including acceptance, rejection, and timeout) at the invitee side ends, the invitation process ends.

   ![](https://main.qcloudimg.com/raw/764eae198d01855a4e87f6611b056b28.png)

   ### Rejecting an invitation
   When receiving an invitation notification [onReceiveNewInvitation](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnReceiveNewInvitationCallback.html), an invitee can reject the invitation via [reject](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMSignalingManager/reject.html) before the invitation times out and the inviter cancels the invitation. If the invitee rejects the invitation, the inviter will receive an invitation rejection notification [onInviteeRejected](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnInviteeRejectedCallback.html). After the processing (including acceptance, rejection, and timeout) at the invitee side ends, the invitation process ends.
   ### Invitation timeout
   If the timeout duration of the invitation API is greater than 0 and an invitee does not respond within the timeout duration, the invitation times out, and the inviter and invitee will receive a timeout notification [onInvitationTimeout](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnInvitationTimeoutCallback.html). After the processing (including acceptance, rejection, and timeout) at the invitee side ends, the invitation process ends. If the timeout duration of the invitation API is 0, there will be no timeout notification.

   ![](https://main.qcloudimg.com/raw/293e604a66d65413be7b3b1e68b299c5.png)

   ## Use Cases
   ### Audio/Video call
   In the open-source project [TRTCFlutterScenesDemo](https://github.com/tencentyun/TRTCFlutterScenesDemo), we developed an audio/video call solution suitable for one-to-one and multi-person chatting based on [TRTC](https://intl.cloud.tencent.com/document/product/647/41691). You can directly modify the demo for adaptation. The following takes the one-to-one video call process as an example to introduce how signaling APIs work with the TRTC SDK.

   **One-to-one video call process:**
   1. The inviter enters the TRTC room based on the room ID generated at the service layer and calls the signaling invitation API [invite](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMSignalingManager/invite.html) to initiate an audio/video call request, including the room ID in the custom field of the invitation API.
   2. The invitee receives the signaling invitation notification [onReceiveNewInvitation](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnReceiveNewInvitationCallback.html) and gets the room ID based on the custom data. The invitee's phone begins to ring.
   3. The invitee processes the invitation notification:
    - Accepting the invitation: the invitee calls the [accept](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMSignalingManager/accept.html) signaling API and enters the TRTC room based on the room ID, and calls the `openCamera()` function to enable the local camera. The inviter and invitee receive the `onRemoteUserEnterRoom` callback from the TRTC SDK, and the systems of the two parties record the start time of the call.
    - Rejecting the invitation: the invitee calls the [reject](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMSignalingManager/reject.html) signaling API to end the call.
    - If the invitee is on the phone with someone else, the invitee calls the [reject](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMSignalingManager/reject.html) signaling API to reject the invitation and specify the rejection reason (busy local line) in the custom data.
   4. After the invitee answers the call and the audio/video channel between the inviter and invitee is established, both the inviter and invitee will receive the `onUserVideoAvailable` event notification from the TRTC SDK, which indicates that they have received each other's video image. At this point, they can call the `startRemoteView` API of the TRTC SDK to display the remote video image, and the remote audio will be played back by default.
   5. After the call ends (either the inviter or invitee hangs up), the party who hangs up exits the TRTC room. The other party receives the `onRemoteUserLeaveRoom` callback from the TRTC SDK, and its system calculates the total duration of the call and initiates an invitation again, including the call end event and call duration in the custom data to facilitate UI display.

   **Flowchart**
   ![](https://main.qcloudimg.com/raw/868a811fe706f1cbb04014c1058c393d.png)

   ### Education: teacher inviting students to "raise hands"
   In this scenario, the teacher asks students to "raise hands" and then chooses one of the students to speak. The process is as follows:
   1. The teacher calls the [inviteInGroup](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMSignalingManager/inviteInGroup.html) API to invite students to "raise hands", specifying the "hand raising" operation in the custom field `data`. The students receive the [onReceiveNewInvitation](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSignalingListener.html#aecc2341ca87eb58be37fdadf7a58c014) callback.
   2. Based on the `inviteeList` and `data` fields in [onReceiveNewInvitation](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnReceiveNewInvitationCallback.html), a student determines that he/she is one of the invitees and the operation is hand raising. Then the student calls the [accept](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMSignalingManager/accept.html) API to raise her/his hand.
   3. If a student raises her/his hand, others can receive the [onInviteeAccepted](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnInviteeAcceptedCallback.html) callback. The system determines that the `data` field is hand raising and displays the list of students who raise hands.
   4. The teacher calls the [inviteInGroup](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMSignalingManager/inviteInGroup.html) API to invite one of the students who raise their hands to speak. At this time, the system specifies the "speaking" operation in the custom field `data`. The students receive the [onReceiveNewInvitation](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnReceiveNewInvitationCallback.html) callback.
   5. Based on the `inviteeList` and `data` fields in the [onReceiveNewInvitation](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnReceiveNewInvitationCallback.html) callback, a student determines that he/she is one of the invitees and the operation is speaking. Then the student calls the [accept](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMSignalingManager/accept.html) API to speak.
   6. If a student speaks, others can receive the [onInviteeAccepted](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnInviteeAcceptedCallback.html) callback, and their systems determine that the data field is speaking and display the list of students who speak.
