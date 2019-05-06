## 概要
本文はサブネット、委託者とVPC IDを制限するバケットポリシー例を示します。当該バケットポリシーにより、バケット及びそのデータに特定のアクセスを行うことができます。アクセスポリシー言語の詳しい情報については、[アクセスポリシー言語の概要](https://cloud.tencent.com/document/product/436/18023)を参照してください。
>!
>- COSコンソールによりバケットポリシーを構成する場合、ユーザーにバケットの関連権限を付与しておく必要があります。例えば、バケット位置の取得とバケット権限のリスト。
- バケットポリシーのサイズは20KBに限られています。


### 例1：サブネット10.1.1.0/24 IPアドレス範囲とvpcidがaqp5jrc1であるリクエストを制限します
構文例を下記に示します：
```
{
  "Statement": [
    {
      "Action": [
        "name/cos:*"
      ],
      "Condition": {
        "ip_equal": {
          "qcs:ip": [
            "10.1.1.0/24"
          ]
        },
        "string_equal": {
          "vpc:requester_vpc": [
            "vpc-aqp5jrc1"
          ]
        }
      },
      "Effect": "deny",
      "Principal": {
        "qcs": [
          "qcs::cam::anyone:anyone"
        ]
      },
      "Resource": [
        "qcs::cos:ap-guangzhou:uid/1251668577:jimmyyantest-1251668577/*"
      ]
    }
  ],
  "version": "2.0"
}
```


### 例2：vpcidがaqp5jrc1であり、特定委託者と特定バケットのリクエストを制限します
構文例を下記に示します：
```
{
  "Statement": [
    {
      "Action": [
        "name/cos:*"
      ],
      "Condition": {
        "string_equal": {
          "vpc:requester_vpc": [
            "vpc-aqp5jrc1"
          ]
        }
      },
      "Effect": "allow",
      "Principal": {
        "qcs": [
          "qcs::cam::uin/3280754170:uin/100005212150"
        ]
      },
      "Resource": [
        "qcs::cos:ap-beijing:uid/1252921383:x3cmplay-1252921383/*"
      ]
    }
  ],
  "version": "2.0"
}
```
