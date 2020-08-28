This document describes some basic concepts that may be involved in the use of the TRTC service.

### Application

TRTC manages different businesses or projects in the form of **applications**. You can create different applications for them in the [TRTC Console](https://console.cloud.tencent.com/trtc/app) to isolate their data. Up to 100 TRTC applications can be created under one Tencent Cloud account.

### SDKAppID
`SDKAppID` (application identifier/ID) is a unique ID used by the Tencent Cloud backend to differentiate between different TRTC applications. It is automatically generated when a project is created in the [TRTC Console](https://console.cloud.tencent.com/trtc/app). The data under different `SDKAppID` values is not interconnected.

### UserID

`UserID` (user ID) is used to uniquely identify a user in a TRTC application.

- `UserID` maps a user account in your business system to Tencent Cloud. Usually, you can directly use a username as the `UserID`.
- Its recommended length is below 32 bytes. It can be a combination of case-insensitive letters, digits, and underscores but cannot only contain digits.

### Room

A room is an audio/video space where users can receive each other's real-time audio/video data.

- In TRTC, room is a virtual concept used to separate a group of users from another group.
- A user's audio/video streams can be received only by other users in the same room.
- A user can be in only one room at any time point and can enter another room only after exiting the current room.

>!
- The first user who enters a room will be the room owner, but this user cannot dismiss the room actively.
- After all users actively exit the current room, it will be immediately dismissed on the backend.
- If a user in the room is disconnected exceptionally, the server will remove this user from the room after 30 seconds. If all users in the room are disconnected exceptionally, the server will automatically dismiss the room after 30 seconds.
- When a user attempts to enter a room that does not exist, the backend will create the room first.

### RoomID

`RoomID` (room number/room ID) is used to uniquely identify a room in a TRTC application. It is a number in the uint32 range that is maintained and assigned on your own. It can range between 1 and 4294967295.

### UserSig

`UserSig` (user signature) is a security protection signature designed by Tencent Cloud to authenticate user login, check whether a user is real, and thus prevent attackers from misappropriating your Tencent Cloud service permissions. For more information, please see [How to Calculate UserSig](https://intl.cloud.tencent.com/document/product/647/35166).

### Push
Push is an operation where a user uploads the local audio/video data to the TRTC server, which corresponds to "stream push".

### Subscription
Subscription is an operation where a user requests the TRTC server to pull the audio/video data of a specified user, which corresponds to "stream pull".

### Role

TRTC supports two roles: **anchor** (`TRTCRoleAnchor`) and **viewer** (`TRTCRoleAudience`), which have the following differences:

- An anchor can push the local audio/video data to the server and subscribe to and play back the audio/video data of other anchors from the server.
- A viewer **can only** subscribe to and play back the audio/video data of an anchor from the server.

In call mode, all users in a room are in the anchor role. In live streaming mode, you can categorize users in a room into anchors and viewers based on your actual business needs, and a user can switch the role at any time.

### CDN Live Watching

CDN live watching is also known as "CDN relayed live streaming". UDP audio and video streams in TRTC are converted to RTMP streams by the relayed transcoding clusters in Tencent Cloud, and then are pushed to the standard LVB system and distributed through CDN to viewers. For more information, please see [CDN Live Watching](https://intl.cloud.tencent.com/document/product/647/35242).

### On-cloud Recording

On-cloud (audio/video) recording features based on [LVB](https://intl.cloud.tencent.com/zh/document/product/267) are provided through relayed push during the entire live streaming process. Recording files can be stored in the [VOD](https://intl.cloud.tencent.com/zh/document/product/266) platform to ensure recording reliability and real-timeliness. For more information, please see [On-cloud Recording and Playback](https://intl.cloud.tencent.com/document/product/647/35426).

### On-cloud MixTranscoding

In use cases such as **CDN live watching** and **on-cloud recording**, you may need to mix multiple audio/video streams in a TRTC room into one stream, which can be achieved by using the MCU On-cloud MixTranscoding cluster on the TRTC backend. The MCU cluster can mix multiple audio/video streams as needed and distribute the final output stream to CDN and the on-cloud recording system. For more information, please see [On-cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618).
