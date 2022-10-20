Tencent CloudのCloud Monitor（CM）はCLBおよびバックエンドインスタンスにデータ収集およびデータ表示機能を提供します。Tencent Cloud CMを使用すると、CLBの統計データを確認し、システムが正常に動作しているかを検証できるほか、それに応じたアラートを作成することもできます。CMに関するその他の情報については、[CM](https://intl.cloud.tencent.com/doc/product/248)製品ドキュメントをご参照ください。

Tencent CloudはデフォルトですべてのユーザーにCM機能をご提供しています。手動でのアクティブ化は必要なく、CLBを使用するだけで、CMが関連の監視データの収集をサポートします。CLBの監視データは次のいくつかの方法で確認できます。

## CLBコンソール
1. [CLBコンソール](https://console.cloud.tencent.com/clb)にログインし、CLBインスタンスIDの横の監視アイコンをクリックすると、監視フローティングウィンドウから各インスタンスのパフォーマンスデータをすぐに閲覧することができます。
![](https://main.qcloudimg.com/raw/6580c81d6fd1eee2234fcb5262a976bb.png)
2. CLBインスタンスIDをクリックし、CLB詳細ページに進み、【モニタリング】オプションタブをクリックすると、現在のCLBインスタンスの監視データを確認できます。
![](https://main.qcloudimg.com/raw/3eb231b336c9325ae16bfe2937e41b39.png)

## CMコンソール
[CMコンソール](https://console.cloud.tencent.com/monitor/overview)にログインし、左側ナビゲーションバーの「クラウド製品監視」モジュールの[【Cloud Load Balancer-CLB】](https://console.cloud.tencent.com/monitor/clb)をクリックし、CLBインスタンスIDをクリックして監視詳細ページに進むと、そのCLBインスタンスの監視データを確認できます。インスタンスを表示すると、リスナー、バックエンドサーバーなどの監視情報を確認できます。

## API方式
GetMonitorDataインターフェースを使用して全製品の監視情報を取得することができます。具体的な内容については[指標のモニタリングデータのプル](https://intl.cloud.tencent.com/document/product/248/33881)をご参照ください。CLBのネームスペースについては、[パブリックネットワークCLBの監視指標](https://intl.cloud.tencent.com/zh/document/product/248/10997)、[プライベートネットワークCLBレイヤー4プロトコルの監視指標](https://intl.cloud.tencent.com/document/product/248/39529)および[レイヤー7プロトコルの監視指標](https://intl.cloud.tencent.com/document/product/248/39530)をご参照ください。
