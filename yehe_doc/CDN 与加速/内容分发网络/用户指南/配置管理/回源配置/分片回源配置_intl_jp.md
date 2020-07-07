## 設定シナリオ
Tencent Cloud CDNがリソースをキャッシュする際に、ストレージ効率を改善するために、ファイルをシャードに分割して格納し、Rangeリクエストもサポートします。リクエストにHTTPヘッダー`Range: bytes = 0-999`が含まれている場合、ファイルの最初の1,000バイトがユーザーに返されます。

Range back-to-origin設定を有効にすると、ユーザーがリクエストしたファイルの一部が期限切れの場合、CDNはユーザーのリクエストに従ってシャードしてback-to-originします。ユーザーが必要とするファイルのみををプルしてキャッシュし、ユーザーに返します。Range back-to-origin設定を無効にすると、ユーザーが一部のファイルのみをリクエストした場合でも、CDNはback-to-originするときにファイル全体を取り出して、キャッシュして、リクエストされた一部のファイルをユーザーに返します。

Range back-to-origin設定を有効にすると、大容量ファイルの配信効率が効果的に向上し、応答時間が改善され、オリジンサーバーへの負荷が軽減されます。
<div class="doc-video-mod"><iframe src="https://cloud.tencent.com/edu/learning/quick-play/2209-31085?source=gw.doc.media&withPoster=1&notip=1"></iframe></div>


>Range back-to-origin設定を有効にすると、リソースはノードのシャードにキャッシュされますが、各シャードのキャッシュの有効期限が全部一致し、ユーザーが指定したキャッシュ有効期限ルールに従います。

## 設定ガイド
### 設定の確認
[CDNコンソール](https://console.cloud.tencent.com/cdn)にログインし、左側のナビゲーションメニューバーで【ドメイン管理】を選択して、ドメイン名の右側にある【管理】をクリックすると、ドメイン名設定画面に入ります。【back-to-origin】タブで、Range back-to-origin設定を確認できます。デフォルトでは無効の状態になっています。COSオリジンサーバードメイン名の場合、デフォルトでは有効の状態になっています。
![](https://main.qcloudimg.com/raw/04b9ec63d365b60ba2c3a8c16bc61c36.png)

### 設定の変更
スイッチを切り替えて、Range back-to-origin設定を有効または無効にすることができます。Range back-to-origin設定を有効にする場合、オリジンサーバーがRangeリクエストをサポートしていることを確認する必要があります。そうしないと、back-to-originが失敗する可能性があります。
![](https://main.qcloudimg.com/raw/0c7d65308c5ae22693bb29b51345ce83.png)

>ご利用のアクセラレーションドメイン名がグローバルアクセラレーション用に設定されている場合、設定されたRange back-to-origin設定はグローバルに有効になり、中国本土と中国本土以外との異なる設定に対応しません。

## 設定例
ドメイン名`cloud.tencent.com`のRange back-to-origin設定は、次のようになります。
![](https://main.qcloudimg.com/raw/04b9ec63d365b60ba2c3a8c16bc61c36.png)
ユーザーAがリソース`http://cloud.tencent.com/test.apk`をリクエストしてから、ノードがリクエストを受信し、キャッシュされている`test.apk`ファイルがすでに期限切れであることが判明した時に、back-to-originリクエストを送信します。ノードback-to-originはRangeリクエストを使用し、シャードによってリソースを取得してキャッシュします。この時に、ユーザーBもRangeリクエストを送信し、ノードに保存されているシャードがすでにRangeリクエストで指定されたバイトセグメントと一致する場合、リソースは直接にユーザーに返して、すべてのシャードの取得が完了するまで待つ必要がありません。

