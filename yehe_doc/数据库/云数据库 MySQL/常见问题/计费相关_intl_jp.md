### 購入したインスタンスが要らない場合、どのように返金してもらえますか？
返金をご希望の場合は、インスタンス状況に応じて処理してください。
- 従量課金インスタンス：MySQLがリソースを直接クリアし、返金を申請することができません。
- サブスクリプションインスタンス
  - 5日間の理由なしセルフサービス返金：各エンティティの下で、サブスクリプション前払いのTencentDB for MySQLは新規購入日から5日（5日を含む）以内に、1つのMySQLがデフォルトで5日間理由なしにセルフサービス返金されます。
  - 通常のセルフサービス返金：5日間の理由なしセルフサービス返金を使用した後、サブスクリプションの199個のMySQLインスタンスがいつでもコンソールから返金することもサポートします。

詳細については、[返金について](https://intl.cloud.tencent.com/document/product/236/14618)をご参照ください。 

### 従量課金制がサブスクリプションインスタンスに変換されると、業務にどのような影響がありますか？課金方法は?
従量課金制からサブスクリプションへの変換中、業務アクセスにはまったく影響はありませんので、安心してご利用ください。 

課金の詳細については、[課金説明](https://intl.cloud.tencent.com/document/product/236/18335)をご参照ください。 


### 私のインスタンスはサブスクリプション課金モードですが、他の料金がかかっているのはなせですか？
バックアップスペースが無料利用枠を超えているかどうかを確認してください。無料利用枠を超えたバックアップスペースは課金されます。
バックアップキャパシティの使用情報は[MySQLコンソール](https://console.cloud.tencent.com/mysql/backup/index)のデータベースバックアップページで確認できます。バックアップキャパシティの課金の詳細については、[バックアップキャパシティ課金説明](https://intl.cloud.tencent.com/document/product/236/32344)をご参照ください。

### 従量課金インスタンスが使用されていない場合、料金はかかりますか？
従量課金インスタンスが使用されなくても、そのまま課金されます。課金されることを避けるためにはタイムリーに廃棄してください。


### バックアップスペースの料金はどのように計算されますか？
TencentDB for MySQLは一定レベルの無料バックアップキャパシティをエリアごとにプレゼントします。無料バックアップキャパシティのサイズは、お客様の対応エリアでのすべての2つのノードと3つのノードインスタンス（マスターインスタンス、ディザスタリカバリインスタンスを含む）のストレージキャパシティの和です。
単一ノードのクラウドディスクインスタンスが実際に使用する容量と、受け取った無料メモリ容量は別々に反映され、単一ノードのクラウドディスクインスタンスのバックアップ復元ページで確認できます。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/t726987_19.png)
無料限度額を超えたバックアップキャパシティの課金の詳細については、[バックアップキャパシティの課金説明](https://intl.cloud.tencent.com/document/product/236/32344)をご参照ください。

バックアップ支出を削減する必要がある場合は、[バックアップ支出削減に関するアドバイス](https://intl.cloud.tencent.com/document/product/236/32344#.E5.87.8F.E5.B0.91.E5.A4.87.E4.BB.BD.E5.BC.80.E9.94.80.E5.BB.BA.E8.AE.AE)をご参照ください。

