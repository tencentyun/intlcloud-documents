<span id="que1"></span>
###  モバイル端末(Andriod / iOS)は、何種類のシステム音量モードをサポートしていますか？
2つのシステム音量タイプ、すなわち通話音量タイプとメディア音量タイプをサポートしています。
- 通話音量は、携帯電話の通話シーン向けに設計された音量タイプです。携帯電話に付属されているエコーキャンセル機能を使用すると、メディア音量タイプよりも音質が落ちます。音量ボタンで音量をゼロに調節することはできませんが、Bluetoothヘッドセットのマイクはサポートされています。
- メディア音量は、携帯電話の音楽シーン向けに設計された音量タイプです。音質は通話音量タイプよりも優れています。音量ボタンを押して、音量をゼロに調節できます。メディア音量タイプを使用する場合、AEC機能を有効にすると、SDKは内蔵された音響処理アルゴリズムを起動して、音声の2次処理を行います。メディア音量モードでは、Bluetoothヘッドセットは内蔵マイクを使用して集音することはできず、携帯電話のマイクでしか集音できません。

<span id="que2"></span>
###  モバイルSDKのプッシュを1080p解像度に設定するにはどうすればいいですか？
1080PはTX_Enum_Type_VideoResolutionにおいて114と定義されているので、解像度を直接設定し列挙値を渡すだけで設定できます。

<span id="que4"></span>
###  TRTCモバイル端末でスクリーンキャプチャ（画面共有）を行うにはどうすればいいですか？	
バージョン7.2以降、Android端末は携帯電話のスクリーンキャプチャをサポートし、iOS端末はアプリ内のスクリーンキャプチャをサポートしています。[公式 Demo](https://github.com/tencentyun/TRTCSDK)のソースコードを直接ご参照ください。

<span id="que5"></span>
###  TRTCAndroid端末は64ビットのarm64-v8aアーキテクチャをサポートしていますか？
TRTC 6.3バージョンでは、arm64-v8aアーキテクチャABIのサポートが開始されています。

<span id="que7"></span>
###  iOS端末はSwiftの統合をサポートしていますか？
サポートしています。サードパーティライブラリのフローにそのまま従ってSDKを統合すればOKです。また、[Demoクイックスタート(iOS&Mac)](https://intl.cloud.tencent.com/document/product/647/35086)も参照することができます。

<span id="que9"></span>
###  TRTC SDKはiOSのバックグラウンド処理をサポートしていますか？
サポートしています。現在のプロジェクトを選択し、**Capabilities**において**Background Modes**を**ON**に設定して、**Audio、AirPlay and Picture in Picture**にチェックを入れると、バックグラウンド処理が実行されます。詳細を下図に示します。
![](https://main.qcloudimg.com/raw/d960dfec88388936abce2d4cb77ac766.jpg)

<span id="que10"></span>
### iOS端末はリモート退室を監視できますか？
[onRemoteUserLeaveRoom](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#afa7d16e1e4c66d938fc2bc69f3e34c28)を使用すれば、ユーザーの退室イベントを監視できます。またこのインターフェースは、VideoCallのすべてのユーザーが退室するかまたはLIVEモードのホストが退室したときにのみコールバックをトリガーします。視聴者が退室するときに、コールバックはありません。 

<span id="que11"></span>
### 携帯電話がロックされている状態で、ビデオ通話を行うにはどうすればいいですか？
オフライン応答などの機能で行います。詳細については、[オフライン応答の実現](https://intl.cloud.tencent.com/document/product/647/36068)をご参照ください。

<span id="que12"></span>
### AndroidとWebとの相互運用性をサポートしていますか？
サポートしています。同じ[SDKAppID](https://console.cloud.tencent.com/trtc/app)を使用し、同じルームに入室して通話します。詳細については、下記リンクのドキュメントを参照してDemoを設定してください。
- [Demoクイックスタート(Android)](https://intl.cloud.tencent.com/document/product/647/35084)
- [Demoクイックスタート（デスクトップブラウザ）](https://intl.cloud.tencent.com/document/product/647/35607)

<span id="que13"></span>
### ライブストリーミング中、ホスト側と視聴側のマイクを接続しますが、どちら側からもマイク接続を起動することができますか？
どちら側からも起動することができます。視聴者とホスト側の開始のロジックは同じです。具体的な操作については、[ライブストリーミングクイックスタート(Android)](https://intl.cloud.tencent.com/document/product/647/35108)をご参照ください。

<span id="que14"></span>
### 多人数でのビデオミーティング中に、モバイル端末とWeb端末から同じルームに入室できますか？
入室できます。[SDKAppID](https://console.cloud.tencent.com/trtc/app)とルーム番号が一致し、異なるユーザーIDを使用する必要があります。

<span id="que15"></span>
### 同じページで、N個のTRTCオブジェクトを作成し、N個のユーザーIDでN個のルームにそれぞれログインすることはできますか？
できます。[Version 7.6バージョン](https://intl.cloud.tencent.com/document/product/647/34615)以降、1人のユーザーによる複数ルームへの入室をサポートしています。
