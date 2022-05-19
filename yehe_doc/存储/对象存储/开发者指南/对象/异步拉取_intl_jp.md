
## 概要

非同期プル機能では、ユーザーがオリジンサーバーから指定のファイルをプルし、データをCloud Object Storage（COS）上に保存することが可能です。非同期プル機能はCOSのサービスロールによって操作することが可能ですが、ユーザーがCOSのサービスロールに対し対応する権限を与えてから非同期プルを行うことが前提となります。

## COSサービスロールへの権限承認 

非同期プル機能ではCOSのサービスロールに対し、指定のオリジンサーバーのデータを指定のバケットにアップロードする権限を承認する必要があります。このため、ユーザーはバケット内に対応するバケットポリシーを追加しなければなりません。ポリシー構文は次のとおりです。

```
{
      "Statement": [
        {
          "Principal": {
             "service": "cos.qcloud.com"
          },
          "Effect": "Allow",
          "Action": [
             "name/cos:PutObject",
             "name/cos:InitiateMultipartUpload",
             "name/cos:UploadPart",
             "name/cos:CompleteMultipartUpload"
          ],
          "Resource": [
             "qcs::cos:<Region>:uid/<APPID>:<BucketName-APPID>/*"
          ]
        }
      ],
      "version": "2.0"
}
```

>? ポリシー構文で変更が必要な入力パラメータはResourceフィールドの6つの部分から成るリソースです。Regionをユーザーのバケットの所在リージョンに変更し、APPIDをユーザーのAPPIDに変更し、BucketNameをユーザーのバケット名に変更してください。
>

広州リージョンのexamplebucket-12500000000を例に挙げると、ファイルをルートディレクトリ下にアップロードする権限を承認する場合、ポリシー構文は次のようになります。

```
"Resource": [
         "qcs::cos:ap-guangzhou:uid/12500000000:examplebucket-12500000000/*"
]
```

ファイルをprefixディレクトリ下にアップロードする権限を承認する場合、ポリシー構文は次のようになります。

```
"Resource": [
         "qcs::cos:ap-guangzhou:uid/12500000000:examplebucket-12500000000/prefix/*"
]
```

## 利用方法

### REST APIの使用

REST APIを直接使用して非同期プルリクエストを送信できます。 詳細については、[照会のプロセス](https://intl.cloud.tencent.com/document/product/436/39775)および[オフラインback-to-originの開始](https://intl.cloud.tencent.com/document/product/436/39774)をご参照ください。

### SDKの使用

SDKを直接呼び出して非同期プル操作を行うことができます。詳細については、[Githubの例](https://github.com/tencentyun/cos-python-sdk-v5/blob/master/demo/fetch_demo.py)をご参照ください。

