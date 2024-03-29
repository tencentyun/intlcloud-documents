このチュートリアルでは、「通常のコールバック」と「信頼できるコールバック」という2つのメソッドをはじめとするVODのイベント通知の使用方法について、詳しくご説明します。

## 前提条件

- [Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)および[実名認証](https://intl.cloud.tencent.com/document/product/378/3629)を完了していること。実名認証を行っていないユーザーは、中国国内のVODインスタンスを購入できません。
- 通常のコールバックでは、Python 2 .7ランタイム環境が必要です。

## 通常のコールバック
### コールバック受信サービスのデプロイ

[通常のコールバック](https://intl.cloud.tencent.com/document/product/266/33948) を使用してイベント通知を取得するには、パブリックIPのあるサーバーにコールバック受信サービスをデプロイする必要があります。ここでは例としてCVMインスタンスにこのサービスをデプロイする方法をご説明します。

1. CVMコンソールの[インスタンスリスト](https://console.cloud.tencent.com/cvm/index) ページ に入り、【新規作成】をクリックします。
2. 【クイックコンフィグレーション】メニューを選択し、【イメージ】で“**Ubuntu Server**”または“**CentOS**”を選択して、【パブリックネットワーク帯域幅】で“**1Mbps**”を選択し、“**無料のパブリックIPの割り当て **”にチェックを入れて、【今すぐ購入】をクリックします。
3. [インスタンスリスト](https://console.cloud.tencent.com/cvm/index) ページに再度入り、作成に成功したCVMインスタンス を見つけ、【プライマリIPアドレス】のパブリックIPをコピーします（この例では**134.XXX.XXX.167**）。
![](https://main.qcloudimg.com/raw/89e8b56123b9155e880658bad20eec1e.png)
4. 購入したCVMにログインし、[ソースコード圧縮パッケージ](http://document-1251659802.coscd.myqcloud.com/NotificationTuition.zip) をダウンロードして作業ディレクトリに解凍し、次のコマンドを実行します。
		python NotificationReceiveServer.py
コマンドが実行された後、CVMの標準出力で `Started httpserver on port 8080`が出力されます。サービスプロセスが開始されてポート8080を監視していることを意味します。
5. ブラウザに`http://134.XXX.XXX.167:8080`と入力すると、CVMの標準出力で次のHTTPリクエスト情報が出力されます。
![](https://main.qcloudimg.com/raw/4e7eaffe641002f9b0307244e4bec8dc.png)

### 通常のコールバックのコンフィグレーション
1. [VODコンソール](https://console.cloud.tencent.com/vod/overview)にログインし、左側メニューバーの【コールバック設定】をクリックします。
2. 【設定】をクリックします。
	- コールバックモード：「**通常のコールバック**」を選択します。
	- コールバックURL：`http://134.XXX.XXX.167:8080`を入力します。
	- コールバックイベント：「**ビデオアップロード完了コールバック**」にチェックを入れます。
3. 【OK】をクリックして設定を完了してください。

### 通常のコールバックの開始と受信

[デモビデオ](http://1255566954.vod2.myqcloud.com/ca75586fvodgzp1255566954/484c46995285890788305672872/xUCHV5kOGyIA.wmv) をローカルにダウンロードして、手引きとしてご利用ください。
1. 左側メニューバーの【メディア資産管理】をクリックし、【アップロード済み】を選択して、【ビデオのアップロード】をクリックします。
![](https://main.qcloudimg.com/raw/4724951966b46c801498efed4b6ebec9.png)
2. 「**ビデオのアップロード**」ダイアログボックスが表示されたら、【ローカルからのアップロード】を選択し、【ビデオの選択】をクリックして**デモビデオ**をVODプラットフォームにアップロードします。
![](https://main.qcloudimg.com/raw/e0eb51db29de59e948b332ad05a069db.png)
 アップロードを実行すると、“**アップロード中**”バーにビデオアップロードの進行状況が表示されます。
![](https://main.qcloudimg.com/raw/7f072f0e67b4f3be6907ff1f5a414848.png)
 アップロードが完了すると、“**アップロード済み**”バーのビデオリストに、アップロードされたビデオとビデオに対応するID（FileId）が表示されます。
![](https://main.qcloudimg.com/raw/6c18e73eb8576fc120fe903fc0848927.png)
3. CVMをチェックして、標準出力で[ビデオアップロード完了](https://intl.cloud.tencent.com/document/product/266/33950) 通知の内容を出力します。
 <img src="https://main.qcloudimg.com/raw/f6439edcd8ae59cab1d393987382e136.png" width="818">
4. 【メディア資産管理】の「**アップロード済み**」バーで、先ほどアップロードしたビデオにチェックを入れ、[【ビデオ処理】](https://intl.cloud.tencent.com/document/product/266/33892) をクリックします。【処理タイプ】で「**トランスコードテンプレートの手動選択**」オプションを選択し、【トランスコードテンプレート】の「**MP4-LD-FLU (10)**」にチェックを入れ、【ビデオカバー】にチェックを入れたまま、【OK】をクリックします。
5. 10分間待った後、CVMをチェックし、標準出力で[タスクフローステータスの変更](https://intl.cloud.tencent.com/document/product/266/33953) 通知の内容を出力します。ここには、トランスコードの結果（`Type`が`Transcode`の場合）やカバー生成時点のスクリーンキャプチャの結果（`Type`が`CoverBySnapshot`の場合）が含まれます。
 <img src="https://main.qcloudimg.com/raw/4e577e7feb5524ff82e8a82c8e1cbdd2.png" width="818">

この時点で、ビデオをアップロードしてトランスコードタスク実行が完了しています。アップロードとトランスコードが完了すると、コールバック受信サービスは「**ビデオのアップロードの完了**」と「タスクフロー状態の変更」通知を受信します。

## 信頼できるコールバック

1. [VODコンソール](https://console.cloud.tencent.com/vod/overview)にログインし、左側メニューバーの【コールバック設定】をクリックします。
2. 【設定】をクリックします。
	- コールバックモード：「**信頼できるコールバック**」を選択します。
	- コールバックイベント：「**ビデオアップロード完了コールバック**」にチェックを入れます。
3. 【OK】をクリックして設定を完了してください。

### 信頼できるコールバックの開始

1. 左側メニューバーの【メディア資産管理】をクリックし、【アップロード済み】を選択して、【ビデオのアップロード】をクリックします。
![](https://main.qcloudimg.com/raw/4724951966b46c801498efed4b6ebec9.png)

2. 「**ビデオのアップロード**」ダイアログボックスが表示されたら、【ローカルからのアップロード】を選択し、【ビデオの選択】をクリックして**デモビデオ**をVODプラットフォームにアップロードします。
![](https://main.qcloudimg.com/raw/e0eb51db29de59e948b332ad05a069db.png)

 アップロードを実行すると、“**アップロード中**”バーにビデオアップロードの進行状況が表示されます。
![](https://main.qcloudimg.com/raw/7f072f0e67b4f3be6907ff1f5a414848.png)

 アップロードが完了すると、“**アップロード済み**”バーのビデオリストに、アップロードされたビデオとビデオに対応するID（FileId）が表示されます。
![](https://main.qcloudimg.com/raw/6c18e73eb8576fc120fe903fc0848927.png)

3. 【メディア資産管理】の「**アップロード済み**」バーで、先ほどアップロードしたビデオにチェックを入れ、[【ビデオ処理】](https://intl.cloud.tencent.com/document/product/266/33892) をクリックします。【処理タイプ】で「**トランスコードテンプレートの手動選択**」オプションを選択し、【トランスコードテンプレート】の「**MP4-LD-FLU (10)**」にチェックを入れ、【ビデオカバー】にチェックを入れたまま、【OK】をクリックします。

この時点で、ビデオは再度アップロードされ、ビデオのトランスコードタスクが開始されました。これらの操作によりイベント通知がトリガーされます。

### 信頼できるコールバックのプル

イベント通知がトリガーされたら、信頼できるコールバックを自発的にプルする必要があります。[APIツール](https://intl.cloud.tencent.com/document/product/266/34183)を介して`PullEvents`コマンドを実行し、消費されていないイベント通知をクエリーすることができます。具体的な手順は次のとおりです。
1. [VOD PullEventsコマンドのAPI 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=vod&Version=2018-07-17&Action=PullEvents&SignVersion=)に入り、お客様の「**パーソナルキー**」を入力します（【キーの確認】をクリックし、[APIキー管理コンソール](https://console.cloud.tencent.com/cam/capi)から取得できます）。
2. 右側のバーの中から【オンラインコール】を選択し、【リクエスト送信】をクリックします。

リクエストを送信した後、もどってきた結果の中のイベントリスト`EventSet`を見ます。イベントリストの中には2つのイベント通知が含まれ、タイプは「**ビデオアップロード完了**」と「**タスクフロー状態の変更**」で、対応するイベントハンドラはそれぞれ`8078360634045903972`と`8078360634045903972`です。
	 <img src="https://main.qcloudimg.com/raw/1497a3fd83ce599ef0a03437df53b6b4.png" width="579">
 <img src="https://main.qcloudimg.com/raw/9bf358ef2231a05237fe226cadebe136.png" width="579">

この時点で、信頼できるコールバックの方式で、「**ビデオアップロード完了**」と「**タスクフロー状態の変更**」の2つの通知をプルしました。続いて、プルしたイベント通知をすみやかに確認する必要があります。

### 信頼できるコールバックの確認

プルした信頼できるコールバックは、**30秒以内**に確認を終える必要があります。そうでない場合、

* イベントハンドラが30秒後に再びAPIを呼び出して確認を行い、呼び出しに失敗します。
* イベントは30秒を超えても確認がないと、次の回の信頼できるコールバックのプルの時に再びプルされます。

[APIツール](https://intl.cloud.tencent.com/document/product/266/34184)を使用して`ConfirmEvents`コマンドを実行し、消費されていないイベント通知をクエリーすることができます。具体的な手順は次のとおりです。

1. [VOD ConfirmEvents コマンドのAPI 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=vod&Version=2018-07-17&Action=ConfirmEvents&SignVersion=)に入り、お客様の「**パーソナルキー**」を入力します。

2. 「**EventHandles.N**」の入力ボックスに、イベント通知をプルした時に取得したイベントハンドラを入力します。

3. 右側のバーの中から【オンラインコール】を選択し、【リクエスト送信】をクリックします。

 リクエストに成功すると、次の情報が返ってきます。

	レスポンスに失敗した場合は、次をご確認ください。
	- イベントハンドラの入力ミス。
	- イベントがプルされ30秒以上経過していないか。
4. 5分経ってから、再び[APIツール](https://intl.cloud.tencent.com/document/product/266/34183)を使用して`PullEvents`コマンドを実行し、イベント通知をプルします。

 **ResourceNotFound**のエラーが戻ってきた場合は、プルできる通知がすでにないことを意味します。



