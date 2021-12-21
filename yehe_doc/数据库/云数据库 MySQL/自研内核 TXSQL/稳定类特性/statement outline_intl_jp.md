## 機能の説明
SQLチューニングはデータベースのパフォーマンス最適化において非常に重要なプロセスの一つです。オプティマイザが適切な実行計画を選択できないことによる影響を防ぐため、TXSQLはOUTLINE機能を提供し、ユーザーが実行計画をバインドできるようにしました。MySQLデータベースにはHINTによって実行計画を人為的にバインドできる機能があります。HINT情報には、SQLがどの最適化ルールを採用しているか、どのアルゴリズムを実行しているか、データスキャンにどのインデックスを採用しているかなどが含まれます。OUTLINEは主にHINTによって照会計画を指定するもので、弊社はシステムテーブルmysql.outlineを提供し、ユーザーが計画バインドルールを追加できるようにしています。この機能をオンにするかどうかはスイッチ（cdb_opt_outline_enabled）で制御します。

## サポートするバージョン
カーネルバージョン MySQL 8.0 20201230およびそれ以降

## ユースケース
オンライン実行計画のインデックス選択ミスなど、オンラインでの実行計画に誤りがあったが、業務上、SQLを変更して新バージョンをリリースする解決方法を取りたくないケース。

## パフォーマンスへの影響
- cdb_opt_outline_enabledスイッチがオンになっている状態で、outlineにヒットしないSQLの実行効率は影響を受けません。
- outlineにヒットしたSQLの実行効率は正常な実行よりは低下しますが、一般的にoutlineバインドによる上昇は、それまでの計画パフォーマンスに比べて数倍の上昇となります。
- このスイッチを使用する場合は、問い合わせと運用保守またはカーネルの担当者を置き、発生する可能性のあるバインドエラーによるパフォーマンスの後退を防止する必要があります。

## 利用説明
OUTLINE構文の設定に用いる新しい構文形式：
- OUTLINE情報を設定する：`outline "sql" set outline_info "outline";`
- OUTLINE情報を空にする：`outline reset ""; outline reset all;`
- OUTLINE情報をフラッシュする：`outline flush;`

次にOUTLINEの主な使用方法を紹介します。以下のschemaを例に説明します。
```
create table t1(a int, b int, c int, primary key(a));
create table t2(a int, b int, c int, unique key idx2(a));
create table t3(a int, b int, c int, unique key idx3(a));
```

| パラメータ名                  | 動的 | タイプ | デフォルト  | パラメータ値範囲 | 説明                |
| ----------------------- | ---- | ---- | ----- | ---------- | ------------------- |
| cdb_opt_outline_enabled | yes  | bool | fasle | true/false | outline機能をオンにするかどうか |

### OUTLINEのバインド
OUTLINEの直接バインド方式とは、1文のSQLを、SQLの意味は変えずに別の1文に置き換えるもので、いくつかのHINT情報を追加して、どう実行するかをオプティマイザに通知するだけのものです。
構文形式は`outline "sql" set outline_info "outline";`です。outline_infoの後の文字列は必ず"OUTLINE:"で開始し、"OUTLINE:"の後にHINTの後のSQLを追加することに注意してください。例えば、`select *from t1, t2 where t1.a = t2.a`というSQLのt2テーブルにa列のインデックスを加えます。
```
outline "select* from t1, t2 where t1.a = t2.a" set outline_info "OUTLINE:select * from t1, t2 use index(idx2) where t1.a = t2.a";
```

### optimizer hintのバインド
機能をさらに柔軟にするため、TXSQLでは、SQL中にoptimizer hintを増分追加することが許容されています。同様の機能はoutlineの直接バインドによっても実現できます。
構文形式は`outline "sql" set outline_info "outline";`です。outline_infoの後の文字列は必ず"OPT:"で開始し、"OPT:"の後を追加したいoptimizer hint情報とすることに注意してください。例えば、s`elect *from t1 where t1.a in (select b from t2)`というSQLにMATERIALIZATION/DUPSWEEDOUTのSEMIJOINを指定します。
```
outline "select* from t1 where t1.a in (select b from t2)" set outline_info "OPT:2#qb_name(qb2)";
outline "select * from t1 where t1.a in (select b from t2)" set outline_info "OPT:1#SEMIJOIN(@qb2 MATERIALIZATION, DUPSWEEDOUT)";
```

オリジナルのSQLステートメントにOPTIMIZERのHINTを追加する場合は、1回につき1個のHINTの追加のみサポートしています。構文については3つの点に注意する必要があります。
- OPTキーワードは必ず"のすぐ後に入力します。
- バインドしたい新しいステートメントの前には必ず':'を入力します。
- 2つのフィールドを追加したい場合は（query blockの番号#optimizer hintの文字列）、間を必ず#で区切ります（`ie. "OPT:1#max_execution_time(1000)"`）。

### index hintのバインド
機能をさらに柔軟にするため、TXSQLでは、SQL中にindex hintを増分追加することが許容されています。同様の機能はoutlineの直接バインドによっても実現できます。
構文形式は`outline "sql" set outline_info "outline";`です。outline_infoの後の文字列は必ず"INDEX:"で開始し、"INDEX:"の後を追加したいindex hint情報とすることに注意してください。
次に例を挙げます。`select *from t1 where t1.a in (select t1.a from t1 where t1.b in (select t1.a from t1 left join t2 on t1.a = t2.a))` というSQLのquery block 3上のデータベースtest下のt1テーブルにUSE INDEXのインデックスidx1を追加します。タイプはFOR JOINです。
```
outline "select* from t1 where t1.a in (select t1.a from t1 where t1.b in (select t1.a from t1 left join t2 on t1.a = t2.a))" set outline_info "INDEX:3#test#t1#idx1#1#0";
```

オリジナルのSQLステートメントにINDEXのHINTを追加する場合は、1回につき1個のHINTの追加のみサポートしています。構文については4つの点に注意してください。
- INDEXキーワードは必ず"のすぐ後に入力します。
- バインドしたい新しいステートメントの前には必ず':'を入力します。
- 5つのフィールド（query blockの番号 #db_name#table_name#index_name#index_type#clause）を追加する必要があります。
- その中のindex_typeにはさらに3つの値があり（0はINDEX_HINT_IGNORE、1はINDEX_HINT_USE、2はINDEX_HINT_FORCE）、clauseには3つの値があり（1はFOR JOIN、2はFOR ORDER BY、3はFOR GROUP BY）、間は必ず#で区切ります（`ie. "INDEX:2#test#t2#idx2#1#0"`は2番目のquery block中のtest.t2テーブル中に、タイプがUSE INDEX FOR JOINであるidx1インデックスをバインドすることを表す）。

### あるSQLに対応するOUTLINE情報を削除
TXSQLでは、ユーザーがあるSQLステートメントのOUTLINEバインド情報を削除することが許容されています。
構文は`outline reset "sql";`であり、`select *from t1, t2 where t1.a = t2.a`のoutline情報を削除する場合は、`outline reset "select* from t1, t2 where t1.a = t2.a";`となります。

### すべてのOUTLINE情報を空にする
TXSQLでは、ユーザーがカーネル内のすべてのOUTLINEバインド情報を削除することが許容されています。構文は`outline reset all`、実行ステートメントは`outline reset all;`です。

オンライン業務中には、時にいくつかの非常に特殊な問題が発生し、強制的にインデックスをバインドする必要が生じることがあります。その場合は直接OUTLINEを設定してバインドすることができます。
OUTLINEの設定後に起こる可能性のあるパフォーマンスの後退を分析し、許容可能なパフォーマンス後退の範囲でバインドを行う必要があります。 必要に応じ、カーネル担当者と相談してください。

## 関連パラメータステータス説明
TXSQLはユーザーのSQLのOUTLINEバインドを確認するための様々な方法を提供しています。まず、mysql.outlineテーブルを通じてユーザーのOUTLINE設定状況を確認できます。次に、show cdb_outline_info、select * from information_schema.cdb_outline_infoという2つのインターフェースによって、メモリ内のOUTLINE情報を確認できます。入力したSQLが変更可能かどうかは、メモリ内にOUTLINE情報があるかどうかによって決まるため、ユーザーはこの2つのインターフェースを使用してデバッグを行うことができます。

mysql.outlineシステムテーブルが追加され、ユーザーが設定したOUTLINE情報のレコードはこのテーブルに保存されます。このテーブルのフィールドは次のとおりです。

| フィールド名       | 説明                                   |
| ------------ | -------------------------------------- |
| Id                | OUTLINE設定情報番号                    |
| Digest         | オリジナルSQLステートメントのハッシュ値                    |
| Digest_text  | オリジナルSQLステートメントの指紋情報テキスト              |
| Outline_text | OUTLINEバインド後のSQLステートメントの指紋情報テキスト |

show cdb_outline_infoまたはselect * from information_schema.cdb_outline_infoでもメモリ内のレコードを確認でき、SQLを実行するとその中のOUTLINEレコードバインド計画にヒットする場合があります。パラメータは次のとおりです。

| フィールド名  | 説明                         |
| ------- | ---------------------------- |
| origin  | オリジナルSQLステートメントの指紋              |
| outline | OUTLINEバインド後のSQLステートメントの指紋 |

