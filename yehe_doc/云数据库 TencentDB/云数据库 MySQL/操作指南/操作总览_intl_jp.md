クラウドデータベースMySQLを使用するときは、以下のようなインスタンスのアクセスと保守、データベースとテーブルの作成、データバックアップとロールバックなどの問題に遭遇することがあります。このドキュメントではクラウドデータベースMySQLインスタンスおよびクラウドデータベースMySQL関連の製品使用過程でよく使う操作をご紹介します。
## インスタンス
[インスタンス](https://intl.cloud.tencent.com/document/product/236/5147) とはクラウドデータベースMySQLのインスタンスのことです。1つのデータベースインスタンスにはユーザーが作成した複数のデータベースを含むことができ、独立したデータベースインスタンスにアクセスするのと同じツールやアプリケーションプログラムを使用してアクセスできます。以下にクラウドデータベースMySQLインスタンス、データベース、テーブルでよく使う操作を列挙します。

### よく使う操作
- [MySQLデータベースへのアクセス](https://intl.cloud.tencent.com/document/product/236/3130)

- インスタンスの保守
 - [インスタンス保守時間の設定](https://intl.cloud.tencent.com/document/product/236/10929)
 - [インスタンス指定項目](https://intl.cloud.tencent.com/document/product/236/8460)

- インスタンスの変更
 - [データベースエンジンのバージョンアップグレード](https://intl.cloud.tencent.com/document/product/236/8126)
 - [データベースインスタンス仕様の調整](https://intl.cloud.tencent.com/document/product/236/19707)

- インスタンスの拡張
 - [読み取り専用インスタンス](https://intl.cloud.tencent.com/document/product/236/7270)
 - [読み取り専用インスタンスROグループ](https://intl.cloud.tencent.com/document/product/236/11361)

- [インスタンスの終了](https://intl.cloud.tencent.com/document/product/236/31895)

### データベース管理
- [データベースおよびテーブルの作成](https://intl.cloud.tencent.com/document/product/236/8465)
- [一括操作インスタンス](https://intl.cloud.tencent.com/document/product/236/8466)
- [データベースおよびテーブルの削除](https://intl.cloud.tencent.com/document/product/236/31905)

## パラメータテンプレート
[パラメータテンプレート](https://intl.cloud.tencent.com/document/product/236/8461)データベースエンジンのパラメータ設定の管理に使用します。データベースパラメータグループはエンジン設定値の容器のようなもので、これらの値は1つまたは複数のデータベースインスタンスに応用できます。以下にクラウドデータベースインスタンスパラメータのテンプレートが現在サポートしている、よくある操作をご紹介します。
#### よくある操作
- [パラメータテンプレートの新規作成](https://intl.cloud.tencent.com/document/product/236/31906#.E6.96.B0.E5.BB.BA.E5.8F.82.E6.95.B0.E6.A8.A1.E6.9D.BF)
- [パラメータテンプレートのコピー](https://intl.cloud.tencent.com/document/product/236/31906#.E5.A4.8D.E5.88.B6.E5.8F.82.E6.95.B0.E6.A8.A1.E6.9D.BF)
- [パラメータテンプレートの修正](https://intl.cloud.tencent.com/document/product/236/31906#.E4.BF.AE.E6.94.B9.E5.8F.82.E6.95.B0)
- [パラメータのインポート](https://intl.cloud.tencent.com/document/product/236/31906#.E5.AF.BC.E5.85.A5.E5.8F.82.E6.95.B0)

## データ
データに対するクラウドデータベースMySQLでよくある操作は次のとおりです。

### バックアップとロールバック
- [物理バックアップを使用してデータベースを復旧](https://intl.cloud.tencent.com/document/product/236/31910)
- [論理バックアップを使用してデータベースを復旧](https://intl.cloud.tencent.com/document/product/236/31909)
- [データベースロールバック](https://intl.cloud.tencent.com/document/product/236/7276)

### データのインポートとエクスポート
- [データのインポート](https://intl.cloud.tencent.com/document/product/236/8463)
- [オフラインでのデータマイグレーション](https://intl.cloud.tencent.com/document/product/236/8464)

## セキュリティグループ
[クラウドデータベースセキュリティグループ](https://intl.cloud.tencent.com/document/product/236/14470)は、一種のフィルター機能を含むバーチャルファイアウォールがある状態で、1台または複数台のクラウドデータベースのネットワークアクセス制御を設定するのに使用します。Tencent Cloudが提供する重要なネットワークセキュリティの隔絶手段です。次にクラウドデータベースセキュリティグループでよくある操作をご紹介します。

