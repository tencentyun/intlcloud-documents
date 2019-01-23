### ゲームマルチメディアエンジン（GME）Demo及びSDKはどこでダウンロードできますか？

[ダウンロードガイド](https://cloud.tencent.com/document/product/607/18521)で関連するDemo及びSDKをダウンロードしてください。現在、公式サイトにはUnityエンジンDemo、Cocos2DエンジンDemo、Androidネイティブ開発Demo及びiOSネイティブ開発Demoがあります。

### ゲームマルチメディアエンジン（GME）Demoをダウンロード後、自分が申請したアカウントに変更することはできますか？
- できます。コンソールでsdkappidと権限暗号鍵の2つの番号を取得する必要があります。
- お客様が自身のappidを使用する場合、AVChatViewController中のGetAuthBufferでリアルタイムボイスのKeyを変更する必要があります。

### Demoを使用する時、エラーメッセージerrinfo=priv map info errorが出ました。どうすればいいですか？
関連するルーム参加パラメータにエラーが発生した場合、sdkappid、権限暗号鍵が置き換えられていないか確認してください。



### どのようにログを取得しますか？
QAVSDK_日付.logファイルは、ログファイルです。ディレクトリは以下のとおりです。

| プラットフォーム    | パス                                                         |
| ------- | ------------------------------------------------------------ |
| Windows | %appdata%\Tencent\GME\ProcessName                            |
| iOS     | Application/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/Documents   |
| Android | /sdcard/Android/data/xxx.xxx.xxx/files                       |
| Mac     | /Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents |

### 音声遅延の主な原因は？
-  **音楽再生遅延：**司会者が外部デバイスを使用して音楽を再生し、別の携帯電話で声音を収集し配信する場合（この場合必ず遅延が発生するため、イヤフォンを付けることをお勧め）。
-  **ネットワーク遅延：**上りリンクのパケットロス率が高すぎる、または上りリンクの遅延変動が大きい状況において、オーディエンスには遅延した音声が聞こえます。

