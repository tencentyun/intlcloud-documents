## Static Sticker

```
- (void) setPasterList:(NSArray *)pasterList;

// The `TXPaster` parameters are as follows:
@interface TXPaster: NSObject
@property (nonatomic, strong) UIImage*              pasterImage;    // Sticker image
@property (nonatomic, assign) CGRect                frame;          // Sticker frame (please note that the frame coordinates here are relative to the rendering view)
@property (nonatomic, assign) CGFloat               startTime;      // Sticker start time in s
@property (nonatomic, assign) CGFloat               endTime;        // Sticker end time in s
@end

```
 
## Animated Sticker

```
- (void) setAnimatedPasterList:(NSArray *)animatedPasterList;

// The `TXAnimatedPaster` parameters are as follows:
@interface TXAnimatedPaster: NSObject
@property (nonatomic, strong) NSString*             animatedPasterpath;  // Animated image file path
@property (nonatomic, assign) CGRect                frame;          // Animated image frame (please note that the frame coordinates here are relative to the rendering view)
@property (nonatomic, assign) CGFloat               rotateAngle;    // Animated image rotation angle. Value range: 0–360
@property (nonatomic, assign) CGFloat               startTime;      // Animated image start time in s
@property (nonatomic, assign) CGFloat               endTime;        // Animated image end time in s
@end
```

Demo:

```
- (void)setVideoPasters:(NSArray*)videoPasterInfos
{
    NSMutableArray* animatePasters = [NSMutableArray new];
    NSMutableArray* staticPasters = [NSMutableArray new];
    for (VideoPasterInfo* pasterInfo in videoPasterInfos) {
        if (pasterInfo.pasterInfoType == PasterInfoType_Animate) {
            TXAnimatedPaster* paster = [TXAnimatedPaster new];
            paster.startTime = pasterInfo.startTime;
            paster.endTime = pasterInfo.endTime;
            paster.frame = [pasterInfo.pasterView pasterFrameOnView:_videoPreview];
            paster.rotateAngle = pasterInfo.pasterView.rotateAngle * 180 / M_PI;
            paster.animatedPasterpath = pasterInfo.path;
            [animatePasters addObject:paster];
        }
        else if (pasterInfo.pasterInfoType == PasterInfoType_static){
            TXPaster *paster = [TXPaster new];
            paster.startTime = pasterInfo.startTime;
            paster.endTime = pasterInfo.endTime;
            paster.frame = [pasterInfo.pasterView pasterFrameOnView:_videoPreview];
            paster.pasterImage = pasterInfo.pasterView.staticImage;
            [staticPasters addObject:paster];
        }
    }
    [_ugcEditer setAnimatedPasterList:animatePasters];
    [_ugcEditer setPasterList:staticPasters];
}
```

## Custom Animated Sticker
Adding an animated sticker is actually to arrange **a series of images** in **a certain sequence** at **a certain interval** and insert them to the video to implement an animated sticker effect.

How do I customize a sticker?
Here, an animated sticker in the SDK demo is used as an example:

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
Video subtitling is supported. You can add subtitles to each frame of a video and set the start and end time to display each subtitle. All subtitles form a subtitle list, which can be passed to the SDK, and the SDK will automatically add the subtitles to the video at the corresponding points in time.

You can set subtitles as follows:  

```
- (void) setSubtitleList:(NSArray *)subtitleList;

The `TXSubtitle` parameters are as follows:
@interface TXSubtitle: NSObject
@property (nonatomic, strong) UIImage*              titleImage;     // Subtitle image (here, you need to convert the text loading control to an image)
@property (nonatomic, assign) CGRect                frame;          // Subtitle frame (please note that the frame coordinates here are relative to the rendering view)
@property (nonatomic, assign) CGFloat               startTime;      // Subtitle start time in s
@property (nonatomic, assign) CGFloat               endTime;        // Subtitle end time in s
@end
```

- titleImage: subtitle image. If controls like `UILabel` are used by the upper layer, please convert the control to `UIImage` first. For detailed directions, please see the sample code of the demo.  
- frame: subtitle frame (please note that the frame is relative to the frame of the rendering view passed in during `initWithPreview`). For more information, please see the sample code of the demo.  
- startTime: subtitle start time.  
- endTime: subtitle end time.  

As the subtitle UI logic is complicated, a complete method is provided at the demo layer. We recommend you directly implement subtitling as instructed in the demo, which greatly reduces your integration costs.

Demo:
```
@interface VideoTextInfo : NSObject
@property (nonatomic, strong) VideoTextFiled* textField;
@property (nonatomic, assign) CGFloat startTime; //in seconds
@property (nonatomic, assign) CGFloat endTime;
@end

videoTextInfos = @[VideoTextInfo1, VideoTextInfo2 ...];

 for (VideoTextInfo* textInfo in videoTextInfos) {
        TXSubtitle* subtitle = [TXSubtitle new];
        subtitle.titleImage = textInfo.textField.textImage;  //UILabel (UIView) -> UIImage
        subtitle.frame = [textInfo.textField textFrameOnView:_videoPreview]; // Calculate the coordinates relative to the rendering view
        subtitle.startTime = textInfo.startTime;  // Subtitle start time
        subtitle.endTime = textInfo.endTime;      // Subtitle end time
        [subtitles addObject:subtitle];           // Add the subtitle list
  }    
    
 [_ugcEditer setSubtitleList:subtitles];          // Set the subtitle list
```
### 2. How do I customize bubble subtitles?
#### Parameters required by bubble subtitles
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
