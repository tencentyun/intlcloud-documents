How the shooting drafts feature works
#### Starting a shooting
1. Start shooting a video.
2. Pause/End the shooting. 
3. Cache the video segment locally (draft box).

#### Resuming the shooting
1. Preload the locally cached video segment.
2. Continue with the shooting.
3. End the shooting.

```plaintext
//Get the object of the previous shooting
record = [TXUGCRecord shareInstance];

//Start shooting a video.
[record startRecord];

//Pause the shooting and cache the video segment
[record pauseRecord:^{
NSArray *videoPathList = record.partsManager.getVideoPathList;
//Set `videoPathList` to a local path.
}];

//Get the object of the resumed shooting.
record2 = [TXUGCRecord shareInstance]；

//Preload the locally cached video segment.
[record2.partsManager insertPart:videoPath atIndex:0];

//Start the shooting
[record2 startRecord];

//End the shooting. The SDK will splice together the two video segments.
[record2 stopRecord];
```


>! For detailed instructions, see the `UGCKitRecordViewController` class in [(Demo) Source Code for All-Feature UGSV Apps](https://intl.cloud.tencent.com/document/product/1069/37914).
