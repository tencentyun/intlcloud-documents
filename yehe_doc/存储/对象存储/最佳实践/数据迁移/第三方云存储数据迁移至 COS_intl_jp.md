## プラクティスの背景

サードパーティのクラウドプラットフォームを使用しているユーザーの場合、Cloud Object Storage(COS)は、ストレージデータをサードパーティのクラウドプラットフォームからCOSに速やかに移行するときに役立ちます。


| 移行方法&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | インタラクティブ形式       | ファイルサイズを区別するためのしきい値 | 移行の同時実行性 | HTTPSセキュア送信 |
| ------------------------------------------------------------ | -------------- | ------------------ | ---------- | -------------- |
| [Migration Service Platform](#msp)                                     | ビジュアルページ操作 | デフォルト設定の使用      | グローバル統合   | 有効化           |


このプラットフォームは、データ移行の進捗確認、ファイルの整合性チェック、再送の失敗、中断からの再開などの機能をサポートしており、ユーザーの基本的な移行ニーズを満たすことができます。


## 移行のプラクティス

<span id=msp></span>

### Migration Service Platform

Migration Service Platform(MSP)は、さまざまな移行ツールを統合し、大規模なデータ移行タスクをユーザーが手軽に監視、管理できるビジュアルインターフェースを提供するプラットフォームです。中でも「ファイルマイグレーションツール」は、ユーザーがさまざまなパブリッククラウドやデータソースサイトからCOSにデータを移行する際に役立つツールです。

移行操作の手順は次のとおりです。

1. [Migration Service Platformコンソール](https://console.cloud.tencent.com/msp)にログインします。
2. 左のナビゲーションバーにある**COS移行**をクリックし、COS移行ページに進みます。
3. **タスクの新規作成**をクリックして、移行タスクを新規作成し、タスク情報を設定します。
4. タスクを起動します。

具体的な操作については、以下の移行チュートリアルをご参照ください。

- [Alibaba Cloud OSSの移行](https://intl.cloud.tencent.com/document/product/1036/35578)
- Huawei Cloud OBSの移行
- Qiniu Cloud KODOの移行
- UCLOUD UFileの移行
- Kingsoft Cloud KS3の移行
- Baidu Cloud BOSの移行
- [AWS S3の移行](https://intl.cloud.tencent.com/document/product/1036/32522)

#### 操作テクニック

データ移行プロセスでは、ネットワーク環境によってデータソースの読み込み速度が異なる場合がありますが、お客様は「ファイル移行タスクの新規作成」時に高いQPS同時実行性を選択することで、移行速度を向上させることが可能です。

<span id=cos>



