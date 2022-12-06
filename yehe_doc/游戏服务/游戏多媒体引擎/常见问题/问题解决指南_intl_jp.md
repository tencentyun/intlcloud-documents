ここでは、開発者が開発中に発生した問題を速やかに解決できるように、GMEの問題処理方法について説明します。

##　よくある質問ガイド
開発中に発生する一般的な問題について、次のドキュメントを使用して、問題のタイプを分析して解決することができま：

|ドキュメント|解決される問題|
|---|----|
|[機能の特徴に関する問題](https://intl.cloud.tencent.com/document/product/607/39520)|サポートされているプラットフォームなど、GMEの機能に関する問題。|
|[課金に関する問題](https://intl.cloud.tencent.com/document/product/607/30255)|課金モデルや課金のタイミングについて疑問がある場合は、このドキュメントをご参照ください。|
|[Demo使用上の問題](https://intl.cloud.tencent.com/document/product/607/39521)|GMEのSampleProjectを使用するとき、またはDemoを体験するときに発生した問題。|
[認証に関する問題](https://intl.cloud.tencent.com/document/product/607/39824)|GMEを使用するには認証が必要です。問題が発生した場合はこのドキュメントをご参照ください。|
|[リアルタイム音声のルーム参入失敗問題](https://intl.cloud.tencent.com/document/product/607/39523)、[リアルタイム音声の無音とオーディオの問題](https://intl.cloud.tencent.com/document/product/607/39524)、[ネットワークの問題](https://intl.cloud.tencent.com/document/product/607/39519)|GMEリアルタイム音声を使用する過程で発生した問題です。問題のタイプを判断し、ドキュメントを参照して解決することができます。|
|[ボイスツーテキスト変換の問題](https://intl.cloud.tencent.com/document/product/607/39716)|ボイスツーテキスト変換機能を使用する際に発生する問題のまとめ。|
|[プロジェクトエクスポートの問題](https://intl.cloud.tencent.com/document/product/607/39522)|各プラットフォームで、アプリケーションのエクスポートに問題が発生した場合や、実機で問題が発生した場合は、参考にして解決できます。|


## 開発問題

開発中、機能的な問題が発生した場合、まず返されたエラーコードで判断します。エラーコードで問題が解決できない場合は、[チケット](https://console.tencentcloud.com/workorder/category)を使用してエラー解析についてGME開発者に連絡してください。


###　エラーコード

GME [エラーコードドキュメント](https://intl.cloud.tencent.com/document/product/607/33223)では、エラーコードの数値と、そのエラーコードの原因と解決策が記載されていますので、トラブルシューティングの参考にしてください。


### ログはどのように取得しますか？

ログを提供する際には、問題が発生した時点と、受信側（聞く）および送信側（話す）のログを併せて提供してください。

**ログパス**
`QAVSDK_`に日付が付いている`.log`ファイルは、ログファイルです。ディレクトリは以下のとおりです：

| フラットフォーム    | パス                                                         |
| ------- | ------------------------------------------------------------ |
| Windows | `%appdata%\GMEGLOBAL\GME\processName`                            |
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


**ログの暗号化**

現在のGMEログはデフォルトで暗号化されていますが、インターフェースを呼び出して暗号化を解除することができます。開発段階では暗号化を解除し、リリースの前に暗号化を復元することをお勧めします。インターフェースはinitの前に呼び出してください。

```
SetAdvanceParams("DisableEncryptLog", "1");
```

|パラメータ|意味|
|--|--|
|パラメータ1|「DisableEncryptLog」を入力すると、暗号化関連の機能が無効になります|
|パラメータ2|「1」を入力するとログの暗号化が解除され、「0」を入力するとログの暗号化が維持されます|


##　クラッシュの問題


クラッシュが発生した場合は、まず[プロジェクトのエクスポートに関する問題](https://intl.cloud.tencent.com/document/product/607/39522)を参照して対処します。解決できない場合は、スタックをGME開発者に提供してください。
- サードパーティの異常報告プラグインをインストールした場合は、GME開発者に連絡してクラッシュスタックリンクを共有することができます。
- iOSやAndroidプラットフォームの場合、マシンをパソコンに接続してXcodeやAndroidStudio内のLogCatを使用してクラッシュスタックを取得し、コピーしてGME開発者に提供することができます。
- Windowsプラットフォームの場合は、DUMPファイルを提供してください。
