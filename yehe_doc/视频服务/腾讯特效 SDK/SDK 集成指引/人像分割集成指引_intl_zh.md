在直播、会议等场景实现虚拟背景，实时精准分割，支持自定义背景：
<img src="https://qcloudimg.tencent-cloud.cn/raw/4ed25f2dba2445c929e757879ae83547.png" width=700>

## iOS 接口使用

### iOS 集成指引

iOS 集成 SDK 指引，请参见 [独立集成腾讯特效](https://intl.cloud.tencent.com/document/product/1143/45384)。

### 虚拟背景设置
```objectivec
NSString *motionSegResPath = [[NSBundle mainBundle] pathForResource:@"segmentMotionRes" ofType:@"bundle"];//这里是segmentMotionRes文件夹的绝对路径
NSString *propertyType = @"motion";         //配置美颜的效果类型，这里以分割为例
NSString *propertyName = @"video_segmentation_blur_75"; //配置美颜的名称，这里以背景模糊-强为例
NSString *propertyValue = motionSegResPath;  //配置动效的路径
NSDictionary *dic = @{@"bgName":@"BgSegmentation.bg.png", @"bgType":@0, @"timeOffset": @0},@"icon":@"segmentation.linjian.png"};//配置预留字段
[self.beautyKit configPropertyWithType:propertyType withName:propertyName withData:propertyValue withExtraInfo:dic];
```

### 自定义背景设置
```objectivec
NSString *motionSegResPath = [[NSBundle mainBundle] pathForResource:@"segmentMotionRes" ofType:@"bundle"];//这里是segmentMotionRes文件夹的绝对路径
NSString *propertyType = @"motion";         //配置美颜的效果类型，这里以分割为例
NSString *propertyName = @"video_empty_segmentation"; //配置美颜的名称，这里以自定义背景为例
NSString *propertyValue = motionSegResPath;  //配置动效的路径
NSString *imagePath = @"/var/mobile/Containers/Data/Application/06B00BBC-9060-450F-8D3A-F6028D185682/Documents/MediaFile/image.png"; //自定义背景图片的绝对路径。如果自定义背景选择的是视频，需要对视频进行压缩转码处理，使用压缩转码处理后的绝对路径
int bgType = 0;//自定义背景的类型。 0表示图片，1表示视频
int timeOffset = 0；//时长。图片背景时，为0；视频背景时为视频的时长
NSDictionary *dic = @{@"bgName":imagePath, @"bgType":@(bgType), @"timeOffset": @(timeOffset)},@"icon":@"segmentation.linjian.png"};//配置预留字段
[self.beautyKit configPropertyWithType:propertyType withName:propertyName withData:propertyValue withExtraInfo:dic];
```



## Android 接口使用

### Android 集成指引
Android 集成 SDK 指引，请参见 [独立集成腾讯特效](https://intl.cloud.tencent.com/document/product/1143/45385)。

### 设置属性接口
```java
void updateProperty(XmagicProperty<?> p) 
```

**分割参数：**

| 属性字段 | 说明                                                         |
| :------- | :----------------------------------------------------------- |
| category | Category.SEGMENTATION                                        |
| ID       | 资**源文件夹名称**，必填示例：`video_segmentation_blur_45`，<li>“无” ID 为 `XmagicProperty.ID_NONE`</li><li>自定义分割 ID 值必须使用：`XmagicConstant.SegmentationId.CUSTOM_SEG_ID`</li> |
| resPath  | 必填，参考 Demo                                              |
| effkey   | null（自定义背景除外），自定义背景的值为选择的资源路径       |
| effValue | null                                                         |


### 虚拟背景设置
```java
//初始化XmagicProperty
XmagicProperty xmagicProperty = new XmagicProperty(Category.SEGMENTATION,"video_segmentation_blur_45",resPath,null,null);
//设置属性
xmagicApi.updateProperty(xmagicProperty) 
```

### 自定义背景设置
```java
XmagicProperty xmagicProperty = new XmagicProperty(Category.SEGMENTATION,XmagicConstant.SegmentationId.CUSTOM_SEG_ID,resPath,null,null);

xmagicApi.updateProperty(xmagicProperty) 
```

