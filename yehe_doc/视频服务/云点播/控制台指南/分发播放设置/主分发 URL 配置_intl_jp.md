## 操作シナリオ
ドメイン名を追加して解決 すると、新しいドメイン名を介してビデオリソースにアクセスできますが、APIインターフェースやコンソールから取得したビデオURLでは、Hostは元のドメイン名のままになります。従って、コンソールにログインして、プライマリ配信URL設定でHost情報を更新する必要があります。
## 操作手順
1. [VODコンソール](https://console.cloud.tencent.com/vod/overview)にログインし、左側ナビゲーションバーの【配信と再生の設定】>【プライマリ配信URLの設定】を選択し、「プライマリ配信URLの設定」ページに進みます。
2. 右隅の【編集】をクリックして、対応するパラメータを設定します。
 - プライマリ配信プロトコルタイプ：HTTPとHTTPSをサポートします。
 - プライマリ配信ドメイン名：システムが割り当てた`xxx.vod2.myqcloud.com`がデフォルトで使用されますが、プライマリ配信ドメイン名として、カスタムドメイン名を[追加](https://intl.cloud.tencent.com/document/product/266/14056#.E6.B7.BB.E5.8A.A0.E5.9F.9F.E5.90.8D) をして [解決](https://intl.cloud.tencent.com/document/product/266/14056#.E8.A7.A3.E6.9E.90.E5.9F.9F.E5.90.8D) することもできます。
 
![](https://main.qcloudimg.com/raw/21cda66e8aff5a237f0ef926cebfa5c4.png)
