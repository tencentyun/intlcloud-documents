ここでは、主にTencent CloudのTRTC SDK(Flutter)をプロジェクトに素早く統合する方法を紹介します。以下の手順に従って設定すれば、 SDK の統合作業を完了できます。

## 環境要件
- Flutter 1.12およびそれ以降のバージョン。
- Androidの開発：
  - Android Studio 3.5およびそれ以降のバージョン。
  - AppにはAndroid 4.1およびそれ以降のバージョンのデバイスが必要です。
- iOSの開発：
  - Xcode 11.0およびそれ以降のバージョン。
  - プロジェクトが有効な開発者による署名を設定済みであることを確認してください。

## SDKの統合

Flutter SDKは[pubライブラリ](https://pub.dev/packages/tencent_trtc_cloud)に公開されています。`pubspec.yaml` を設定することで、更新を自動的にダウンロードできます。

1. プロジェクトの`pubspec.yaml` に次の依存関係を記述します。
```
dependencies:
  tencent_trtc_cloud: 最新バージョン番号
```

2. **カメラ**と**マイク**の許可が有効になると、音声通話機能が起動します。

#### iOS
1.`Info.plist`にカメラとマイクの許可申請を追加する必要があります。
```
<key>NSCameraUsageDescription</key>
<string>通常のビデオ通話が行えるようにカメラを許可します</string>
<key>NSMicrophoneUsageDescription</key>
<string>通常の音声通話が行えるようにマイクを許可します</string>
```
2.フィールド`io.flutter.embedded_views_preview`を追加し、値をYESに設定します。

#### Android
1. `/android/app/src/main/AndroidManifest.xml`ファイルを開きます。
2. `xmlns:tools="http://schemas.android.com/tools"` をmanifestの中に追加します。
3. `tools:replace="android:label"をapplicationの中に追加します。
>? この手順を実行しないと、[Android Manifest merge failed コンパイルの失敗](https://intl.cloud.tencent.com/zh/document/product/647/39242#que6)という問題が発生します。
![アイコン](https://main.qcloudimg.com/raw/7a37917112831488423c1744f370c883.png)





## よくあるご質問
- [iOSパッケージはCrashを実行しますか？](https://intl.cloud.tencent.com/zh/document/product/647/39242#que3)
- [iOSでビデオを表示できません（Androidでは正常です）。なぜですか？](https://intl.cloud.tencent.com/zh/document/product/647/39242#que4)
- [SDKバージョンを更新した後、iOS CocoaPodsはエラーを報告しますか？](https://intl.cloud.tencent.com/zh/document/product/647/39242#que5)
- [Android Manifest merge failedとは、コンパイルに失敗したのですか？](https://intl.cloud.tencent.com/zh/document/product/647/39242#que6)
- [署名がないことで、実機でのデバッグでエラーが報告されますか？](https://intl.cloud.tencent.com/zh/document/product/647/39242#que7)
- [プラグインのswiftファイルを追加または削除した後、buildする際に対応するファイルが見つからなくなりますか？](https://intl.cloud.tencent.com/zh/document/product/647/39242#que8)
- [実行エラー“Info.plit, error: No value at that key path or invalid key path: NSBonjourServices”とは？](https://intl.cloud.tencent.com/zh/document/product/647/39242#que9)
- [Pod installエラーとは？](https://intl.cloud.tencent.com/zh/document/product/647/39242#que10)
- [実行時にiOSのバージョンに依存するエラーが報告されますか？](https://intl.cloud.tencent.com/zh/document/product/647/39242#que11)


