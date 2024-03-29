## 操作シナリオ

このドキュメントで、サーバーフリートを通じたAuto Scaling機能の実現方法について主にガイドします。



## 前提条件
[ビギナー向け例](https://intl.cloud.tencent.com/document/product/1055/37401)を完了しています。

## 操作手順

### スケールイン・アウト構成とプロセス数の修正 

1. [GSEコンソール](https://console.cloud.tencent.com/gse/asset)にログインし、左側のメニュー**サーバフリート**をクリックします。
2. ビギナー向け例で作成したサーバーフリートのIDをクリックして、サーバーフリートの詳細ページに入ります。**スケールイン・アウト**タブをクリックし、スケールイン・アウト詳細ページに入ります。
![](https://main.qcloudimg.com/raw/36b0bb5d3fd052bb79d87247555e637e.png)
3. そのページ右上の**修正**をクリックして、スケールイン・アウト構成を修正します。詳細は次の通りです。
 1. 調節方法では、「自動調節」を選択します。
 2. インスタンス範囲は0 - 3に調整し、広いスペースを空けてください。
 3. ゲームサービスセッションバッファーを30%に構成した場合、そのサーバーがサポートするゲーム対局が70%を超えるときに、スケールアウトが実行されます。 
 4. 構成修正完了後、**確定**をクリックします。
![](https://main.qcloudimg.com/raw/e4805f7c77db319c80a46fade73b4170.png)
 >? 
 >-ゲームサーバーセッションバッファー  = 使用可能なゲームサーバーセッション数 / 最大ゲームサーバーセッション数
 >=（最大ゲームサーバーセッション - アクティブなゲームサーバーセッション数 ）/ 最大ゲームサーバーセッション数。
 >
 >- ゲームサーバーセッションバッファー構成が30%である場合、使用可能なゲームサーバーセッションが30%以下になると、スケールアウトが実行され、30%以上になると、スケールインが実行されます。

### ゲームサーバーセッションを作成し、スケールアウト状況を詳しく見る
1. コンソールの左側のメニュー**ビギナー向け例**をクリックし、[ビギナー向け例](https://intl.cloud.tencent.com/document/product/1055/37401)の操作手順に基づき、最初の3つのステップの操作を完了してから、**ゲームサーバーセッションの作成**を7回連続クリックすると、8個のゲームサーバーセッションが作成され、スケールアウトがトリガーされます。
![](https://main.qcloudimg.com/raw/9c3a7488abacb89bf8c31a254f294220.png)

>?
>- GSEコンソールのビギナー向け例のデフォルトで構成される1台のサーバーは最大10個（変更可能）のゲームサーバーセッションをサポートします。このため、7個のゲームサーバーセッションをサポートする場合、ゲームサーバーセッションバッファー = 使用可能なゲームサーバーセッション数 / 最大ゲームサーバーセッション数 =（最大ゲームサーバーセッション数 - アクティブなゲームサーバーセッション数）/ 最大ゲームサーバーセッション数 =（10 - 7）/ 10 = 30%になります。
>- アクティブなゲームサーバーセッション数が7個を超えると、スケールアウトの実行が必要になります。このためスケールアウト状況を詳しく見て、ゲームサーバーセッションを8個以上作成する必要があります。

2. 左側のメニュー[**サービスフリート**](https://console.cloud.tencent.com/gse/fleet)をクリックして、ワンクリックで作成したばかりのサーバーフリートIDを選択し、フリート詳細に入り、**インスタンスリスト**タブをクリックします。このページでサービスインスタンス数量を詳しく見てください。2分後にはサーバーが2台にスケールアウトしたことが分かるでしょう。
![](https://main.qcloudimg.com/raw/fff0c7e124e3e234c6cb5b33e3629e51.png)
>?8個のゲームサーバーセッションの作成が完了しても、**完了**をクリックして次の体験に**進まないで**ください。スケールイン状況を詳しく見て、これをベースにしてその後の操作をする必要があります。

### ゲームサーバーセッションを終了し、スケールイン状況を詳しく見る

1. コンソールの左側のメニュー**ビギナー向け例**をクリックして、上記のスケールアウト状況を詳しく見るという操作手順へと進み、それぞれゲームサーバーセッション1個を選択して、**プレイヤーセッションの作成**をクリックすると、プレイヤーセッションを作成できます。
![](https://main.qcloudimg.com/raw/2bc7069636a21972a9ca18ebb6264b92.png)
2. **クライアントWebページにリダイレクト**をクリックしてクライアントページに入り、**接続**をクリックすると、サーバーに接続できます。**ゲームセッション終了**をクリックすると、ゲームサーバーセッションを終了できます。手順1、2を連続でそれぞれ2回操作すると、2個のゲームサーバーセッションが終了し、スケールインがトリガーされます。

>? 
>ゲームサーバーセッションバッファー = 使用可能なゲームサーバーセッション数 / 最大ゲームサーバーセッション数 =（最大ゲームサーバーセッション数 - アクティブなゲームサーバーセッション数）/ 最大ゲームサーバーセッション数 =（20 - 6）/ 20 = 70%になります。
>- アクティブなゲームサーバーセッション数が残り6個で、使用可能なゲームサーバーセッションは70%です。30%以上になると、スケールインが実行されます。
>- 現在のバージョンでは、クライアントWebページを閉じてしまうと、以前に作成したプレイヤーセッションをクライアントに再接続できなくなります。プレイヤーセッションを新規作成してからでないと、クライアントに再接続できないため、ゲームサーバーセッションを閉じる必要があります。

3. 左側のメニュー[**サービスフリート**](https://console.cloud.tencent.com/gse/fleet)をクリックして、ワンクリックで作成したばかりのサーバーフリートIDを選択し、フリート詳細に入り、**インスタンスリスト**タブをクリックします。このページでサービスインスタンス数量を詳しく見てください。2分後にはサーバーが1台にスケールインしたことが分かるでしょう。
![](https://main.qcloudimg.com/raw/08b123eb22e7bf84f6ebf812bc23e924.png)




