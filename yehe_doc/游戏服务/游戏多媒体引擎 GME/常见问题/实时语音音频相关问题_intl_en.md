### How do I choose the audio type that suits me?

Different application scenarios require different audio types. For more information, see [Sound Quality Selection](https://intl.cloud.tencent.com/document/product/607/18522).
The first user entering the room determines the room's audio type, which will be applied to subsequent users entering the room. To change the room audio type, please call the `ChangeRoomType` API.

### What should I do if the mobile phone volume level becomes very low after room entry but becomes very high after the mic turns on?

A mobile phone's volume can divide into media volume and call volume. If the mic is not enabled during room entry, the media volume will be used by default. In this case, when the media volume level is low, even if the call volume is high, the actual volume level will be low. You need to ensure that the media volume level is appropriate. Similarly, if the volume level becomes low after the mic is enabled, you need to adjust the mobile phone's call volume.

### What should I do if I cannot hear other users speaking after entering a room on iPhone?

Please check whether the mute switch on the side of iPhone is on.


### What should I do if I can still hear sound in the room after I turn on the mute switch on iPhone?

You should configure AVAudioSession in XCode for the mute switch to work.


### What should I do if the sound comes out of the receiver instead of the speaker after the microphone is enabled on Android?

Grant the `&lt;uses-permission android:name=&quot;android.permission.MODIFY_AUDIO_SETTINGS&quot; /&gt;` permission to GME.


### How do I set enabling speaker instead of receiver by default after integrating the SDK?

It’s automatically set so by default.

### Does the SDK support playing sound from receiver?

No, it does not.


### How do I implement the scenario where only two members in a room can talk to each other while other members can only listen to them?

The developer can implement a feature on client that prevents other members from enabling the microphone.

### How do I remind a user that no local mic is available?

`GetMicListCount` can be used to get the number of mics, so you can use this API for checking.

### Can the microphone volume be set before a user enters a room?

No. The voice chat API `ITMGAudioCtrl ITMGAudioEffectCtrl` can be called only when the user is in the room.


### How do I get and release the microphone permission?

- You can get the microphone permission after calling the function `EnterRoom` successfully, and other programs cannot capture audio data from the microphone during your use of microphone.
- Calling `EnableMic(false)` does not release the microphone.
- If it is required to release the microphone, call `PauseAudio`. After that, the entire engine will be paused. To resume it, call `ResumeAudio`.


### Is there an API to obtain the microphone status before the function `EnableMic` is called?

The API `getMicCount` can be used to check whether the microphone is available.

### How often can the mic volume level be returned when the GME method for getting the real-time volume level is used?

The `GetMicLevel` API collects the volume level once every 20 milliseconds. Therefore, you can get the volume level as frequently as once every 20 milliseconds at most.

### How can the developer determine whether there is music played in the background?

Use the API `IsAccompanyPlayEnd()`.

### How to avoid the situation where if I enter a room and play back accompaniment with my microphone on, then the accompaniment will stop when I turn off my microphone?

After entering a room, try to call `EnableAudioCaptureDevice`, play back the accompaniment, and then call `EnableAudioSend` to control audio up- and downstreaming. For more information, see [Accompaniment in Voice Chat](https://intl.cloud.tencent.com/document/product/607/31504).


### What formats of local audio files does the SDK support?

The SDK supports M4A, WAV, and .MP3 formats.


### When the SDK is used, why cannot music be played back and the sound card of the computer cannot be used in the simulator?

The simulator does not support MP3.


### Are files generated when the voice changing effect is enabled?

The voice changing effect is real-time. No files will be generated and sent.

### How can GME Voice Chat's range voice mode be accessed? Does range voice have distance attenuation?

For more information on how to access range voice, see [Range Voice](https://intl.cloud.tencent.com/document/product/607/17972). After the range voice is enabled, there is no distance attenuation in the same team, but the global voice will attenuate as the distance increases. For the attenuation coefficients, see the documentation.


### What are the requirements for microphone and speaker to achieve 3D sound effect?

Dual-channel output devices are required to realize 3D sound effect.


### How do I access 3D sound effect of GME Voice Chat?

For more information on how to access Voice Chat's 3D sound effect, see [3D Sound Effect](https://intl.cloud.tencent.com/document/product/607/18218).


### What are the main reasons for sound stutter?

-  **Stutter during music playback:** the host plays music using speaker on a phone, and captures and broadcasts audio through another phone. (This can inevitably cause stutter, so it is recommended for the host to use a headset).
-  **Network stutter**: the audience will experience the stutter when the upstream packet loss rate is too high or the upstream latency fluctuates greatly.
-  You need to determine whether the lagging occurs in the sound itself or is caused by the sound transfer latency.
