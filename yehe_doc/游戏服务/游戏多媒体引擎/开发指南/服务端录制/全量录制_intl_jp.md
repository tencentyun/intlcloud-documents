本書では、フルレコーディングで**GMEサーバー側のレコーディング**機能に素早くアクセスする方法を説明します。



## 運用シーン

GMEはリアルタイム音声ストリーム向けの**サーバー側のレコーディング**機能を提供し、開発者がコンテンツの保存/管理/二次創作などのシーンを実装することに役立ちます。フルレコーディング：アプリケーションにおけるすべての音声ルームに対して、ルームによるミックスストリーミングとユーザーによるシングルストリーミングをレコーディングすることをサポートします。カスタムレコーディング：ユーザーが指定したルームに対して、ルームによるミックスストリーミングとユーザーによるシングルストリーミングをレコーディングすることをサポートします。レコーディングしたオーディオファイルは、ご利用のアカウント配下の**COS**サービスに保存されます。


本書では、**フルレコーディング**の開発・アクセス方法のみを説明します。アプリケーションに対して、カスタムレコーディングを有効にするには、[開発ガイド-カスタムレコーディング](https://www.tencentcloud.com/ko/document/product/607/53748)をご参照ください。

>! 
>- GMEサーバー側のレコーディング機能を使用すると、レコーディング中にGMEでレコーディングサービスの使用料金が発生します。GME国際サイトのレコーディングサービスは、2023年4月1日より正式に課金を開始いたします。詳細な料金情報は、事前に[GME購入ガイド](https://www.tencentcloud.com/zh/document/product/607/50009)で公開いたします。
>- レコーディングしたファイルは、ご利用のTencent Cloudアカウント配下の**COS**サービスに保存されます。**COS**請求書は、実際のストレージ使用量、保存期間、アクセス頻度などに応じて作成されます。料金情報の詳細については、[COS料金説明](https://www.tencentcloud.com/zh/document/product/436/16871)をご参照ください。

##  前提条件

- **リアルタイム音声サービスが有効になっていること：[サービス有効化ガイド](https://www.tencentcloud.com/document/product/607/10782)をご参照ください。
- **サーバー側のレコーディングサービスが有効になっていること**：現在、サーバー側のレコーディングサービスは、ホワイトリストユーザーだけに提供しています。ホワイトリストを有効化するには、こちらに連絡してください。
- **GME SDK導入済み**：コアインターフェースとリアルタイム音声インターフェースの導入を含みます。詳細については、[Native SDKクイックスタート](https://www.tencentcloud.com/document/product/607/40858)、[Unity SDKクイックスタート](https://www.tencentcloud.com/document/product/607/44544)、[Unreal SDKクイックスタート](https://www.tencentcloud.com/document/product/607/44545)をご参照ください。


## サービスアーキテクチャ
![](https://staticintl.cloudcachetci.com/yehe/backend-news/j2pg571_PRELIM__%E6%B8%B8%E6%88%8F%E5%A4%9A%E5%AA%92%E4%BD%93%E5%BC%95%E6%93%8E_%E4%BA%A7%E5%93%81%E7%9B%AE%E5%BD%95_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US-1.png)

## 機能説明
### 1.レコーディング範囲

フルレコーディングを有効にすると、すべてのリアルタイム音声ルームがレコーディングされます。レコーディングは、ルームミックスストリーミングのみ、ユーザーシングルストリーミングのみ、シングルストリーミングとミックスストリーミング両方を設定できます。

### 2.レコーディングメカニズム


### レコーディングタスクの起動メカニズム

- 最初のユーザーがルームに参加すると、レコーディングタスクが開始します

### レコーディングタスクの停止メカニズム

- 最後のユーザーがルームを退出すると、レコーディングタスクが終了します

### レコーディングタスクのマルチパートメカニズム

- 単一オーディオファイルの長さが2時間になると、オーディオファイルを自動的にマルチパートに分割します
- ユーザーがマイクの接続を切断すると、ユーザーシングルストリーミングレコーディングオーディオを自動的にマルチパートに分割します。ユーザーがマイクの接続を確立すると、新しいマルチパートが作成されます
- レコーディング中のタスクが異常で中断した場合、タスクが自動的に再接続すると、新しいマルチパートが作成されます


#### レコーディングタスクのイベント通知メカニズム

- レコーディングタスクのイベントは、コールバックメカニズムにより、設定されたコールバックアドレスに通知されます。**レコーディング開始**、**レコーディング停止**、**レコーディングファイルアップロード完了**、これらのイベントが発生した場合、コールバック通知を受信します
- コールバック情報の詳細については、[レコーディングコールバックの説明](https://www.tencentcloud.com/ko/document/product/607/53749)をご参照ください



### 3.保存先

GMEサーバー側のレコーディングが完了した後、レコーディングしたオーディオファイルは、ご利用のアカウント配下の**COS**サービスの指定されたバケットに保存されます。バケットのリージョンは指定する必要があります。指定可能なリージョンのリストについては、[COSリージョンの説明](https://www.tencentcloud.com/document/product/436/6224)をご参照ください。


### 4.レコーディングファイルのフォーマット

- .mp3


### 5.レコーディングファイルの命名規則

- ユーザーシングルレコーティングファイル：bizid_roomid_userid/${タスクの開始時間}_${id}_audio.mp3
- ルームミックスストリーミングレコーティングファイル：bizid_roomid/${taskid}_${タスクの開始時間}_${id}_audio.mp3

 ***bizid:*** GMEアプリケーションID。[GMEコンソール](https://console.tencentcloud.com/gamegme)から取得できます
 ***roomid:*** 音声ルームID。リアルタイム音声サービスを使用する時に定義してGME SDKに渡します
 ***userid:*** プレイヤーID。リアルタイム音声サービスを使用する時に定義してGME SDKに渡します
 ***taskid:*** レコーティングタスクID。GMEレコーティングサービスにより生成されます。レコーディングタスクごとに１つの特殊なタスクIDがあります
 ***id:*** レコーティングタスクのマルチパートのシリアル番号。シリアル番号は0から始まります



## アクセス手順

<dx-steps>
-<dx-tag-link link="#StartRealTimeASR" tag="业务侧">コンソールでのレコーティングサービスの設定</dx-tag-link>
-<dx-tag-link link="#callback" tag="业务侧">レコーティングタスクのコールバック受信（オプション）</dx-tag-link> 
-<dx-tag-link link="#result" tag="业务侧">レコーディングファイルの確認/管理</dx-tag-link>
</dx-steps>


### ステップ1：コンソールでのレコーティングサービスの設定

- #### レコーディングサービスの有効化/無効化

[GMEコンソール](https://console.tencentcloud.com/gamegme)にログインし、【サービス管理】メニューを開き、レコーディングサービスを有効にするアプリケーションの【設定】をクリックし、アプリケーションの詳細ページに進みます。ページで【音声レコーティングサービス】の**変更**をクリックします。

![](https://qcloudimg.tencent-cloud.cn/raw/9e2c89f462a81ba228c978cd725abf5a.png)

レコーディングスイッチに**有効**を設定します。

レコーディングサービスを初めて有効にした場合、GMEはご利用の**COSサービス**にアクセスする許可を要求します。ポップアップしたダイアログで許可すると、サーバー側のレコーディングサービスが有効になります。


![](https://qcloudimg.tencent-cloud.cn/raw/33407cf16b4ad310b65c4897ea766340.png)

- #### レコーディングファイルのストレージ設定

アプリケーションの詳細ページで、【音声レコーティングサービス】の**変更**をクリックし、**レコーディングファイルのバケット**で**バインディング**をクリックします。
**バケットのバインディング**ダイアログで、既存COSバケット（既存バケットは[COSコンソール](https://console.tencentcloud.com/cos/bucket)で事前に作成する必要がある）のバインディングまたはバケットの新規作成ができます。

![](https://qcloudimg.tencent-cloud.cn/raw/c63e0fd24da877f5f79f49360f4ff9e1.png)

- #### レコーディングイベントのコールバック設定（オプション）
レコーディングサービスのイベントコールバックを受信するには、コールバックアドレスを設定する必要があります。操作パス：アプリケーションの詳細ページで、【音声レコーティングサービス】の**変更**をクリックし、**コールバックアドレス**で**変更**をクリックし、ポップアップしたダイアログにコールバックを受信するurlアドレスを入力します。現在、レコーディングタスクの完了状態のみに対して、イベントコールバックのメッセージをプッシュします。

![](https://qcloudimg.tencent-cloud.cn/raw/92314d86dbf00e8cdafe6ac24d1c17b8.png)

- #### レコーディング範囲の設定
レコーディング範囲は、カスタムレコーディングとフルレコーディングを選択できます。フルを選択し、チェックボックスでシングルストリーミングのレコーディングとミックスストリーミングのレコーディングを指定してください。

上記のように設定し、**保存**をクリックすると、レコーディングサービスが有効になります。レコーディングサービスを使用する必要があ➁場合、予定外の費用の発生を防ぐために、コンソールでレコーディングサービスのスイッチを**無効**にしてください。




### ステップ2：レコーティングタスクのコールバック受信（オプション）

**ステップ1**でコールバックアドレスを設定した場合、レコーディングタスクのイベントコールバックを受信することになります。



### ステップ3：レコーティングファイルの確認/管理

完全なオーディオファイルはレコーディングタスクが終了して数分以内に作成できます。ご利用の[COSコンソール](https://console.tencentcloud.com/cos/bucket)で、レコーディングファイルを確認、管理できます。







