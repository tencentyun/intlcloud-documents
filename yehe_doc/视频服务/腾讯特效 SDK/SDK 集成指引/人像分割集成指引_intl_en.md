This capability allows you to apply virtual backgrounds to videos in scenarios such as live streaming and video conferencing.
<img src="https://qcloudimg.tencent-cloud.cn/raw/4ed25f2dba2445c929e757879ae83547.png" width=700>

## iOS APIs

### iOS integration

For directions on how to integrate the Tencent Effect iOS SDK, see [Integrating Tencent Effect SDK](https://intl.cloud.tencent.com/document/product/1143/45384).

### Configuring a virtual background
```objectivec
NSString *motionSegResPath = [[NSBundle mainBundle] pathForResource:@"segmentMotionRes" ofType:@"bundle"];//The absolute path of the `segmentMotionRes` folder
NSString *propertyType = @"motion";         //Set the effect type
NSString *propertyName = @"video_segmentation_blur_75"; //Specify the effect name. `video_segmentation_blur_75` indicates a blurred background (strong).
NSString *propertyValue = motionSegResPath;  //Set the path of the animated effect
NSDictionary *dic = @{@"bgName":@"BgSegmentation.bg.png", @"bgType":@0, @"timeOffset": @0},@"icon":@"segmentation.linjian.png"};//Configure the reserved parameter
[self.beautyKit configPropertyWithType:propertyType withName:propertyName withData:propertyValue withExtraInfo:dic];
```

### Customizing a background
```objectivec
NSString *motionSegResPath = [[NSBundle mainBundle] pathForResource:@"segmentMotionRes" ofType:@"bundle"];//The absolute path of the `segmentMotionRes` folder
NSString *propertyType = @"motion";         //Set the effect type
NSString *propertyName = @"video_empty_segmentation"; //Specify the effect name. `video_empty_segmentation` indicates a custom background.
NSString *propertyValue = motionSegResPath;  //Set the path of the animated effect
NSString *imagePath = @"/var/mobile/Containers/Data/Application/06B00BBC-9060-450F-8D3A-F6028D185682/Documents/MediaFile/image.png"; //The absolute path of the background image or video (compression required)
int bgType = 0;//The background type. 0: image; 1: video.
int timeOffset = 0；//The duration. If an image is used as the background, this parameter is `0`; if a video is used, this parameter is the video length.
NSDictionary *dic = @{@"bgName":imagePath, @"bgType":@(bgType), @"timeOffset": @(timeOffset)},@"icon":@"segmentation.linjian.png"};//Configure the reserved parameter
[self.beautyKit configPropertyWithType:propertyType withName:propertyName withData:propertyValue withExtraInfo:dic];
```



## Android APIs

### Android integration
For directions on how to integrate the Tencent Effect Android SDK, see [Integrating Tencent Effect SDK](https://intl.cloud.tencent.com/document/product/1143/45385).

### Setting properties
```java
void updateProperty(XmagicProperty<?> p) 
```

**Keying parameters:**

| Parameter | Description                                                         |
| :------- | :----------------------------------------------------------- |
| category | Category.SEGMENTATION                                        |
| ID       | **The name of the resource folder**, such as `video_segmentation_blur_45`. <li>If there isn’t an ID, use `XmagicProperty.ID_NONE`.</li><li>For custom backgrounds, set this to `XmagicConstant.SegmentationId.CUSTOM_SEG_ID`.</li> |
| resPath  | Required. For details, refer to the demo.                                              |
| effkey   | Null (except for custom backgrounds). For custom backgrounds, set this parameter to the resource path.       |
| effValue | Null                                                         |


### Configuring a virtual background
```java
// Initialize `XmagicProperty`
XmagicProperty xmagicProperty = new XmagicProperty(Category.SEGMENTATION,"video_segmentation_blur_45",resPath,null,null);
// Set properties
xmagicApi.updateProperty(xmagicProperty) 
```

### Customizing a background
```java
XmagicProperty xmagicProperty = new XmagicProperty(Category.SEGMENTATION,XmagicConstant.SegmentationId.CUSTOM_SEG_ID,resPath,null,null);

xmagicApi.updateProperty(xmagicProperty) 
```

