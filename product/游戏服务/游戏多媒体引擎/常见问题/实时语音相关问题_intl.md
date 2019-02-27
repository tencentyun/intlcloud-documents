### What gaming scenarios does the Voice Chat service support?
There are mainly three types of applicable scenarios:
- **Microphone order mode:** This mode allows players to join broadcasting in turn with high and fluent sound quality, which is suitable for voice chat-enabled games such as Werewolf.
- **Free call mode:** This mode allows multiple players to speak at the same time with ultra low latency, which is suitable for competitive games such as multi-player team battles.
- **Commanding mode:** This mode is suitable for commander games such as one-to-many command battles and audio interaction with VJ.


### How do I choose the audio type that suits me?
Different application scenarios require different audio types. For details, please see [Sound Quality Selection Document](https://intl.cloud.tencent.com/document/product/607/18522).

### When should I call the Poll function?
Please start calling the Poll function periodically after initializing the SDK.

### The trigger event needs to periodically call the Poll function. Is it okay to start a new thread, wake it up periodically and then call the Poll function?
Our APIs theoretically needs to be called in the same thread. If you choose to call them in a child thread, please be sure to call them in the same child thread, especially for Init and Poll.


### What is an ideal interval for calling the Poll function?
If there are no special requirements, please refer to the relevant settings in the Demo.

### Is there a limit on the number of voice chat rooms or participants in GME?
There is no limits for chat rooms and participants.

### How to troubleshoot failures such as 10001 when entering the room?
The troubleshooting steps are as follows:

1. View and confirm the validity of the parameters in the API for room entering, such as Appid, UIN and AuthBuffer (see the documentation).

2. Check whether the relevant parameters in the console match the local ones.

3. Check whether the console is in arrears.

4. Check the network environment of the developer's testing devices, i.e., whether it is in the developer's private network or a public network.

### Why is Http Invalid id is returned when entering the room?
If your account starts from 0, it is recommended to add 10000 to your account. For example, if your account is 999, the number entered should be 10999.

### What if a network error is returned when entering the room?

The troubleshooting steps are as follows:

1. View and confirm the validity of the parameters in the API for room entering, such as Appid, UIN and AuthBuffer (see the documentation).

2. If they are valid, check the network environment of the developer's testing devices, i.e., whether it is in the developer's private network or a public network.

3. If it is in a private network, ask the developer to check whether the following URL can be connected to: openmsf.3g.qq.com:15000.

4. If yes, check whether the following URL can be connected to: cloud.tim.qq.com:15000.


### Is there an API for room number recycling?
No, after the last participant exits the room, the room will be automatically terminated.

### Is there a requirement for the value of room number?
Room number can be up to 127 characters (null must be entered for the parameter for offline audio room number).



### Is there a requirement for the value of openid?
openid currently supports Int64 type only. Please convert it to a string before passed in to the SDK.


### Can one single openid enter multiple rooms at the same time?
No, an openid can only exist in one room at a time.

### Are the operations for entering and exiting the room async? Can these two APIs be called at the same time?
It is required to call exitroom first and then call enterroom after receiving a callback for successful room exiting.


### What is the timing of member state synchronization? Will there be a notification when entering the room for the first time?
Notifications for audio events have a threshold, and the notification "A member sends an audio packet" will be sent when this threshold is exceeded. If a member of the room does not speak for two seconds, the notification "A member stops sending audio packets" will be sent. There will be a notification when entering the room for the first time.



### Can the microphone volume be set before entering the room?
No, the voice chat-related API ITMGAudioCtrl ITMGAudioEffectCtrl can be called only when in the room.


### When will the microphone permission be occupied?
Microphone permission is occupied after the EnterRoom function is successfully called, during which other programs cannot use the microphone.
Calling EnableMic(false) does not release the microphone occupancy.
If it is required to release, call PauseAudio. After calling PauseAudio, the entire engine will be paused, and ResumeAudio can be called to resume the engine service.


### Is there an API to get the good or bad state of the microphone before calling the EnableMic function?
The API getMicCount can be used to see whether the microphone is usable.


### What solution is suitable for the scenario where it is required that players can talk to one another but viewers can only hear the voice?
The developer should configure the client to make the microphone disabled for viewers.

### What if the sound comes out of the earpiece instead of the speaker after the microphone is enabled on an Android phone?
Grant the "<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />" permission to GME.

### How can the developer judge whether there is music played in the background?
Use the API IsAccompanyPlayEnd().


### When using the SDK, what if music cannot be played back and the sound card of the computer cannot be used in the simulator?
The simulator does not support .mp3.

### Can the SDK play back sound in the earpiece?
Voice Chat does not support the earpiece.

### What formats of local audio files does the SDK support?
.m4a, .wav and .mp3.


### How can GME Voice Chat's range voice mode be accessed? Does range voice have distance attenuation?
For information about how to access range voice, see [Range Voice Document](https://intl.cloud.tencent.com/document/product/607/17972). After range voice is enabled, there is no distance attenuation with the team voice, but the global voice will attenuate as the distance increases. For the attenuation coefficients, see the documentation.


### What are the requirements for the microphone and speaker used by the player in order to achieve 3D sound effect?
The playback client needs to support two sound channels.


### How can GME Voice Chat's 3D sound effect accessed?
For information about how to access Voice Chat's 3D sound effect, see [3D Sound Document](https://intl.cloud.tencent.com/document/product/607/18218).


### What if there is no Authbuffer file in the downloaded SDK documentation and Demo.
Authbuffer file has been merged. Please search for it globally in the SDK.


### Is there a lib file for the tea encryption?
We provide an [Authbuffer compilation document and zip package](https://intl.cloud.tencent.com/document/product/607/30281).


### When will the error ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT appear after disconnection of the network.
It will appear if no heartbeat packets are detected for more than 30 seconds after the network is disconnected.

### Will the blacklist in a room remain valid after exiting the room?
No.

### Does the voice changing effect generate a file?
The voice changing effect is real-time, and no files will be generated for transfer.
