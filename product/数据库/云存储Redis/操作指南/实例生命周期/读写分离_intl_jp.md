TencentDB for Redis は Read/Write Splitting 機能をサポートしています。読み取りが多く書き込みが少ないサービスシナリオにおいて、ホットデータが数中する読み取りニーズを解決するため、最大で1マスター5スレーブモードをサポートし、最大で5倍の読み取り性能拡張能力を提供します。

## Read/Write Splitting 原理

#### コミュニティ Redis クラスタ版
- **Read/Write Splitting 原理**: Redis クラスタ版は、Proxy 層を介して自動 Read/Write Splitting を行います。
- **Read/Write Splitting の重み付け**: Read/Write Splitting を有効にすると、Proxy はマスターノードに基づいて書き込みのみを行い、スレーブノードは均一に読み取りリクエストを割り当てる方法でアクセス行います。
![](https://main.qcloudimg.com/raw/c6965cce2e652177ad04696df57b9456.jpg)

#### CKV クラスタ版
- **Read/Write Splitting 原理**: CKV クラスタ版システムは最初から Read/Write Splitting アーキテクチャをサポートしています。全てのリクエストは 、LB（CLB ゲートウェイ）を介して各クラスタの各ノードに割り当てられ、全ノードにグローバルな Slot ルーティング情報があります。*Read/Write Splitting を有効にすると、読み取りの Key がそのノードに置かれた場合、そのままデータを読み取って返します。そうでない場合、ルーティング情報に基づいて対応するノードにリクエストを転送し、対応するノードがデータを読み取った後にそのノードに戻し、その後クライアントに返します。
- **Read/Write Splitting の重み付け**: CKV クラスタ版のトラフィックは、全て LB によってルーティングされます。そのため、Read/Write Splitting の重み付けは、4種類の TCP 接続（送信元 IP、送信元ポート、送信先 IP、送信先ポート）をもとに均一に割り当てられます。
![](https://main.qcloudimg.com/raw/1f07c6b9437fbcb2fbff10bffca2f29d.jpg)

## Read/Write Splitting の課金
Read/Write Splitting を有効にすると、読み取り専用コピーについてのみ一定の料金がかかります。具体的な料金については、[製品価格](https://cloud.tencent.com/document/product/239/9894)を参照してください。

## Read/Write Splitting を有効にするには
1. [Redis コンソール](https://console.cloud.tencent.com/redis)にログインします。
2. インスタンスリストのページで読み取り専用インスタンスを作成するデータベースを選択し、インスタンス名をクリックすることでインスタンス詳細のページに移行します。
3. 【ノード管理】ページでコピー読み取り専用ボタンをクリックすることにより、Read/Write Splitting が有効になります。
![](https://main.qcloudimg.com/raw/31acc5f160e4b4160f9b79a890990200.png)


