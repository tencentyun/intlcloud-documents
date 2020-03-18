## APPID

You can view the APPID for the Tencent Cloud account in the Tencent Cloud Console’s [Account Information](https://console.qcloud.com/developer).

## Application

An application is a service that a developer creates on the TRTC Console. The data of different applications is not interconnected. For details on the application creation procedure, see the step on creating an application in Activating a Service.
> You can create more than one TRTC application under a single Tencent Cloud account.

## SDKAPPID

SDKAPPID (application ID) is a unique ID used by the Tencent Cloud backend to differentiate between different TRTC applications. It is automatically generated when a project is created on the TRTC Console. The data of different SDKAPPIDs is not interconnected. 

## User ID
User ID is used to uniquely identify a user in a TRTC application.
- User ID represents the mapping of the user's account ID for logging in to developer business system to the Tencent Cloud. Usually, the developer can just directly use their User Name as the User ID.
- The recommended length is not more than 32 bytes. It should be a combination of numbers, letters, and underscores. It cannot be all numbers, and it is case insensitive.

## UserSig

UserSig (user signature) is used for verification for the login authentication of users to make sure that the user’s identity is authentic. The UserSig generation method is explained in the [Generating a Signature](https://intl.cloud.tencent.com/document/product/647/35166) documentation.

## Room

A room is an audio/video space where users can access each other’s real-time videos as long as they are in the same room.

- In TRTC, room is a virtual concept used to separate a group of users from another.
- A user's video is only accessible to the other users in the same room.
- A user can only enter one room at a time, so if a user wants to enter another room, they have to exit the previous room first.

>
- The user who first creates a room is the room owner, but this user does not have the ability to close the room.
- When all users actively exit a room, the server will immediately close the room.
>- If a single user disconnects due to an exception, the server will clear this user from the room after 30 seconds. If all users are disconnected due to an exception, the server will automatically close the room after 30 seconds.
>- When a user wants to enter a room that does not exist, the TRTC backend creates the room first, and then adds the user to the room.

## Room ID

Room ID (room number) is used by the TRTC service to uniquely identify a room. The Room ID is a number in the uint32 range that is maintained and assigned by the developer. 

## Private Map Key

Private Map Key (room ticket) is a credential used for permission verification when users enter a room, making it equivalent to the key for entering the specified room (Room ID). The Private Map Key is usually used for protecting room entry permissions and to implement room entry restriction. It is issued by the developer’s project server, and its generation method is explained in the [Room Entry Permissions Protection](https://intl.cloud.tencent.com/document/product/647/35157) documentation.

## Relayed Live Streaming

Relayed live streaming is a style of live broadcasting that is usually used for data forwarding between audio/video systems with different protocols. The TRTC server pushes the audio/video data within a chat room to the cloud LVB service through RTMP push, thereby implementing the features of relayed live streaming, relayed push, stream mixing on the cloud, and recording on the cloud.

## Cloud LVB Service Terminology

When you need to use relayed live streaming or CDN pull, the services of [Cloud LVB](https://intl.cloud.tencent.com/document/product/267) such as push, stream mixing, recording, transcoding, and delivery will need to be used.

### BIZID

BIZID is an identifier used to differentiate LVB applications in the cloud LVB service. After activating automatic relayed live streaming or activating relayed live streaming automatic recording in the TRTC Console, select a previously created application and click **Account Information** to obtain the BIZID information in “LVB Information”.

### Stream ID

When you have activated the cloud LVB services of relayed live streaming, recording on the cloud, stream mixing on the cloud, and CDN delivery, it means you need to use stream ID. The stream ID calculation rules when TRTC service implements relayed push are [bizid]\_[MD5(roomid_userid_streamtype)] , and you can read the [Independent Image](https://intl.cloud.tencent.com/document/product/647/34617#.E6.AD.A5.E9.AA.A42.EF.BC.9A.E7.8B.AC.E7.AB.8B.E7.94.BB.E9.9D.A2) documentation to learn about the details of the calculation rules for relayed pull stream ID.

### LVB Stream Address

LVB stream addresses are divided into push addresses and pull addresses, which are both mapped using stream ID. When you activate the cloud LVB services of relayed live streaming, recording on the cloud, stream mixing on the cloud, and CDN delivery, you will need to use the LVB stream address.
- A push address uses the format of `rtmp://yourpushdomain.com/appname/streamname?auth=xxxxx`.
- Pull addresses have different formats based on their different types.
	- RTMP type: `rtmp://yourpulldomain.com/appname/streamname?auth=xxxxxx`.
	- HTTP - FLV type: `http://yourpulldomain.com/appname/streamname.flv?auth=xxxxxx`.
	- HLS type: `http://yourpulldomain.com/appname/streamname.m3u8?auth=xxxxxx`.

> 
>- A push address is only used for upstream data, and a pull address is only used for downstream data. Mixing them up could cause unpredictable problems.
>- Pull playback can only be done after first doing push.
>- As required by the authorities, push domain names and playback domain names can only be used in mainland China after [Self Configuration](https://intl.cloud.tencent.com/document/product/267/20381) by the developer.


### Stream Mixing on the Cloud

Stream mixing on the cloud is mixed stream transcoding service provided by cloud LVB. It can mix the data of single-channel or multi-channel LVB stream IDs under the same BIZID to the specified stream ID. By using stream mixing on the cloud, you can implement the scenario features of co-anchoring and cross-room PK. You can read its description in the [On-Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618) documentation. If you need more details for custom configuration, you can implement more refined parameter configuration of stream mixing using [RESTAPI for Stream Mixing on the Cloud](https://intl.cloud.tencent.com/document/product/267/8832).

### Video Recording

Video recording is a recording service provided by Tencent Cloud LVB that can record stream ID data to the [Cloud VOD](https://intl.cloud.tencent.com/document/product/266) service. You can read its description in the [Cloud Video Recording](https://intl.cloud.tencent.com/document/product/647/35152) documentation.

## TRTC Version 1 Specialized Terminology

The following are explanations of the specialized terminology for TRTC version 1. You can read about the differences between V1 and V2 and about the upgrading in the Old Version (iLiveSDK) Upgrading documentation.

### Account Type
Account Type is the account type used to log in to a TRTC application in TRTC version 1. It is automatically assigned for user authentication after the creation of the TRTC application. It is not required to be used in version 2.

### Role

A role is a set of parameters used to manage audio/video parameter configuration (including resolution and capture frame rate) in TRTC version 1. You can create and configure roles under **Image Settings (old version SDK)** in the TRTC Console. It is not required to be used in version 2.

### Role Name

After the role parameters sets are created by a specific terminal platform integrated in TRTC version 1, you can name this set of parameter configuration in the TRTC Console. This name is the role name. After users turn on the camera or mic and uplink the audio/video stream in a room and start to stream data, the role to be used when entering the room can be specified using the role name to confirm the parameters for streaming data. This is not required to be used in version 2.


>
>- When entering a room, if a user uses a role name that has not been configured in the console, he/she can still enter the room with the default role.
>- After entering the room, you can change the role by calling the API used for switching role.
>- Switching to a non-existent role using the API will cause a failure callback.
>- After the role configuration is modified, logging in to the client again is required to make the new configuration take effect (the SDK will fetch the configuration from the backend when login is successful. The failure to fetch the configuration can cause the failure to find the role).

### Group

The group system in TRTC version 1 use the Tencent Cloud [Instant Messaging IM](https://intl.cloud.tencent.com/document/product/1047) service’s [Group](https://intl.cloud.tencent.com/document/product/1047/1502) feature.
> Group and room are two completely different concepts that should not be confused with each other.

### Message

Information that is independently sent and received one time is called a message in TRTC version 1. In iLiveSDK, messages are described using the ILiveMessage class. There are three main types: text messages, custom messages, and other messages. For details, refer to [Instant Message Formats](https://intl.cloud.tencent.com/document/product/1047/2720)
