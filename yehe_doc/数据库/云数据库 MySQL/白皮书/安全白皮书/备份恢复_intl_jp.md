### バックアップ
TencentDB for MySQLは、自動バックアップと手動バックアップをサポートしてデータのリカバー可能性を確保し、それによってデータの完全性と信頼性を確保します。MySQLはデフォルトでデータバックアップとログバックアップ機能を提供しますが、その中で自動バックアップのバックアップサイクルは週に2回以上にしてください。他のバックアップのニーズがある場合は、[コンソール](https://console.cloud.tencent.com/cdb)またはAPIを使用していつでも手動バックアップを開始できます。

また、サービスニーズに応じてバックアップファイルの保存期間を柔軟に設定できます。デフォルトの保存期間は7日で、最大では1830日に設定できます。バックアップの保存期間を超えるバックアップファイルは、有効期限が切れると自動的に削除されます。

機能の使用については、[データベースのバックアップ](https://intl.cloud.tencent.com/document/product/236/32340)をご参照ください。

### リカバー
TencentDB for MySQLは、データリカバー機能を提供します。サービスニーズに応じてロールバック機能を使用してデータをリカバーできます。バックアップ保存期間の任意の時点へのデータリカバーをサポートします。リカバー可能な時点は、バックアップ保存期間によって異なるため、サービスデータのリカバー可能性を確保するために、サービスニーズに応じてバックアップ保存ポリシーを合理的に設定してください。

機能の使用については、[データベースのロールバック](https://intl.cloud.tencent.com/document/product/236/7276)をご参照ください。
