## 集計関数

COS Selectは次の集計関数をサポートしています。

| 関数名          | パラメータタイプ                    | リターンタイプ                                                     |
| :-------------- | :-------------------------- | :----------------------------------------------------------- |
| AVG(expression) | INT、FLOAT、DECIMAL         | 入力パラメータが整数型の場合はDECIMALを返し、入力パラメータが浮動小数点型の場合はFLOATを返し、その他の場合の戻り値は入力パラメータと一致 |
| COUNT           | -                           | INT                                                          |
| MAX(expression) | INT、DECIMAL                | 戻り値は入力パラメータと一致                                             |
| MIN(expression) | INT、DECIMAL                | 戻り値は入力パラメータと一致                                             |
| SUM(expression) | INT、FLOAT、DOUBLE、DECIMAL | 入力パラメータが整数型の場合はINTを返し、入力パラメータが浮動小数点型の場合はFLOATを返し、その他の場合の戻り値は入力パラメータと一致|

## 条件関数

COS Selectは次の条件関数をサポートしています。

### COALESCE

COALESCE関数は入力されたパラメータを順序に従って判断し、空ではない最初のパラメータ値を返します。入力パラメータに空ではないパラメータが含まれない場合は、関数がnull値を返します。

#### 構文

```sql
COALESCE ( expression, expression, ... )
```

> ?expressionパラメータはINT、String、Floatタイプの数値、配列またはネスト関数を渡すことができます。

#### 事例

```shell
COALESCE(1)                -- 1
COALESCE(1, null)          -- 1
COALESCE(null, null, 1)    -- 1
COALESCE(missing, 1)       -- 1
COALESCE(null, 'string')   -- 'string'
COALESCE(null)             -- null
COALESCE(null, null)       -- null
COALESCE(missing)          -- null
COALESCE(missing, missing) -- null
```

### NULLIF

NULLIF関数は渡された2つのパラメータ間の差異を判断し、2つの入力パラメータが同一の値であればNULLを返し、異なっていれば最初の入力パラメータの値を返します。

#### 構文

```sql
NULLIF ( expression1, expression2 )
```

> ? expressionパラメータはINT、String、Floatタイプの数値、配列またはネスト関数を渡すことができます。

#### 事例

```shell
NULLIF(1, 2)             -- 1
NULLIF(1, '1')           -- 1
NULLIF(1, NULL)          -- 1
NULLIF(1, 1)             -- null
NULLIF(1.0, 1)           -- null
NULLIF(missing, null)    -- null
NULLIF(missing, missing) -- null
NULLIF([1], [1])         -- null
NULLIF(NULL, 1)          -- null
NULLIF(null, null)       -- null
```

## 変換関数

COS Selectは次の変換関数をサポートしています。

### CAST

CAST関数はある種類のインスタンスを別の種類のインスタンスに変換することができます。このインスタンスは数値でも、計算によってある確定した数値が出せる関数でも構いません。

#### 構文

```shell
CAST ( expression AS data_type )
```

> ?
>
> - expressionパラメータは数値、配列、演算子または計算によって、ある確定した数値が出せるSQL関数とすることができます。
> - data_typeパラメータは例えばINTタイプのような、変換後のデータタイプです。現在COS Selectがサポートしているデータタイプについては、[データタイプ](https://intl.cloud.tencent.com/document/product/436/32476)をご参照ください。

#### 事例

```shell
CAST('2007-04-05T14:30Z' AS TIMESTAMP)
CAST(0.456 AS FLOAT)
```

## 日付関数

COS Selectは次の日付関数をサポートしています。

### DATE_ADD

DATE_ADD関数は指定のタイムスタンプのある部分（年、月、日、時、分、秒）に指定された時間間隔を加え、新しいタイムスタンプを返すことができます。

#### 構文

```shell
DATE_ADD( date_part, quantity, timestamp )
```

> ?
> - date_partパラメータはタイムスタンプの中の変更したい部分を指定します。年、月、日、時、分、秒とすることができます。
> - quantityパラメータは増分したい数値を表します。正の整数でなければなりません。
> - timestampパラメータは変更したいタイムスタンプです。

#### 事例

```shell
DATE_ADD(year, 5, `2010-01-01T`)                -- 2015-01-01
DATE_ADD(month, 1, `2010T`)                     -- 2010-02T 
DATE_ADD(month, 13, `2010T`)                    -- 2011-02T
DATE_ADD(hour, 1, `2017T`)                      -- 2017-01-01T01:00-00:00
DATE_ADD(hour, 1, `2017-01-02T03:04Z`)          -- 2017-01-02T04:04Z
DATE_ADD(minute, 1, `2017-01-02T03:04:05.006Z`) -- 2017-01-02T03:05:05.006Z
DATE_ADD(second, 1, `2017-01-02T03:04:05.006Z`) -- 2017-01-02T03:04:06.006Z
```

### DATE_DIFF

DATE_DIFF関数は2つの有効なタイムスタンプを比較し、2つのタイムスタンプの差を返します。この差は指定された時間単位で表示することができます。 timestamp1のdate_part値がtimestamp2より大きい場合は、戻り値は正の値となります。逆の場合は負の値を返します。

#### 構文

```shell
DATE_DIFF( date_part, timestamp1, timestamp2 )
```

> ?
> - date_partパラメータは2つのタイムスタンプを比較する時間単位を指定します。年、月、日、時、分、秒とすることができます。
> - timestamp1パラメータは最初に入力されたタイムスタンプです。
> - timestamp2パラメータは2番目に入力されたタイムスタンプです。

#### 事例

```shell
DATE_DIFF(year, `2010-01-01T`, `2011-01-01T`)            -- 1
DATE_DIFF(year, `2010T`, `2010-05T`)                     -- 4 
DATE_DIFF(month, `2010T`, `2011T`)                       -- 12
DATE_DIFF(month, `2011T`, `2010T`)                       -- -12
DATE_DIFF(day, `2010-01-01T23:00T`, `2010-01-02T01:00T`) -- 0 
```

### EXTRACT

 EXTRACT関数は、指定されたタイムスタンプから指定された時間単位の数値を抽出します。

#### 構文

```shell
EXTRACT( date_part FROM timestamp )
```

> ?
> - date_partパラメータは抽出したい時間単位を指定します。年、月、日、時、分、秒とすることができます。
> - timestampパラメータは入力されたタイムスタンプです。

#### 事例

```shell
EXTRACT(YEAR FROM `2010-01-01T`)                           -- 2010
EXTRACT(MONTH FROM `2010T`)                                -- 1 
EXTRACT(MONTH FROM `2010-10T`)                             -- 10
EXTRACT(HOUR FROM `2017-01-02T03:04:05+07:08`)             -- 3
EXTRACT(MINUTE FROM `2017-01-02T03:04:05+07:08`)           -- 4
EXTRACT(TIMEZONE_HOUR FROM `2017-01-02T03:04:05+07:08`)    -- 7
EXTRACT(TIMEZONE_MINUTE FROM `2017-01-02T03:04:05+07:08`)  -- 8
```

### TO_STRING

TO_STRING関数は、タイムスタンプを指定されたフォーマットの時間文字列に変換することができます。

#### 構文

```shell
TO_STRING ( timestamp time_format_pattern )
```

> ?
> - timestampパラメータは変換したいタイムスタンプを指定します。
> - time_format_patternパラメータは変換する時間のフォーマットを指定します。

| フォーマット             | 説明                                                         | 例                              |
| ---------------- | ------------------------------------------------------------ | --------------------------------- |
| yy             | 2桁の年                                                    | 98                              |
| y             | 4桁の年                                                    | 1998                            |
| yyyy           | 固定された4桁の年。桁数に満たない場合はゼロ埋め                                 | 0199                            |
| M              | 月                                                         | 1                              |
| MM             | 固定された2桁の月。桁数に満たない場合はゼロ埋め                                 | 01                              |
| MMM            | 月の英略称                                               | Jan                             |
| MMMM           | 月の英文正式名称                                               | January                         |
| MMMMM          | 月の最初のアルファベットの略称                                             | J（to_timestamp関数には適用しない） |
| d             | 1か月のうちのある1日（1～31）                                       | 1                              |
| dd             | 固定された2桁の日（1～31）                                      | 01                              |
| a             | 午前午後の指標（AM/PM）                                  | AM                              |
| h              | 時間。12時間制                                               | 1                             |
| hh             | 固定された2桁の時刻。12時間制                                    | 01                              |
| H              | 時間。24時間制                                               | 1                              |
| HH             | 固定された2桁の時刻。24時間制                                    | 01                             |
| m              | 分（00～59）                                               | 1                               |
| mm            | 固定された2桁の分。24時間制                                    | 01                              |
| s              | 秒（00～59）                                                  | 1                               |
| ss            | 固定された2桁の時刻。24時間制                                    | 01                              |
| S              | 秒の小数部分（精度0.1、範囲0.0～0.9）                         | 0                              |
|SS             | 秒の小数部分（精度0.01、範囲0.00～0.99）                     | 6                               |
| SSS            | 秒の小数部分（精度0.001、範囲0.000～0.999）                   | 60                              |
| ...              | ...                                                          | ...                               |
| SSSSSSSSS     | 秒の小数部分（精度0.000000001，範囲0.000000000～0.999999999） | 60000000                        |
| n             | ナノ秒                                                         | 60000000                        |
| X              | 時間単位のオフセット。オフセットが0の場合は「Z」                             | +01またはZ                      |
| XXまたはXXXX   | 時間または分単位のオフセット。オフセットが0の場合は「Z」                     | +0100またはZ                    |
| xxxまたはxxxxx | 時間または分単位のオフセット。オフセットが0の場合は「Z」                     | +01:00またはZ                   |
| x              | 時間単位のオフセット                                                 | 1                               |
| xxまたはxxxx   | 時間または分単位のオフセット                                         | 0100                            |
| xxxまたはxxxxx | 時間または分単位のオフセット                                         | 01:00                           |

#### 事例

```shell
TO_STRING(`1998-07-20T20:18Z`,  'MMMM d, y')                    -- "July 20, 1998"
TO_STRING(`1998-07-20T20:18Z`, 'MMM d, yyyy')                   -- "Jul 20, 1998"
TO_STRING(`1998-07-20T20:18Z`, 'M-d-yy')                        -- "7-20-69"
TO_STRING(`1998-07-20T20:18Z`, 'MM-d-y')                        -- "07-20-1998"
TO_STRING(`1998-07-20T20:18Z`, 'MMMM d, y h:m a')               -- "July 20, 1998 8:18 PM"
TO_STRING(`1998-07-20T20:18Z`, 'y-MM-dd''T''H:m:ssX')           -- "1998-07-20T20:18:00Z"
TO_STRING(`1998-07-20T20:18+08:00Z`, 'y-MM-dd''T''H:m:ssX')     -- "1998-07-20T20:18:00Z"
TO_STRING(`1998-07-20T20:18+08:00`, 'y-MM-dd''T''H:m:ssXXXX')   -- "1998-07-20T20:18:00+0800"
TO_STRING(`1998-07-20T20:18+08:00`, 'y-MM-dd''T''H:m:ssXXXXX')  -- "1998-07-20T20:18:00+08:00"
```

### TO_TIMESTAMP

 TO_TIMESTAMP関数は時間文字列をタイムスタンプに変換することができます。

#### 構文

```shell
TO_TIMESTAMP ( string )
```

> ?  stringパラメータは入力された時間文字列です。

#### 事例

```shell
TO_TIMESTAMP('2007T')                         -- `2007T`
TO_TIMESTAMP('2007-02-23T12:14:33.079-08:00') -- `2007-02-23T12:14:33.079-08:00`
```

### UTCNOW

 UTCNOW関数はUTCの現在時刻をタイムスタンプとして返すことができます。

#### 構文

```
UTCNOW()
```

#### 事例

```shell
UTCNOW() -- 2019-01-01T14:23:12.123Z
```

## 文字列関数

COS Selectは次の文字列関数をサポートしています。

### CHAR_LENGTH, CHARACTER_LENGTH

CHAR_LENGTHおよびCHARACTER_LENGTHはいずれも文字列内の文字数を計算することができます。この2つの関数は同一のものです。

#### 構文

```shell
CHAR_LENGTH ( string )
```

> ?  stringパラメータは文字数を計算したい文字列を指定します。

#### 事例

```shell
CHAR_LENGTH('null')      -- 4
CHAR_LENGTH('tencent')   -- 7
```

### LOWER

 LOWER関数は指定された文字列内のすべての大文字アルファベットを小文字アルファベットに変換することができます。大文字アルファベット以外はすべてそのまま維持されます。

#### 構文

```shell
LOWER ( string )
```

> ?  stringパラメータは大文字アルファベットを小文字アルファベットに変換したい文字列を指定します。

#### 事例

```shell
LOWER('TENcent') -- 'tencent'
```

### SUBSTRING

 SUBSTRING関数はある文字列の部分文字列を返すことができます。あるインデックスを指定すると、SUBSTRING関数はそのインデックスから開始し、指定された部分文字列の長さに従って元の文字列から残りの内容を切り取り、結果を返します。

>? 入力された文字列が1文字のみであり、かつインデックスの設定が1より大きい場合、SUBSTRING関数は自動的に1に切り替えます。
>

#### 構文

```shell
SUBSTRING( string FROM start [ FOR length ] )
```

> ?
> - stringパラメータは部分文字列を切り取りたい文字列を指定します。
> - startパラメータは文字列のあるインデックス値であり、切り取る位置を指定します。
> - lengthパラメータは部分文字列の長さを指定します。特に指定されない場合は、文字列の残りのすべての内容を切り取ります。

#### 事例

```shell
SUBSTRING("123456789", 0)      -- "123456789"
SUBSTRING("123456789", 1)      -- "123456789"
SUBSTRING("123456789", 2)      -- "23456789"
SUBSTRING("123456789", -4)     -- "123456789"
SUBSTRING("123456789", 0, 999) -- "123456789" 
SUBSTRING("123456789", 1, 5)   -- "12345"
```

### TRIM

 TRIM関数は指定された文字列の先頭の文字の前または末尾の文字の後の全ての文字を削除することができます。デフォルトの削除文字は「 」です。

#### 構文

```shell
TRIM ( [[LEADING | TRAILING | BOTH remove_chars] FROM] string )
```

> ?
> - stringパラメータは操作したい文字列を指定します。
> - `LEADING | TRAILING | BOTH`パラメータは文字列の前（LEADING）または文字列の後（TRAILING）またはその両方（BOTH）の削除したい余分な文字を指定します。
> -  remove_charsパラメータはどの種類の余分な文字を削除したいかを指定します。remove_charsパラメータは長さが1文字より長い文字列とすることができます。TRIM関数はstringパラメータの前後でこれにマッチする余分な文字列を発見すると、そのすべてに削除処理を行います。

#### 事例

```shell
TRIM('       foobar         ')               -- 'foobar'
TRIM('      \tfoobar\t         ')            -- '\tfoobar\t'
TRIM(LEADING FROM '       foobar         ')  -- 'foobar'
TRIM(TRAILING FROM '       foobar         ') -- 'foobar'
TRIM(BOTH FROM '       foobar         ')     -- 'foobar'
TRIM(BOTH '12' FROM '1112211foobar22211122') -- 'foobar'
```

### UPPER

 UPPER関数はすべての小文字を大文字に変換することができます。小文字以外の文字は変更されません。

#### 構文

```shell
UPPER ( string )
```

> ? stringパラメータは大文字に変換したい文字列を指定します。

#### 事例

```shell
UPPER('tenCENT') -- 'TENCENT'
```

