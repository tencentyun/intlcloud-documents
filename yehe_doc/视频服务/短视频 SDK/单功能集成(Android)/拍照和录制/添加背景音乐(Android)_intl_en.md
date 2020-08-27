## Adding Background Music During Shooting 

```
// Set the background music file path
mTXCameraRecord.setBGM(path);

// Set the callback for background music playback (TXRecordCommon.ITXBGMNotify)
mTXCameraRecord.setBGMNofify(notify);

// Play back the background music
mTXCameraRecord.playBGMFromTime(startTime, endTime)

// Stop the background music
mTXCameraRecord.stopBGM();

// Pause the background music
mTXCameraRecord.pauseBGM();

// Resume the background music
mTXCameraRecord.resumeBGM();

// Set background music volume level. This API is used to control the background music volume level during playback
// Volume level. 1 indicates the normal volume level. The recommended value range is 0–2. If you want to increase the background music volume level, you can set a higher value
mTXCameraRecord.setBGMVolume(x);

// Set the start and end positions for background music playback
mTXCameraRecord.seekBGM(startTime, endTime);
```

## Adding Background Music During Editing

```
// Set the background music file path. If 0 is returned, the path is successfully set. Other returned values indicate a failure, such as unsupported audio format
public int setBGM(String path);

// Set the start and end time for background music playback in milliseconds
public void setBGMStartTime(long startTime, long endTime);

// Set whether to loop the background music. true: yes; false: no
public void setBGMLoop(boolean looping);

// Set the start position where the background music is to be added in the video
public void setBGMAtVideoTime(long videoStartTime);

// Set the video volume level. `volume` indicates the audio volume level, and its value ranges from 0 to 1. 0 indicates muted, and 1 indicates the original volume level
public void setVideoVolume(float volume);

// Set the background music volume level. `volume` indicates the audio volume level, and its value ranges from 0 to 1. 0 indicates muted, and 1 indicates the original volume level
public void setBGMVolume(float volume);
```

>?After you set the background music, when you start the editor for video preview, the background music will be played back according to the configured parameters. After you start the editor for video generation, the background music will be composed into the generated video according to the configured parameters.
