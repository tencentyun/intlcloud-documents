
The following is the basic usage process of multi-segment video shoot: 

1. Start video image preview.
2. Start shoot.
3. Play back the background music.
4. Pause shoot.
5. Pause the background music.
6. Resume shoot.
7. Resume the background music.
8. Stop shoot.
9. Stop the background music.

```
// Start shoot
mTXCameraRecord.startRecord();

// After `pauseRecord` is called, a video segment will be generated, which can be obtained from `TXUGCPartsManager`
mTXCameraRecord.pauseRecord();
mTXCameraRecord.pauseBGM();

// Resume video shoot
mTXCameraRecord.resumeRecord();
mTXCameraRecord.resumeBGM();

// Stop video shoot and compose multiple video segments into one video
mTXCameraRecord.stopBGM();
mTXCameraRecord.stopRecord();

// Get the video segment management object
mTXCameraRecord.getPartsManager();

// Get the total duration of all video segments
mTXUGCPartsManager.getDuration();

// Get the paths of all video segments
mTXUGCPartsManager.getPartsPathList();

// Delete the last video segment
mTXUGCPartsManager.deleteLastPart();

// Delete a specified video segment
mTXUGCPartsManager.deletePart(index);

// Delete all video segments
mTXUGCPartsManager.deleteAllParts();

// You can add videos except the one currently being shot
mTXUGCPartsManager.insertPart(videoPath, index) ;

```
