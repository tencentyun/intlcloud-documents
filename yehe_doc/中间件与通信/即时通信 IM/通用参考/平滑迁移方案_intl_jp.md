Instant Messaging（IM）には、高並列性、高信頼性を有する豊富なオペレーション実績があります。自社開発またはサードパーティのインスタントメッセージサービスを使用しているApp開発者の場合、IMとの接続を希望しているならば、移行の問題を考慮する必要があります。その場合にもIMは、シナリオごとに特化した移行プランを用意しています。

## 用語の定義

後続のドキュメントにおいては、用語を次のように定義します。

- **旧システム：**Appで従来使用しているインスタントメッセージサービス。
- **新システム：**Tencent CloudのInstant Messaging（IM）サービス。
- **App 1.0：**旧システムをベースにインスタントメッセージ機能を実装したApp。
- **App 2.0：**新システムをベースにインスタントメッセージ機能を実装したApp。
- **メッセージルーティング（メッセージコールバック）サービス：**サードパーティ通信キャリアがメッセージを受信した後、Appバックエンドにメッセージを転送します。IMの[シングルチャットメッセージ送信後のコールバック](https://intl.cloud.tencent.com/document/product/1047/34365)に類似しています。

移行プロセスの本質は、インスタントメッセージサービスのバックエンドを旧システムから新システムへ切り替え、App 1.0をApp 2.0にレベルアップするプロセスです。

## 移行プラン

IMでは、次の2種類の移行ソリューションを選択できるようになっています。プランごとに移行効果は異なり、実行難度にもかなり差があります。Appの既存のインスタントメッセージをもとに実現するシナリオを総合的に検討し、合理的な移行プランを確定する必要があります。

### 強制的バージョンアッププラン

強制的バージョンアップストラテジーとは、IMのデータの同期が完了した後、強制的にAppを1.0から2.0にバージョンアップする方式を指します。このプランの実施は簡単で、バージョンアップ後に新旧Appの互換性の問題を処理する必要がありません。具体的なプランは下図のとおりです。

![](https://main.qcloudimg.com/raw/e37a5686c81c73827c20312169c3ecc0.png)

主なフローは以下のとおりです。

1. 履歴データをIMにインポートします。これには以下が含まれます。
   - アカウントのインポート
   - ユーザープロファイルのインポート
   - ユーザーリレーションシップチェーンのインポート
   - シングルチャットメッセージ履歴のインポート
   - グループデータのインポート
   - グループチャットメッセージ履歴のインポート
2. ユーザーをApp 1.0からApp 2.0へ強制的にバージョンアップします。
3. 旧システムのサービスを停止し、すべてのユーザーの通信を新システムで行います。

### 新旧互換性プラン

新旧Appが共存し、メッセージを相互に通信できますが、App 1.0の使用を停止するまで、Appバックエンドは新旧システム間でリアルタイムな双方向の同期を維持する必要があります。このプランはどちらかというと複雑ですが、エンドユーザーの体験はより好ましいものになります。具体的なプランは下図のとおりです。

![](https://main.qcloudimg.com/raw/3b19fed85458fa96ae7110fea8cb8e41.png)

主なフローは以下のとおりです。

1. 履歴データをIMにインポートします。これには以下が含まれます。
   - アカウントのインポート
   - ユーザープロファイルのインポート
   - ユーザーリレーションシップチェーンのインポート
   - シングルチャットメッセージ履歴のインポート
   - グループデータのインポート
   - グループチャットメッセージ履歴のインポート
2. App新旧システムのデータの双方向同期を行います。これには次が含まれます。
   - シングルチャットメッセージのリアルタイムな同期
   - グループデータとグループチャットメッセージのリアルタイムな同期
3. 新旧システムが共存し、メッセージを相互に通信できます。旧Appが自然に消滅するまでこの状態が続きます。

## 詳細な移行操作

### アカウントのインポート

アカウントのインポートは、この後の各種データのインポートの前提となります。
Appバックエンドから、[アカウント一括インポートRESTインターフェース](https://intl.cloud.tencent.com/document/product/1047/34954)を呼び出して、既存のアカウントをすべてIMにインポートする必要があります。アカウントのインポートと同時にユーザーニックネームとプロフィール画像もインポートする必要がある場合は、[単独アカウントインポートRESTインターフェース](https://intl.cloud.tencent.com/document/product/1047/34953)を呼び出す必要があります。

### ユーザープロファイルのインポート

[プロファイル設定RESTインターフェース](https://intl.cloud.tencent.com/document/product/1047/34916)を呼び出して、保有しているユーザープロファイルをIMにインポートします。

### ユーザーリレーションシップチェーンのインポート

[フレンドのインポートRESTインターフェース](https://intl.cloud.tencent.com/document/product/1047/34903)を呼び出して、保有しているリレーションシップチェーンをIMにインポートします。

### シングルチャットメッセージ履歴のインポート

[シングルチャットメッセージインポートRESTインターフェース](https://intl.cloud.tencent.com/document/product/1047/35014)を呼び出して、保有しているシングルチャットメッセージをIMにインポートします。

### シングルチャットメッセージの既読設定

[シングルチャットメッセージ既読設定RESTインターフェース](https://intl.cloud.tencent.com/document/product/1047/38996)を呼び出して、シングルチャットメッセージを既読状態に設定します。

### グループデータおよびグループチャットメッセージ履歴のインポート

グループデータ、グループチャットメッセージ履歴のインポートは、以下の手順に沿って行うものとします。

1. [グループ基本プロファイルインポートRESTインターフェース](https://intl.cloud.tencent.com/document/product/1047/34967)を呼び出してグループを作成します。このインターフェースを呼び出す時に初期グループ参加者を指定できます。
2. グループのインポート時においてグループ参加者をインポートしない場合は、[グループ参加者インポートRESTインターフェース](https://intl.cloud.tencent.com/document/product/1047/34969)を呼び出してグループ参加者をインポートできます。
3. [グループメッセージインポートRESTインターフェース](https://intl.cloud.tencent.com/document/product/1047/34968)を呼び出してグループチャットメッセージ履歴をインポートします。
4. グループ参加者の未読メッセージ数を修正したい場合は、[参加者未読メッセージカウント設定RESTインターフェース](https://intl.cloud.tencent.com/document/product/1047/34909)を呼び出して関連操作を行なうことができます。

シングルチャットメッセージ、グループデータおよびグループチャットメッセージはいずれも新システムでホスティングする必要があります。新システムでこれらのタイプの増分データがあったときは、IMのコールバックを使用して旧システムも同期をとります。また、旧システムの中で発生した増分データも新システムは同期をとります。

### シングルチャットメッセージの同期

旧システムで増分メッセージがあった時は、[シングルチャットメッセージ単独送信RESTインターフェース](https://intl.cloud.tencent.com/document/product/1047/34919)の呼び出しによってIMとの同期がとられ、IMで増分メッセージがあった時も[シングルチャットメッセージ送信後のコールバック](https://intl.cloud.tencent.com/document/product/1047/34365)の呼び出しによって旧システムとの同期がとられます。

### グループデータおよびグループチャットメッセージの同期

**グループプロファイルの同期**

1. 旧システムでのグループ基本プロファイルの変更は、[グループ基本プロファイル変更RESTインターフェース](https://intl.cloud.tencent.com/document/product/1047/34962)を呼び出してリアルタイムに同期をとる必要があります。
2. IM内でのグループ基本プロファイルの変更は、[グループ作成後コールバック](https://intl.cloud.tencent.com/document/product/1047/34369)、[グループ解散後コールバック](https://intl.cloud.tencent.com/document/product/1047/34377)、[グループプロファイル変更後コールバック](https://intl.cloud.tencent.com/document/product/1047/34378)を呼び出して、旧システムとの同期をとる必要があります。

**グループ参加者情報の同期**

1. 旧システムでの参加者の追加・削除は、[グループ参加者追加RESTインターフェース](https://intl.cloud.tencent.com/document/product/1047/34962)および[グループ参加者削除RESTインターフェース](https://intl.cloud.tencent.com/document/product/1047/34949)を呼び出してIMとの同期をとる必要があります。
2. IM内での参加者のグループ参加/退出情報は、[新規参加者のグループ参加後コールバック](https://intl.cloud.tencent.com/document/product/1047/34372)および[グループ参加者の退出後コールバック](https://intl.cloud.tencent.com/document/product/1047/34373)を呼び出して旧システムとの同期をとる必要があります。

**グループメッセージの同期**

1. 旧システム内のグループチャットメッセージの増分は、グループ内の[グループ内一般メッセージ送信RESTインターフェース](https://intl.cloud.tencent.com/document/product/1047/34959)を呼び出してIMとの同期をとる必要があります。
2. IM内のグループチャットメッセージ増分は、[グループ内発信後コールバック](https://intl.cloud.tencent.com/document/product/1047/34375)を呼び出して旧システムとの同期をとる必要があります。

>!Appの既存のインスタントメッセージサービスをカバーすることができない場合は、カスタマーサービスにお問い合わせいただくか、合理的な移行プランについてビジネスマネージャーにご相談ください。
