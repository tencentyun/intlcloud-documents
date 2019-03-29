### API説明

このAPI（ListSAMLProviders）は、SAML IDプロバイダーのリストを取得するために使用されます。
リクエストドメイン名：cam.api.qcloud.com

###　入力パラメータ
以下のリクエストパラメーターリストにはAPIリクエストパラメータのみがリストされ、他の共通パラメータのリストについては、[共通リクエストパラメータ](https://cloud.tencent.com/document/api/213/15692)を参照してください。

| パラメータ名 | 必須項目 | タイプ | 説明|
|---------|---------|---------|---------|
|page | はい | Integer | ページ番号 |
|rp | はい |Integer | ページサイズ |

###　出力パラメータ

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| total | Integer | IDプロバイダーの総数 |
| list | Array Of SAMLProvider | SAML IDプロバイダーリスト |

SAMLProviderフィールドは以下のとおりです。

| 名称 | タイプ | 説明 |
|---------|---------|---------|
| name | String | IDプロバイダーの名称 |
| desc | String | IDプロバイダーの説明|
| createTime | Date | IDプロバイダーの作成時間 |
| modifyTime | Date| IDプロバイダーのアップデート時間 |


###　　例

SAMl IDプロバイダーのリストを照合します。

#####　入力例：

``` 
https://cam.api.qcloud.com/v2/index.php?Action=ListSAMLProviders
&page=1
&rp=5
&<共通リクエストパラメータ>
``` 

#####　出力例：

``` 
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "total": 9,
        "list": [
            {
                "name": "api-test-v2",
                "desc": "APIテスト12121",
                "createTime": "2018-10-30 14:43:37",
                "modifyTime": "2018-10-30 14:57:35"
            },
            {
                "name": "api-test",
                "desc": "APIテスト",
                "createTime": "2018-10-30 11:40:19",
                "modifyTime": "2018-10-30 11:40:19"
            },
            {
                "name": "aaaaaaaaaaa",
                "desc": "テスト",
                "createTime": "2018-10-17 17:16:17",
                "modifyTime": "2018-10-17 17:16:17"
            },
            {
                "name": "test1112222",
                "desc": "111111",
                "createTime": "2018-10-15 21:30:08",
                "modifyTime": "2018-10-15 21:30:08"
            },
            {
                "name": "test111",
                "desc": "111111",
                "createTime": "2018-10-12 18:09:19",
                "modifyTime": "2018-10-12 18:09:19"
            }
        ]
    }
}
``` 

###　　エラーコード
以下に、APIビジネスロジックに関連するエラーコードのみをリストします。その他のエラーコードについては、[共通エラーコード](https://cloud.tencent.com/document/api/213/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)を参照してください。


