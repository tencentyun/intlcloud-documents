Tencent Effect SDKのコアインターフェースクラス`XMagic.h`は、SDKの初期化、美顔の値の更新、モーションの呼出しなどの機能に使用されます。

## Publicメンバー関数

| API                    | 説明                   |
| ------------- | ------------- |
| [initWithRenderSize](#initwithrendersize) | 初期化インターフェース |
| [initWithGlTexture](#initwithgltexture) | 初期化インターフェース |
| [configPropertyWithType](#configpropertywithtype) | 各美顔エフェクトを設定します |
| [emitBlurStrengthEvent](#emitblurstrengthevent) | 後処理のぼかし強度を設定します（すべてのぼかしコンポーネントに機能） |
| [setRenderSize](#setrendersize) | renderSizeを設定します |
| [deinit](#deinit) | リソースを解放するインターフェース |
| [process](#process) | データを処理するインターフェース |
| [processUIImage](#processuiimage) | 画像を処理します |
| [getConfigPropertyWithName](#getconfigpropertywithname) | 美顔パラメーターの設定情報を取得します |
| [registerLoggerListener](#registerloggerlistener) | ログを登録するインターフェース |
| [registerSDKEventListener](#registersdkeventlistener)   | SDKのイベント監視インターフェース |
| [clearListeners](#clearlisteners) | クリア用コールバックを登録するインターフェース |
| [getCurrentGlContext](#getcurrentglcontext) | 現在のGLのコンテキストを取得するインターフェース |
| [onPause](#onpause) | SDKの一時停止インターフェース |
| [onResume](#onresume) | SDKの再開インターフェース |

### initWithRenderSize
初期化インターフェース
```objectivec
- (instancetype _Nonnull)initWithRenderSize:(CGSize)renderSize
                        assetsDict:(NSDictionary* _Nullable)assetsDict;
```

**パラメータ**

| パラメータ                                 | 意味        |
| ---------- | -------- |
| renderSize | レンダリングサイズ |
| assetsDict | アセット Dict |

### initWithGlTexture
初期化インターフェース

```objectivec
- (instancetype _Nonnull)initWithGlTexture:(unsigned)textureID
                        width:(int)width
                        height:(int)height
                        flipY:(bool)flipY
                        assetsDict:(NSDictionary* _Nullable)assetsDict;
```

**パラメータ**

| パラメータ                                 | 意味        |
| ---------- | ------------ |
| textureID  | テクスチャID      |
| width      | レンダリングサイズ     |
| height     | レンダリングサイズ     |
| flipY      | 画像を反転しますか |
| assetsDict | アセット Dict |

### configPropertyWithType

美顔の各エフェクトを設定します

```objectivec
- (int)configPropertyWithType:(NSString *_Nonnull)propertyType withName:(NSString *_Nonnull)propertyName withData:(NSString*_Nonnull)propertyValue withExtraInfo:(id _Nullable)extraInfo;
```

**パラメータ**

| パラメータ                   | 意味                                                         |
| ------------- | --------------------------- |
| propertyType  | エフェクトタイプ                    |
| propertyName  | エフェクト名                    |
| propertyValue | エフェクトの値                    |
| extraInfo     | リザーブド拡張、オプションナル設定項目dictあり |

#### 美顔エフェクトの設定例

- **美顔：**美白エフェクトを設定します
```objectivec
NSString *propertyType = @"beauty";        //美顔のエフェクトタイプを設定します。ここでは美顔を例とします
NSString *propertyName = @"beauty.whiten";       //美顔の名前を設定します。ここでは美白を例とします
NSString *propertyValue = @"60";           //美白のエフェクトの値を設定します
[self.xmagicApi configPropertyWithType:propertyType withName:propertyName withData:propertyValue withExtraInfo:nil];
```
- **フィルター**：ときめきエフェクトを設定します
```objectivec
NSString *propertyType = @"lut";        //美顔のエフェクトタイプを設定します。ここではフィルターを例とします
NSString *propertyName = [@"lut.bundle/" stringByAppendingPathComponent:@"xindong_lf.png"]; //美顔の名前を設定します。ここではときめきを例とします
NSString *propertyValue = @"60";           //フィルターのエフェクトの値を設定します
[self.xmagicApi configPropertyWithType:propertyType withName:propertyName withData:propertyValue withExtraInfo:nil];
```
- **美ボディ**：足長エフェクトを設定します
```objectivec
NSString *propertyType = @"body";        //美顔のエフェクトタイプを設定します。ここでは美ボディを例とします
NSString *propertyName = @"body.legStretch"; //美顔の名前を設定します。ここでは足長を例とします
NSString *propertyValue = @"60";           //足長のエフェクトの値を設定します
[self.xmagicApi configPropertyWithType:propertyType withName:propertyName withData:propertyValue withExtraInfo:nil];
```
- **モーション**：2Dモーションの可愛い落書きエフェクトを設定します
```objectivec
 NSString *motion2dResPath = [[NSBundle mainBundle] pathForResource:@"2dMotionRes" ofType:@"bundle"];//ここでは2dMotionResフォルダーの絶対パスを設定します
 NSString *propertyType = @"motion";         //美顔のエフェクトタイプを設定します。ここではモーションを例とします
 NSString *propertyName = @"video_keaituya"; //美顔の名前を設定します。ここでは2Dアニメーションの可愛い落書きを例とします
 NSString *propertyValue = motion2dResPath;  //モーションのパスを設定します
 [self.xmagicApi configPropertyWithType:propertyType withName:propertyName withData:propertyValue withExtraInfo:nil];
```
- **メイク**：女性アイドルグループ風メイクエフェクトを設定します
```objectivec
NSString *motionMakeupResPath = [[NSBundle mainBundle] pathForResource:@"makeupMotionRes" ofType:@"bundle"];//ここではmakeupMotionResフォルダーの絶対パスを設定します
NSString *propertyType = @"motion";         //美顔のエフェクトタイプを設定します。ここではメイクを例とします
NSString *propertyName = @"video_nvtuanzhuang"; //美顔の名前を設定します。ここでは女性アイドルグループ風メイクを例とします
NSString *propertyValue = motionMakeupResPath;  //モーションのパスを設定します
[self.xmagicApi configPropertyWithType:propertyType withName:propertyName withData:propertyValue withExtraInfo:nil];
//設定するメイクの値を以下に示します（前述したモーションは1回だけ呼び出せばよいです。以下に設定するメイクの値は複数回呼び出すことができます）
 NSString *propertyTypeMakeup = @"custom";         //美顔のエフェクトタイプを設定します。ここではメイクを例とします
 NSString *propertyNameMakeup = @"makeup.strength"; //美顔の名前を設定します。ここでは女性アイドルグループ風メイクを例とします
 NSString *propertyValueMakeup = @"60";             //メイクのエフェクトの値を設定します
 [self.xmagicApi configPropertyWithType:propertyTypeMakeup withName:propertyNameMakeup withData:propertyValueMakeup withExtraInfo:nil];
```
- **分割**：背景のぼかし（強い効果）を設定します
```objectivec
NSString *motionSegResPath = [[NSBundle mainBundle] pathForResource:@"segmentMotionRes" ofType:@"bundle"];//ここではsegmentMotionResフォルダーの絶対パスを設定します
NSString *propertyType = @"motion";         //美顔のエフェクトタイプを設定します。ここでは分割を例とします
NSString *propertyName = @"video_segmentation_blur_75"; //美顔の名前を設定します。ここでは背景のぼかし‐強を例とします
NSString *propertyValue = motionSegResPath;  //モーションのパスを設定します
NSDictionary *dic = @{@"bgName":@"BgSegmentation.bg.png", @"bgType":@0, @"timeOffset": @0},@"icon":@"segmentation.linjian.png"};//リザーブドフィールドを設定します
[self.xmagicApi configPropertyWithType:propertyType withName:propertyName withData:propertyValue withExtraInfo:dic];
```
- **カスタム背景**：
```objectivec
NSString *motionSegResPath = [[NSBundle mainBundle] pathForResource:@"segmentMotionRes" ofType:@"bundle"];//ここではsegmentMotionResフォルダーの絶対パスを設定します
NSString *propertyType = @"motion";         //美顔のエフェクトタイプを設定します。ここでは分割を例とします
NSString *propertyName = @"video_empty_segmentation"; //美顔の名前を設定します。ここではカスタム背景を例とします
NSString *propertyValue = motionSegResPath;  //モーションのパスを設定します
NSString *imagePath = @"/var/mobile/Containers/Data/Application/06B00BBC-9060-450F-8D3A-F6028D185682/Documents/MediaFile/image.png"; //カスタム背景として使用する画像の絶対パス。カスタム背景としてビデオを選択した場合、ビデオに対して圧縮しトランスコーディングした後の絶対パスを使用します。
int bgType = 0;//カスタム背景のタイプ0は画像、1はビデオを表します
int timeOffset = 0；//時間の長さ背景が画像の場合、0とします。背景がビデオの場合、ビデオの長さとします
NSDictionary *dic = @{@"bgName":imagePath, @"bgType":@(bgType), @"timeOffset": @(timeOffset)},@"icon":@"segmentation.linjian.png"};//リザーブドフィールドを設定します
[self.xmagicApi configPropertyWithType:propertyType withName:propertyName withData:propertyValue withExtraInfo:dic];
```

### emitBlurStrengthEvent

後処理のぼかし強度を設定します（すべてのぼかしコンポーネントに機能）

```objectivec
- (void)emitBlurStrengthEvent:(int)strength;
```

**パラメータ**

| パラメータ          | 意味      |
| -------- | -------- |
| strength | エフェクトの値 |

### setRenderSize

renderSizeを設定します

```objectivec
- (void)setRenderSize:(CGSize)size;
```

**パラメータ**

| パラメータ          | 意味      |
| ---- | -------- |
| size | レンダリングサイズ  |

### deinit

リソースを解放するインターフェース |

```objectivec
- (void)deinit;
```

### process

データを処理するインターフェース |

```objectivec
- (YTProcessOutput* _Nonnull)process:(YTProcessInput * _Nonnull)input;
```

**パラメータ**

| パラメータ                                 | 意味        |
| ----- | ---------------- |
| input | 入力データ |

### processUIImage

画像を処理します
```objectivec
- (UIImage* _Nullable)processUIImage:(UIImage* _Nonnull)inputImage needReset:(bool)needReset;
```

**パラメータ**

| パラメータ       | 意味                                                                                                                                        |
| ---------- | ------------------------------------------------------------ |
| inputImage | 入力画像の最大サイズは2160×4096までとすることをお勧めします。このサイズを超えると、画像に対して顔認識がうまく機能できないまたは機能できないことがあり、またOOM問題も起こりやすいため、大きな画像を縮小してからアップロードすることをお勧めします |
| needReset  | 次の運用シーンでは、needResetにtrueを設定してください。<ul style="margin:0"><li>画像の切替</li><li>分割の初回利用</li><li>アニメーションの初回利用</li><li>メイクの初回利用</li></ul> |

### getConfigPropertyWithName

美顔パラメーターの設定情報を取得します

```objectivec
- (YTBeautyPropertyInfo * _Nullable)getConfigPropertyWithName:(NSString *_Nonnull)propertyName;
```

**パラメータ**

| パラメータ                                 | 意味        |
| ------------ | -------- |
| propertyName | 設定項目名 |

### registerLoggerListener

ログを登録するインターフェース

```objectivec
- (void)registerLoggerListener:(id<YTSDKLogListener> _Nullable)listener withDefaultLevel:(YtSDKLoggerLevel)level;
```

**パラメータ**

| パラメータ                                | 意味                         |
| -------- | -------------------------- |
| listener | ログをコールバックするインターフェース               |
| level    | ログの出力レベル。デフォルトではERRORとします |

### registerSDKEventListener

SDKのイベント監視インターフェース |

```objectivec
- (void)registerSDKEventListener:(id<YTSDKEventListener> _Nullable)listener;
```

**パラメータ**

| パラメータ     | 意味                                                        |
| -------- | ----------------------------------------------------------- |
| listener | イベント監視関連のコールバック。主にAIイベント、Tipsイベント、Assetイベントに分けられています |

### clearListeners

クリア用コールバックを登録するインターフェース |

```objectivec
- (void)clearListeners;
```

### getCurrentGlContext

現在のGLのコンテキストを取得するインターフェース

```objectivec
- (nullable EAGLContext*)getCurrentGlContext;
```

### onPause

SDKの一時停止インターフェース

```objectivec
/// @brief APPを一時停止する場合、SDKの一時停止インターフェースを呼び出します
- (void)onPause;
```

### onResume

SDKの再開インターフェース

```objectivec
/// @brief APPを再開する場合、SDKの再開インターフェースを呼び出します
- (void)onResume;
```

## 静的関数

| API                                       | 説明                     |
| ----------------------------------------- | ------------------------ |
| [isBeautyAuthorized](#isbeautyauthorized) | この美顔パラメーターの権限情報を取得します |

### isBeautyAuthorized

この美顔パラメーターの権限情報を取得します（美顔と美ボディのみをサポート）

```objectivec
/// @param featureId 美顔パラメーターを設定します
/// @return 該当する美顔パラメーターの権限付与情報を返します
+ (BOOL)isBeautyAuthorized:(NSString * _Nullable)featureId;
```

## コールバック

| API                                                          | 説明                   |
| ----------------------------------------- | -------------------- |
| [YTSDKEventListener](#ytsdkeventlistener) | SDKの内部イベントコールバックインターエース |
| [YTSDKLogListener](#ytsdkloglistener)     | ログ監視関連のコールバック         |


### YTSDKEventListener

SDK内部イベントコールバックインターエース
```objectivec
@protocol YTSDKEventListener <NSObject>
```

#### メンバー関数
| 返却値のタイプ | 名前                            |
| -------- | ------------------------------- |
| void     | [onYTDataEvent](#onytdataevent) |
| void     | [onAIEvent](#onaievent)         |
| void     | [onTipsEvent](#ontipsevent)     |
| void     | [onAssetEvent](#onassetevent)   |

#### 関数説明

##### onYTDataEvent
YTDataUpdateイベントコールバック

```objectivec
/// @param event NSString*フォーマットのコールバック
- (void)onYTDataEvent:(id _Nonnull)event;
```

JSON string構造体を返します。最大5人の顔情報を返します：

```objectivec
{
 "face_info":[{
  "trace_id":5,
  "face_256_point":[
    180.0,
    112.2,
    ...
  ],
  "face_256_visible":[
    0.85,
    ...
  ],
  "out_of_screen":true,
  "left_eye_high_vis_ratio:1.0,
  "right_eye_high_vis_ratio":1.0,
  "left_eyebrow_high_vis_ratio":1.0,
  "right_eyebrow_high_vis_ratio":1.0,
  "mouth_high_vis_ratio":1.0
 },
 ...
 ]
}
```

**フィールドの意味**

| フィールド                         | タイプ  | 値の範囲                                | 説明                                                   |
| ---------------------------- | ----- | ----------------------------------- | ------------------------------------------------------ |
| trace_id                     | int   | [1,INF)                             | 顔ID。連続してストリームを取得するとき、IDが同じである場合、同じ顔として認識します |
| face_256_point               | float | [0,screenWidth] 或 [0,screenHeight] | 計512数字あり、顔の256重要特徴点があり、画面の左上隅は(0,0)です |
| face_256_visible             | float | [0,1]                               | 顔の256重要特徴点の可視度                                    |
| out_of_screen                | bool  | true/false                          | 顔が枠を超えていますか                                           |
| left_eye_high_vis_ratio      | float | [0,1]                               | 左目の特徴点のうち高視認度のものが占める割合                                   |
| right_eye_high_vis_ratio     | float | [0,1]                               | 右目の特徴点のうち高視認度のものが占める割合                                   |
| left_eyebrow_high_vis_ratio  | float | [0,1]                               | 左眉の特徴点のうち高視認度のものが占める割合                                   |
| right_eyebrow_high_vis_ratio | float | [0,1]                               | 右眉の特徴点のうち高視認度のものが占める割合                                   |
| mouth_high_vis_ratio         | float | [0,1]                               | 口の特徴点のうち高視認度のものが占める割合                                     |

##### onAIEvent
AIイベントコールバック

```objectivec
/// @param event dictフォーマットのコールバック
- (void)onAIEvent:(id _Nonnull)event;
```

##### onTipsEvent
ヒントイベントコールバック

```objectivec
/// @param event dictフォーマットのコールバック
- (void)onTipsEvent:(id _Nonnull)event;
```

##### onAssetEvent
アセットイベントコールバック

```objectivec
/// @param event stringフォーマットのコールバック
- (void)onAssetEvent:(id _Nonnull)event;
```

### YTSDKLogListener

ログ監視関連のコールバック

```objectivec
@protocol YTSDKLogListener <NSObject>
```

#### メンバー関数

| 返却値のタイプ | 関数名 |
| -------- | -------- |
| void     | onLog    |

#### 関数説明

##### onLog

ログ監視関連のコールバック

```objectivec
/// @param loggerLevel 現在のログレベルを返します
/// @param logInfo 現在のログ情報を返します
- (void)onLog:(YtSDKLoggerLevel) loggerLevel withInfo:(NSString * _Nonnull) logInfo;
```

