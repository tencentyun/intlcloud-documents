## Adding Background Music During Shooting 
```objc
// Get the `recorder` object
TXUGCRecord *recorder =  [TXUGCRecord shareInstance];

// Set the background music file path
[recorder setBGMAsset:path];

// Set the background music. If the music file is loaded from the system media library, you can directly pass in the corresponding `AVAsset`
[recorder setBGMAsset:asset];

// Play back the background music
[recorder playBGMFromTime:beginTime
                   toTime:endTime
          withBeginNotify:^(NSInteger errCode) {
      // Callback for the start of playback. If `errCode` is 0, it is a success; otherwise, it is a failure
     } withProgressNotify:^(NSInteger progressMS, NSInteger durationMS) {
      // progressMS: duration of the part that has been played back. durationMS: total duration
      } andCompleteNotify:^(NSInteger errCode) {
      // Callback for the end of playback. If `errCode` is 0, it is a success; otherwise, it is a failure
      }];

// Stop the background music
[recorder stopBGM];

// Pause the background music
[recorder pauseBGM];

// Resume the background music
[recorder resumeBGM];

// Set mic volume level. It is used to adjust the mic volume level when background music is played back
// volume: volume level. 1 indicates the normal volume level. The recommended value range is 0–2. If you want to increase the volume level, you can set a higher value
[recorder setMicVolume:1.0];

// `setBGMVolume` is used to set the background music volume level. It controls the background music volume level during playback.
// volume: volume level. 1 indicates the normal volume level. The recommended value range is 0–2. If you want to increase the background music volume level, you can set a higher value
[recorder setBGMVolume:1.0];
```
## Adding Background Music During Editing
```objc
// Initialize the editor
TXPreviewParam *param = [[TXPreviewParam alloc] init];
param.videoView = videoView;
param.renderMode = PREVIEW_RENDER_MODE_FILL_EDGE;
ugcEdit = [[TXVideoEditer alloc] initWithPreview:param];

// Set the background music file path
 [ugcEdit setBGMAsset:fileAsset result:^(int result) {
 }];

// Set the start and end time for background music playback
[ugcEdit setBGMStartTime:0 endTime:5];

// Set whether to loop the background music
[ugcEdit setBGMLoop:YES];

// Set the start position where the background music is to be added in the video
[ugcEdit setBGMAtVideoTime:0];

// Set the video volume level
[ugcEdit setVideoVolume:1.0];

// Set the background music volume level
[ugcEdit setBGMVolume:1.0];
```
After you set the background music, when you start the editor for video preview, the background music will be played back according to the configured parameters. After you start the editor for video generation, the background music will be composed into the generated video according to the configured parameters.
