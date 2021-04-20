

## 設定シナリオ
リソースに加えて、Tencent Cloud CDNはデフォルトでオリジンサーバーからの次のヘッダーをキャッシュし、ユーザーに返します。
+ Access-Control-Allow-Origin
+ Timing-Allow-Origin
+ Content-Disposition
+ Accept-Ranges

オリジンサーバーに特別なヘッダーがある場合は、CDNによってキャッシュしてユーザーに返す必要がある場合は、ヘッダーキャッシュ設定を有効にすることで実現できます。

## 設定ガイド
### 設定の確認
 [CDNコンソール](https://console.cloud.tencent.com/cdn)にログインし、左側のナビゲーションメニューバーで【ドメイン名管理】を選択して、ドメイン名の右側にある【管理】をクリックすると、ドメイン名設定画面に入ります。【キャッシュ設定】タブで、HTTPヘッダーキャッシュ設定を確認できます。デフォルトでは無効になっています。
![](https://main.qcloudimg.com/raw/0fb4739f743b6242c463672a2f059098.png)






