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
[onRemoteUserLeaveRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#afa7d16e1e4c66d938fc2bc69f3e34c28)を使用すれば、ユーザーの退室イベントを監視できます。またこのインターフェースは、VideoCallのすべてのユーザーが退室するかまたはLIVEモードのキャスターが退室したときにのみコールバックをトリガーします。視聴者が退室するときに、コールバックはありません。 

[](id:que11)
### 携帯電話がロックされている状態、Appがバックエンドにある場合、またはAppがオフの場合に、音声ビデオ通話を行うにはどうすればいいですか。
オフライン応答などの機能で行います。詳細については、[オフライン応答の実現](https://intl.cloud.tencent.com/document/product/647/36068)をご参照ください。

[](id:que12)
### AndroidとWebとの相互運用性をサポートしていますか？
サポートしています。同じ[SDKAppID](https://console.cloud.tencent.com/trtc/app)を使用し、同じルームに入室して通話します。詳細については、下記リンクのドキュメントを参照してDemoを設定してください。
- [Demoクイックスタート(Android)](https://intl.cloud.tencent.com/document/product/647/35084)
- [Demoクイックスタート（Web）](https://intl.cloud.tencent.com/document/product/647/35607)

[](id:que13)
### ライブストリーミング中、キャスター側と視聴側のマイクを接続しますが、どちら側からもマイク接続を起動することができますか？
どちら側からも起動することができます。視聴者とキャスター側の開始のロジックは同じです。具体的な操作については、[ライブストリーミングクイックスタート(Android)](https://intl.cloud.tencent.com/document/product/647/35108)をご参照ください。

[](id:que14)
### 多人数でのビデオミーティング中に、モバイル端末とWeb端末から同じルームに入室できますか？
入室できます。[SDKAppID](https://console.cloud.tencent.com/trtc/app)とルーム番号が一致し、異なるユーザーIDを使用する必要があります。

[](id:que15)
### 同じページで、N個のTRTCオブジェクトを作成し、N個のユーザーIDでN個のルームにそれぞれログインすることはできますか？
できます。[Version 7.6バージョン](https://intl.cloud.tencent.com/document/product/647/34615)以降、1人のユーザーによる複数ルームへの入室をサポートしています。


[](id:que16)
### SDKの最新のバージョン番号はどのように確認しますか。
- 自動ロードを使用する場合は、`latest.release`により最新バージョンとマッチングされて自動ロードが実行されるため、バージョン番号を変更する必要はありません。具体的な統合方法については[SDKクイックインテグレーション](https://intl.cloud.tencent.com/document/product/647/35092)をご参照ください。
- 現在のSDKの最新バージョン番号はリリースノートから確認することができます。以下をご参照ください。
  - iOS & Androidでは、[リリースノート（App）](https://intl.cloud.tencent.com/document/product/647/39426)をご参照ください。
  - デスクトップブラウザでは、[リリースノート（Web）](https://intl.cloud.tencent.com/document/product/647/39779)をご参照ください。
  - Electronでは、[リリースノート（Electron）](https://intl.cloud.tencent.com/document/product/647/38702)をご参照ください。


