## GME_SDK2.5 6/27/2019
### New features
1. Add APIs to get room member's upstream and downstream volume for real-time voice chat.
2. Add APIs to set recording/playback volume and get recording/playback volume for offline voice.
3. Add APIs to pause and restore recording of offline voice.

### Optimizations
Update error codes for more detailed description.


## GME_SDK2.3.5 3/25/2019
### New features
1. Support Android v8a architecture.
2. Adapt to low latency capture playback on Android.

### Optimizations
Improve stability.

## GME_SDK2.3 1/11/2019
### New features
1.  Support voice message during real-time voice chat.
2.  Support real-time voice filtering and identify information such as horror, violence, porn and politics. 
3.  Support real-time voice chat in HTML5 and enable real-time intercommunication among all platforms.

### Optimizations
1. Optimize the voice range function API of SDK to reduce the integration complexity.
2. Improve the quality of noise suppression on voice.
3. Reduce the memory consumption of using SDK.

## GME_SDK2.2 10/29/2018
### New features
1. Support a variety of karaoke sound effects.
2. Optimize the user experience in super-large rooms with lower latency and higher fluency.
3. Support streaming voice-to-text converting for voice message.
4. Support accompaniment on Windows.

### Optimizations
1. Optimize voice bandwidth, saving your traffic.
2. Optimize CPU and memory performance.

## GME_SDK2.1.5 9/13/2018
### API changes
1. Change the type of parameter roomId in GenAuthBuffer from int32 to string.
2. Change the type of parameter roomId in EnterRoom from int32 to string.
3. Change the function of SetMicVolume from setting the microphone device volume to setting the microphone software volume.
4. Change the function of GetMicVolume from getting the microphone device volume to getting the microphone software volume.

### Optimizations:
1. Upgrade the type of room number from int32 to string.
2. Change the functions of the APIs for setting/getting device volume to setting/getting software volume.
3. Fix bugs to improve stability.


## GME_SDK2.1 8/21/2018
### New features
1. Support voice changing on Windows.
2. Support voice message on Windows.
3. Support 3D sound effect on Windows.
4. Support x86 architecture in Android SDK.
5. Adapt iOS and Mac SDKs to XCode10.

### Optimizations
1. Optimize authentication for voice message.
2. Support turning on/off audio input and output devices separately on mobile devices.
3. Optimize the standard sound quality's immunity to bad network condition.

## GME_SDK2.0 6/22/2018
### New features
1. Support PC Native and PC Unity versions.
2. Support Unreal engine.
3. Support offline voice-to-text converting in up to 120 languages.
4. Support 3D voice chat on PC.

### Optimizations
1. Improve the sound quality of voice chats.
2. Lower the bar for integration, and provide multiple sound quality options - Fluent, Standard, and HD.
3. Improve stability.

## GME_SDK1.2    4/2/2018

### New features
1. Support Cocos engine.
2. Provide the API for adjusting microphone volume.
3. Support team chatting on mobile devices to better support battle royale games.
4. Support accompaniment playback in various formats on PC.
5. Support accompaniment playback in various formats on Android devices.

### Optimizations
1. Optimize the audio pre-processing effect for Werewolf scenarios to deliver a more clear sound quality in multi-person chatting.
2. Optimize the sound quality in online Karaoke and other scenarios and supports configuring higher sound quality.
3. Reduce the voice delay in MOBA scenarios to achieve lower delay in team chatting.
4. Optimize the noise cancellation algorithm to deliver a more clear sound.

## GME_SDK1.1    10/18/2017
### New features
1. Support accompaniments and sound effects in various formats.
2. Add voice message and voice-to-text converting in game scenarios.

### Optimizations
1. Provide the module for authentication of user entering room on client and lowers the bar for integrating SDK.
2. Optimize the howling suppressing effect on iOS/Android.
3. Optimize the sound quality consistency, immunity to bad network condition and other metrics in Werewolf scenario.

### Bug fixes
Fix the system crash issue on Android 4.2 and below.
