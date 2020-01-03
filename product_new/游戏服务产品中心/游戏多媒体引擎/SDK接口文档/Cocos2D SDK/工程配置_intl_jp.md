Tencent Cloud Gaming Multimedia Engine SDKをご購入いただき、ありがとうございます。Cocos2D開発者のデバッグ作業、及びTencent Cloud Gaming Multimedia EngineのAPI製品へのアクセスを容易にするために、ここで、Cocos2D開発に適用されるプロジェクトコンフィギュレーションを説明させていただきます。

## SDK 準備

 [ダウンロードガイド](https://intl.cloud.tencent.com/document/product/607/18521) から関連するDemo及び SDKをダウンロードしてください。

###  SDKリソースの解凍

1. 取得したSDKリソースを解凍します
2. フォルダーの内容は下記の通りです。

|フォルダーの名称                     | フォルダーの詳細|
| ----------------------|-----------------------------------        |
| TMG_SDK                    |ゲームビデオ・オーディオ SDK frameworkファイル        |
| TMGCocosDemo          |ゲームビデオ・オーディオ SDK プロジェクトの例                       |

## システム要求

SDKはMacシステムでコンパイルをサポートしています。

## iOS Xcode 準備作業

### 1.  SDKの関連するframeworkファイルをインポートします

frameworkをXcodeプロジェクトに追加し、ヘッダーファイル引用位置を設定する必要があります。

TMG_SDKフォルダーにはGMESDK.frameworkのゲームビデオ・オーディオSDK frameworkファイルがあり、プロジェクトに追加しなければなりません。

### 2. 依存ライブラリの追加
下図を参考してください。  
![](https://main.qcloudimg.com/raw/b6156b8c7a596248c148607070e38f67.png)

## Android 準備作業

### 1.  gmesdk、jarをlibsライブラリに追加します。
![](https://main.qcloudimg.com/raw/167b3fb575b65539aeaf9c700383e7c8.png)

### 2. Activity の中にsoファイルをインポートします

```
public class AppActivity extends Cocos2dxActivity {
    static final String TAG = "AppActivity";
    static OpensdkGameWrapper gameWrapper ;
    static {
        OpensdkGameWrapper.loadSdkLibrary();
    }
}
```

### 3. 初期化

oncreate 関数の中で初期化を行います、順序を間違えてはいけません。
```
protected void onCreate(Bundle savedInstanceState) {
        super.setEnableVirtualButton(false);
        super.onCreate(savedInstanceState);

        //初期化します、順序を間違えてはいけません。
        gameWrapper = new OpensdkGameWrapper(this);
        runOnGLThread(new Runnable() {
            @Override
            public void run() {
                gameWrapper.initOpensdk();
            }
        });
}
```

## 異なるプラットホームのエクスポート

Cocos2Dエンジンから異なるプラットホームをエクスポートするには、対応するプロジェクトコンフィギュレーションを行う必要があります。

|プラットホーム       | プロジェクトコンフィギュレーション      |
| ------------- |:-------------:|
| Android |[Android プロジェクトコンフィギュレーションドキュメンテーション](https://intl.cloud.tencent.com/document/product/607/10783)|
| iOS     |[iOS プロジェクトコンフィギュレーションドキュメンテーション](https://intl.cloud.tencent.com/document/product/607/10783)|
| Mac     |[Mac プロジェクトコンフィギュレーションドキュメンテーション](https://intl.cloud.tencent.com/document/product/607/10783)|