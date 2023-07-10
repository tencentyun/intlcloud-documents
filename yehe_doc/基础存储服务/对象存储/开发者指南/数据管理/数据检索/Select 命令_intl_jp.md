## 概要

COS Select機能はSELECT SQL照会コマンドのみをサポートし、必要なデータの一部を検索できるようにすることで、転送データ量を削減することができます。こうすることでコストが削減でき、リクエストの遅延も低減できます。SELECT照会でサポートする標準句は次のとおりです。

- SELECTステートメント
- WHERE句
- LIMIT句

> !COS Selectは現時点では句の照会またはjoinsをサポートしていません。

## SELECTステートメント

SELECTステートメントはCOSオブジェクトの中からお客様が見たいデータを検索できるようにするもので、列の名称、関数または式などの次元で照会を行い、リスト形式で照会結果が返されます。SELECTステートメントの呼び出し形式は次のとおりです。

```shell
SELECT *
SELECT projection [ AS column_alias | column_alias ] [, ...]
```

最初のSELECTステートメントには`*`（アスタリスク）が付いており、COSオブジェクトのすべての列が返されます。2番目のSELECTステートメントはユーザー定義の出力スカラー式、**projection**を各列に使用した、カスタム名の出力リストを作成します。


## WHERE句

WHERE句は次の構文を使用します。

```shell
WHERE condition
```

WHERE句は**condition**によってフィルタリングされます。**condition**はブール型の結果を返すことができる式であり、戻り値がTRUEの行のみ結果として出力されます。

## LIMIT句

LIMIT句は次の構文を使用します。

```shell
LIMIT number
```

LIMIT句は毎回の照会で返されるレコード数を制限します。**number**パラメータによってこの制限を指定することができます。

## 属性アクセス

SELECTおよびWHERE句は、次の任意の方法で照会するフィールドを選択することができます。ファイル形式がCSVかJSONかによって選択できます。

#### CSV

- **列番号**：`_N`によって、N番目の列のデータの照会を指定できます。任意のCSVファイルの場合、列番号は1から順に増加します。1列目の番号が`_1`であれば、2列目の番号は`_2`となります。SELECTおよびWHERE句では、`_N`または`alias._N`によって、照会を行いたい列をすべて正しい方法で指定できます。
- **列ヘッダー**：照会対象のCSVファイルにヘッダーが含まれる場合、SELECTおよびWHERE句ではこのヘッダーによって照会を行いたい列を指定することができます。SQLステートメントでは、SELECTおよびWHERE句で`alias.column_name`または`column_name`の方法によって指定できます。

#### JSON 

- **ドキュメント（Document）**：`alias.name`の方法によってJSONドキュメントにアクセスできます。ネスト配列には`alias.name1.name2.name3`の方法でアクセスできます。
- **リスト（List）**：インデックスによってリスト内の要素にアクセスできます。インデックス番号は0から開始し、オペレーター`[]`を使用します。例えば、`alias[1]`によってJSONリスト内の2番目の要素にアクセスできます。ネスト配列にアクセスしたい場合は、`alias.name1.name2[1].name3`のような方法によってアクセスすることもできます。

**事例** 
この事例のデータサンプルを次に示します。

```shell
{
	"name": "Leon",
	"org": "Tencent",
	"projects":
		[
		 {"project_name":"project1", "completed":true},
		 {"project_name":"project2", "completed":false}
		]
}
```

- 事例1：データサンプルにおいてnameのSQLステートメントを照会した結果：
  ```shell
  Select s.name from COSObject s
  ```
  ```shell
  {"name":"Leon"}
  ```
- 事例2：データサンプルにおいてproject_nameのSQLステートメントを照会した結果：
  ```shell
  Select s.projects[0].project_name from COSObject s
  ```
  ```shell
  {"project_name":"project1"}
  ```

## ヘッダーおよび属性名の大文字と小文字の区別

二重引用符を使用して、CSVファイルのヘッダーおよびJSONファイルの属性名が大文字と小文字を区別するかどうかを表示できます。二重引用符を追加しない場合、ヘッダー/属性名の大文字と小文字は区別されないことを表します。設定が不明確な場合、COS Selectがエラーをスローする場合があります。

- 事例1：照会したヘッダー/属性名の中に「NAME」のオブジェクトがある場合
  次のSQLの例では二重引用符を使用していないため、大文字と小文字は区別されないことを表します。テーブルの中にこのヘッダーがあるため、最終的に正しく値が返されます。
  ```shell
  SELECT s.name from COSObject s
  ```

  次のSQLの例では二重引用符を使用しているため、大文字と小文字が区別されることを表します。テーブルの中に実際にこのヘッダーが含まれないため、最終的にエラーコード400の`SQLParsingError`が返されます。
  ```shell
  SELECT s."name" from COSObject s
  ```

- 事例2：照会したヘッダー/属性名の中に"NAME"と"name"のオブジェクトがある場合
  次のSQLの例では二重引用符を使用していないため、大文字と小文字は区別されないことを表します。テーブルの中に「NAME」と「name」という2つのヘッダーがあるため、照会コマンドの設定が不明確であり、エラーAmbiguousFieldNameがスローされます。
  ```shell
  SELECT s.name from COSObject s
  ```

  次のSQLの例では二重引用符を使用しているため、大文字と小文字は区別されることを表します。テーブルの中に「NAME」ヘッダーが存在するため、照会結果が正しく返されます。
  ```shell
  SELECT s."NAME" from COSObject s
  ```

## 予約フィールドをユーザーカスタムフィールドとして使用する

COS SelectのSQL式には、関数名、データタイプ、オペレーターなどを含むいくつかの予約フィールドがあります。状況によっては、ユーザーがこれらの予約フィールドをCSVファイルの列ヘッダーまたはJSONファイルの属性名として使用する可能性がありますが、その場合、予約フィールドとの競合が発生する可能性があります。このような場合は、二重引用符を使用することで、カスタムフィールドを使用中であることを明らかにすることができます。これを行わない場合、COSは`400 parse error`を返します。

完全な予約フィールドリストをご覧になりたい場合は、[予約フィールド](https://intl.cloud.tencent.com/document/product/436/32475)をご参照ください。

- 事例：照会対象のオブジェクトのヘッダー/属性名に予約フィールド「CAST」が含まれる場合
  次のSQLの例では二重引用符を使用し、CASTがユーザーカスタムフィールドであることを明らかにしていますので、照会結果が正しく返されます。
  ```shell
  SELECT s."CAST" from COSObject s
  ```
  次のSQLの例では、二重引用符を使用せず、CASTがユーザーカスタムフィールドであることを明らかにしていませんので、COSは予約フィールドとして処理し、`400 parse error`が返されます。
  ```shell
  SELECT s.CAST from COSObject s
  ```

## スカラー式

SELECTステートメントとWHERE句では、SQLスカラー式（値を返す式）を使用することができます。現在COS Selectでは次の形式をサポートしています。

- **literal**：SQLのテキスト。
- **column_reference**：column_nameまたはalias.column_name。
- **unary_op** **expression**： SQLの単項演算子。
- **expression** **binary_op** **expression**：SQLの二項演算子。
- **func_name**：呼び出された値関数の名称。
- **expression** [ NOT ] BETWEEN **expression** AND **expression**
- **expression** LIKE **expression** [ ESCAPE **expression** ]
