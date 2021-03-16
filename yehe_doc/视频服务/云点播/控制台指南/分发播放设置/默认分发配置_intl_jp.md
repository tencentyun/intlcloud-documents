## 操作シナリオ
ドメイン名を追加して解決 すると、新しいドメイン名を介してビデオリソースにアクセスできますが、APIインターフェースやコンソールから取得したビデオURLでは、Hostは元のドメイン名のままになります。従って、コンソールにログインして、デフォルト配信設定でHost情報を更新する必要があります。
## 操作手順
1. [VODコンソール](https://console.cloud.tencent.com/vod/overview)にログインし、左側ナビゲーションバーの【配信と再生の設定】>【デフォルト配信設定】を選択して、「デフォルト配信設定」の画面に入ります。
2. 右隅の【編集】をクリックして、対応するパラメータを設定します。
 - プライマリ配信プロトコルタイプ：HTTPとHTTPSをサポートします。
 - デフォルト配信ドメイン名：システムが割り当てた`xxx.vod2.myqcloud.com`がデフォルトで使用されます。カスタムドメイン名を[追加](https://intl.cloud.tencent.com/document/product/266/35572) し [解決](https://intl.cloud.tencent.com/document/product/266/35572) 完了してデフォルト配信ドメイン名とすることもできます。
 
![](https://main.qcloudimg.com/raw/a7be2ffd1ec48a3fea0b5a661700a6f0.png)
