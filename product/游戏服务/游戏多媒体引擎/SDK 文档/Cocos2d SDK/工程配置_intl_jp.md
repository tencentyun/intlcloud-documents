Tencent Cloudゲームマルチメディアエンジン（GME）SDKへようこそ。Cocos2D開発者がTencent Cloud GME製品のAPIを容易にデバッグして導入するために、ここでCocos2D開発のためのプロジェクト構成を紹介します。

## SDKの準備

[ダウンロードガイド](https://cloud.tencent.com/document/product/607/18521)で関連のDemoとSDKをダウンロードしてください。

### SDKリソースの解凍

1. 取得されたSDKリソースを解凍します
2. フォルダの内容は以下の通りです。

|フォルダ名称                     | フォルダ詳細
| ----------------------|-----------------------------------        |
| TMG_SDK                    |ゲーム音声ビデオSDK frameworkファイル        |
| TMGCocosDemo          |ゲーム音声ビデオSDKサンプルプロジェクト                        |

## システム要件

SDKは、Macシステムでのコンパイルをサポートします。

## iOS Xcodeの準備作業

### 1. SDKに関連するframeworkファイルをインポートします

Xcodeプロジェクトにframeworkを追加し、ヘッダファイルの参照場所を設定する必要があります。

TMG_SDKフォルダには、GMESDK.frameworkゲームの音声ビデオSDK frameworkファイルが含まれています。これらをプロジェクトに追加する必要があります。

### 2. 依存ライブラリを追加します

下図を参照します。  
![](https://main.qcloudimg.com/raw/b6156b8c7a596248c148607070e38f67.png)

## Androidの準備作業

### 1. tmgsdk.jarをlibsライブラリに追加します。

![](https://main.qcloudimg.com/raw/fe1bde45a15f273aa9b9707420bb2696.png)

### 2. soファイルをActivityにインポートします

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

oncreate関数で初期化します。順序は間違ってはいけません。
```
protected void onCreate(Bundle savedInstanceState) {
        super.setEnableVirtualButton(false);
        super.onCreate(savedInstanceState);

        //初期化、順序は間違ってはいけません
        AVChannelManager.setIMChannelType(AVChannelManager.IMChannelTypeImplementInternal);
        gameWrapper = new OpensdkGameWrapper(this);
        runOnGLThread(new Runnable() {
            @Override
            public void run() {
                gameWrapper.initOpensdk();
            }
        });
}
```

