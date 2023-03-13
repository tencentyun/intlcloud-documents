
### GME Sample ProjectおよびSDKをダウンロードするには、どうすればよいですか？

GMEに関連するSample ProjectおよびSDKをダウンロードし、詳細については、[ダウンロードガイド](https://intl.cloud.tencent.com/document/product/607/18521)をご参照ください。公式サイトでは、現在、Unityエンジン、Unrealエンジン、Cocos2Dエンジン、Android、iOS、Windows、macOS、およびWebネイティブ開発のSample Projectを提供しています。

### GMEのWindows Sample ProjectはどのバージョンのVSで起動しますか。
### VS2015を使用して起動してください。VS2010で起動したい場合、事前にプロジェクトをダウングレードしてください。

### GME Sample Projectをダウンロードした後、申請したアカウントに置き換えるにはどうすればよいですか？

- コンソール[サービス管理-アプリケーション設定](https://console.cloud.tencent.com/gamegme)でAppIDと権限キーを取得する必要があります。
- お客様が自身のAppIDを使用する場合、AVChatViewController中のGetAuthBufferでリアルタイム音声のKeyを変更してください。


### GMEの複数のユーザーが同じOpenIDを使用すると、問題になりますか？
GMEエンジンを初期化するとき、OpenIdを使用する必要があります。OpenIdはアプリケーションにおけるユーザーを一意に識別するものです。複数の端末で同じOpenIdを使用すれば（例えば遠隔地の端末でログインすれば）、アカウント異常が発生し、GMEの機能を正常に使用できません。

### ルームには1人だけいますが、どのようにローカルで体験しますか？

別の端末デバイスでSample Projectを使って同じルームに入ってください。

### Sample Projectを使用するとき、errinfo=priv map info errorというエラーが報告されると、どうすればよいですか？

これは、ルーム参加のパラメータにエラーが発生したためです。SDKAppID、権限キーが変更されているかを確認してください。

### ダウンロードされたSample ProjecまたはDemoを使用するには、どうすればよいですか？

- [Demo使用ドキュメント](https://www.tencentcloud.com/document/product/607/39154)をご参照ください。
- Unity Demoの場合、[Unity Demoマニュアル](https://intl.cloud.tencent.com/document/product/607/50219)をご参照ください。

### UnityによってエクスポートされたSample Projecを使用するとき、しばしば無音になるのはなぜですか？
UnityのSample ProjecではOnApplicationFocusが設定されています。プログラムがフォーカスを失うとき、Pauseで音声を一時停止します。バックグラウンドで音声を再生する必要がある場合、Pauseインターフェースを呼び出すソースコードをリムーブしてください。

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


### GME Unity SDKはどのUnityバージョンをサポートしていますか？
GME Unity SDKがサポートするUnityには、バージョンの制限はありません。



### GME Androidのsoライブラリにはarmv8がありますか？
有ります。2.3.5バージョンでは対応しております。


### Androidのsoライブラリはx86_64バージョンが提供されていますか？
提供していません。
