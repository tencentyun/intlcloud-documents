ここでは、主にTencent Cloud TRTC SDK（Unity）をプロジェクトに素早く統合する方法をご紹介します。以下の手順に従って設定すれば、SDKの統合作業を完了できます。

## 環境要件
* Unityの推奨バージョン： 2020.2.1f1c1。
* 現在、Android、iOS、Windows、Mac（Macはベータ版テスト中です)プラットフォームをサポートしています。
* `Android Build Support`、`iOS Build Support`、`Winodows Build Support`および`MacOs Build Support`モジュールが含まれている必要があります。
- その内、iOS端末の開発には以下が必要です。
  - Xcode 11.0およびそれ以降のバージョン。
  - プロジェクトが有効な開発者による署名を設定済みであることを確認してください。

## SDKの統合
1. SDKおよび付属する[Demoソースコード](https://github.com/tencentyun/TRTCUnitySDK)をダウンロードします。
2. 解凍後、プロジェクト内の`TRTCUnitySDK/Assets/TRTCSDK/SDK`フォルダを自分のプロジェクトのAssetsディレクトリ下にコピーします。

## よくあるご質問
### Androidではネットワーク権限の問題が表示されますか。
プロジェクト内の`/Assets/Plugins/AndroidManifest.xml`ファイルを同じレベルのディレクトリ下に配置してください。

### Androidではオーディオビデオの権限はないのですか。
Android端末のマイク、カメラの権限は手動で申請します。具体的な方法については以下のコードをご参照ください。
```
#if PLATFORM_ANDROID
if (!Permission.HasUserAuthorizedPermission(Permission.Microphone))
 {
     Permission.RequestUserPermission(Permission.Microphone);
 }
 if (!Permission.HasUserAuthorizedPermission(Permission.Camera))
 {
     Permission.RequestUserPermission(Permission.Camera);
 }
 #endif
```  
