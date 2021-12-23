
You can implement the drafts logic as follows: 
#### First Shooting
1. Start shooting.
2. Pause/End the first shooting.
3. Cache the video segment locally (in drafts).

#### Second Shooting
1. Preload the locally cached video segment.
2. Resume shooting.
3. End shooting.


<dx-codeblock>
::: android 
// Get the first video shooting object
mTXCameraRecord = TXUGCRecord.getInstance(this.getApplicationContext());

// Start shooting
mTXCameraRecord.startRecord();

// Pause shooting
mTXCameraRecord.pauseRecord();

// Get the cached video segment and write it locally
List<String> pathList = mTXCameraRecord.getPartsManager().getPartsPathList(); // Write `pathList` locally

// Open the application again and get the shooting object
mTXCameraRecord2 = TXUGCRecord.getInstance(this.getApplicationContext());

// Preload the locally cached segment
mTXCameraRecord2.getPartsManager().insertPart(videoPath, 0);

// Start shooting
mTXCameraRecord2.startRecord();

// End shooting, and the SDK will compose the cached video segment with the currently shot one
mTXCameraRecord2.stopRecord();
:::
</dx-codeblock>


>?For the specific implementation method, please see the usage of the `RecordDraftManager` class in the shooting module in the [UGSV application demo source code](https://intl.cloud.tencent.com/document/product/1069/37914).
