[](id:que1)
### 2台の携帯電話で同時にDemoを実行しているのに、お互いの画面が表示されないのはなぜですか？
2台の携帯電話でDemoを操作するとき、UserIDが異なるものを使用してください。TRTCでは、同一のUserID（SDKAppIDが異なる場合を除く）が2つの端末で同時に使用することをサポートしていません。


[](id:que2)
### ファイアウォールにはどのような制限がありますか？
SDK が UDP プロトコルを使用してオーディオビデオ伝送を行っていることから、 UDPに対してブロックがあるオフィスネットワークでは使用することができません。類似の問題があれば、 [企業ファイアウォール制限の対応](https://intl.cloud.tencent.com/document/product/647/35164)をご参照の上、問題原因を調べ解決してください。

[](id:que3)
### iOSのパッケージングの実行時にCrashした場合は？
iOS14以上のdebugモードの問題かどうか調査してください。より詳細な説明をご覧になる場合は、[公式の説明](https://flutter.cn/docs/development/ios-14#launching-debug-flutter-without-a-host-computer)をご参照ください。

[](id:que4)
### iOSでビデオが表示できない（Androidは正常）場合は？
お客様のプロジェクトの`info.plist`の `io.flutter.embedded_views_preview` の値がYESになっていることを確認してください。

[](id:que5)
### SDKのバージョンを更新した後、iOS CocoaPodsの実行エラーが出た場合は？
1. iOSディレクトリの下の`Podfile.lock`ファイルを削除します。
2. `pod repo update`を実行します。
3. `pod install`を実行します。
4. 再度実行します。

[](id:que6)
### Android Manifest merge failedでコンパイルに失敗した場合は？
1. `/example/android/app/src/main/AndroidManifest.xml` のファイルを開いてください。
2. `xmlns:tools="http://schemas.android.com/tools"` をmanifestの中に追加します。
3. `tools:replace="android:label"をapplicationの中に追加します。

![img](https://main.qcloudimg.com/raw/7a37917112831488423c1744f370c883.png)

[](id:que7)
### 署名がないために、実機でのデバックでエラーが出た場合は?
エラーメッセージが出る場合、下図のように表示されます。
![](https://main.qcloudimg.com/raw/809ae94061575b4e670f3a80ac9f3781.png)
1. Appleの署名証明書を購入する必要があります。その後、設定、署名の操作を実行すると、実機でデバックできるようになります。
2. 証明書の購入完了後、`target > signing & capabilities`で設定を行います。

[](id:que8)
### プラグインの中のswiftファイルを追加・削除した後、ビルド時に対応するファイルが見つからない場合は？
メインプロジェクトディレクトリの`/ios`ファイルパスで`pod install`を使用できます。

[](id:que9)
### Run エラー“Info.plit, error: No value at that key path or invalid key path: NSBonjourServices”が出た場合は？
`flutter clean`の実行後、再度実行してください。

[](id:que10)
### Pod install のエラーは？
エラーメッセージが出る場合、下図のように表示されます。
![](https://main.qcloudimg.com/raw/73db67cfc9e6b934fed947b63c6d2120.png)
エラーメッセージの中に pod install 時に `generated.xconfig`ファイルがないと表示され、このため実行エラーとなっています。解決には表示のとおりに**flutter pub getの実行が必要** です。
>? この問題は flutterのコンパイル後のトラブルです。新しいプロジェクトまたは`flutter clean`の実行後は、この問題が起きることはありません。

[](id:que11)
### 実行時のiOS版の依存エラーは？
エラーメッセージが出る場合、下図のように表示されます。
![](https://main.qcloudimg.com/raw/9102b3394560ca9df2f70549baabe3ff.png)
podsのtargetバージョンが依存するプラグインに対応できないため、エラーが生じている可能性があります。エラーの起きたpodsの中のtargetを対応するバージョンに変更する必要があります。

[](id:que12)
### Flutterはユーザー定義キャプチャとレンダリングをサポートしていますか。
現時点ではサポートしていません。ユーザー定義キャプチャとレンダリングのサポートの詳細については、[サポートしているプラットフォーム](https://intl.cloud.tencent.com/document/product/647/35158)をご参照ください。
