## ステップ1：美顔リソースのダウンロードと統合

1. 購入したパッケージに応じて[SDKのダウンロード](https://intl.cloud.tencent.com/document/product/1143/45377)を行います。
2. ファイルをご自身のプロジェクトに追加します。
<dx-tabs>
::: Android
1. appモジュール下でbuild.gradleファイルを見つけ、対応するパッケージのmaven参照アドレスを追加します。例えばS1-04パッケージを選択した場合は下記を追加します。
```groovy
dependencies{
      implementation 'com.tencent.mediacloud:TencentEffect_S1-04:latest.release'
   }
```
**各パッケージに対応するmavenアドレスについては、[ドキュメント](https://intl.cloud.tencent.com/document/product/1143/45385)をご参照ください**。
2. appモジュール下でsrc/main/assetsフォルダを見つけます。存在しない場合は作成し、ダウンロードしたSDKパッケージにMotionResフォルダがあるかどうかをチェックし、もしあればそのフォルダを`../src/main/assets`ディレクトリ下にコピーします。
3. appモジュール下でAndroidManifest.xmlファイルを見つけ、applicationテーブルに次のタグを追加します
```xml
 <uses-native-library
           android:name="libOpenCL.so"
           android:required="true" />
```
追加すると下図のようになります。
![](https://qcloudimg.tencent-cloud.cn/raw/adca155b8fa60600465bdfc6e78ebb2b.png)
:::
::: iOS
1. 美顔リソースをプロジェクトに追加します。追加すると下図のようになります（リソースの種類と下図は完全には一致しません）。
![](https://qcloudimg.tencent-cloud.cn/raw/e5cb4984aa2bfa14fd4f837acf465cfa.png)
2. demoの中からdemo/lib/producer内の4つのクラスである、BeautyDataManager、BeautyPropertyProducer、BeautyPropertyProducerAndroid、BeautyPropertyProducerIOSをコピーしてご自身のFlutterプロジェクトに追加します。これらの4つのクラスは、美顔リソースを設定し、美顔タイプを美顔パネルに表示するために用いられます。
:::
</dx-tabs>


## ステップ2：FlutterバージョンSDKの参照

プロジェクトのpubspec.yamlファイルに下記の参照を追加します。
```json
 tencent_effect_flutter:
   git:
     url: https://github.com/TencentCloud/tencenteffect-sdk-flutter
```

## ステップ3：TRTCとのバインド
<dx-tabs>
::: Android
アプリケーションのapplicationクラスのoncreateメソッド（またはFlutterActivityのonCreateメソッド）に次のコードを追加します。
```jav
TRTCCloudPlugin.register(new XmagicProcesserFactory());
```
:::
::: iOS
アプリケーションのAppDelegateクラスのdidFinishLaunchingWithOptionsメソッドに次のコードを追加します。
```objective-c
XmagicProcesserFactory *instance = [[XmagicProcesserFactory alloc] init];
[TencentTRTCCloud registerWithCustomBeautyProcesserFactory:instance];
```
追加すると下図のようになります。
![](https://qcloudimg.tencent-cloud.cn/raw/3f2de0a60696f18daedde2228d65076a.png)

:::
</dx-tabs>

## ステップ4：リソース初期化インターフェースの呼び出し
```dart
  String dir =  await BeautyDataManager.getInstance().getResDir();
   TXLog.printlog('ファイルパス：$dir');
   TencentEffectApi.getApi()?.initXmagic(dir,(reslut) {
     _isInitResource = reslut;
     callBack.call(reslut);
     if (!reslut) {
       Fluttertoast.showToast(msg: "リソースの初期化に失敗しました");
     }
   }); TencentEffectApi.getApi()?.initXmagic((reslut) {
     if (!reslut) {
       Fluttertoast.showToast(msg: "リソースの初期化に失敗しました");
     }
   });
```

## ステップ5：美顔権限承認を実行
```dart
TencentEffectApi.getApi()?.setLicense(licenseKey, licenseUrl,
           (errorCode, msg) {
         TXLog.printlog("認証結果を印刷します errorCode = $errorCode   msg = $msg");
         if (errorCode == 0) {
            //認証に成功しました
         }
       });
```

## ステップ6：美顔を有効にする
```dart
///美顔操作を有効にします
 var enableCustomVideo = await trtcCloud.enableCustomVideoProcess(open);
```

## ステップ7：美顔属性の設定

```dart
    TencentEffectApi.getApi()?.updateProperty(_xmagicProperty!);
///_xmagicPropertyではBeautyDataManager.getInstance().getAllPannelData();によってすべての属性を取得できます。美顔属性を使用したい場合はupdatePropertyメソッドによって属性を設定できます。
```

## ステップ8：その他の属性の設定

- **美顔サウンドエフェクトの一時停止**
```dart
 TencentEffectApi.getApi()?.onPause();  
```
- **美顔サウンドエフェクトの再開**
```dart
TencentEffectApi.getApi()?.onResume();
```
- **美顔イベントの監視**
```dart
TencentEffectApi.getApi()
       ?.setOnCreateXmagicApiErrorListener((errorMsg, code) {
         TXLog.printlog("美顔オブジェクトの作成にエラーが発生しました errorMsg = $errorMsg , code = $code");
   });   ///美顔を作成する前に設定が必要です
```
- **顔、ジェスチャー、体の検出状態コールバックの設定**
```dart
TencentEffectApi.getApi()?.setAIDataListener(XmagicAIDataListenerImp());
```
- **動的エフェクトプロンプトのコールバック関数の設定**
```dart
TencentEffectApi.getApi()?.setTipsListener(XmagicTipsListenerImp());
```
- **顔の特徴点位置情報などのデータコールバックの設定（S1-05およびS1-06パッケージの場合のみコールバック）**
```dart
TencentEffectApi.getApi()?.setYTDataListener((data) {
     TXLog.printlog("setYTDataListener  $data");
   });
```
- **すべてのコールバックの削除**。ページが破棄された場合はすべてのコールバックを削除する必要があります。
```dart
 TencentEffectApi.getApi()?.setOnCreateXmagicApiErrorListener(null);
 TencentEffectApi.getApi()?.setAIDataListener(null);
 TencentEffectApi.getApi()?.setYTDataListener(null);
 TencentEffectApi.getApi()?.setTipsListener(null);
```

>? インターフェースの詳細についてはインターフェースドキュメントを、その他についてはDemoプロジェクトをそれぞれ参照できます。

## ステップ9：美顔パネル上の美顔データの追加と削除
BeautyDataManager、BeautyPropertyProducer、BeautyPropertyProducerAndroid、BeautyPropertyProducerIOSの4つのクラスでは、美顔パネルデータの設定を自由に操作できます。
- **美顔リソースの追加**
ステップ1の方法に従ってリソースファイルを対応するリソースフォルダ内に追加します。例えば、2D動的エフェクトのリソースを追加したい場合は次のようになります。
	1. リソースを必ずプロジェクトの`android/xmagic/src.mian/assets/MotionRes/2dMotionRes`ディレクトリ下に置きます。
<img src="https://qcloudimg.tencent-cloud.cn/raw/7e91b97099e3d337de31c4893686759b.png" style="zoom:50%;" />
	2. その上で、リソースをプロジェクトの`ios/Runner/xmagic/2dMotionRes.bundle`ディレクトリ下に追加します。
<img src="https://qcloudimg.tencent-cloud.cn/raw/8c806cb1c77d9c49b787ab17f77a2f0d.png" style="zoom:50%;" />
- **美顔リソースの削除**
Licenseによっては美顔と美ボディの一部機能の権限がない場合があります。この一部機能は美顔パネル上に表示する必要はないため、美顔パネルデータの設定でこの一部機能の設定を削除する必要があります。
例えばリップのエフェクトを削除する場合は、BeautyPropertyProducerAndroidクラスおよびBeautyPropertyProducerIOSクラスのgetBeautyDataメソッドから次のコードをそれぞれ削除します。
<img src="https://qcloudimg.tencent-cloud.cn/raw/774aa1367fce726b17e34319d1b08bc2.png" style="zoom:50%;" />

