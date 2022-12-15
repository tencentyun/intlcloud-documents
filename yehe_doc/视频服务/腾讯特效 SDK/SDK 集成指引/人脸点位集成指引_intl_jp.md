顔検出（顔の枠外へのはみ出し、複数の顔、顔部分の遮蔽の認識）では、顔の256個の重要特徴点の位置を認識し出力します。

## 顔の256ポイント対応インデックス図
<img src="https://qcloudimg.tencent-cloud.cn/raw/ebf9e5e6ed208b6e8571520e3ff173e5.png" width=400>


## iOSインターフェースの説明

### iOS統合ガイド
iOSのSDKの統合ガイドについては、[Tencent Effectの独立した統合](https://intl.cloud.tencent.com/document/product/1143/45384)をご参照ください。

### Xmagicインターフェースのコールバック登録
```objectivec
/// @brief SDKイベント監視インターフェース
/// @param listener イベントリスナーコールバックです。主に、AIイベント、Tips表示イベント、Assetイベントがあります
- (void)registerSDKEventListener:(id<YTSDKEventListener> _Nullable)listener;
```

### YTSDKEventListenerコールバック説明
```objectivec
#pragma mark - イベントコールバックインターフェース
/// @brief SDK内部イベントコールバックインターフェース
@protocol YTSDKEventListener <NSObject>
/// @brief YTDataUpdateイベントコールバック
/// @param event NSString*フォーマットのコールバック
- (void)onYTDataEvent:(id _Nonnull)event;
/// @brief AIイベントコールバック
/// @param event dictフォーマットのコールバック
- (void)onAIEvent:(id _Nonnull)event;
/// @brief 表示イベントコールバック
/// @param event dictフォーマットのコールバック
- (void)onTipsEvent:(id _Nonnull)event;
/// @brief リソースパックイベントコールバック
/// @param event stringフォーマットのコールバック
- (void)onAssetEvent:(id _Nonnull)event;
@end
```

コールバックの設定に成功すると、各フレームの顔イベントごとに次のコールバックを行います。
```objectivec
- (void)onYTDataEvent:(id _Nonnull)event;
```
コールバックdataはJSON形式のデータで、具体的な意味は次のとおりです（256のポイントは上図の位置に対応します）。
```objectivec
/// @note フィールド意味リスト
/**
| フィールド | タイプ | 値の範囲 | 説明 |
| :---- | :---- |:---- | :---- |
| trace_id | int | [1,INF) | 顔id。連続ストリーム取得の過程で、idが同一であれば同じ顔であると認識できます |
| face_256_point | float | [0,screenWidthまたはscreenHeight] | 計512個。顔の256個の重要特徴点であり、画面左上隅が(0,0)です |
| face_256_visible             | float | [0,1]                               | 顔の256重要特徴点の可視度                                    |
| out_of_screen | bool | true/false | 顔が枠外に出ていないか |
| left_eye_high_vis_ratio      | float | [0,1]                               | 左目の特徴点のうち高視認度のものが占める割合                                   |
| right_eye_high_vis_ratio     | float | [0,1]                               | 右目の特徴点のうち高視認度のものが占める割合                                   |
| left_eyebrow_high_vis_ratio  | float | [0,1]                               | 左眉の特徴点のうち高視認度のものが占める割合                                   |
| right_eyebrow_high_vis_ratio | float | [0,1]                               | 右眉の特徴点のうち高視認度のものが占める割合                                   |
| mouth_high_vis_ratio         | float | [0,1]                               | 口の特徴点のうち高視認度のものが占める割合                                     |
**/
- (void)onYTDataEvent:(id _Nonnull)event;
```

## Androidインターフェースの説明

### Android統合ガイド

AndroidのSDKの統合ガイドについての詳細は、[Tencent Effectの独立した統合](https://intl.cloud.tencent.com/document/product/1143/45385)をご参照ください。

### Xmagicインターフェースのコールバック登録

顔の特徴点位置情報などのデータのコールバックを設定します。
```java
void setYTDataListener(XmagicApi.XmagicYTDataListener ytDataListener)
顔の情報などのデータのコールバックを設定します

public interface XmagicYTDataListener {
    void onYTDataUpdate(String data)
}
```
onYTDataUpdateはJSON string構造を返します。最大で5つの顔の情報を返します。
```json
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

### フィールドの意味

| フィールド                         | タイプ  | 値の範囲                                | 説明                                                   |
| :--------------------------- | :---- | :---------------------------------- | :------------------------------------------------------- |
| trace_id                     | int   | [1,INF)                             | 顔ID。連続してストリームを取得するとき、IDが同じである場合、同じ顔として認識します |
| face_256_point               | float | [0,screenWidth]または[0,screenHeight] | 計512個。顔の256個の重要特徴点であり、画面左上隅が(0,0)です。          |
| face_256_visible             | float | [0,1]                               | 顔の256個の重要特徴点の視認度。                                    |
| out_of_screen                | bool  | true/false                          | 顔が枠外に出ていないか。                                           |
| left_eye_high_vis_ratio      | float | [0,1]                               | 左目の特徴点のうち高視認度のものが占める割合。                                   |
| right_eye_high_vis_ratio     | float | [0,1]                               | 右目の特徴点のうち高視認度のものが占める割合。                                   |
| left_eyebrow_high_vis_ratio  | float | [0,1]                               | 左眉の特徴点のうち高視認度のものが占める割合。                                   |
| right_eyebrow_high_vis_ratio | float | [0,1]                               | 右眉の特徴点のうち高視認度のものが占める割合。                                   |
| mouth_high_vis_ratio         | float | [0,1]                               | 口の特徴点のうち高視認度のものが占める割合。                                     |

#### パラメータ

| パラメータ                                          | 意味             |
| :-------------------------------------------- | :--------------- |
| XmagicApi.XmagicYTDataListener ytDataListener | コールバック関数実装クラス。 |
