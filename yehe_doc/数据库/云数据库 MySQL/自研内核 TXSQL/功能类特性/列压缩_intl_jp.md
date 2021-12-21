## 機能の説明
現在、行形式の圧縮とデータページの圧縮がありますが、これら2つの圧縮方法は、テーブル内のいくつかの大きなフィールドと他の多くの小さなフィールドを処理すると同時に、小さなフィールドの読み取りと書き込みを頻繁に行います。大きなフィールドへのアクセス頻度が低い場合、その読み取り/書き込みアクセスの際に、コンピューティングリソースに不必要な浪費が多く発生します。

列圧縮機能では、アクセス頻度の低い大きなフィールドを圧縮する一方、アクセス頻度の高い小さなフィールドは圧縮しないことが可能です。これによって、フィールドの行全体のストレージ容量を削減できるだけでなく、読み取り/書き込みアクセスの効率も向上します。

例えば、1枚の従業員表`create table employee(id int, age int, gender boolean, other varchar(1000) primary key (id))`があり、小さなフィールドである`id,age,gender`へのアクセス頻度が比較的高い一方、大きなフィールドである`other`へのアクセス頻度が比較的低い場合は、`other`列を圧縮列として作成することができます。一般的な状況下では、`other`の読み取り/書き込みの場合のみ、その列の圧縮と解凍がトリガーされ、その他の列へのアクセスでは列の圧縮と解凍はトリガーされません。これにより、行データストレージのサイズをさらに小さくできるため、アクセス頻繁が高い小さなフィールドはより速くなり、 ストレージ容量は比較的大きいがアクセス頻度が比較的低いフィールドについては、ストレージ容量をさらに削減することができます。

## サポートするバージョン
カーネルバージョン MySQL 5.7 20210330およびそれ以降

## ユースケース
テーブル内にいくつかの大きなフィールドと他の多くの小さなフィールドがあり、小さなフィールドの読み取りと書き込みは頻繁に行われ、大きなフィールドへのアクセス頻度が低い場合、大きなフィールドを圧縮列に設定することができます。

## 利用説明
### サポートするデータタイプ
1. `BLOB`（`TINYBLOB`、`MEDIUMBLOB`、`LONGBLOB`を含む）
2. `TEXT`（`TINYTEXT`、`MEDUUMTEXT`、`LONGTEXT`を含む）
3. `VARCHAR`
4. `VARBINARY`

>!このうち`LONGBLOB`と`LONGTEXT`のサポートする長さは最大$2^{32}-2$であり、公式[String Type Storage Requirements](https://dev.mysql.com/doc/refman/5.7/en/storage-requirements.html)のサポートする$2^{32}-1$より1バイト少なくなっています。

### サポートするDDL構文タイプ
公式の[テーブル作成構文](https://dev.mysql.com/doc/refman/5.7/en/create-table.html)と比較すると、その中の`column_definition`の`COLUMN_FORMAT`の定義が一部異なります。また、列圧縮はInnodbストレージエンジンタイプのテーブルのみサポートしています。
```sql
      column_definition:
        data_type [NOT NULL | NULL] [DEFAULT default_value]
          [AUTO_INCREMENT] [UNIQUE [KEY]] [[PRIMARY] KEY]
          [COMMENT 'string']
          [COLLATE collation_name]
          [COLUMN_FORMAT {FIXED|DYNAMIC|DEFAULT}|COMPRESSED=[zlib]]  # COMPRESSED圧縮列キーワード
          [STORAGE {DISK|MEMORY}]
          [reference_definition]
```

簡単なサンプルを次に示します。
```javascript
CREATE TABLE t1(
  id INT PRIMARY KEY,
  b BLOB COMPRESSED
);
```

ここでは圧縮アルゴリズムを省略し、デフォルトの`zlib`圧縮アルゴリズムを選択しています。圧縮アルゴリズムキーワードを表示させて指定することも可能ですが、現時点でサポートしているのは`zlib`圧縮アルゴリズムのみです。
```javascript
CREATE TABLE t1(
  id INT PRIMARY KEY,
  b BLOB COMPRESSED=zlib
);
```

サポートするDDL構文を次にまとめます。
**create tableに関するもの：**

| DDL                                         | 圧縮属性継承の有無 |
| ------------------------------------------- | ---------------- |
| `CREATE TABLE t2 LIKE t1;`                  | Y                |
| `CREATE TABLE t2 SELECT * FROM t1;`         | Y                |
| `CREATE TABLE t2(a BLOB) SELECT * FROM t1;` | N                |

**alter tableに関するもの：**

| DDL                                               | 説明                 |
| ------------------------------------------------- | -------------------- |
| `ALTER TABLE t1 MODIFY COLUMN a BLOB;`            | 圧縮列を非圧縮に変更 |
| `ALTER TABLE t1 MODIFY COLUMN a BLOB COMPRESSED;` | 非圧縮列を圧縮に変更 |

 
### 追加された変数の説明

| パラメータ名                                  | 動的 | タイプ    | デフォルト | パラメータ値範囲      | 説明                                                         |
| --------------------------------------- | ---- | ------- | ---- | --------------- | ------------------------------------------------------------ |
| innodb_column_compression_zlib_wrap     | Yes  | bool    | TRUE | true/false   | オンにするとデータのzlibヘッダーとzlibフッターを生成し、adler32チェックを行います    |
| innodb_column_compression_zlib_strategy | Yes  | Integer | 0    | [0,4]           | 列圧縮に使用する圧縮ポリシー。最小値は0、最大値は4で、0 - 4はそれぞれzlib中の圧縮ポリシー Z_DEFAULT_STRATEGY、Z_FILTERED、Z_HUFFMAN_ONLY、Z_RLE、Z_FIXED 一一に対応します。<br>一般的に、テキストデータにはZ_DEFAULT_STRATEGYが最適な場合が多く、画像データにはZ_RLEが最適です |
| innodb_column_compression_zlib_level    | Yes  | Integer | 6    | [0,9]           | 列圧縮に使用する圧縮レベル。最小値は0、最大値は9で、0は圧縮しないことを表します。この値が大きいほど、圧縮後のデータは小さくなりますが、圧縮時間は長くなります |
| innodb_column_compression_threshold     | Yes  | Integer | 256  | [0, 0xffffffff] | 列圧縮に使用する圧縮しきい値。最小値は1、最大値は0xffffffff、単位はバイト。長さがこの値と同じか大きい場合のみデータが圧縮され、そうでない場合はオリジナルデータが維持されて圧縮ヘッダーのみ追加されます |
| innodb_column_compression_pct           | Yes  | Integer | 100  | [1, 100]        | 列圧縮に使用する圧縮率。最小値は1、最大値は100、単位は百分率。**圧縮後のデータサイズ/圧縮前のデータサイズ**がこの値より低い場合のみデータが圧縮され、そうでない場合はオリジナルデータが維持されて圧縮ヘッダーのみ追加されます |


### 追加されたステータスの説明

| 名称                         | タイプ    | 説明                                                |
| ---------------------------- | ------- | ---------------------------------------------------------- |
| `Innodb_column_compressed`   | Integer | 列圧縮の圧縮回数。非圧縮形式と圧縮形式の2種類のステータスの圧縮を含む   |
| `Innodb_column_decompressed` | Integer | 列圧縮の解凍回数。非圧縮形式と圧縮形式の2種類のステータスの解凍を含む |

### 追加されたエラーの説明

| 名称                                                         | 範囲                       | 説明                                                  |
| ------------------------------------------------------------ | ------------------------------- | ------------------------------------------------------------ |
| `Compressed column '%-.192s' can't be used in key specification` | 圧縮する列名を指定                  | インデックスのある列に対し圧縮属性を指定することはできません                                 |
| `Unknown compression method: %s"`                            | DDLステートメントの中で指定する圧縮アルゴリズム名 | `create table`または`alter table`の際に`zlib`以外の不正な圧縮アルゴリズムを指定しています |
| `Compressed column '%-.192s' can't be used in column format specification` | 圧縮する列名を指定                  | 同一の列に、すでに`COLUMN_FORMAT`属性が指定されている場合は圧縮属性を指定できません。この`COLUMN_FORMAT`はNDBでのみ使用できます |
| `Alter table ... discard/import tablespace not support column compression` | \                 | 圧縮列のあるテーブルでは`Alter table ... discard/import tablespace`ステートメントは実行できません |

### パフォーマンス
全体のパフォーマンスはDDLとDMLに関するものに分けられます。
DDLに関しては、sysbenchを使用してテストしています。
- 列圧縮はCOPYアルゴリズムのDDLに対して比較的大きなパフォーマンス面の影響があり、圧縮後のパフォーマンスはそれ以前より7倍から8倍遅くなりました。
- inplaceへの影響については圧縮後のデータ量サイズに左右されます。圧縮した後、全体のデータサイズが低下すれば、DDLのパフォーマンスは上昇します。その逆であれば、パフォーマンスは一定程度低下します。
- instantについては、列圧縮がこのタイプのDDLに影響することは基本的にありません。

DMLに関しては、最も一般的な圧縮のケース（圧縮比1:1.8）を考えます。8列のテーブルがあり、テーブル内に1つの大きなvarcharタイプの列があり、その挿入データの長さは1～6000の間で均一かつランダムであり、挿入する文字は0 -9 、a - bの間でランダムです。その他のいくつかの列データのタイプはchar(60)またはintタイプです。このとき、非圧縮列の挿入、削除および照会に対しては10%以内の上昇がみられましたが、非圧縮列の更新には10%以内の低下がみられ、圧縮列の更新には15%以内のパフォーマンス低下がみられました。これは、更新のプロセスにおいて、MySQLは先にこの行の値を読み出した後にその行の更新後の値を書き込むため、更新プロセス全体が1回の解凍と圧縮をトリガーしますが、一方で挿入と照会は圧縮または解凍を1回しか行わないためです。

### 注意事項
1. 論理エクスポートに関しては、論理エクスポートの際にcreate tableにはCompressed関連のキーワードが付与されます。このため、インポートの際はTencentDB for MySQL内部でサポートされます。その他のMySQLブランチおよび公式バージョンは次のとおりです。
   - 公式のバージョン番号が5.7.18より小さい場合は、直接インポートできます。
   - 公式のバージョン番号が5.7.18かそれより大きい場合は、論理エクスポート後に圧縮キーワードを削除する必要があります。
2. DTSによって他のクラウドまたはユーザーにエクスポートする場合は、binlogの同期中に互換性の問題が発生する可能性があるため、圧縮キーワード付きのDDLステートメントをスキップすることができます。

