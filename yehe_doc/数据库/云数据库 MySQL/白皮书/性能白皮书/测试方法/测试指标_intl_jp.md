このドキュメントでは、MySQL性能テストにおけるテスト指標をご説明します。

## テスト指標
- **1秒あたりのトランザクションの実行数TPS（Transactions Per Second）**
データベースが1秒あたり実行するトランザクションの数、COMMIT成功回数を基準とします。
- **1秒あたりのリクエストの実行数QPS（Queries Per Second）**
INSERT、SELECT、UPDATE、DETELE、COMMITなど、データベースが1秒あたり実行するSQLの数です。。
- ** すべてのeventのかかる平均時間avg_lat（Average Latency）**

