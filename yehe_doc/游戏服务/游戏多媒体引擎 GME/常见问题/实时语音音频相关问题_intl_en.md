### How do I choose the audio type that suits me?
Different application scenarios require different audio types. For more information, please see [Sound Quality Selection](https://intl.cloud.tencent.com/document/product/607/18522).
The first user entering the room determines the room's audio type, which will be applied to subsequent users entering the room. To change the room audio type, please call the `ChangeRoomType` API.

### What should I do if the mobile phone volume level becomes very low after room entry but becomes very high after the mic turns on?
A mobile phone's volume can divide into media volume and call volume. If the mic is not enabled during room entry, the media volume will be used by default. In this case, when the media volume level is low, even if the call volume is high, the actual volume level will be low. You need to ensure that the media volume level is appropriate. Similarly, if the volume level becomes low after the mic is enabled, you need to adjust the mobile phone's call volume.

### What should I do if I cannot hear other users speaking after entering a room on iPhone?
Please check whether the mute switch on the side of iPhone is on.

### What if the sound comes out of the receiver instead of the speaker after the mic is enabled on an Android phone?
Grant the `&lt;uses-permission android:name=&quot;android.permission.MODIFY_AUDIO_SETTINGS&quot; /&gt;` permission to GME.


### How do I set enabling speaker instead of receiver by default after integrating the SDK?
The speaker is enabled by default in GME.

### Can the SDK play back sound in the receiver?
Voice chat does not support the receiver.


### How do I implement the scenario where only two members in a room can talk to each other while other members can only listen to them?
You should configure the client so that mic cannot be enabled by other members.

### How do I remind a user that no local mic is available?
`GetMicListCount` can be used to get the number of mics, so you can use this API for checking.

### Can I set the mic volume level before room entry?
No, the voice chat API `ITMGAudioCtrl ITMGAudioEffectCtrl` can be called only after room entry.


### When will the mic be occupied?
- Mic is occupied after the `EnterRoom` function is successfully invoked, during which other applications cannot use the mic.
- Calling `EnableMic(false)` does not release the mic.
- If it is required to release the mic, call `PauseAudio`. After `PauseAudio` is called, the entire engine will be paused, and `ResumeAudio` can be called to resume the engine service.


### Is there an API to get the mic status before the `EnableMic` function is invoked?
The `getMicCount` API can be used to see whether the mic is available.

### How often can the mic volume level be returned when the GME method for getting the real-time volume level is used?
The `GetMicLevel` API collects the volume level once every 20 milliseconds. Therefore, you can get the volume level as frequently as once every 20 milliseconds at most.

### How can I determine whether there is music played in the background?
Use the `IsAccompanyPlayEnd()` API.


### What formats of local audio files does the SDK support?
The SDK supports the .m4a, .wav, and .mp3 formats.


### When the SDK is used, what if music cannot be played back and the sound card of the computer cannot be used in the simulator?
The simulator does not support .mp3.


### Does the voice changing effect generate a file?
The voice changing effect is real-time, and no files will be generated for transfer.

### How can GME voice chat's range voice mode be accessed? Does range voice have distance attenuation?
For more information on how to access range voice, please see [Range Voice](https://intl.cloud.tencent.com/document/product/607/17972). After range voice is enabled, there is no distance attenuation for team voice, but the global voice will attenuate as the distance increases. For the attenuation coefficients, please see the documentation.


### What are the requirements for the mic and speaker in order to achieve 3D sound effect?
The playback client needs to support dual-channel.


### How can GME voice chat's 3D sound effect be accessed?
For more information on how to access voice chat's 3D sound effect, please see [3D Sound](https://intl.cloud.tencent.com/document/product/607/18218).


### What are the main causes for sound lagging?
- **Poor sound source:** for example, the host uses an external device to play back music and uses a mobile phone to capture the sound for live streaming (lagging is inevitable in this case, and the host is recommended to use earphones).
- **Poor network connection:** viewers will hear lagged sound if the upstream packet loss rate is too high or the upstream latency fluctuates greatly.
- You need to determine whether the lagging occurs in the sound itself or is caused by the sound transfer delay.
