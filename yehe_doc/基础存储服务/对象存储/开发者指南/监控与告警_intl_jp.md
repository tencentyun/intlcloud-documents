## 概要

COSの読み取り/書き込みリクエスト量、トラフィックなどのデータは[BCM](https://www.tencentcloud.com/document/product/248) によって集計され、表示されます。COSコンソールまたはBCMの[コンソール](https://console.cloud.tencent.com/monitor)上で、COSの読み取り/書き込みリクエスト量、トラフィックなどの詳細な監視データを確認することができます。

>?
>- ここでは主に、COSコンソールで統計データを取得するケースについて述べます。データインターフェースを使用してより詳細な情報を取得する方法について知りたい場合は、CMインターフェースをご利用ください。詳細については、[CM](https://www.tencentcloud.com/document/product/248)製品ドキュメントをご参照ください。
>- 現在、CMにレポートされるすべての指標は、全COSリージョンでサポートされています。詳細については、[リージョンとアクセスドメイン名](https://intl.cloud.tencent.com/document/product/436/6224)をご参照ください。

## 基本機能

BCMはCOSに次のポータルを提供し、監視およびアラート機能を実現します。

| モジュール       | 機能                                     | 主な機能                                                     |
| ---------- | ---------------------------------------- | ------------------------------------------------------------ |
| 監視概要   | 製品の現在のステータスを表示                       | 全体状況、アラートの状況、全体監視情報一覧を提供します                     |
| アラート管理   | アラートの管理と設定をサポート                       | COSのアラートポリシー、カスタムメッセージおよびトリガー条件テンプレートの新規追加をサポートします       |
| 監視プラットフォーム   | トラフィックの監視およびユーザー定義の監視指標データの確認 | ユーザーの帯域幅全体情報を確認します。ユーザーは監視指標および報告するデータをあらかじめ定義することができます |
| クラウド製品監視 | COS下のバケットの監視ビューを確認           | 現在の各バケット下の読み取り/書き込みリクエスト量、トラフィックなどの監視ビューおよびデータを照会します       |

## シナリオ

- **日常管理のケース**：BCMコンソールにログインし、COSの実行ステータスをリアルタイムに確認します。
- **異常処理のケース**：監視データがアラート閾値に達した時点でアラート情報が発出されるため、異常通知を迅速に取得し、異常の原因を照会するとともに、異常状況の処理を速やかに行うことができます。

## コンソールからの設定と照会

[BCMコンソール](https://console.cloud.tencent.com/monitor)からCOSのアラートポリシーを作成することができます。監視指標が設定値に達するとアラートを受信します。関連の操作ガイドについては、[モニタリングアラートの設定](https://intl.cloud.tencent.com/document/product/436/39104)をご参照ください。

監視データを確認したい場合は、**クラウド製品監視>[COS](https://console.cloud.tencent.com/monitor/product/COS)**ページで、すべてのバケットの監視データ、ヘルスステータス、アラートポリシー数を確認することができます。またCOSコンソールでも確認できます。操作ガイドについては、[データ概要の確認](https://intl.cloud.tencent.com/document/product/436/36542)および[データモニタリングの照会](https://intl.cloud.tencent.com/document/product/436/31634)をご参照ください。

## インターフェース呼び出しによる確認

インターフェースを呼び出してCOSの監視データを確認することができます。COSの監視項目は次のとおりです。COSの監視インターフェースの詳細についてお知りになりたい場合は、[COS監視指標](https://intl.cloud.tencent.com/document/product/248/37269)のドキュメントをご参照ください。

## 監視指標

> ?COSは共通リージョンを使用するため、バケットがどのリージョンにあるかにかかわらず、COS監視指標データをプルする際、Regionは常に「広州」リージョンを選択してください。
> - [API Explorer](https://console.cloud.tencent.com/api/explorer?Product=monitor&Version=2018-07-24&Action=DescribeBaseMetrics)を使用してデータをプルする際は、Regionフィールドは常に「華南リージョン(広州)」を選択します。
> - SDKを使用してデータをプルする際は、Regionフィールドには常に「ap-guangzhou」と入力します。

### リクエストクラス

| 指標の英語名           | 指標の日本語名               | 指標の意味                                                     | 単位 | ディメンション          |
| -------------------- | ------------------------ | ------------------------------------------------------------ | ---- | ------------- |
| StdReadRequests      | 標準ストレージ読み取りリクエスト           | 標準ストレージタイプの読み取りリクエスト回数です。リクエスト回数はリクエストコマンドの送信回数に基づいて計算されます | 回   | appid、bucket |
| StdWriteRequests     | 標準ストレージ書き込みリクエスト           | 標準ストレージタイプの書き込みリクエスト回数です。リクエスト回数はリクエストコマンドの送信回数に基づいて計算されます | 回   | appid、bucket |
| IaReadRequests       | 低頻度ストレージ読み取りリクエスト           | 低頻度ストレージタイプの読み取りリクエスト回数です。リクエスト回数はリクエストコマンドの送信回数に基づいて計算されます | 回   | appid、bucket |
| IaWriteRequests      | 低頻度ストレージ書き込みリクエスト           | 低頻度ストレージタイプの書き込みリクエスト回数です。リクエスト回数はリクエストコマンドの送信回数に基づいて計算されます | 回   | appid、bucket |
| DeepArcReadRequests  | ディープアーカイブストレージ読み取りリクエスト           | ディープアーカイブストレージタイプの読み取りリクエスト回数です。リクエスト回数はリクエストコマンドの送信回数に基づいて計算されます | 回   | appid、bucket |
| DeepArcWriteRequests | ディープアーカイブストレージ書き込みリクエスト           | ディープアーカイブストレージタイプの書き込みリクエスト回数です。リクエスト回数はリクエストコマンドの送信回数に基づいて計算されます | 回   | appid、bucket |
| ItReadRequests       | INTELLIGENT_TIERINGストレージ読み取りリクエスト           | INTELLIGENT_TIERINGストレージタイプの読み取りリクエスト回数です。リクエスト回数はリクエストコマンドの送信回数に基づいて計算されます | 回   | appid、bucket |
| ItWriteRequests      | INTELLIGENT_TIERINGストレージ書き込みリクエスト           | INTELLIGENT_TIERINGストレージタイプの書き込みリクエスト回数です。リクエスト回数はリクエストコマンドの送信回数に基づいて計算されます | 回   | appid、bucket |
| TotalRequests        | 総リクエスト数                 | すべてのストレージタイプの読み取り/書き込み総リクエスト回数です。リクエスト回数はリクエストコマンドの送信回数に基づいて計算されます | 回   | appid、bucket |
| GetRequests          | GETクラス総リクエスト数                 | すべてのストレージタイプのGETクラスの総リクエスト回数です。リクエスト回数はリクエストコマンドの送信回数に基づいて計算されます | 回   | appid、bucket |
| PutRequests          | PUTクラス総リクエスト数                 | すべてのストレージタイプのPUTクラスの総リクエスト回数です。リクエスト回数はリクエストコマンドの送信回数に基づいて計算されます | 回   | appid、bucket |

### ストレージクラス

| 指標の英語名                   | 指標の日本語名                        | 単位 | ディメンション          |
| ---------------------------- | --------------------------------- | ---- | ------------- |
| StdStorage                   | 標準ストレージ-ストレージ容量                 | MB   | appid、bucket |
| SiaStorage                   | 低頻度ストレージ-ストレージ容量                 | MB   | appid、bucket |
| ItFreqStorage                | INTELLIGENT_TIERINGストレージ-高頻度階層ストレージ容量       | MB   | appid、bucket |
| ItInfreqStorage              | INTELLIGENT_TIERINGストレージ-低頻度階層ストレージ容量       | MB   | appid、bucket |
| ArcStorage                   | アーカイブストレージ-ストレージ容量                 | MB   | appid、bucket |
| DeepArcStorage               | ディープアーカイブストレージ-ストレージ容量             | MB   | appid、bucket |
| StdObjectNumber              | 標準ストレージ-オブジェクト数                 | 個   | appid、bucket |
| IaObjectNumber               | 低頻度ストレージ-オブジェクト数                 | 個   |appid、bucket |
| ItFreqObjectNumber           | INTELLIGENT_TIERINGストレージ_高頻度階層オブジェクト数           | 個   |appid、bucket |
| ItInfreqObjectNumber         | INTELLIGENT_TIERINGストレージ_低頻度階層オブジェクト数           | 個   |appid、bucket |
| ArcObjectNumber              | アーカイブストレージオブジェクト数                  | 個   | appid、bucket |
| DeepArcObjectNumber          | ディープアーカイブストレージオブジェクト数              | 個   | appid、bucket |
| StdMultipartNumber           | 標準ストレージ-ファイルフラグメント数               | 個   | appid、bucket |
| IaMultipartNumber            | 低頻度ストレージ-ファイルフラグメント数               | 個   |appid、bucket |
| ItFrequentMultipartNumber    | INTELLIGENT_TIERING-高頻度ファイルフラグメント数           | 個   |appid、bucket |
| ArcMultipartNumber           | アーカイブストレージ-ファイルフラグメント数               | 個   |appid、bucket |
| DeepArcMultipartNumber       | ディープアーカイブストレージ-ファイルフラグメント数           | 個   |appid、bucket |

### トラフィッククラス

| 指標の英語名                    | 指標の日本語名           | 指標の意味                                                 | 単位 | ディメンション          |
| ----------------------------- | -------------------- | -------------------------------------------------------- | ---- | ------------- |
| InternetTraffic           | パブリックネットワークダウンストリームトラフィック         | データをインターネット経由でCOSからクライアントにダウンロードする際に発生するトラフィック              | B    | appid、bucket |
| InternetTrafficUp             | パブリックネットワークアップストリームトラフィック         | データをインターネット経由でクライアントからCOSにアップロードする際に発生するトラフィック              | B    | appid、bucket |
| InternalTraffic          | プライベートネットワークダウンストリームトラフィック         | データをTencent Cloudプライベートネットワーク経由でCOSからクライアントにダウンロードする際に発生するトラフィック          | B    | appid、bucket |
| InternalTrafficUp             | プライベートネットワークアップストリームトラフィック         | データをTencent Cloudプライベートネットワーク経由でクライアントからCOSにアップロードする際に発生するトラフィック          | B    | appid、bucket |
| CdnOriginTraffic              | CDN back-to-originトラフィック         | データをCOSからTencent Cloud CDNエッジノードに転送する際に発生するトラフィック           | B    | appid、bucket |
| InboundTraffic                | パブリックネットワーク、プライベートネットワークアップロード総トラフィック | データをインターネット、Tencent Cloudプライベートネットワーク経由でクライアントからCOSにアップロードする際に発生するトラフィック  | B    | appid、bucket |
| CrossRegionReplicationTraffic | 地域間コピートラフィック       | データをあるリージョンのバケットから別のリージョンのバケットに転送する際に発生するトラフィック | B    | appid、bucket |

### 戻りコードクラス

| 指標の英語名      | 指標の日本語名     | 指標の意味                                        | 単位 | ディメンション          |
| --------------- | -------------- | ----------------------------------------------- | ---- | ------------- |
| 2xxResponse     | ステータスコード2xx     | ステータスコード2xxが返されたリクエストの回数                     | 回   | appid、bucket |
| 3xxResponse     | ステータスコード3xx     | ステータスコード3xxが返されたリクエストの回数                     | 回   | appid、bucket |
| 4xxResponse     | ステータスコード4xx     | ステータスコード4xxが返されたリクエストの回数                     | 回   | appid、bucket |
| 5xxResponse     | ステータスコード5xx     | ステータスコード5xxが返されたリクエストの回数                     | 回   | appid、bucket |
| 2xxResponseRate | ステータスコード2xx比率 | ステータスコード2xxが返されたリクエストの回数が総リクエスト回数に占める割合 | %    | appid、bucket |
| 3xxResponseRate | ステータスコード3xx比率 | ステータスコード3xxが返されたリクエストの回数が総リクエスト回数に占める割合 | %    | appid、bucket |
| 4xxResponseRate | ステータスコード4xx比率 | ステータスコード4xxが返されたリクエストの回数が総リクエスト回数に占める割合 | %    | appid、bucket |
| 5xxResponseRate | ステータスコード5xx比率 | ステータスコード5xxが返されたリクエストの回数が総リクエスト回数に占める割合 | %    | appid、bucket |
| 400Response     | ステータスコード400     | ステータスコード400が返されたリクエストの回数                     | 回   | appid、bucket |
| 403Response     | ステータスコード403     | ステータスコード403が返されたリクエストの回数                     | 回   | appid、bucket |
| 404Response     | ステータスコード404     | ステータスコード404が返されたリクエストの回数                     | 回   | appid、bucket |
| 400ResponseRate | ステータスコード400比率 | ステータスコード400が返されたリクエストの回数が総リクエスト回数に占める割合 | %    | appid、bucket |
| 403ResponseRate | ステータスコード403比率 | ステータスコード403が返されたリクエストの回数が総リクエスト回数に占める割合 | %    | appid、bucket |
| 404ResponseRate | ステータスコード404比率 | ステータスコード404が返されたリクエストの回数が総リクエスト回数に占める割合 | %    | appid、bucket |
| 500ResponseRate | ステータスコード500比率 | ステータスコード500が返されたリクエストの回数が総リクエスト回数に占める割合 | %    | appid、bucket |
| 501ResponseRate | ステータスコード501比率 | ステータスコード501が返されたリクエストの回数が総リクエスト回数に占める割合 | %    | appid、bucket |
| 502ResponseRate | ステータスコード502比率 | ステータスコード502が返されたリクエストの回数が総リクエスト回数に占める割合 | %    | appid、bucket |
| 503ResponseRate | ステータスコード503比率 | ステータスコード503が返されたリクエストの回数が総リクエスト回数に占める割合 | %    | appid、bucket |

> ?
> 1. ステータスコード3xx、4xx、5xxの具体的な詳細については[エラーコードリスト](https://intl.cloud.tencent.com/document/product/436/7730)をご確認ください。
> 2. 各指標の統計粒度（Period）の入手可能な値はそれぞれ異なります。[DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882)インターフェースによって、各指標のサポートする統計粒度を取得することができます。

### データ読み取りクラス

| 指標の英語名   | 指標の日本語名     | 指標の意味                                                     | 単位 | ディメンション          |
| ------------ | -------------- | ------------------------------------------------------------ | ---- | ------------- |
| StdRetrieval | 標準データ読み取り量 | 標準データ読み取りの際に発生するトラフィックであり、標準ストレージのパブリックネットワークダウンストリームトラフィック、プライベートネットワークダウンストリームトラフィック、CDN back-to-originトラフィックの総和 | B    | appid、bucket |
| IaRetrieval  | 低頻度データ読み取り量 | 低頻度データ読み取りの際に発生するトラフィックであり、低頻度ストレージのパブリックネットワークダウンストリームトラフィック、プライベートネットワークダウンストリームトラフィック、CDN back-to-originトラフィックの総和 | B    | appid、bucket |


### データ処理クラス

インターフェースを呼び出してCloud Infiniteの監視データを確認することができます。Cloud Infiniteの監視インターフェースの詳細について知りたい場合は、Cloud Infinite監視指標のドキュメントをご参照ください。



## 各ディメンションに対応するパラメータ一覧

| パラメータ名                        | ディメンション名 | ディメンションの説明                | 形式                                               |
| ------------------------------- | -------- | ----------------------- | -------------------------------------------------- |
| &Instances.N.Dimensions.0.Name  | appid    | ルートアカウントAPPIDのディメンション名 | Stringタイプのディメンション名を入力：appid                     |
| &Instances.N.Dimensions.0.Value | appid    | ルートアカウントの具体的なAPPID      | ルートアカウントAPPIDを入力（例：1250000000）                 |
| &Instances.N.Dimensions.1.Name  | bucket   | バケットのディメンション名          | Stringタイプのディメンション名を入力：bucket                    |
| &Instances.N.Dimensions.1.Value | bucket   | 具体的なバケット名          | 具体的なバケット名を入力（例：examplebucket-1250000000） |



## 入力パラメータの説明

COS監視データを照会する際の入力パラメータ値は次のとおりです。

&Namespace=QCE/COS
&Instances.N.Dimensions.0.Name=appid
&Instances.N.Dimensions.0.Value=ルートアカウントのAPPID
&Instances.N.Dimensions.1.Name=bucket
&Instances.N.Dimensions.1.Value=バケット名 


## 監視の説明

- **監視間隔**：BCMは、リアルタイム、直近24時間、直近7日間、カスタマイズした日付などの様々な統計区間におけるデータ監視を行うことができます。時間粒度は1分、5分、1時間、1日をサポートしています。
- **データストレージ**：粒度が1分間隔の監視データは15日間、粒度が5分間隔の監視データは31日間保存されます。粒度が1時間間隔の監視データは93日間、粒度が1日間隔の監視データは186日間保存されます。
- **アラート表示**：BCMはCOSの監視データを統合し、データを見やすいチャート形式で表示します。製品ごとにあらかじめ定義したアラート指標に基づいてアラートを発出することができ、ユーザーが全体的な実行状況を把握するのに役立ちます。
- **アラート設定**：監視指標の閾値を設定します。監視データがアラート条件をトリガーした時点で、CMが当該グループに速やかにアラート情報を送信することができます。詳細については、[アラートの概要](https://www.tencentcloud.com/document/product/248/6126)および[モニタリングアラートの設定](https://intl.cloud.tencent.com/document/product/436/39104)をご参照ください。




