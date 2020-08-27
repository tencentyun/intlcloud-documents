

The following is the basic usage process of multi-segment video shoot:

1. Start video image preview. 
2. Start shoot.
3. Play back the background music.
4. Pause shoot.
5. Pause the background music.
6. Resume the background music.
7. Resume shoot.
8. Stop shoot.
9. Stop the background music.

```objc
// Start video image preview
recorder = [TXUGCRecord shareInstance];
[recorder startCameraCustom:param preview:preview];

// Start shoot
[recorder startRecord];

// Set the background music
[recorder setBGM:BGMPath];

// Play back the background music
[recorder playBGMFromTime:beginTime toTime:_BGMDuration withBeginNotify:^(NSInteger errCode) {
// Start playback
} withProgressNotify:^(NSInteger progressMS, NSInteger durationMS) {
// Playback progress
} andCompleteNotify:^(NSInteger errCode) {
 // End playback
}];

// After `pauseRecord` is called, a video segment will be generated, which can be obtained from and managed in `TXUGCPartsManager`
[recorder pauseRecord];

// Pause the background music
[recorder pauseBGM];

// Resume the background music
 [recorder resumeBGM];

// Resume video shoot
[recorder resumeRecord];

// Stop video shoot and compose multiple video segments into one video
[recorder stopRecord];

// Stop the background music
[recorder stopBGM];

// Get the video segment management object
TXUGCPartsManager *partsManager = recorder.partsManager;

// Get the total duration of all video segments
[partsManager getDuration];

// Get the paths of all video segments
[partsManager getVideoPathList];

// Delete the last video segment
[partsManager deleteLastPart];

// Delete a specified video segment
[partsManager deletePart:1];

// Delete all video segments
[partsManager deleteAllParts];

 // You can add videos except the one currently being shot
[partsManager insertPart:videoPath atIndex:0];

// Compose all video segments
[partsManager joinAllParts: videoOutputPath complete:complete];
```
