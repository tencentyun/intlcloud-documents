### 概要

**タグ**クラウド上のリソースを識別するためにTencent Cloudが提供するタグであり、キー-値ペア（Key-Value）で構成されます。詳細は[タグの概要](http://intl.cloud.tencent.com/document/product/651/13334)をご参照ください。
様々なディメンション（業務、用途、担当者など）に基づき、タグを使用してMySQLリソースを分類、管理することができます。タグによって、対応するリソースを簡単にフィルタリング、除外することができます。タグのキー値ペアはTencent Cloudに対して特に意味を持たず、文字列に従って厳密に解析、マッチングを行います。使用中は、[使用制限](http://intl.cloud.tencent.com/document/product/651/13354) のみに注意する必要があります。
タグの使用について、以下に具体的なケースをもとに説明します。

### ケースの背景
ある会社はTencent Cloudに10台のMySQLサーバーを所有しており、eコマース、ゲーム、エンターテインメントの3つの部門に分けてマーケティング活動、ゲームA、ゲームB、ポストプロダクションなどの業務を行っています。そして、3つの部門に対応するメンテナンス担当者は張三、黎四、王五です。

### タグの設定
この会社は、管理をしやすくするために、タグを使用して対応するMySQLリソースを分類、管理し、下記のタグキー/値を定義しました。

| タグキー     | タグ値                             |
| :---------- | ---------------------------------- |
| 部門       | eコマース、ゲーム、エンターテインメント                   |
| 業務       | マーケティング活動、ゲームA、ゲームB、ポストプロダクション |
| メンテナンス担当者 | 張三、黎四、王五                   |

これらのタグキー/値をMySQLにバインドします。下表にリソースとタグキー/値の関係を示します。

|instance-id	|部門	|業務	|メンテナンス担当者|
|----------------|-------|----|--------------|
|cdb-abcdef1	|eコマース	|マーケティング活動	|王五|
|cdb-abcdef2	|eコマース	|マーケティング活動|	王五|
|cdb-abcdef3	|ゲーム|	ゲームA	|張三|
|cdb-abcdef3	|ゲーム|	ゲームB	|張三|
|cdb-abcdef4|	ゲーム	|ゲームB	|張三|
|cdb-abcdef5|	ゲーム	|ゲームB	|黎四|
|cdb-abcdef6	|ゲーム	|ゲームB|	黎四|
|cdb-abcdef7	|ゲーム	|ゲームB	|黎四|
|cdb-abcdef8	|エンターテインメント	|ポストプロダクション|	王五|
|cdb-abcdef9	|エンターテインメント	|ポストプロダクション	|王五|
|cdb-abcdef10|	エンターテインメント	|ポストプロダクション|	王五|

### タグの使用
タグの作成及び削除方法は、[操作ガイド](https://intl.cloud.tencent.com/document/product/651/41684)をご参照ください。

MySQLタグの編集方法は、[タグの編集](https://intl.cloud.tencent.com/document/product/236/31918)をご参照ください。

