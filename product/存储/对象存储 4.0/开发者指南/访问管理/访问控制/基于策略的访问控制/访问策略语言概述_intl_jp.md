## 概要
アクセスポリシーは、COSリソースへのアクセス権限を付与するために使用されます。アクセスポリシーはJSONに基づくアクセスポリシー言語を使用します。アクセスポリシー言語により、指定委託者（principal）が指定のCOSリソースに対して指定の操作を行うように認証することができます。

アクセスポリシー言語はバケットポリシー（Bucket Policy）の基本的要素と使い方を説明しています。ポリシー言語の説明については、[CAMポリシーの管理](https://intl.cloud.tencent.com/document/product/598/10600)を参照してください。

## アクセスポリシーにおける要素

アクセスポリシー言語は下記の基本的要素を含みます：
- 委託者（principal）：ポリシーで認証されるエンティティを説明します。例えば、ユーザー（開発者、サブアカウント、匿名ユーザー）やユーザーグループなど。この要素はバケットのアクセスポリシーには有効だが、ユーザーのアクセスポリシーに追加してはなりません。
- ステートメント（statement）：1つまたは複数の権限の詳しい情報を説明します。この要素は効力、操作、リソース、条件などの複数のその他の要素の権限または権限集合を含みます。1つのポリシーには1つのステートメント要素のみがあります。
  - 効力（effect）：ステートメントにより生じる結果が「許可」か「明示的拒否」かを示します。それはallowとdenyの2つの可能性を含みます。この要素は記入必須項目です。
  - 操作（action）：許可または拒否される操作を説明します。操作はAPI（nameプレフィックスで説明）あるいは機能集合（一連の特定のAPI、permidプレフィックスで説明）である可能性があります。この要素は記入必須項目です。
  - リソース（resource）：認証の詳細なデータを説明します。リソースは6段階式の説明を採用しています。それぞれの商品のリソース定義は詳細が異なります。リソース情報の指定に関して、作成されたソース宣言に関連する製品ドキュメントを参照してください。この要素は記入必須項目です。
  - 条件（condition）：ポリシー有効化の制約条件を説明します。条件は、演算子、操作キーおよび操作値を含みます。条件値は、時間、IPアドレスなどの情報を含むことができます。一部のサービスでは、条件に他の値を指定することができます。この要素は非必須です。

## 要素の使い方
### 委託者の指定
委託者principal要素はリソースへのアクセスを許可または拒否されるユーザー、アカウント、サービスまたはその他のエンティティの指定に使用されます。要素principalはバケットのみにおいて有効です。ユーザーポリシーが特定ユーザーに直接付けられているため、ユーザーポリシーにおいてそれを指定する必要がありません。下記は、principal指定の例です。
```json
"principal": {
  "qcs": [
    "qcs::cam::uin/1:uin/1"
  ]
}
```
匿名ユーザーへの認証：
```json
"principal": {
  "qcs": [
    "qcs::cam::anonymous:anonymous"
  ]
}
```
ルートアカウントUIN 1200000313への認証：
```json
"principal": {
  "qcs": [
    "qcs::cam::uin/1200000313:uin/1200000313"
  ]
}
```
サブアカウントUIN 3030313（ルートアカウントUINは1200000313）への認証：
>**注意：**
>操作する前、サブアカウントがルートアカウントのサブアカウントリストに追加されていることを確認する必要があります。

```json
"principal": {
  "qcs": [
    "qcs::cam::uin/1200000313:uin/3030313"
  ]
}
```

### 効力の指定
明示的にリソースへのアクセス権限を付与（許可）していなければ、暗示的にアクセスを拒否します。また、明示的にリソースへのアクセス権限を付与（deny）することもできます。これでその他のポリシーがアクセス権限を付与した場合にも、ユーザーがこのリソースにアクセスできないように確保できます。以下は許可効力指定の例です。
```json
"effect" : "allow"
```

### 操作の指定
COSはポリシーにおいて指定された特定COS操作を定義しています。指定の操作と出されるAPIリクエスト操作は完全に一致です。
#### バケットの操作
| 説明                    | 対応するAPI               |
| --------------------- | ------------------------ |
| name/cos:GetService   | GET Service              |
| name/cos:GetBucket    | GET Bucket (List Object) |
| name/cos:PutBucket    | PUT Bucket               |
| name/cos:DeleteBucket | DELETE Bucket            |

#### オブジェクトの操作
| 説明                    | 対応するAPI    |
| --------------------- | ------------- |
| name/cos:GetObject    | GET Object    |
| name/cos:PutObject    | PUT Object    |
| name/cos:HeadObject   | HEAD Object   |
| name/cos:DeleteObject | DELETE Object |

下記は許可操作指定の例です：
```json
"action": [
  "name/cos:GetObject",
  "name/cos:HeadObject"
]
```

### リソースの指定
リソース（resource）要素は1つまたは複数の操作オブジェクトを説明しています。例えば、COSバケットまたはオブジェクトなど。すべてのリソースは下記の六段階式の説明方式を採用します。
```json
qcs:project_id:service_type:region:account:resource
```

そのうち：
1. qcsはqcloud serviceの略称で、Tencent Cloudのクラウドサービスを意味します。
2. project_idはプロジェクト情報を説明します。その目的はCAMの早期ロジックとの互換性にのみあります。ここでは記入しないでください。
3. service_typeは製品略称を説明します。例えば、COS。
4. regionは地域情報を説明します。Tencent Cloud COSの対応する[可能な地域](https://cloud.tencent.com/document/product/436/6224)を参照してください。
5. accountはリソース保有者のルートアカウント情報を説明します。現時点では、2つの方式によるリソース保有者の説明に対応します。1つの方式はuin方式で、すなわちルートアカウントのqq番号で、そのフォーマットはuin/${uin}です。例：uin/164256472。もう1つの方式はuid方式で、すなわちルートアカウントのappidで、そのフォーマットはuid/${appid}です。例：uid/1000382392。現時点では、COSのリソース保有者に対して、uid方式による表示に統一しており、即ちルートアカウントの開発者appidを採用します。
6. resourceはリソースの詳細を説明します。COSサービスにおいてバケットXML APIアクセスドメイン名により説明します。

下記はバケットburningtest-1251500699指定の例です。
```json
"resource": ["qcs::cos:ap-guangzhou:uid/1251500699:burningtest-1251500699/*"]
```

下記はバケットburningtest-1251500699における/test/フォルダのすべてのオブジェクトを指定する例です。
```json
"resource": ["qcs::cos:ap-guangzhou:uid/1251500699:burningtest-1251500699/test/*"]
```

下記はバケットburningtest-1251500699における/test/1.txtオブジェクトを指定する例です。
```json
"resource": ["qcs::cos:ap-guangzhou:uid/1251500699:burningtest-1251500699/test/1.txt"]
```

### 条件の指定
アクセスポリシー言語により、認証時に条件を指定することができます。例えば、ユーザーのアクセス元や認証時間などの制限を指定できます。以下は現時点で対応する条件演算子リストおよび通用の条件キーと例などの情報を示しています。

| 条件演算子                   | 意味     | 条件名              | 例                                       |
| ----------------------- | ------ | ---------------- | ---------------------------------------- |
| ip_equal                | IP＝  | qcs:ip           | {"ip_equal":{"qcs:ip ":"10.121.2.0/24"}} |
| ip_not_equal            | IP≠ | qcs:ip           | {"ip_not_equal":{"qcs:ip ":["10.121.1.0/24", "10.121.2.0/24"]}} |
| date_not_equal          | 時間≠  | qcs:current_time | {"date_not_equal":{"qcs:current_time":"2016-06-01T00:01:00Z"}} |
| date_greater_than       | 時間＞   | qcs:current_time | {" date_greater_than ":{"qcs:current_time":"2016-06-01T00:01:00Z"}} |
| date_greater_than_equal | 時間≥ | qcs:current_time | {" date_greater_than_equal ":{"qcs:current_time":"2016-06-01T00:01:00Z"}} |
| date_less_than          | 時間＜   | qcs:current_time | {" date_less_than ":{"qcs:current_time":"2016-06-01T 00:01:00Z"}} |
| date_less_than_equal    | 時間≤ | qcs:current_time | {" date_less_than ":{"qcs:current_time":"2016-06-01T 00:01:00Z"}} |
| date_less_than_equal    | 時間≤ | qcs:current_time | {"date_less_than_equal ":{"qcs:current_time":"2016-06-01T00:01:00Z"}} |

下記はアクセス元IPが10.121.2.0/24というIPアドレス範囲内にある場合の例です。

```json
"ip_equal":{"qcs:ip ":"10.121.2.0/24"}
```

下記はアクセス元IPが101.226.\*\*\*.185と101.226.\*\*\*.186である場合の例です。

```json
"ip_equal": {
  "qcs:ip": [
    "101.226.***.185",
    "101.226.***.186"
  ]
}
```

## 実際のケース

アクセス元IPが101.226.\*\*\*.185/101.226.\*\*\*.186である場合、華南地区のバケットburningtest-1251500699におけるオブジェクトにGET（ダウンロード）とHEAD操作を行うことを、ルートアカウントが匿名ユーザーに対して許可すれば、認証はいりません。詳細については、[権限設定関連ケース](https://cloud.tencent.com/document/product/436/12514)を参照してください。

```json
{
   "version": "2.0",
   "principal": {
      "qcs": [
         "qcs::cam::anonymous:anonymous"
      ]
   },
    "statement": [
        {
            "action": [
                "name/cos:GetObject",
                "name/cos:HeadObject"
            ],
            "condition": {
                "ip_equal": {
                    "qcs:ip": [
                        "101.226.***.185",
                        "101.226.***.186"
                    ]
                }
            },
            "effect": "allow",
            "resource": [
                "qcs::cos:cn-south:uid/1251500699:burningtest-1251500699.cn-south.myqcloud.com/*"
            ]
        }
    ]
}
```
