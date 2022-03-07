## Adding music during shooting 
<dx-codeblock>
::: java 
// Specify the path of the music to add
mTXCameraRecord.setBGM(path);

// Set the callback (TXRecordCommon.ITXBGMNotify) for music playback
mTXCameraRecord.setBGMNofify(notify);

// Play the music
mTXCameraRecord.playBGMFromTime(startTime, endTime)

// Stop the music
mTXCameraRecord.stopBGM();

// Pause the music
mTXCameraRecord.pauseBGM();

// Resume the music
mTXCameraRecord.resumeBGM();

// Set the volume of the music mixed into other audio of the video
// Volume. The normal volume is 1. We recommend 0-2, but you can set it to a larger value if you want louder music.
mTXCameraRecord.setBGMVolume(x);

// Set the start and end time for music playback. This API must be called before startPlay to take effect.
mTXCameraRecord.seekBGM(startTime, endTime);
:::
</dx-codeblock>

## Adding music during editing
<dx-codeblock>
::: java 
// Set the path of the music to add. If 0 is returned, the setting is successful. Other values indicate failure to set the path due to reasons such as unsupported audio format.
public int setBGM(String path);

// Set the start and end time (ms) for music playback
public void setBGMStartTime(long startTime, long endTime);

// Set whether to loop the music. true: loop; false: do not loop
public void setBGMLoop(boolean looping);

// Set where to start adding the music
public void setBGMAtVideoTime(long videoStartTime);

// Set the audio volume of the video. The value range of the volume parameter is 0-1. 0 means to mute the video, and 1 means to use the original volume.
public void setVideoVolume(float volume);

// Set the volume of the music. The value range of the volume parameter is 0-1. 0 means to mute the music, and 1 means to use the original volume.
public void setBGMVolume(float volume);
:::
</dx-codeblock>

>? After you complete the settings, the music will be played as configured when the video is previewed and will also be added to the video generated.
