Media Processing Service（MPS）を経た後、ビデオタスクコールバック通知を完了するのが標準的なスキームです。MPSでは、ユーザーが使用できるように、Serverless Cloud Function（SCF）の中でテンプレートを設定しています。

## 操作シナリオ
このドキュメントの例では、Media Processing Service（MPS）およびServerless Cloud Function（SCF）を使用します。このうち、MPSは主にビデオ処理のタスクに使用し、SCFは主にコールバックメッセージの処理を提供します。

## 操作手順
### 手順1：SCFの作成
1. [SCFコンソール](https://intl.cloud.tencent.com/login)にログインし、左側ナビゲーションバーから【[関数サービス](https://intl.cloud.tencent.com/login)】を選択します。
![](https://main.qcloudimg.com/raw/29cd2fc9d699ac2af763749c2e67a472.png)
2. 関数サービスのページの上方の**北京**リージョンを選択し、【新規作成】をクリックして関数の新規作成ページに入ります。
3. 次のパラメータ情報を下図のとおりに設定します。
	- **関数名**：名称はカスタマイズ可能です。ここでは、例として「MPSAnalysis」とします。
	- **実行環境**：タスクコールバックテンプレートは現在Nodejs 8.9のみをサポートしています。
	- **作成方式**：テンプレートの関数を選択します。
	- **あいまい検索**：「MPS Webhookテンプレート」と入力し、検索を行います。
![](https://main.qcloudimg.com/raw/43b6ba09c92932a51ccdec290eb11726.png)
>?テンプレートの中の【詳細の表示】をクリックすると、ポップアップした「テンプレート詳細」のウィンドウに関連情報が表示され、ダウンロードの操作を行うことができます。
4. 【次のステップ】をクリックして、関数設定ページに進みます。
![](https://main.qcloudimg.com/raw/2c06ed43e1a410f451c490cc4570c7b1.png)
5. デフォルトの設定を維持し、【完了】をクリックしてください。これで関数の作成が完了します。


### 手順2：MPSトリガーの設定
1. 【[SCFコンソール](https://intl.cloud.tencent.com/login)】のページで、左側ナビゲーションバーから【[関数サービス](https://intl.cloud.tencent.com/login)】を選択し、対応する関数名をクリックすると、この関数の詳細ページに移動します。
![](https://main.qcloudimg.com/raw/8f4478df3d76662f8a5241bebe3761bf.png)
2. 【トリガーの管理】>【トリガーの作成】をクリックすると、トリガー作成のウィンドウがポップアップしますので、トリガーの方法に「MPSトリガー」を選択してください。
![](https://main.qcloudimg.com/raw/e067ef8e3e09c07b723d041193b66c62.png)
主要パラメータの情報は次のとおりです。その他の設定項目はデフォルトを維持してください。
	- **イベントタイプ**：MPSトリガーはアカウント次元のイベントタイプによってEvent（イベント）をプッシュします。現在はワークフロータスク（WorkflowTask）とビデオ編集タスク（EditMediaTask）の2種類のイベントタイプのトリガーをサポートしています。
	>?
	>- MPSトリガーの初回作成時には、関連サービスのロール状態の異常が表示されます。プロンプトにしたがって対応するサービス【SCF_QcsRole】、【MPS_QcsRole】をクリックし、権限を与えてください。
	>![](https://main.qcloudimg.com/raw/e6a5802db5fe9e054c2c50020f0403b1.png)
	>- MPSトリガーはサービス次元で発生するイベントをイベントソースとし、リージョン、リソースなどの属性の区分はありません。各アカウントでは、2種類のイベントに対してそれぞれ関数を1つバインドすることが許されます。複数の関数にてタスクを処理する必要がある場合は、[関数間の呼び出しSDK](https://intl.cloud.tencent.com/zh/document/product/583/32747)をご参照ください。
3. 【サブミット】をクリックすると、MPSトリガーの設定が完了します。
![](https://main.qcloudimg.com/raw/6a7d7009e36538491683173553b809fd.png)


### 手順3：関数機能のテスト
1. [MPSコンソール](https://intl.cloud.tencent.com/login)にログインし、MPSワークフローを実行します。
2. 【[SCFコンソール](https://intl.cloud.tencent.com/login)】に切り替え、実行結果を表示します。
関数の詳細ページで【ログのクエリー】のタグを選択すると、出力されたログ情報を見ることができます。下図のとおりです。
![](https://main.qcloudimg.com/raw/f5d10848b674f137826689ac1dc28c8a.png)
3. [COSコンソール](https://intl.cloud.tencent.com/login)に切り替え、データのダンプおよび加工結果を表示します。

>?自身のニーズに基づき、具体的なデータの加工処理方法を編集することができます。
