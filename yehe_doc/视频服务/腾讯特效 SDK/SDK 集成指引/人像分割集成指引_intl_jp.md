ライブストリーミング、ミーティングなどのシーンでバーチャル背景を実装し、リアルタイムで正確な分割を行います。カスタム背景をサポートしています。
<img src="https://qcloudimg.tencent-cloud.cn/raw/4ed25f2dba2445c929e757879ae83547.png" width=900>

## iOSインターフェースの使用

### iOS統合ガイド

iOSのSDKの統合ガイドについては、[Tencent Effectの独立した統合](https://intl.cloud.tencent.com/document/product/1143/45384)をご参照ください。

### バーチャル背景の設定
```objectivec
NSString *motionSegResPath = [[NSBundle mainBundle] pathForResource:@"segmentMotionRes" ofType:@"bundle"];//ここではsegmentMotionResフォルダーの絶対パスを設定します
NSString *propertyType = @"motion";         //美顔のエフェクトタイプを設定します。ここでは分割を例とします
NSString *propertyName = @"video_segmentation_blur_75"; //美顔の名前を設定します。ここでは背景のぼかし‐強を例とします
NSString *propertyValue = motionSegResPath;  //モーションのパスを設定します
NSDictionary *dic = @{@"bgName":@"BgSegmentation.bg.png", @"bgType":@0, @"timeOffset": @0},@"icon":@"segmentation.linjian.png"};//リザーブドフィールドを設定します
[self.beautyKit configPropertyWithType:propertyType withName:propertyName withData:propertyValue withExtraInfo:dic];
```

### カスタム背景の設定
```objectivec
NSString *motionSegResPath = [[NSBundle mainBundle] pathForResource:@"segmentMotionRes" ofType:@"bundle"];//ここではsegmentMotionResフォルダーの絶対パスを設定します
NSString *propertyType = @"motion";         //美顔のエフェクトタイプを設定します。ここでは分割を例とします
NSString *propertyName = @"video_empty_segmentation"; //美顔の名前を設定します。ここではカスタム背景を例とします
NSString *propertyValue = motionSegResPath;  //モーションのパスを設定します
NSString *imagePath = @"/var/mobile/Containers/Data/Application/06B00BBC-9060-450F-8D3A-F6028D185682/Documents/MediaFile/image.png"; //カスタム背景として使用する画像の絶対パス。カスタム背景としてビデオを選択した場合、ビデオに対して圧縮しトランスコーディングした後の絶対パスを使用します。
int bgType = 0;//カスタム背景のタイプ0は画像、1はビデオを表します
int timeOffset = 0；//時間の長さ背景が画像の場合、0とします。背景がビデオの場合、ビデオの長さとします
NSDictionary *dic = @{@"bgName":imagePath, @"bgType":@(bgType), @"timeOffset": @(timeOffset)},@"icon":@"segmentation.linjian.png"};//リザーブドフィールドを設定します
[self.beautyKit configPropertyWithType:propertyType withName:propertyName withData:propertyValue withExtraInfo:dic];
```



## Androidインターフェースの使用

### Android統合ガイド
AndroidのSDKの統合ガイドについては、[Tencent Effectの独立した統合](https://intl.cloud.tencent.com/document/product/1143/45385)をご参照ください。

### 属性インターフェースの設定
```java
void updateProperty(XmagicProperty<?> p) 
```

**分割パラメータ：**

| 属性フィールド | 説明                                                         |
| :------- | :----------------------------------------------------------- |
| category | Category.SEGMENTATION                                        |
| ID       | **リソースフォルダ名**。入力必須項目の例：`video_segmentation_blur_45`、<li>「なし」の場合のIDは`XmagicProperty.ID_NONE`</li><li>カスタム分割IDの値には必ず`XmagicConstant.SegmentationId.CUSTOM_SEG_ID`を使用します</li> |
| resPath  | 入力必須、Demo参照                                              |
| effkey   | null（カスタム背景を除く）。カスタム背景の値は選択するリソースパスとします       |
| effValue | null                                                         |


### バーチャル背景の設定
```java
//XmagicPropertyの初期化
XmagicProperty xmagicProperty = new XmagicProperty(Category.SEGMENTATION,"video_segmentation_blur_45",resPath,null,null);
//属性の設定
xmagicApi.updateProperty(xmagicProperty) 
```

### カスタム背景の設定
```java
XmagicProperty xmagicProperty = new XmagicProperty(Category.SEGMENTATION,XmagicConstant.SegmentationId.CUSTOM_SEG_ID,resPath,null,null);

xmagicApi.updateProperty(xmagicProperty) 
```

