## 機能説明
カメラのopenGLテクスチャを入力すると、Apple ARKitのルールに従って、52種類の顔の表情のBlendShapeデータがリアルタイムで出力されます。詳細については、[ARFaceAnchor](https://developer.apple.com/documentation/arkit/arfaceanchor/blendshapelocation)をご参照ください。これらの表情データを利用して、Unityに渡してモデルを動かすといった、さらに進んだ開発を行うことができます。

## Android統合ガイド
AndroidのSDKの統合ガイドについての詳細は、[Tencent Effectの独立した統合](https://intl.cloud.tencent.com/document/product/1143/45385)をご参照ください。

### インターフェースの呼び出し
1. 機能スイッチをオンにします。
```
//XmagicApi.java
//featureName = XmagicConstant.FeatureName.ANIMOJI_52_EXPRESSION
public void setFeatureEnableDisable(String featureName, boolean enable);

```
2. 顔の特徴点位置情報データのコールバックを設定します。
```java
//XmagicApi.java
void setYTDataListener(XmagicApi.XmagicYTDataListener ytDataListener)

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
  "mouth_high_vis_ratio":1.0,
  "expression_weights":[
		0.12,
		-0.32
		...
	]
 },
 ...
 ]
}
```

### フィールドの意味
- **trace_id**：顔ID。連続ストリーム取得の過程で、IDが同一であれば同じ顔であると認識できます。
- **expression_weights**：リアルタイムの表情blendshapeデータです。配列の長さは52で、各数値の値の範囲は-1.0～1.0です。
- その他のフィールドは、[顔情報](https://intl.cloud.tencent.com/document/product/1143/45399)にあります。関連するLicenseを購入した場合に、それらのフィールドを取得できます。表情データのみを取得したい場合は、それらのフィールドを無視してください。