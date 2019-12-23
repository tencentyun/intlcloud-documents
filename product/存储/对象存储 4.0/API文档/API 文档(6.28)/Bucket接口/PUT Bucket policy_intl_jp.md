## 機能説明
PUT Bucket policyリクエストは、バケットに権限ポリシーを書き込むことができます。バケットは権限ポリシーを持っている場合、このリクエストによってアップロードされたポリシーは元の権限ポリシーを上書きします。

## リクエスト

### リクエスト例

```shell
PUT /?policy HTTP/1.1
Host:<BucketName-APPID>.cos.<Region>.myqcloud.com
Date: date
Content-Type:application/json
Content-MD5:MD5
Authorization: Auth String
```

> Authorization: Auth String（詳細については、[リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)ドキュメントを参照してください）。


### リクエストヘッダー

#### 共通のヘッダー

このリクエスト操作の実現では、共通リクエストヘッダーを使用します。共通リクエストヘッダーの詳細については、[共通リクエストヘッダー](https://cloud.tencent.com/document/product/436/7728"公共请求头部")セクションを参照してください。

#### リクエストパラメータ
特別なリクエストパラメータが無し。

### リクエストボディ

```shell
{
    "Statement": [
        {
            "Principal": {
                "qcs": [
                    "qcs::cam::uin/${owner_uin}:uin/${sub_uin}"
                ]
            },
            "Effect": "${effect}",
            "Action": [
                "name/cos:${action}"
            ],
            "Resource": [
                "qcs::cos:${region}:uid/${appid}:${bucket}/*"
            ]
        }
    ],
    "version": "2.0"
}
```

## 応答

### 応答ヘッダー
#### 共通の応答ヘッダー

この応答は、共通応答ヘッダーを使用します。共通応答ヘッダーの詳細については、[共通応答ヘッダー](https://cloud.tencent.com/document/product/436/7729)セクションを参照してください。

#### 特有の応答ヘッダー

このリクエスト操作には、特別な応答ヘッダー情報はありません。

### 応答ボディ
このリクエストの応答ボディはブランクです。

###　エラーコード

特別なエラーコードの戻りがありません。一般的なエラーコードについては、[エラーコード](https://cloud.tencent.com/document/product/436/7730)ドキュメントを参照してください。

## 実際のケース
### リクエスト

```shell
PUT /?policy HTTP/1.1
Host:examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
Authorization:q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484813288;32557709288&q-key-time=1484813288;32557709288&q-header-list=host&q-url-param-list=policy&q-signature=05f7fc936369f910a94a0c815e1f1752f034d47a
Content-Type: application/json
Content-Length: 233

{
  "Statement": [
    {
      "Principal": {
        "qcs": [
          "qcs::cam::uin/1250000000:uin/1250000000"
        ]
      },
      "Effect": "allow",
      "Action": [
        "name/cos:GetBucket"
      ],
      "Resource": [
        "qcs::cos:ap-chengdu:uid/1250000000:examplebucket-1250000000/*"
      ]
    }
  ],
  "version": "2.0"
}

```

### 応答

```shell
HTTP/1.1 204 No Content
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Thu Jan 19 16:19:22 2017
Server: tencent-cos
x-cos-request-id: NTg4MDc2OGFfNDUyMDRlXzc3NTlfZTc4
```

