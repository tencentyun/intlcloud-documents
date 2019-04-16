### What gaming scenarios does the Voice Chat service support?
There are mainly three types of applicable scenarios:
- **Broadcasting-in-sequence mode:** This mode allows players to join broadcasting in turn with high and fluent sound quality, which is best suited for voice chat-enabled games such as Werewolf.
- **Multi-person video mode:** This mode allows multiple players to speak at the same time with ultra low latency, which is best suited for competitive games such as multi-player team chat.
- **Commanding mode:** This mode is best suited for commander games such as one-to-many command battles and audio interaction with VJ.


### How do I choose an audio type that works best for me?
Different application scenarios require different audio types. For more information, see [Sound Quality Selection](https://cloud.tencent.com/document/product/607/18522).

### When should I call the Poll function?
Call the Poll function periodically after initializing the SDK.

### As calling the poll function periodically is required for triggering events, can I start a new thread, wake it up periodically and then call the Poll function?
Theoretically, all of our APIs need to be called in the same thread. If you choose to call them in a child thread, make sure to call them in the same child thread, especially for Init and Poll.


### How frequent should I call the poll function?
Call the poll function as described in Demo if there is no special requirement.

### Is there a limit on the number of voice chat rooms and members in GME?
There is no limits for chat rooms and members.

###  If an error code such as 10001 is returned when entering the room? How do I troubleshoot?
Follow the steps below for troubleshooting:
1. View and confirm the validity of the parameters in the API for room entering, such as Appid, UIN and AuthBuffer (see the documentation).
2. Check whether the relevant parameters in the console match the local ones.
3. Go to Console and check whether your account is in arrears.
4. Check whether the network environment of the developer's testing devices is a private network or a public network.


### Why is HTTP Invalid ID returned when I enter a room?
If your account ID starts from 0, it is recommended to add 10000 to your account ID. For example, if your account ID is 999, the number entered is 10999.

### What if a network error is returned when I enter a room?
Follow the steps below for troubleshooting:
1. View and confirm the validity of the parameters in the API for room entering, such as Appid, UIN and AuthBuffer (see the documentation).
2. If they are valid, check whether the network environment of the developer's testing devices is a private network or a public network..
3. If it is a private network, ask the developer to check whether the following URL can be connected to: openmsf.3g.qq.com:15000.
4. If yes, check whether the following URL can be connected to: cloud.tim.qq.com:15000.


### Is there an API for reclaiming room ID?
No. After the last member exits the room, the room is terminated automatically.

### Is there a requirement for the value of room ID?
Room ID is up to 127 characters (for voice message, enter "null").

### How do I call the API if I enter a room immediately after exiting it?
If a user enters the room immediately after exiting a room in the application, the developer does not have to wait for the RoomExitComplete notification as a callback of ExitRoom in the API call process, but just calls the API directly.

### Is there a requirement for the value of openid?
Only a 64-bit unsigned integer is allowed for openid. Convert it to a string before passing it to SDK.


### Can I enter multiple rooms at the same time using a single openid?
No. You can only enter one room using one openID at a time.

### Are the operations for entering and exiting the room async? Can these two APIs be called at the same time?
You need to call exitroom first, and then call enterroom after receiving a callback indicating exitroom operation is successful.


### When is the member status synced? Will a user receive a notification when entering the room for the first time?
Notifications for audio events are triggered when reaching a preset threshold. The notification that "A member sends an audio packet" is sent when this threshold reached. If a room member does not speak for two seconds, the notification "A member stops sending audio packets" will be sent. There is a notification when a user enters the room for the first time.



### Can the microphone volume be set before a user enters a room?
No. The voice chat-related API ITMGAudioCtrl ITMGAudioEffectCtrl can be called only when the user is in the room.


### How do I get and release the microphone permission?
You can get the microphone permission after calling the function EnterRoom successfully, and other programs cannot capture audio data from the microphone during your use of microphone.
Calling EnableMic(false) does not release the microphone.
If it is required to release the microphone, call PauseAudio. After PauseAudio is called, the entire engine will be paused, and ResumeAudio can be called to resume the engine service.


### Is there an API to obtain the microphone status before the function EnableMic is called?
The API getMicCount can be used to check whether the microphone is available.


### What should I do if I don't want the viewers listening to the chat between players to join the chat?
The developer can implement a feature on client that prevents other viewers from enabling the microphone.

### What should I do if the sound comes out of the receiver instead of the speaker after the microphone is enabled on Android?
Grant the "<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />" permission to GME.

### How can the developer determine whether there is music played in the background?
Use the API IsAccompanyPlayEnd().


### When using the SDK, what if music cannot be played and the sound card of the computer cannot be used in the simulator?
The simulator does not support mp3.

### Does the SDK support playing sound from receiver?
The voice chat service does not support receiver.

### What formats of local audio files does the SDK support?
m4a, wav, and mp3.


### How can GME Voice Chat's range voice mode be accessed? Does range voice have distance attenuation?
For more information on how to access range voice, see the [Range Voice](https://cloud.tencent.com/document/product/607/17972) document. After the range voice is enabled, there is no distance attenuation in the same team, but the global voice will attenuate as the distance increases. For the attenuation coefficients, see the documentation.


### What are the requirements for the microphone and speaker used by the player in order to achieve 3D sound effect?
Dual-channel output devices are required to realize 3D sound effect.


### How do I access 3D sound effect of GME Voice Chat?
For more information on how to access Voice Chat's 3D sound effect, see [3D Sound Effect](https://cloud.tencent.com/document/product/607/18218).


### What do I do if there is no Authbuffer file in the downloaded SDK documentation and Demo?
The Authbuffer file has been incorporated into another file. Please search for it globally in the SDK.


### Is the lib file available for TEA encryption?
[Authbuffer compiled document and zip package](https://cloud.tencent.com/document/product/607/30281) are provided.


### When does the error ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT occur after disconnection of the network.
This occurs if no heartbeat packet is received within 30 seconds after the network is disconnected completely.

### Will the blacklist in a room remain valid after I exit the room?
No.

### Are files generated when the voice changing effect is enabled?
The voice changing effect is real-time. No files will be generated and sent.
