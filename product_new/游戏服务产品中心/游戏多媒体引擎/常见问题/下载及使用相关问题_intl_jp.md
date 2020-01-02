### Gaming Multimedia EngineのDemoとSDKは どこからダウンロードできますか？

 [ダウンロードガイド](https://intl.cloud.tencent.com/document/product/607/18521)  からDemoとSDKをダウンロードしてください。現在、公式サイトには Unity エンジン Demo、Cocos2D エンジン Demo、Android ネイティブ開発 Demo 及び iOS ネイティブ開発Demoがあります。

### Gaming Multimedia Engine Demoをダウンロードした後に、自分で申請したアカウントに変更することは可能ですか？
- 可能です、コンソールから sdkappidと権限キーの2つ番号を取得する必要があります。
- お客様がご自分で申請したappidを使用する場合、AVChatViewController 内の GetAuthBufferでリアルタイム音声のKeyを変更する必要があります。

### Demo使用中にerrinfo=priv map info errorというエラーが表示されました。どう対処しますか？
関連入室パラメータのエラーが発生した場合、sdkappid、権限キーが置き換えられたかどうかを確認してください。



### ログはどのように取得しますか？
QAVSDK_日付付き.logというファイルはログファイルです。ディレクトリは下記の通りです。

| フラットフォーム    | パス                                                         |
| ------- | ------------------------------------------------------------ |
| Windows | %appdata%\Tencent\GME\ProcessName                           |
| iOS    | Application/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/Documents   |
| Android | /sdcard/Android/data/xxx.xxx.xxx/files                       |
| Mac     | /Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents |

### 音声ラグの主な原因は何ですか？
-  **音楽再生時の音声ラグ：**ホストは外部のデバイスで音楽を放送し、別の携帯を使って採集・ホストします（ここでは音声ラグを回避することができません、この場合、ホストがイヤホンを付けることをお勧めします）。
-  **ネットワークのラグ：**上がりのパケットロス率が高い場合や上がりの遅延変動が大きい場合は、観客が音声に違和感を感じてしまいます。


### iOS Demo をダウンロードした後に実行できなくなった
公式 のiOS Demoをダウンロードした後、 Xcode（10以上のバージョン）コンパイルの際に、「ld: warning: directory not found for option」などのエラーが発生します、この場合、 Demo 同一レベルのディレクトリにある「GME_SDK」フォルダの「GMESDK.framework」ファイルをプロジェクトの Frameworkリストに手動で追加する必要があります。


### Unity Demoをダウンロードし、実行可能なファイルをエクスポートする際にエラーが発生した
使用中にFound plugins with same names and architecturesのようなエラーが発生した場合、その原因は、GME SDK がx86アーキテクチャーのSDK バージョンとx86_64アーキテクチャーのSDK バージョンをデフォルトで提供しているためです、plugins フォルダからいずれかの1部を削除してください。