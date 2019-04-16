
TencentDB for Redis について理解したい場合に、通常関連する概念は次の通りです。

**インスタンス**：Tencent Cloud 内で独立して実行されるデータベース環境です。1つのデータベースインスタンスにユーザーが作成した複数のデータベースを含むことができます。

[**Virtual Private Cloud（VPC）**](https://cloud.tencent.com/document/product/215/20046)：カスタマイズされた仮想ネットワーク空間です。他のリソースから論理的に隔離されます。

[**セキュリティグループ**](https://cloud.tencent.com/document/product/239/30911)：Redis インスタンスに対して安全なアクセス制御を行います。 インスタンスに入る IP、プロトコルおよびポートルールを指定します。

[**リージョンとアベイラビリティゾーン**](https://cloud.tencent.com/document/product/239/4106)：Redis のインスタンスとその他のリソースの物理的な位置です。

[**Tencent Cloud コンソール**](https://console.cloud.tencent.com/cdb)：Web に基づいたユーザーインターフェースです。

[**プロジェクト**](https://cloud.tencent.com/document/product/378/10863)：開発業者がより簡単にクラウド製品を管理して開発できるようにする機能です。この機能は主にプロジェクト単位で実行し、各クラウド製品をそれぞれのプロジェクトに割り当てることで実現されます。

[**Read/Write Splitting**](https://cloud.tencent.com/document/product/239/19543)：TencentDB for Redis は Read/Write Splitting 機能をサポートしています。読み取りが多く書き込みが少ないサービスシナリオにおいて、ホットデータが集中する読み取りニーズを解決するため、最大で1マスター5スレーブモードをサポートし、最大で読み取り性能を5倍拡張します。
