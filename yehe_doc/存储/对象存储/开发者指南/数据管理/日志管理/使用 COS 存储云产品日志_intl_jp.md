## 概要

Tencent Cloud製品を使用する際には大量のログが生成されます。これらのログはお客様の業務の状況を記録するもので、業務状況の分析に役立ち、業務の発展と方針決定を支援します。COSのストレージ機能を利用することで、クラウド製品ログの永続ストレージを実現することができるほか、API、SDKまたはツールなどの方法で、COSから便利かつスピーディーにログを取得し、分析を行うことができます。

COSを使用したクラウド製品ログのストレージは、次のような問題の解決に役立ちます。

- **永続ストレージ**：COSは安定した永続的なストレージサービスをご提供します。ログをCOSに保存することで、永続ストレージを極めて低コストで実現することができます。業務上、ログに基づいた分析または方針決定が必要な場合は、COSによっていつでもどこでも任意の時間帯のログを取得することが可能です。
- **データ検索**：COSはSelect機能をご提供しています。この機能を使用することで、COSに保存されたログを簡単に検索および抽出することができます。ログのフィールドを結合し、必要な情報の検索とデータダウンロードトラフィックの削減に役立てることも可能です。


## ログ配信方式

次の2つの方法でTencent Cloud製品のログをCOS上に保存することができます。

- クラウド製品に付属しているログ配信機能を使用：例えばCloud Object Storage（COS）、Cloud Load Balancer（CLB）、CloudAudit（CA）などの製品では、ログを直接COSに配信することができます。
- Cloud Log Service（CLS）の配信機能を使用：CLSに配信されるクラウド製品のログは、CLSによってCOS上に配信されて永続ストレージとなります。

現在のTencent Cloud製品の、これらの2つの方法に対するサポート状況は次のとおりです。

| クラウド製品名          | COSへの直接配信をサポートしているか | CLSへの配信をサポートしているか     |
| ------------------- | ---------------------- | ---------------------- |
| CloudAudit（CA）           | はい                     | いいえ                     |
| Cloud Load Balancer（CLB）        | いいえ                     | はい                     |
| Cloud Kafka     | はい                     | いいえ                     |
| API Gateway | いいえ                     | はい                     |
| Serverless Cloud Function（SCF）      | いいえ                     | はい                     |
| Tencent Kubernetes Engine（TKE）        | いいえ                     | はい                     |
| CSS          | いいえ                     | はい                     |
| クラウド開発TCB          | いいえ                     | はい、ただしCLSによるCOSへの配信はサポートなし |
| COS（Cloud Object Storage）        | はい                     |  ホワイトリストアクティブ化申請のサポートあり。[テクニカルサポートWeChatグループ](https://intl.cloud.tencent.com/contact-sales)に加入し、ホワイトリストアクティブ化についてお問い合わせください       |

### COSへのログ直接配信

次のTencent Cloud製品はCOSへのログ直接配信機能を備えています。対応する製品ドキュメントガイドをご参照の上、ログ配信ルールを設定し、ログをCOSに配信することができます。

| クラウド製品名     | ログ配信ドキュメント                                                 | ログ配信間隔      | ログ配信パス                                                 |
| --------------- | ------------------------------------------------------------ | -------------------- | ------------------------------------------------------------ |
|CA（CloudAudit） |[ここをクリックして確認](https://intl.cloud.tencent.com/document/product/1021/30338) | 10～15分 |  cloudaudit/customprefix/timestamp|
| Cloud Kafka | [ここをクリックして確認](https://intl.cloud.tencent.com/document/product/597) | 5分～60分<br>配信間隔を指定可能 | instance id/topic id/timestamp                           |
| Cloud Object Storage（COS）    | [ここをクリックして確認](https://intl.cloud.tencent.com/document/product/436/17040) | 5分                | パスのプレフィックスはご自身で指定できます。例えばcos_bucketname_access_log/timestampのように、識別可能なパスを設定することをお勧めします |

>?Cloud Kafkaではその製品上で生成されたメッセージデータの配信をサポートしています。CKafkaインスタンスの作成などの行動ログを取得したい場合は、CloudAudit製品のログ配信を選択することができます。

### Cloud Log Service（CLS）によるCOSへのログ配信

次のTencent Cloud製品は、ユーザーの検索と分析に役立つよう、Cloud Log Service（CLS）へのログ配信をサポートしています。CLSはまたCOSへの配信を行う製品機能をご提供し、ログストレージの永続化に役立てることができます。CLSへのログ配信をサポートする製品では、CLS側でCOSへのログ配信を有効化する方式により、データを永続ストレージにしてストレージコストを引き下げ、さらなるオフライン分析に役立てることも可能です。現在、CLSへのログ直接配信をサポートしている製品は次のとおりです。

| クラウド製品名           | ログ配信ドキュメント                                                 |
| -------------------- | ------------------------------------------------------------ |
| API Gateway | [ここをクリックして確認](https://intl.cloud.tencent.com/document/product/628/34636) |
| Tencent Kubernetes Engine（TKE）         | [ここをクリックして確認](https://intl.cloud.tencent.com/document/product/457/32419) |
| CSS           | ここをクリックして確認|

CLSによるCOSへの配信には3つの方式がサポートされています。

- 区切り文字形式による配信：データを区切り文字形式でCOSに配信できます。詳細については、[区切り文字形式による配信](https://intl.cloud.tencent.com/document/product/614/31582)をご参照ください。
- JSON形式による配信：データをJSON形式でCOSに配信できます。詳細については、[JSON形式による配信](https://intl.cloud.tencent.com/document/product/614/31583)をご参照ください。
データをオリジナルテキスト形式で配信することができます。シングルライン全文、マルチライン全文の配信をサポートし、CSV形式の配信も一部サポートしています。詳細については、[オリジナルテキスト形式による配信](https://intl.cloud.tencent.com/document/product/614/31584)をご参照ください。

CLSによるCOSへのログ配信では、次の操作を実行する必要があります。

1. 業務上のニーズに応じて対応する製品を選択し、上記でご提供した製品ログ配信についてのドキュメントリンクガイドに従ってログセットとログトピックを設定し、業務で発生したデータをCLSに結合します。
2. その後、業務上の必要に応じ、適切な形式を選択してデータをCOS上に配信します。ログをCOSに配信する際は、複数の製品のログを区別するため、製品名をパスのプレフィックスとすることをお勧めします。例えばTKEのログの場合、`TKE_tkeid_log/timestamp`と命名することができます。
3. 配信ルールを設定した後、さらにSCF製品にファイルアップロードイベント通知を追加で設定し、ログデータがCOSに配信された後、イベント通知に基づいて次の操作を実行できるようにすることも可能です。詳細については、[イベントの通知](https://intl.cloud.tencent.com/document/product/436/31648)をご参照ください。

## ログに対する分析

### ログをローカルにダウンロードしてオフライン分析を実施

ログデータをローカルにダウンロードしたい場合は、コンソール、SDK、APIまたはツールなどの複数の方式で行うことができます。各ダウンロード方式で使用するドキュメントの説明は次のとおりです。下記のドキュメントを参照し、コードの中のファイルパスに関わる部分をログのストレージパスに置き換えることで、ログデータをローカルにダウンロードすることができます。

| ダウンロード方式       | 使用説明                                                     |
| -------------- | ------------------------------------------------------------ |
| コンソール         | [ここをクリックして確認](https://intl.cloud.tencent.com/document/product/436/13322) |
| cosbrowser     | [ここをクリックして確認](https://intl.cloud.tencent.com/document/product/436/32565) |
| coscmd         | [ここをクリックして確認](https://intl.cloud.tencent.com/document/product/436/10976) |
| Android SDK    | [ここをクリックして確認](https://intl.cloud.tencent.com/document/product/436/37675) |
| C SDK          | [ここをクリックして確認](https://intl.cloud.tencent.com/document/product/436/31518) |
| C++ SDK        | [ここをクリックして確認](https://intl.cloud.tencent.com/document/product/436/31522) |
| .NET SDK       | [ここをクリックして確認](https://intl.cloud.tencent.com/document/product/436/30594) |
| Go SDK         | [ここをクリックして確認](https://intl.cloud.tencent.com/document/product/436/31526) |
| iOS SDK        | [ここをクリックして確認](https://intl.cloud.tencent.com/document/product/436/37684) |
| Java SDK       | [ここをクリックして確認](https://intl.cloud.tencent.com/document/product/436/31534) |
| JavaScript SDK | [ここをクリックして確認](https://intl.cloud.tencent.com/document/product/436/31538) |
| Node.js SDK    | [ここをクリックして確認](https://intl.cloud.tencent.com/document/product/436/31710) |
| PHP SDK        | [ここをクリックして確認](https://intl.cloud.tencent.com/document/product/436/31542) |
| Python SDK     | [ここをクリックして確認](https://intl.cloud.tencent.com/document/product/436/31546) |
| ミニプログラムSDK     | [ここをクリックして確認](https://intl.cloud.tencent.com/document/product/436/32457) |
| API            | [ここをクリックして確認](https://intl.cloud.tencent.com/document/product/436/7753) |

### COS Selectを使用したログ分析の実施

COS Select機能を使用して、COS上に保存されたログファイルを直接検索および分析することもできます。前提として、ログファイルがCSVまたはJSON形式で保存されていることが必要です。COS Select機能によって必要なログフィールドをフィルタリングできるため、COSの転送ログデータ量を大幅に削減することができ、使用コストを引き下げると同時にデータ取得効率を向上させることが可能です。COS Select機能について詳しくお知りになりたい場合は、[Selectの概要](https://intl.cloud.tencent.com/document/product/436/32472)をご参照ください。

現在、COS Select機能はコンソールまたはAPI方式でご利用いただけます。

| 使用方式 | 使用説明                                                     |
| -------- | ------------------------------------------------------------ |
| コンソール   | [ここをクリックして確認](https://intl.cloud.tencent.com/document/product/436/32538) |
| API      | [ここをクリックして確認](https://intl.cloud.tencent.com/document/product/436/32360) |


