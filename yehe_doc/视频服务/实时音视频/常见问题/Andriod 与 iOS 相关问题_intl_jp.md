[](id:que1)
###  モバイル端末(Andriod / iOS)は、何種類のシステム音量モードをサポートしていますか？
2つのシステム音量タイプ、すなわち通話音量タイプとメディア音量タイプをサポートしています。
- 通話音量は、携帯電話の通話シーン向けに設計された音量タイプです。携帯電話に付属されているエコーキャンセル機能を使用すると、メディア音量タイプよりも音質が落ちます。音量ボタンで音量をゼロに調節することはできませんが、Bluetoothヘッドセットのマイクはサポートされています。
- メディア音量は、携帯電話の音楽シーン向けに設計された音量タイプです。音質は通話音量タイプよりも優れています。音量ボタンを押して、音量をゼロに調節できます。メディア音量タイプを使用する場合、AEC機能を有効にすると、SDKは内蔵された音響処理アルゴリズムを起動して、音声の2次処理を行います。メディア音量モードでは、Bluetoothヘッドセットは内蔵マイクを使用して集音することはできず、携帯電話のマイクでしか集音できません。

[](id:que2)
###  モバイルSDKのプッシュを1080p解像度に設定するにはどうすればいいですか？
1080PはTX_Enum_Type_VideoResolutionにおいて114と定義されているので、解像度を直接設定し列挙値を渡すだけで設定できます。

[](id:que4)
###  TRTCモバイル端末でスクリーンキャプチャ（画面共有）を行うにはどうすればいいですか？	
- **Android 端末**：Version 7.2以降のバージョンで携帯電話のスクリーンキャプチャをサポートしています。具体的な実践方法は[リアルタイム画面共有（Android）](https://intl.cloud.tencent.com/document/product/647/37337)をご参照ください。
- **iOS 端末**：Version 7.2以降のバージョンでアプリ内のスクリーンキャプチャをサポートしています。Version 7.6以降のバージョンでは携帯電話のスクリーンキャプチャおよびアプリ内のスクリーンキャプチャをサポートしています。具体的な実践方法は[リアルタイム画面共有（iOS）](https://intl.cloud.tencent.com/document/product/647/37338)をご参照ください。



[](id:que5)
###  TRTC Android端末は64ビットのarm64-v8aアーキテクチャをサポートしていますか？
TRTC 6.3バージョンでは、arm64-v8aアーキテクチャABIのサポートが開始されています。


[](id:que7)
###  iOS端末はSwiftの統合をサポートしていますか？
サポートしています。サードパーティライブラリのフローにそのまま従ってSDKを統合すればOKです。また、[Demoクイックスタート(iOS&Mac)](https://intl.cloud.tencent.com/document/product/647/35086)も参照することができます。


[](id:que9)
###  TRTC SDKは、iOSのバックグラウンド処理をサポートしていますか？
サポートしています。現在のプロジェクトを選択し、**Capabilities**において**Background Modes**を**ON**に設定して、**Audio、AirPlay and Picture in Picture**にチェックを入れると、バックグラウンド処理が実行されます。詳細を下図に示します。
![](https://main.qcloudimg.com/raw/d960dfec88388936abce2d4cb77ac766.jpg)

[](id:que10)
### iOS端末はリモート退室を監視できますか？
[onRemoteUserLeaveRoom](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#afa7d16e1e4c66d938fc2bc69f3e34c28)を使用すれば、ユーザーの退室イベントを監視できます。またこのインターフェースは、VideoCallのすべてのユーザーが退室するかまたはLIVEモードのホストが退室したときにのみコールバックをトリガーします。視聴者が退室するときに、コールバックはありません。 

[](id:que11)
### 携帯電話がロックされている状態で、ビデオ通話を行うにはどうすればいいですか？
オフライン応答などの機能で行います。詳細については、[オフライン応答の実現](https://intl.cloud.tencent.com/document/product/647/36068)をご参照ください。

[](id:que12)
### AndroidとWebとの相互運用性をサポートしていますか？
サポートしています。同じ[SDKAppID](https://console.cloud.tencent.com/trtc/app)を使用し、同じルームに入室して通話します。詳細については、下記リンクのドキュメントを参照してDemoを設定してください。
- [Demoクイックスタート(Android)](https://intl.cloud.tencent.com/document/product/647/35084)
- [Demoクイックスタート（デスクトップブラウザ）](https://intl.cloud.tencent.com/document/product/647/35607)

[](id:que13)
### ライブストリーミング中、キャスター側と視聴側のマイクを接続しますが、どちら側からもマイク接続を起動することができますか？
どちら側からも起動することができます。視聴者とキャスター側の開始のロジックは同じです。具体的な操作については、[ライブストリーミングクイックスタート(Android)](https://intl.cloud.tencent.com/document/product/647/35108)をご参照ください。

[](id:que14)
### 多人数でのビデオミーティング中に、モバイル端末とWeb端末から同じルームに入室できますか？
入室できます。[SDKAppID](https://console.cloud.tencent.com/trtc/app)とルーム番号が一致し、異なるユーザーIDを使用する必要があります。

[](id:que15)
### 同じページで、N個のTRTCオブジェクトを作成し、N個のユーザーIDでN個のルームにそれぞれログインすることはできますか？
できます。[Version 7.6バージョン](https://intl.cloud.tencent.com/document/product/647/34615)以降、1人のユーザーによる複数ルームへの入室をサポートしています。

[](id:que16_flutter)
### 2台の携帯電話で同時にDemoを実行しているのに、お互いの画面が表示されないのはなぜですか？
2台の携帯電話でDemoを操作するとき、UserIDが異なるものを使用してください。TRTCでは、同一のUserID（SDKAppIDが異なる場合を除く）が2つの端末で同時に使用することをサポートしていません。

[](id:que17_flutter)
### ファイアウォールにはどのような制限がありますか？
SDK が UDP プロトコルを使用してオーディオビデオ伝送を行っていることから、 UDPに対してブロックがあるパブリックネットワークでは使用することができません。類似の問題があれば、 [企業ファイアウォール制限の対応](https://intl.cloud.tencent.com/document/product/647/35164)をご参照の上、問題原因を調べ解決してください。

[](id:que18_flutter)
### iOSのパッケージングの実行時にCrashした場合は？
iOS14以上のdebugモードの問題かどうか調査してください。具体的には [公式の説明](https://flutter.cn/docs/development/ios-14#launching-debug-flutter-without-a-host-computer)をご参照ください。

[](id:que19_flutter)
### iOSでビデオが表示できない（Androidは正常）場合は？
お客様のプロジェクトの`info.plist`の `io.flutter.embedded_views_preview` の値がYESになっていることを確認してください。

[](id:que20_flutter)
### SDKのバージョンを更新した後、iOS CocoaPodsの実行エラーが出た場合は？
1. iOSディレクトリの下の`Podfile.lock`ファイルを削除します。
2. `pod repo update`を実行します。
3. `pod install`を実行します。
4. 再度実行します。

[](id:que21_flutter)
### Android Manifest merge failedでコンパイルに失敗した場合は？
1. `/example/android/app/src/main/AndroidManifest.xml` のファイルを開いてください。
2. `xmlns:tools="http://schemas.android.com/tools"` をmanifestの中に追加します。
3. `tools:replace="android:label"をapplicationの中に追加します。

![img](https://main.qcloudimg.com/raw/7a37917112831488423c1744f370c883.png)

[](id:que22_flutter)
### 署名がないために、実機でのデバックでエラーが出た場合は?
エラーメッセージが出る場合、下図のように表示されます。
![](https://main.qcloudimg.com/raw/809ae94061575b4e670f3a80ac9f3781.png)
1. Appleの署名証明書を購入する必要があります。その後、設定、署名の操作を実行すると、実機でデバックできるようになります。
2. 証明書の購入完了後、`target > signing & capabilities`で設定を行います。

[](id:que23_flutter)
### プラグインの中のswiftファイルを追加・削除した後、ビルド時に対応するファイルが見つからない場合は？
メインプロジェクトディレクトリの`/ios`ファイルパスで`pod install`を使用できます。

[](id:que24_flutter)
### Run エラー“Info.plit, error: No value at that key path or invalid key path: NSBonjourServices”が出た場合は？
`flutter clean`の実行後、再度実行してください。

[](id:que25_flutter)
### Pod install のエラーは？
エラーメッセージが出る場合、下図のように表示されます。
![](https://main.qcloudimg.com/raw/73db67cfc9e6b934fed947b63c6d2120.png)
エラーメッセージの中に pod install 時に `generated.xconfig`ファイルがないと表示され、このため実行エラーとなっています。解決には表示のとおりに**flutter pub getの実行が必要** です。
>? この問題は flutterのコンパイル後のトラブルです。新しいプロジェクトまたは`flutter clean`の実行後は、この問題が起きることはありません。

[](id:que26_flutter)
### 実行時のiOS版の依存エラーは？
エラーメッセージが出る場合、下図のように表示されます。
![](https://main.qcloudimg.com/raw/9102b3394560ca9df2f70549baabe3ff.png)
podsのtargetバージョンが依存するプラグインに対応できないため、エラーが生じている可能性があります。エラーの起きたpodsの中のtargetを対応するバージョンに変更する必要があります。












