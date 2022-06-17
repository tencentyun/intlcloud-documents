[](id:senderConfig)
## 送信者設定オプション
SESは現在、Eメール送信方法として、Tencent Cloud SESコンソール、Tencent Cloud SES API、Tencent Cloud SES SMTPという3種類の方法を提供しています。SESコマンドラインインターフェース(SES CLI)、[SES開発キット(SDK)によるAPIへのアクセス](https://intl.cloud.tencent.com/document/product/1084/39387)またはSMTPインターフェースの呼び出してメールを送信することができます。

Eメール送信を開始するには、[コンソールガイド > メール送信](https://intl.cloud.tencent.com/document/product/1084/40178)をご参照ください。
## フレキシブルなデプロイオプション
### 共有IPアドレス
一般的にSESでは、デフォルトで共有IPプールの共有IPアドレスを使用してEメールを送信します。確立されたIPを使ってすぐにEメール送信を始めたいユーザーも多く、共有アドレスは便利で安全なオプションです。Tencent Cloudは共有IPの品質を保証し、高い到達率を確保することができます。
### 専用IPアドレス
専用IPとは、Tencent Cloudによって特別に割り当てられたSESのIPのことです。これらのIPは通常、送信したことのないIPまたは過去に良いレピュテーションを得たことのあるIPであり、反スパム団体にスパムIPとしてマークされていないことを保証することができます。専用IPを申請するには、ある程度の送信量が必要です。送信ニーズが多い場合は、ビジネスマネージャーに連絡して専用IPを申請することができます。


## 送信者のID管理とセキュリティ
インターネットサービスプロバイダ（ISP）がEメールを受信すると、まずID認証が行われているかチェックしてから受信者に送信します。この場合のID認証とは、ISPに対して、お客様がEメールの送信先のメールアドレスを所有していることを証明することをいいます。SESは、Sender Policy Framework(SPF)、Domain Key Identified Mail(DKIM)、ドメインベースのメッセージ検証、報告、および適合性(DMARC)といったあらゆる業界規格の検証メカニズムをサポートしています。お客様のEメールが確実にISPのチェックをパスし、受信者にスムーズに届くようにします。
### 送信統計情報
SESは、Eメールの到達率、開封率、クリック率および購読解除データなど、メール返信パイプライン全体に関する情報をキャプチャして正確なデータ分析を行うといった、Eメール送信アクティビティを監視するさまざまな方法を提供しています。また、個々のEメールについては、[メール送信ステータス取得インターフェース](https://intl.cloud.tencent.com/document/product/1084/39502)から、メール送信ステータスを照会し、メール送信ポリシーの調整に役立てることができます。

[](id:warmUp)
## 自動warm up 
### 製品の特徴
Eメール配信のプロセスは非常に複雑で、メールの配信能力と到達率を引き上げるには、IP/ドメイン名のレピュテーションが非常に重要です。warm upは、徐々にレピュテーションを高めていくプロセスです。メールの送信量は日々漸増する必要があり、一足飛びに目標の規模に達することはできません。送信量は、（日）単位で段階的に増加します。適切なwarm upは、Eメールサービスプロバイダ(ISP)の良好なレピュテーションにつながります。
>?自動warm upとは、IPアドレスまたは送信ドメイン名が、人手を介さずに自動的にウォームアップされることを意味します。
### 機能説明
自動warm upは、[標準版ルール（デフォルト）](#default)と[アップグレード版ルール](#customize) という2つのランクがあります。

#### デフォルトルール
一斉送信モードから、デフォルトでwarm up標準版ルールに進みます。製品のバックエンドが一連のポリシーに従ってその日の送信クォータを自動的に割り当てることで、すべてのプロセスが人手を介さずに自動的に完了します。その日の最大受信量を超えると、自動的に送信は中断され、残りの未送信メールはキューキャッシュに入れられ、現在時刻から24時間後に自動的に送信されます。標準版warm up計画は次のとおりです。[](id:default)

<table style="width: 200px;">
   <tr>
      <th width="0px" style="text-align:center">時間</td>
      <th width="0px" style="text-align:center">送信量/日</td>
   </tr>
	<tr>
		<td style="text-align:center"style="text-align:center">1日目</td>
		<td style="text-align:center">500</td>
	</tr>
	<tr>
		<td style="text-align:center">2日目</td>
		<td style="text-align:center"sdval="200" >1000</td>
	</tr>
	<tr>
		<td style="text-align:center">3日目</td>
		<td style="text-align:center"sdval="500" >2000</td>
	</tr>
	<tr>
		<td style="text-align:center">4日目</td>
		<td style="text-align:center"sdval="1000" >5000</td>
	</tr>
	<tr>
		<td style="text-align:center">5日目</td>
		<td style="text-align:center"sdval="2000" >10000</td>
	</tr>
	<tr>
		<td style="text-align:center">6日目</td>
		<td style="text-align:center"sdval="5000" >20000</td>
	</tr>
	<tr>
		<td style="text-align:center">7日目</td>
		<td style="text-align:center"sdval="10000" >40000</td>
	</tr>
	<tr>
		<td style="text-align:center">8日目</td>
		<td style="text-align:center"sdval="20000" >60000</td>
	</tr>
	<tr>
		<td style="text-align:center">9日目</td>
		<td style="text-align:center"sdval="30000" >80000</td>
	</tr>
	<tr>
		<td style="text-align:center">10日目</td>
		<td style="text-align:center"sdval="40000" >100000</td>
	</tr>
	<tr>
		<td style="text-align:center">11日目</td>
		<td style="text-align:center"sdval="60000" >150000</td>
	</tr>
	<tr>
		<td style="text-align:center">12日目</td>
		<td style="text-align:center"sdval="80000" >200000</td>
	</tr>
	<tr>
		<td style="text-align:center">13日目</td>
		<td style="text-align:center"sdval="100000" >300000</td>
	</tr>
	<tr>
		<td style="text-align:center">14日目</td>
		<td style="text-align:center"sdval="120000" >400000</td>
	</tr>
	<tr>
		<td style="text-align:center">15日目</td>
		<td style="text-align:center"sdval="150000" >500000</td>
	</tr>
	<tr>
		<td style="text-align:center">16日目</td>
		<td style="text-align:center"sdval="200000" >600000</td>
	</tr>
	<tr>
		<td style="text-align:center">17日目</td>
		<td style="text-align:center"sdval="400000" >700000</td>
	</tr>
	<tr>
		<td style="text-align:center">18日目</td>
		<td style="text-align:center"sdval="600000" >800000</td>
	</tr>
	<tr>
		<td style="text-align:center">19日目</td>
		<td style="text-align:center"sdval="800000" >900000</td>
	</tr>
		<tr>
		<td style="text-align:center">20日目</td>
		<td style="text-align:center"sdval="800000" >1000000</td>
	</tr>
</table>

[](id:customize)
#### カスタマイズルール：
高品質なメールのため、標準版warm up計画がお客様のご要望に合わない場合は、アップグレード版のwarm up計画をお申込みいただけますので、専任のビジネスマネージャーまでご連絡ください。
[](id:batch)
## バッチ機能セット
マーケティングメールや通知メールといった一斉送信に適しています。トリガーメール（ID認証、取引関連など）は、API-SendEmailインターフェースを介して送信することをお勧めします。
### 製品の特徴
SESのバッチ機能サービスを利用する場合、2つの方法で呼び出すことができます。
•	コンソールからメールを一斉送信します。テンプレートの呼び出しが必要で、メールのサイズは10MB以内とします。添付ファイルは現時点ではサポートされていません。
•	APIインターフェースからメールを一斉送信します。テンプレートの呼び出しが必要で、メールのサイズは10MB以内とします。添付ファイルがサポートされています。

### 機能説明
コンソールでは、**メール送信** > **受信者リスト**ページで送信アドレスを管理することができます。

一斉送信には自動warm up標準版計画が設定されており、現在のIP/ドメイン名レピュテーションを自動的に認識し、その日の送信クォータを割り当て、自動的にその日の最大送信量を超えているかどうかを判断します。超えている場合はメール送信が自動的に中断し、残りの未送信メールはキューキャッシュに入れられ、現在時刻から24時間遅れで自動的に送信されます。

## 一斉送信
コンソールで送信タスクを新規作成し、タスクタイプで「一斉送信」を選択します。さらに送信タスクの入力必須項目をすべて入力すると、メールの一斉送信を行うことができます。
## 時間指定送信
すべてのメールはお客様のスケジュールに従って所定の時間に送信することができます。タスクの開始時間を選択すれば、特定の時間帯にメールを自動的に順次送信できます。
## 予約送信
コンソールでメールの予約送信の設定を行い、タスクの開始時間とタスク期間を選択します。コンソールは、メールの予約送信を自動的に完了させます。
