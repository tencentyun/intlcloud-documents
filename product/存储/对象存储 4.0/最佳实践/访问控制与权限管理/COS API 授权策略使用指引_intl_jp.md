## 概要
COSが一時暗号鍵サービスを使用する時、異なるCOS API操作には異なる操作権限が必要であり、かつ１つの操作または一連の操作を同時に指定できます。

COS API権限付与ポリシー（policy）はjson文字列です。例えば、APPIDが1253653367で、地域が`ap-beijing`で、バケットが`example-1253653367`で、パスプレフィックスが`test`のアップロード操作権限、パスプレフィックスが`test2`のダウンロード操作権限を付与するポリシー内容は以下のとおりです：

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:PutObject",
        "name/cos:InitiateMultipartUpload",
        "name/cos:ListParts",
        "name/cos:UploadPart",
        "name/cos:CompleteMultipartUpload",
        "name/cos:AbortMultipartUpload"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/*"
      ]
    },
    {
      "action": [
        "name/cos:GetObject"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test2/*"
      ]
    }
  ]
}
```

<a id="policy"></a>
#### 権限付与ポリシー（policy）の要素の説明

| 名称     | 説明                                                       |
| -------- | ------------------------------------------------------------ |
| version  | ポリシーの構文バージョンは、デフォルトでは2.0です                                     |
| effect   | allow （許可）とdeny（明示的な拒否）の両方があります                |
| resource | 権限付与操作の具体的なデータは、任意のリソース、パスプレフィックスが指定されたリソース、絶対パスが指定されたリソース、またはそれらの組み合わせであってもよいです |
| action   | ここで、COS APIが必要に応じて1つまたは一連の操作の組み合わせまたはすべての操作（*）を指定することを指します      |
|condition|制約条件は記入されなくてもよく、具体的な説明については、[condition](https://intl.cloud.tencent.com/document/product/598/10603#6..E7.94.9F.E6.95.88.E6.9D.A1.E4.BB.B6(condition)) の説明を参照してください  |

以下、COS APIに基づいて権限付与ポリシーを詳細に説明します。

## Service API

### バケットリストの取得

バケットリストの取得：Get Serviceについて、その操作権限を付与すれば、ポリシーの`action`は` name / cos：GetService`であり、`resource`は`*`です。

#### 例

バケットリストの取得の操作権限を付与するポリシーの詳細は以下のとおりです：

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:GetService"
      ],
      "effect": "allow",
      "resource": [
        "*"
      ]
    }
  ]
}
```

## Bucket API

Bucket APIポリシーの`resource`は以下のいくつかの状況にまとめることができます：

- 任意の地域のバケットを操作でき、ポリシーの`resource`は`*`です。
- 地域が指定されたバケットのみを操作でき、例えば、APPIDが1253653367で、地域が`ap-beijing`のバケットのみを操作でき、ポリシーの`resource`は`qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/*`です。
- 地域が指定され、かつ名称が指定されたバケットのみを操作でき、例えば、APPIDが1253653367で、地域が`ap-beijing`で、かつ名称が`example-1253653367`のバケットのみを操作でき、ポリシーの`resource`は`qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/`です。



Bucket APIポリシーの`action`は操作によって値が異なり、すべてのBucket API権限付与ポリシーを以下に列挙します。

### バケットの作成

バケットの作成：Put Bucketについて、その操作権限を付与すれば、ポリシーの`action`は`name/cos:PutBucket`です。

#### 例

APPIDが1253653367で、地域が`ap-beijing`で名称が任意のバケットを作成できる操作権限を付与し、そのポリシーの詳細は以下のとおりです：

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:PutBucket"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/*"
      ]
    }
  ]
}
```

### バケットの検索  

バケットの検索：Head Bucketについて、その操作権限を付与すれば、ポリシーの`action`は`name/cos:HeadBucket`です。

#### 例

APPIDが1253653367で、地域が`ap-beijing`で、バケットが`example-1253653367`のバケットのみを検索できる操作権限を付与し、そのポリシーの詳細は以下のとおりです：

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:HeadBucket"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/"
      ]
    }
  ]
}
```

### バケット地域情報の照合

バケット地域情報の照合：Get Bucket Locationについて、その操作権限を付与すれば、ポリシーの`name/cos:GetBucketLocation`です。

#### 例

APPIDが1253653367で、地域が`ap-beijing`で、バケットが`example-1253653367`のバケット地域情報のみを照合できる操作権限を付与し、そのポリシーの詳細は以下のとおりです：

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:GetBucketLocation"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/"
      ]
    }
  ]
}
```

### バケットのオブジェクトリストの取得

バケットのオブジェクトリストの取得：Get Bucketについて、その操作権限を付与すれば、ポリシーの`action`は`name/cos:GetBucket`です。

#### 例

APPIDが1253653367で、地域が`ap-beijing`で、バケットが`example-1253653367`のオブジェクトリストのみを取得できる操作権限を付与し、そのポリシーの詳細は以下のとおりです：

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:GetBucket"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/*"
      ]
    }
  ]
}
```

### バケットの削除

バケットの削除：Delete Bucketについて、その操作権限を付与すれば、ポリシーの`action`は`name/cos:DeleteBucket`です。

#### 例

APPIDが1253653367で、地域が`ap-beijing`で、バケットが`example-1253653367`のバケットのみを削除できる操作権限を付与し、そのポリシーの詳細は以下のとおりです：

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:DeleteBucket"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/"
      ]
    }
  ]
}
```

### バケットACLの設定

バケットACLの設定：Put Bucket ACLについて、その操作権限を付与すれば、ポリシーの`action`は`name/cos:PutBucketACL`です。

#### 例

APPIDが1253653367で、地域が`ap-beijing`で、バケットが`example-1253653367`のACLのみを設定できる操作権限を付与し、そのポリシーの詳細は以下のとおりです：

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:PutBucketACL"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/"
      ]
    }
  ]
}
```

### バケットACLの取得

バケットACLの取得：Get Bucket ACLについて、その操作権限を付与すれば、ポリシーの`action`は`name/cos:GetBucketACL`です。

#### 例

APPIDが1253653367で、地域が`ap-beijing`で、バケットが`example-1253653367`のACLのみを取得できる操作権限を付与し、そのポリシーの詳細は以下のとおりです：

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:GetBucketACL"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/"
      ]
    }
  ]
}
```

### バケットクロスオリジン構成の設定

バケットクロスオリジン構成の設定：Put Bucket CORSについて、その操作権限を付与すれば、ポリシーの`action`は`name/cos:PutBucketCORS`です。

#### 例

APPIDが1253653367で、地域が`ap-beijing`で、バケットが`example-1253653367`のクロスオリジン構成のみを設定できる操作権限を付与し、そのポリシーの詳細は以下のとおりです：

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:PutBucketCORS"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/"
      ]
    }
  ]
}
```

### バケットクロスオリジン構成の取得

バケットクロスオリジン構成の取得：Get Bucket CORSについて、その権限を付与すれば、ポリシーの`action`は`name/cos:GetBucketCORS`です。

#### 例

APPIDが1253653367で、地域が`ap-beijing`で、バケットが`example-1253653367`のクロスオリジン構成のみを取得できる操作権限を付与し、そのポリシーの詳細は以下のとおりです：

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:GetBucketCORS"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/"
      ]
    }
  ]
}
```

### バケットクロスオリジン構成の削除

バケットクロスオリジン構成の削除：Delete Bucket CORSについて、その操作権限を付与すれば、ポリシーの`action`は`name/cos:DeleteBucketCORS`です。

#### 例

APPIDが1253653367で、地域が`ap-beijing`で、バケットが`example-1253653367`のクロスオリジン構成のみを削除できる操作権限を付与し、そのポリシーの詳細は以下のとおりです：

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:DeleteBucketCORS"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/"
      ]
    }
  ]
}
```

### バケットライフサイクルの設定

バケットライフサイクルの設定：Put Bucket Lifecycleについて、その操作権限を付与すれば、ポリシーの`action`は`name/cos:PutBucketLifecycle`です。

#### 例

APPIDが1253653367で、地域が`ap-beijing`で、バケットが`example-1253653367`のライフサイクル構成のみを設定できる操作権限を付与し、そのポリシーの詳細は以下のとおりです：

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:PutBucketLifecycle"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/"
      ]
    }
  ]
}
```

### バケットライフサイクルの取得

バケットライフサイクルの取得：Get Bucket Lifecycleについて、その操作権限を付与すれば、ポリシーの`action`は`name/cos:GetBucketLifecycle`です。

#### 例

APPIDが1253653367で、地域が`ap-beijing`で、バケットが`example-1253653367`のライフサイクル構成のみを取得できる操作権限を付与し、そのポリシーの詳細は以下のとおりです：

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:GetBucketLifecycle"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/"
      ]
    }
  ]
}
```

### バケットライフサイクルの削除

バケットライフサイクルの削除：Delete Bucket Lifecycleについて、その操作権限を付与すれば、ポリシー　の`action`は`name/cos:DeleteBucketLifecycle`です。

#### 例

APPIDが1253653367で、地域が`ap-beijing`で、バケットが`example-1253653367`のライフサイクル構成のみを削除できる操作権限を付与し、そのポリシーの詳細は以下のとおりです：

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:DeleteBucketLifecycle"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/"
      ]
    }
  ]
}
```

### バケット内のマルチパートアップロード中の情報の取得

バケット内のマルチパートアップロード中の情報の取得：List Multipart Uploadsについて、その操作権限を付与すれば、ポリシーの`action`は`name/cos:ListMultipartUploads`です。

#### 例

APPIDが1253653367で、地域が`ap-beijing`で、バケットが`example-1253653367`のマルチパートアップロード中の情報のみを取得できる操作権限を付与し、そのポリシーの詳細は以下のとおりです：

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:ListMultipartUploads"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/"
      ]
    }
  ]
}
```



## Object API

Object APIポリシーの`resource`は以下のいくつかの状況にまとめることができます：<br>

- 任意のオブジェクトを操作でき、ポリシーの`resource`は`*`です。
- 指定されたバケット内の任意のオブジェクトのみを操作でき、例えば、APPIDが1253653367で、地域が`ap-beijing`で、かつ名称が`example-1253653367`のバケット内の任意のオブジェクトのみを操作でき、ポリシーの`resource`は`qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/*`です。
- バケットが指定され、かつパスプレフィックスが指定された任意のオブジェクトのみを操作でき、例えば、APPIDが1253653367で、地域が`ap-beijing`で、バケットが`example-1253653367`で、パスプレフィックスが`test`の任意のオブジェクトのみを操作でき、ポリシーの`resource`は`qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/*`です。
- 絶対パスが指定されたオブジェクトのみを操作でき、例えば、APPIDが1253653367で、地域が`ap-beijing`で、バケットが`example-1253653367`で、絶対パスが`test/audio.mp3`のオブジェクトのみを操作でき、ポリシーの`resource`は`qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/audio.mp3`です。



Object APIポリシーの`action`は操作によって値が異なり、すべてのObject API権限付与ポリシーを以下に列挙します。

### 簡単なアップロード

簡単なアップロード：Put Objectについて、その操作権限を付与すれば、ポリシーの`action`は`name/cos:PutObject`です。

#### 例

APPIDが1253653367で、地域が`ap-beijing`で、バケットが`example-1253653367`で、パスプレフィックスが`test`の条件のみで簡単なアップロードを行うことができる操作権限を付与し、そのポリシーの詳細は以下のとおりです：

```shell
 {
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:PutObject"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/*"
      ]
    }
  ]
}
```

### マルチパートアップロード

マルチパートアップロードは、Initiate Multipar tUpload、List Parts、Upload Part、Complete Multipart Upload、Abort Multipart Uploadを含みます。その操作権限を付与すれば、ポリシーの`action`は`"name/cos:InitiateMultipartUpload","name/cos:ListParts","name/cos:UploadPart","name/cos:CompleteMultipartUpload","name/cos:AbortMultipartUpload"`の集合です。

#### 例

APPIDが1253653367で、地域が`ap-beijing`で、バケットが`example-1253653367`で、パスプレフィックスが`test`の条件のみでマルチパートアップロードを行うことができる操作権限を付与し、そのポリシーの詳細は以下のとおりです：

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:InitiateMultipartUpload",
        "name/cos:ListParts",
        "name/cos:UploadPart",
        "name/cos:CompleteMultipartUpload",
        "name/cos:AbortMultipartUpload"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/*"
      ]
    }
  ]
}
```

### Postアップロード

Postアップロード：Post Objectについて、その操作権限を付与すれば、ポリシーの`action`は`name/cos:PostObject`です。

#### 例

APPIDが1253653367で、地域が`ap-beijing`で、バケットが`example-1253653367`で、パスプレフィックスが`test`の条件のみでPostアップロードを行うことができる操作権限を付与し、そのポリシーの詳細は以下のとおりです：

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:PostObject"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/*"
      ]
    }
  ]
}
```

### オブジェクトの検索

オブジェクトの検索：Head Objectについて、その操作権限を付与すれば、ポリシーの`action`は`name/cos:HeadObject`です。

#### 例

APPIDが1253653367で、地域が`ap-beijing`で、バケットが`example-1253653367`で、パスプレフィックスが`test`のオブジェクトのみを検索できる操作権限を付与し、そのポリシーの詳細は以下のとおりです：

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:HeadObject"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/*"
      ]
    }
  ]
}
```

### オブジェクトリストのダウンロード

オブジェクトのダウンロード：Get Objectについて、その操作権限を付与すれば、ポリシーの`action`は`name/cos:GetObject`です。

#### 例

APPIDが1253653367で、地域が`ap-beijing`で、バケットが`example-1253653367`で、パスプレフィックスが`test`のオブジェクトのみをダウンロードできる操作権限を付与し、そのポリシーの詳細は以下のとおりです：

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:GetObject"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/*"
      ]
    }
  ]
}
```

### 簡単なコピー

簡単なコピー：Put Object Copyについて、その操作権限を付与すれば、ポリシーのターゲットオブジェクトの`action`は`name/cos:PutObject`であり、ソースオブジェクトの`action`は`name/cos:GetObject`です。

#### 例

APPIDが1253653367で、地域が`ap-beijing`で、バケットが`example-1253653367`のパスプレフィックス`test`とパスプレフィックス`test2`との間で簡単なコピーを行う操作権限を付与し、そのポリシーの詳細は以下のとおりです：

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:PutObject"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/*"
      ]
    },
    {
      "action": [
        "name/cos:GetObject"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test2/*"
      ]
    }
  ]
}
```

そのうち`"qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test2/*"`はソースオブジェクトです。

### パートコピー

シャードコピー：Upload Part Copyについて、その操作権限を付与すれば、ポリシーのターゲットオブジェクトの`action`は`"name/cos:InitiateMultipartUpload","name/cos:ListParts","name/cos:PutObject","name/cos:CompleteMultipartUpload","name/cos:AbortMultipartUpload"`の集合であり、ソースオブジェクトの`action`は`name/cos:GetObject`です。

#### 例

APPIDが1253653367で、地域が`ap-beijing`で、バケットが`example-1253653367`のパスプレフィックス`test`とパスプレフィックス`test2`との間でシャードコピーを行う操作権限を付与し、そのポリシーの詳細は以下のとおりです：

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:InitiateMultipartUpload",
        "name/cos:ListParts",
        "name/cos:PutObject",
        "name/cos:CompleteMultipartUpload",
        "name/cos:AbortMultipartUpload"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/*"
      ]
    },
    {
      "action": [
        "name/cos:GetObject"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test2/*"
      ]
    }
  ]
}
```

そのうち`"qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test2/*"`はソースオブジェクトです。

### オブジェクトACLの設定

オブジェクトACLの設定：Put Object ACLについて、その操作権限を付与すれば、ポリシーの`action`は`name/cos:PutObjectACL` です。

#### 例

APPIDが1253653367で、地域が`ap-beijing`で、バケットが`example-1253653367`で、パスプレフィックスが`test`のオブジェクトACLのみを設定できる操作権限を付与し、そのポリシーの詳細は以下のとおりです：

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:PutObjectACL"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/*"
      ]
    }
  ]
}
```

### オブジェクトACLの取得

オブジェクトACLの取得：Get Object ACLについて、その操作権限を付与すれば、ポリシーの`action`は`name/cos:GetObjectACL`です。

#### 例

APPIDが1253653367で、地域が`ap-beijing`で、バケットが`example-1253653367`で、パスプレフィックスが`test`のオブジェクトACLのみを取得できる操作権限を付与し、そのポリシーの詳細は以下のとおりです：

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:GetObjectACL"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/*"
      ]
    }
  ]
}
```

### オプションリクエスト

オプションリクエスト：Options Objectについて、その操作権限を付与すれば、ポリシーの`action`は`name/cos:OptionsObject`です。

#### 例

APPIDが1253653367で、地域が`ap-beijing`で、バケットが`example-1253653367`で、パスプレフィックスが`test`の条件のみでOptionsリクエストを行うことができる操作権限を付与し、そのポリシーの詳細は以下のとおりです：

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:OptionsObject"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/*"
      ]
    }
  ]
}
```

### アーカイブオブジェクトの回復

アーカイブオブジェクトの回復：Post Object Restoreについて、その権限を付与すれば、ポリシーの`action`は`name/cos:PostObjectRestore`です。

#### 例

APPIDが1253653367で、地域が`ap-beijing`で、バケットが`example-1253653367`で、パスプレフィックスが`test`の条件のみでアーカイブの回復を行うことができる操作権限を付与し、そのポリシーの詳細は以下のとおりです：

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:PostObjectRestore"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/*"
      ]
    }
  ]
}
```

### オブジェクトの削除

オブジェクトの削除：Delete Objectについて、その操作権限を付与すれば、ポリシーの`action`は`name/cos:DeleteObject`です。

#### 例

APPIDが1253653367で、地域が`ap-beijing`で、バケットが`example-1253653367`のオブジェクト`audio.mp3`のみを削除できる操作権限を付与し、そのポリシーの詳細は以下のとおりです：

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:DeleteObject"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/audio.mp3"
      ]
    }
  ]
}
```

### オブジェクトの一括削除

オブジェクトの一括削除：Delete Multiple Objectsについて、その操作権限を付与すれば、ポリシーの`action`は`name/cos:DeleteObject`です。

#### 例

APPIDが1253653367で、地域が`ap-beijing`で、バケットが`example-1253653367`の2つのオブジェクト`audio.mp3`および`video.mp4`のみを一括削除できる操作権限を付与し、そのポリシーの詳細は以下のとおりです：

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:DeleteObject"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/audio.mp3",
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/video.mp4"
      ]
    }
  ]
}
```

## 一般的なシナリオの権限付与ポリシー

### すべてのリソースに対する完全な読み書き権限の付与
すべてのリソースに対する完全な読み書き権限を付与し、そのポリシーの詳細は以下のとおりです：
```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "*"
      ],
      "effect": "allow",
      "resource": [
        "*"
      ]
    }
  ]
}
```

### すべてのリソースに対する読み取り専用権限の付与
すべてのリソースに対する読み取り専用権限を付与し、そのポリシーの詳細は以下のとおりです：
```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:Head*",
        "name/cos:Get*",
        "name/cos:List*",
        "name/cos:OptionsObject"
      ],
      "effect": "allow",
      "resource": [
        "*"
      ]
    }
  ]
}
```

### パスプレフィックスが指定された読み書き操作の権限付与
バケットがexample-1253653367で、パスプレフィックスがuserID123456のファイルにのみアクセスでき、かつ他のパスのファイルを操作できない操作権限をユーザーに付与し、このポリシーの詳細は以下のとおりです：
```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "*"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-shanghai:uid/1253653367:prefix//1253653367/example/userID123456/*"
      ]
    }
  ]
}
```
