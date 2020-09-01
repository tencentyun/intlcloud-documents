## Static Sticker 
You can set a static sticker as follows:
```
public void setPasterList(List pasterList);

// The `TXPaster` parameters are as follows:
public final static class TXPaster {
    public Bitmap pasterImage;                                // Sticker image
    public TXRect frame;                                      // Sticker frame (please note that the frame coordinates here are relative to the rendering view)
    public long startTime;                                    // Sticker start time in ms
    public long endTime;                                      // Sticker end time in ms
}

```
## Animated Sticker
You can set an animated sticker as follows:

```
public void setAnimatedPasterList(List animatedPasterList);

// The `TXAnimatedPaster` parameters are as follows:
public final static class TXAnimatedPaster {
    public String animatedPasterPathFolder;                  // Address of animated sticker image
    public TXRect frame;                                      // Animated sticker frame (please note that the frame coordinates here are relative to the rendering view)
    public long startTime;                                    // Animated sticker start time in ms
    public long endTime;                                      // Animated sticker end time in ms
    public float rotation;
}
```
Demo:

```
List animatedPasterList = new ArrayList<>();
List pasterList = new ArrayList<>();
for (int i = 0; i < mTCLayerViewGroup.getChildCount(); i++) {
    PasterOperationView view = (PasterOperationView) mTCLayerViewGroup.getOperationView(i);
    TXVideoEditConstants.TXRect rect = new TXVideoEditConstants.TXRect();
    rect.x = view.getImageX();
    rect.y = view.getImageY();
    rect.width = view.getImageWidth();
    TXCLog.i(TAG, "addPasterListVideo, adjustPasterRect, paster x y = " + rect.x + "," + rect.y);

    int childType = view.getChildType();
    if (childType == PasterOperationView.TYPE_CHILD_VIEW_ANIMATED_PASTER) {
        TXVideoEditConstants.TXAnimatedPaster txAnimatedPaster = new TXVideoEditConstants.TXAnimatedPaster();

        txAnimatedPaster.animatedPasterPathFolder = mAnimatedPasterSDcardFolder + view.getPasterName() + File.separator;
        txAnimatedPaster.startTime = view.getStartTime();
        txAnimatedPaster.endTime = view.getEndTime();
        txAnimatedPaster.frame = rect;
        txAnimatedPaster.rotation = view.getImageRotate();

        animatedPasterList.add(txAnimatedPaster);
        TXCLog.i(TAG, "addPasterListVideo, txAnimatedPaster startTimeMs, endTime is : " + txAnimatedPaster.startTime + ", " + txAnimatedPaster.endTime);
    } else if (childType == PasterOperationView.TYPE_CHILD_VIEW_PASTER) {
        TXVideoEditConstants.TXPaster txPaster = new TXVideoEditConstants.TXPaster();

        txPaster.pasterImage = view.getRotateBitmap();
        txPaster.startTime = view.getStartTime();
        txPaster.endTime = view.getEndTime();
        txPaster.frame = rect;

        pasterList.add(txPaster);
        TXCLog.i(TAG, "addPasterListVideo, txPaster startTimeMs, endTime is : " + txPaster.startTime + ", " + txPaster.endTime);
    }
}

mTXVideoEditer.setAnimatedPasterList(animatedPasterList);  // Set an animated sticker
mTXVideoEditer.setPasterList(pasterList);                  // Set a static sticker
```
## Custom Animated Sticker
Adding an animated sticker is actually to arrange **a series of images** in **a certain sequence** at **a certain interval** and insert them to the video to implement an animated sticker effect.

#### Encapsulation format
Here, an animated sticker in the demo is used as an example:
```
{
  "name":"glass",                        // Sticker name
  "count":6,                             // Number of stickers
  "period":480,                          // Playback period: time taken for playing back the sticker once in ms
  "width":444,                           // Sticker width
  "height":256,                          // Sticker height
  "keyframe":6,                          // Key image, which can represent the animated sticker
  "frameArray": [                        // Set of all images
                 {"picture":"glass0"},
                 {"picture":"glass1"},
                 {"picture":"glass2"},
                 {"picture":"glass3"},
                 {"picture":"glass4"},
                 {"picture":"glass5"}
               ]
}
```
The SDK will get the corresponding `config.json` of the animated sticker and display it in the format defined in the .json file.

>?As this encapsulation format is required by the SDK, please describe animated stickers strictly in this format.

## Adding Subtitles
### 1. Bubble subtitles
Bubble video subtitling is supported. You can add subtitles to each frame of a video and set the start and end time to display each subtitle. All subtitles form a subtitle list, which can be passed to the SDK, and the SDK will automatically add the subtitles to the video at the corresponding points in time.

You can set bubble subtitles as follows:
```
public void setSubtitleList(List subtitleList);

// The `TXSubtitle` parameters are as follows:
public final static class TXSubtitle {
        public Bitmap titleImage;                                // Subtitle image
        public TXRect frame;                                      // Subtitle frame
        public long startTime;                                    // Subtitle start time in ms
        public long endTime;                                      // Subtitle end time in ms
}

public final static class TXRect {
        public float x;
        public float y;
        public float width;
}
```

- titleImage: subtitle image. If controls like `TextView` are used by the upper layer, please convert the control to `Bitmap` first. For detailed directions, please see the sample code of the demo.
- frame: subtitle frame (please note that the frame is relative to the frame of the rendering view passed in during `initWithPreview`). For more information, please see the sample code of the demo.
- startTime: subtitle start time.
- endTime: subtitle end time.

As the subtitle UI logic is complicated, a complete method is provided at the demo layer. We recommend you directly implement subtitling as instructed in the demo, which greatly reduces your integration costs.

Demo:
```
mSubtitleList.clear();
for (int i = 0; i < mWordInfoList.size(); i++) {
    TCWordOperationView view = mOperationViewGroup.getOperationView(i);
    TXVideoEditConstants.TXSubtitle subTitle = new TXVideoEditConstants.TXSubtitle();
    subTitle.titleImage = view.getRotateBitmap();  // Get `Bitmap`
    TXVideoEditConstants.TXRect rect = new TXVideoEditConstants.TXRect();
    rect.x = view.getImageX();        // Get the X coordinate relative to the parent view
    rect.y = view.getImageY();        // Get the Y coordinate relative to the parent view
    rect.width = view.getImageWidth(); // Image width
    subTitle.frame = rect;
    subTitle.startTime = mWordInfoList.get(i).getStartTime();  // Set the start time
    subTitle.endTime = mWordInfoList.get(i).getEndTime();      // Set the end time
    mSubtitleList.add(subTitle);
}
mTXVideoEditer.setSubtitleList(mSubtitleList); // Set the subtitle list
```
### 2. How do I customize bubble subtitles?
**Parameters required by bubble subtitles**
* Font area dimensions: top, left, right, bottom
* Default font size
* Width and height

>?The parameters above are all in px.

#### Encapsulation format
As bubble subtitles contain many parameters, we recommend you encapsulate relevant parameters at the demo layer. For example, the Tencent Cloud demo uses the JSON format for encapsulation:

```
{
  "name":"boom",     // Bubble subtitle name
  "width": 376,      // Width
  "height": 335,     // Height
  "textTop":121,     // Top margin of text area
  "textLeft":66,     // Left margin of text area
  "textRight":69,    // Right margin of text area
  "textBottom":123,  // Bottom margin of text area
  "textSize":40      // Font size
}
```
>?You can determine the encapsulation format by yourself, which is optional for the SDK.

#### Overlong subtitle
**If a subtitle is too long, how do I arrange the layout to make the subtitle neatly fit in the bubble?**
An automatic layout control is provided in the demo. If a subtitle is too long, the control will automatically decrease the font size until the entire subtitle can fit in the bubble.
You can also modify the relevant control source code to meet your unique business needs.
