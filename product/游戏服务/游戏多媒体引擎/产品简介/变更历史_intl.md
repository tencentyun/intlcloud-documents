## GME_SDK2.3 2019-01-11

### New features:
1.  Support the use of offline voice message during real-time voice chat.
2.  Support real-time voice filtering that is able to identify horror, violence, porn and politics-related information. 
3.  Support real-time voice in HTML5, allowing real-time intercommunication among all platfoms.

### Optimizations:
1. Optimize the voice range function API of SDK to reduce the integration complexity.
2. Improve the quality of noise suppression on voice.
3. Reduce the memory consumption of SDK.

## GME_SDK2.2 2018-10-29

### New features:
1. Support a variety of karaoke sound effects.
2. Optimize the user experience in large rooms with lower latency and higher fluency.
3. Support streamlined voice-to-text conversion for office voice message.
4. Support music accompaniment on Windows.

### Optimizations:
1. Optimize voice bandwidth and save traffic.
2. Optimize CPU and memory performance.

## GME_SDK2.1.5 2018-09-13

### API Changes:

1. Change the type of parameter roomId in GenAuthBuffer from int32 to string.
2. Change the type of parameter roomId in EnterRoom from int32 to string.
3. Change the function of SetMicVolume from setting the microphone device volume to setting the microphone software volume.
4. Change the function of GetMicVolume from getting the microphone device volume to getting the microphone software volume.

### Optimizations:

1. Upgrade the type of room number from int32 to string.
2. Change the functions of the APIs for setting/getting device volume to setting/getting software volume.
3. Fix bugs to improve stability.


## GME_SDK2.1 2018-08-21

### New features:

1. Support voice changing on Windows.
2. Support voice message on Windows.
3. Support 3D sound effect on Windows.
4. Support x86 architecture in Android SDK.
5. iOS and Mac SDKs are adapted to XCode10.

### Optimizations:

1. Optimize authentication for voice message.
2. Support turning on/off audio input and output devices separately on mobile devices.
3. Optimize the standard sound quality's immunity to bad network condition.

## GME_SDK2.0 2018-06-22

### New features:

1. PC Native and PC Unity versions of GME are made available.
2. GME supports Unreal engine.
3. Offline voice-to-text conversion is supported in up to 120 languages in GME.
4. GME supports 3D voice chat on PC.

### Optimizations:

1. Improve the sound quality of voice chats.
2. Simplify integration and provide multiple sound quality options - Fluent, Standard, and HD.
3. Improve stability.

## GME_SDK1.2    2018-04-02

### New features

1. GME supports Cocos engine.
2. Provide the API for adjusting microphone volume.
3. Support team chatting on mobile devices to better support battle royale games.
4. Support music accompaniment playback in various formats on PC.
5. Support music accompaniment playback in various formats on Android devices.

### Optimizations

1. Optimize the audio pre-processing effect for Werewolf scenarios to deliver better sound quality in multi-person chatting.
2. Optimize the sound quality in online Karaoke and other scenarios and support configuring better sound quality.
3. Reduce the voice delay in Moba scenarios to achieve lower delay in team chatting.
4. Optimize the noise cancellation algorithm to deliver a clearer sound.

## GME_SDK1.1    2017-10-18

### New features

1. Game SDK supports accompaniments and sound effects in various formats.
2. Add voice message and voice-to-text conversion in game scenarios.

### Optimizations

1. Provide the module for user authentication on client and simplify SDK integration.
2. Optimize the howling suppressing effect on iOS/Android.
3. Optimize the sound quality consistency, immunity to bad network condition and other metrics in Werewolf scenario.

### Fixes

Fixes the system crash issue on Android 4.2 and below.






