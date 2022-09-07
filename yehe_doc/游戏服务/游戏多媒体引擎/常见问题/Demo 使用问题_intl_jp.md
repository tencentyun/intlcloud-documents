
### どのようにGMEのDemoとSDKをダウンロードしますか？

GMEに関連するDemoとSDKのダウンロードについては、[ダウンロードガイド](https://intl.cloud.tencent.com/document/product/607/18521)をご参照ください。現在、公式サイトではUnityエンジンのDemo、Cocos2DエンジンのDemo、Android及びiOSのオリジナルDemoが提供されています。

### GMEのWindows DemoはどのバージョンのVSで起動しますか？
### VS2015を使用して起動してください。VS2010で起動したい場合、事前にプロジェクトをダウングレードしてください。

### GMEのDemoをダウンロードした後、どのように自分で申請したアカウントに切り替えますか？

- [コンソール](https://console.cloud.tencent.com/gamegme/detail/1400391524)のサービス管理でAppIDと権限キーを取得してください。
- お客様が自身のAppIDを使用する場合、AVChatViewController中のGetAuthBufferでリアルタイム音声のKeyを変更してください。

### GMEではOpenIdを1つだけ使用することができますか？

GMEエンジンを初期化するときOpenIdを使用する必要があります。OpenIdはユーザを一意に識別するものです。複数の端末で同じOpenIdを使用すれば、例えば、遠隔地の端末でログインすれば、アカウント異常が発生し、GMEの機能を使用できません。

### ルームには1人だけいますが、どのようにローカルで体験しますか？

他の端末でdemoを使用し同じルームに参加してください。

### Demoを使用するとき、エラーメッセージerrinfo=priv map info errorが出力されました。どうすればいいですか？

これは、ルーム参加のパラメータにエラーが発生したためです。SDKAppID、権限キーが変更されているかを確認してください。

### どのようにダウンロードしたDemoを使用しますか？

- Demo利用ガイドドキュメントをご参照ください。
- Unity Demoの場合、[Unity Demoマニュアル](https://intl.cloud.tencent.com/document/product/607/38535)をご参照ください。

### UnityでエクスポートしたDemoを使用するとき、音声が聞こえない問題がよく発生します。これはなぜでしょうか？
UnityのDemoではOnApplicationFocusが設定されています。プログラムがフォーカスを失うとき、Pauseインターフェースを呼び出して、音声を一時停止します。バックグランドで音声を再生する場合、Pauseインターフェースを呼び出すソースコードをリムーブすればよいです。

### ログはどのように取得しますか？

**ログを提供するとき、問題の発生時間も一緒に提供してください**
`QAVSDK_`に日付が付いている`.log`ファイルは、ログファイルです。ディレクトリは以下のとおりです：

| フラットフォーム    | パス                                                         |
| ------- | ------------------------------------------------------------ |
| Windows | `%appdata%\Tencent\GMEGLOBAL\ProcessName`                            |
| iOS     | `Application/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/Documents`   |
| Android | `/sdcard/Android/data/xxx.xxx.xxx/files`                       |
| Mac     | `/Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents` |

Unityエンジンを使用しPCで開発する場合、 `%appdata%\Tencent\GME\Unity.exe`パスの配下でログを探してください。

iOSの物理デバイスで、APPのファイル共有を通してログを取得することができます。具体的な操作手順は以下のとおりです：
1. APPの`Info.plist`ファイルにUIFileSharingEnabledキーを追加し、キーの値に“YES”を設定します。
2. 共有するファイルをAPPのDocumentsディレクトリに置きます。
3. デバイスをユーザのコンピューターに挿入すると、iTunesは選択したデバイスのAppsタグにFile Sharingエリアを表示します。
4. その後、ユーザはこのディレクトリにファイルを追加したり、ファイルをコンピューターに移動したりすることができます。

>?GME2.8.4以前のバージョンを使用した場合、Windows系のログパスは`%appdata%\Tencent\GME\ProcessName`です。

**ログレベル**

ログを提供するとき、SetLogLevelを呼び出してログレベルを設定したことがあれば、デフォルトのログレベルに復元することをお勧めします。
