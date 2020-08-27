You can implement the drafts logic as follows:
#### First Shooting
1. Start shooting.
2. Pause/End the first shooting. 
3. Cache the video segment locally (in drafts).

#### Second Shooting
1. Preload the locally cached video segment.
2. Resume shooting.
3. End shooting.

```objc
// Get the first video shooting object
record = [TXUGCRecord shareInstance];

// Start shooting
[record startRecord];

// Pause shooting and cache the video segment
[record pauseRecord:^{
NSArray *videoPathList = record.partsManager.getVideoPathList;
// Write `videoPathList` locally
}];

// Get the second video shooting object
record2 = [TXUGCRecord shareInstance];

// Preload the locally cached segment
[record2.partsManager insertPart:videoPath atIndex:0];

// Start shooting
[record2 startRecord];

// End shooting, and the SDK will compose the cached video segment with the currently shot one
[record2 stopRecord];
```
#### For the specific implementation method, please see the `TCVideoRecordViewController` class in the [UGSV application demo source code](https://intl.cloud.tencent.com/document/product/1069/37914).
