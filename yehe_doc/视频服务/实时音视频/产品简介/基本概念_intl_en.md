This document explains some of the basic concepts you may encounter while using TRTC services.

### Application

In TRTC, business and projects are managed with **applications**. You can create different applications for your projects in the [TRTC console](https://console.cloud.tencent.com/trtc/app) to separate their data. Each Tencent Cloud account can create up to 100 TRTC applications.

### SDKAppID
Tencent Cloud uses `SDKAppID` (application ID) to uniquely identify TRTC applications. It is generated automatically when you create an application in the [TRTC console](https://console.cloud.tencent.com/trtc/app). Applications that do not have the same `SDKAppID` cannot communicate data with each other.

### UserID

UserID (user ID) uniquely identifies a user in a TRTC application.

- `UserID` is a mapping of the user accounts of your project in Tencent Cloud. Normally, you can use a username as `UserID`.
- `UserID` should preferably be 32 bytes or shorter. It can contain digits, underscores, and letters (case sensitive).

### Room

A room is a space where users can receive each other’s audio and video data in real time.

- Rooms are virtual spaces TRTC uses to separate one user group from another.
- Only users in the same room can receive each other’s audio and video.
- A user can be in only one room at a time. A user who is already in a room must exit the room before they can enter another.

>!
>- The first user who enters a room is the owner of the room. Room owners cannot close rooms manually.
>- In call modes, TRTC closes a room when all users leave the room.
>- In live streaming modes, if the last user who exits a room is an anchor, TRTC will close the room immediately; if the user is an audience member, TRTC will close the room after 10 minutes.
>- A user is removed from a room 90 seconds after an unexpected disconnection occurs. If all users are disconnected, the room is closed after 90 seconds. **The waiting time after a disconnection occurs is also billed**.
>- If a user attempts to enter a room that does not exist, TRTC creates a room automatically.

### Room ID

`RoomID` (room number/ID) uniquely identifies a room in a TRTC application. It is a UInt32 number that you assign to a room and maintain. Its value range is 1-4294967295.

### UserSig

`UserSig` (user signature) is a security signature designed by Tencent Cloud to authenticate user logins and verify that a user is real. It helps prevent attackers from accessing your Tencent Cloud account. For more information, see [FAQs > UserSig](https://intl.cloud.tencent.com/document/product/647/35166).

### Push
Push is the operation in which a user uploads local audio/video data to the TRTC server.

### Subscription
Subscription is the operation in which a user sends a request to the TRTC server to pull the audio/video data of a specified user.

### Role

In TRTC, users can have either of two roles: **anchor** (`TRTCRoleAnchor`) and **audience** (`TRTCRoleAudience`).

- An anchor can push local audio/video data to the server. They can also subscribe to and play back the audio/video data of other anchors.
- Audience members **can only** subscribe to and play back the audio/video data of anchors.

In call modes, all users in a room have the anchor role. In live streaming modes, users in a room can be either anchors or audience memebers. A user can switch roles as needed.

### CDN Live Watching

CDN live watching is also known as CDN relayed live streaming. TRTC uses relayed transcoding clusters to convert its UDP audio/video streams into RTMP streams in the cloud. The streams are then pushed to a standard live streaming system and distributed through CDNs to the audience. For details, see [CDN Relayed Live Streaming](https://intl.cloud.tencent.com/document/product/647/35242).

### On-cloud recording

TRTC leverages the capabilities of [CSS](https://intl.cloud.tencent.com/document/product/267) to record entire audio/video calls in the cloud. Recording files are securely saved in real time to [VOD](https://intl.cloud.tencent.com/document/product/266). For details, see [On-Cloud Recording and Playback](https://intl.cloud.tencent.com/document/product/647/35426).

### On-Cloud MixTranscoding

In scenarios such as **CDN live watching** and **on-cloud recording**, you may need to mix multiple audio/video streams in a TRTC room into one stream. This can be achieved using TRTC’s stream mixing and transcoding MCU cluster. The MCU cluster can mix multiple audio/video streams as needed and distribute the mixed stream to live streaming CDNs and the on-cloud recording system. For more information, please see [On-Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618).


### Dumb terminal
A user entering a room on a dumb terminal will not be detected by the SDK, and remote users will not receive notifications when the user enters or exits the room.
