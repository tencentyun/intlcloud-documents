## No Sound

### Why is there no sound after two clients entered a voice chat room?

Please check the following for troubleshooting:
1. Whether the two clients have successfully entered the room.
2. Whether the two clients have entered the same room.
3. Whether the two clients have entered using the same `OpenId`.
4. Whether their microphones have been allowed to use and enabled on the main thread.
5. Whether the two clients have blocked each other.

### After I entered a room on an iPhone, I can't hear other members speaking. How to fix it?

Please check whether the mute switch on iPhone is on.

### After I entered a room, my mobile phone volume level becomes very low, and then it becomes very high after I turned on the microphone. How to fix it?

A mobile phone's volume can be divided into media volume and call volume. If you don't enable the microphone before entering a room, the media volume will be used by default. In this case, when the media volume is low, even if the call volume is high, the actual volume will be low. Therefore, you need to ensure that the media volume is appropriate. Similarly, if the volume becomes high after the microphone is enabled, you need to adjust the mobile phone's call volume.

### After exporting the APK to an Android mobile phone, when I enable the microphone, an error message pops up indicating that the phone has no microphone permission. How to fix it?

The permission management is of the system operations of the mobile phone. Please troubleshoot by following the steps below:
1. Please make sure that the microphone permission is included in the `AndroidManifest`.
2. You can apply for the microphone permission through the code.


## Audio

### Why is there a harsh noise when two devices with enabled microphones nearing each other?

This is a screeching noise that is common in phone calling scenarios as well. In real gaming scenarios, it is not likely that two players near each other would communicate through their microphones, so the audio is enhanced by default for better audio reach.

Generally, it may happen a lot during program development rather than real use cases, as people can directly speak to whom in front of them.

### I can still hear sound in the room after I turned on the mute switch on an iPhone. How to fix it?

You should configure `AVAudioSession` in Xcode for the mute switch to work.

### The sound comes out of the receiver instead of the speaker after the microphone is enabled on an Android mobile phone. How to fix it?

Grant the `&lt;uses-permission android:name=&quot;android.permission.MODIFY_AUDIO_SETTINGS&quot; /&gt;` permission to GME.

### How to enable the speaker instead of the receiver by default after integrating the SDK?

It's automatically set so by default.

### Does the SDK support playing sound from receiver?
No.

### How to only allow two room members to talk to each other while others can only listen to them?

You can implement a feature on the client that prevents other members from enabling their microphones.

### How do I remind users if they have no available microphones?

You can use the `GetMicListCount` API to get the number of microphones.

### Can I set the microphone volume before entering a room?

No. The voice chat APIs such as `ITMGAudioCtrl` and `ITMGAudioEffectCtrl` can be used only when you are in the room.

### How do I get and release the microphone permission?

- You can get the microphone permission after calling the function `EnterRoom` successfully, and other programs cannot capture the audio data from the microphone then.
- Calling the function `EnableMic(false)` does not release the microphone.
- Please call `PauseAudio` if you need to release the microphone, and then the entire engine will be paused and can be resumed by calling `ResumeAudio`.

### Is there an API to obtain the microphone status before the function `EnableMic` is called?

The API `getMicCount` can be used to check whether the microphone is available.

### How often can the microphone volume be reported?

The `GetMicLevel` API collects the volume every 20 milliseconds. Therefore, you can get the volume information as frequently as every 20 milliseconds.

### How can I determine whether music is played in the background?

Use the API `IsAccompanyPlayEnd()`.

### After I entered a room, the accompaniment can only be played back when my microphone is on. How to fix it?

After entering a room, you can call `EnableAudioCaptureDevice`, play back the accompaniment, and then call `EnableAudioSend` to control audio up- and downstreaming. For more information, please see [Accompaniment in Voice Chat](https://intl.cloud.tencent.com/document/product/607/31504).

### Why does sound stutter?

- **Music stutter**: a host plays music using a speaker, and captures and broadcasts the audio through another phone. This will inevitably cause stutter, so we recommend the host to use a headset.
- **Network stutter**: the audience will experience stutter when the upstream packet loss rate is too high or the upstream latency fluctuates greatly.
- It needs to be determined whether the stutter occurs in the sound itself or is caused by the sound transfer latency.

### What are the requirements for the microphone and speaker to achieve the 3D sound effect?

Dual-channel playback is required.
