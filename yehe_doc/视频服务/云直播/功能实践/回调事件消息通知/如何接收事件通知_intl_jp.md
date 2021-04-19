ライブストリーミングの過程でドメイン名をテンプレートに関連付けしたイベントがトリガーされると、Tencent Cloudが自動的にリクエストを顧客のサーバーに送信し、顧客のサーバーがリクエストの応答を担当します。検証を通過した後、顧客側では受動的にCSSイベントコールバック情報が含まれたJSONデータパックを取得できます。

現在CSSのイベントトリガーのメッセージ通知でサポートされているイベントには、CSSプッシュ、CSSストリーム切断、CSSレコーディング、CSSスクリーンキャプチャ、CSSポルノ検出のイベントメッセージ通知があります。

## 全体フロー

<img src="https://main.qcloudimg.com/raw/252b7e06b322350c8520283e7826d5a3.png" data-nonescope="true">

**フロー説明：**
1. キャスターが、コンソールまたはTencentCloud APIを直接呼び出して、イベントメッセージ通知のURLおよびレコーディング、スクリーンキャプチャなどの関連機能を設定します。
2. キャスターがCSSプッシュを切断します。
3. CSSサービス内部にイベントが発生すると、メッセージがイベントメッセージ通知サービス経由で視聴者に一括してコールバックされます。
<span id="protocol"></span>
## イベントメッセージ通知のプロトコル

### ネットワークプロトコル
- リクエスト：HTTP POSTリクエスト。パケットの中身はJSON。各メッセージの具体的なパケットの内容は後述をご参照ください。
- 応答：HTTP STATUS CODE = 200、サーバーは応答パケットの具体的な内容を無視します。プロトコルとの親和性のため、クライアントの応答内容に JSON： `{"code":0}`を付けることをお勧めします

### 通知の信頼性

イベント通知サービスにはリトライ機能が含まれ、リトライの間隔は60秒、合計リトライ数は3回です。リトライとお客様のサーバーやネットワーク帯域幅との衝突が起きるのを避けるため、正常なリターンパケットを維持してください。リトライがトリガーされる条件は以下となります。

- 長時間（20 秒）リターンパケットの応答がない場合。
- HTTP STATUSの応答が200でない場合。

<span id="configuration"></span>
## コールバックイベントの設定方式
コールバック設定は、主に2種類の方式で実現します。1つは、 [CSSコンソール](#c_callback)を利用し、もう1つは [サーバーAPI]の呼び出し(#api_callback)によるものです。
>?CSSのイベントメッセージ通知のコールバックURLでは、プッシュイベント、ストリーム切断イベント、レコーディングイベント、スクリーンキャプチャイベント、ポルノ検出イベントの設定に対して単独のコールバックURLをサポートしています。



<span id="c_callback"></span>
### CSSコンソール
1. CSSコンソールの【機能テンプレート】>【[コールバック設定](https://console.cloud.tencent.com/live/config/callback)】に入り、コールバックテンプレートを作成します。具体的な操作については、[コールバックテンプレートの作成](https://intl.cloud.tencent.com/document/product/267/31074)をご参照ください。
![](https://main.qcloudimg.com/raw/e487fbb21c3e7018c97f82f7055b8f8a.png)
2. [【Domain Management】](https://console.cloud.tencent.com/live/domainmanage)で操作が必要なプッシュドメイン名を見つけ、【管理】>【テンプレート設定】をクリックして、このドメイン名とトランスコードテンプレートの関連付けを行います。具体的な操作については、 [コールバック設定](https://cloud.tencent.com/document/product/267/35254)をご参照ください。
<span id="api_callback"></span>
### サーバーAPI
1.  [CreateLiveCallbackTemplate](https://intl.cloud.tencent.com/document/product/267/30815) を呼び出して、コールバックテンプレートのインターフェースを作成し、必要なコールバックパラメータ情報を設定します。
2. [CreateLiveCallbackRule](https://intl.cloud.tencent.com/document/product/267/30816) を呼び出して、コールバックルールを作成し、パラメータのプッシュドメイン名DomainName 、TemplateIdを設定します（ステップ1を繰り返す）。プッシュおよび再生アドレスのものと一致するAppNameを入力すると、一部のライブストリーミングでコールバック起動の効果が実現されます。

## コールバック情報パラメータの説明
コールバックテンプレートとドメイン名の関連付けが成功した後、ライブストリーミングの過程でテンプレートのイベントがトリガーされると、Tencent Cloudは自動的にコールバック情報が含まれたJSONパッケージを顧客のサーバーに送信します。コールバック情報の具体的なパラメータ説明は次となります。
- [プッシュイベントメッセージ通知](https://intl.cloud.tencent.com/zh/document/product/267/38081)
- [ストリーム切断イベントメッセージ通知](https://intl.cloud.tencent.com/zh/document/product/267/38081)
- [レコーディングイベントメッセージ通知](https://intl.cloud.tencent.com/zh/document/product/267/38082)
- [スクリーンキャプチャイベントメッセージ通知](https://intl.cloud.tencent.com/zh/document/product/267/38083)
- [ポルノ検出イベントメッセージ通知](https://intl.cloud.tencent.com/zh/document/product/267/38084)






