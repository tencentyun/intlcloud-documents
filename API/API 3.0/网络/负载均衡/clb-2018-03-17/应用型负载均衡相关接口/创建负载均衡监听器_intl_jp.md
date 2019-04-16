## 1. API説明

APIリクエストドメイン名：clb.tencentcloudapi.com。

ロードバランサーインスタンス下でリスナーを作成します。
このAPIは非同期APIであり、APIの返し動作が完了した後、返されたRequestIDを入力パラメータとする必要があり、DescribeTaskStatus APIを呼び出して今回のタスクが成功したか照合します。

デフォルトのAPIリクエスト頻度制限：20回/秒。

注意：このAPIは金融区地域をサポートします。金融区と非金融区は分離されており、相互通信できないため、共通パラメータRegionが金融区地域（例えば、ap-shanghai-fsi）の場合は、金融区地域のドメイン名を同時に指定する必要があります。Region地域と一致するようにするのは一番です。例：clb.ap-shanghai-fsi.tencentcloudapi.com。



## 2. 入力パラメータ

次のリクエストパラメータリストには、APIリクエストパラメータと一部の共通パラメータのみがリストされています。完全な共通パラメータのリストについては、[共通リクエストパラメータ](/document/api/214/30670)を参照してください。

| パラメータ名 | 必須項目 | タイプ | 説明 |
|---------|---------|---------|---------|
| Action | はい | String | 共通パラメータ、このAPIの値：CreateListener |
| Version | はい | String | 共通パラメータ、このAPIの値：2018-03-17 |
| Region | はい | String | 共通パラメータ、詳細については、製品がサポートする[地域リスト](/document/api/214/30670#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)を参照してください。 |
| LoadBalancerId | はい | String | ロードバランサーインスタンスID |
| Ports.N | はい | Array of Integer | リスナーを作成するポート番号の配列。各ポートは1つ新しいリスナーに対応します |
| Protocol | はい | String | リスナーのプロトコル：HTTP &#124; HTTPS &#124; TCP &#124; TCP_SSL|
| ListenerNames.N | いいえ | Array of String | 作成するリスナー名リストであり、名称とPorts配列は順に1対1で対応します。直ちに命名する必要がない場合、このパラメータを提供する必要はありません |
| HealthCheck | いいえ | [HealthCheck](/document/api/214/30694#HealthCheck) | 正常性検査関連パラメータであり、このパラメータはTCP/UDP/TCP_SSLリスナーにのみ適用されます |
| Certificate | いいえ | [CertificateInput](/document/api/214/30694#CertificateInput) | 証明書関連情報であり、このパラメータはHTTPS/TCP_SSLリスナーにのみ適用されます |
| SessionExpireTime | いいえ | Integer | セッション保留時間であり、単位は秒です。選択可能な値は30～3600であり、デフォルトは0で、有効でないことを示します。このパラメータはTCP/UDPリスナーにのみ適用されます。 |
| Scheduler | いいえ | String | リスナーの転送方式。選択可能な値はWRR、LEAST_CONN。<br/>それぞれ重み付きラウンドロビン、最小接続数を表し、デフォルトはWRRです。このパラメータは、TCP/UDP/TCP_SSLリスナーにのみ適用されます。 |
| SniSwitch | いいえ | Integer | SNI特性を有効にするかどうかということであり、このパラメータは、HTTPSリスナーにのみ適用されます。 |

## 3. 出力パラメータ

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| ListenerIds | Array of String | 作成したリスナーの唯一のタグ配列|
| RequestId | String | 唯一のリクエストID、リクエストごとに返します。問題を特定するときに、このリクエストのRequestIdが必要です。|

## 4. 例

### 例1 2つのTCPリスナーを作成し、それぞれポート7569と7570を監視し、また、lis0とlis1と命名

2つのTCPリスナーを作成し、それぞれポート7569と7570を監視し、また、lis0とlis1と命名します。

#### 入力例

```
https://clb.tencentcloudapi.com/?Action=CreateListener
&LoadBalancerId=lb-cuxw2rm0
&Protocol=TCP
&Ports.0=7569
&Ports.1=7570
&ListenerNames.0=lis0
&ListenerNames.1=lis1
&<共通リクエストパラメータ>
```

#####　出力例

```
{
    "Response": {
        "ListenerIds": [
            "lbl-d1ubsydq",
            "lbl-4udz130k"
        ],
        "RequestId": "8f272cef-14ff-458c-b67e-1bd21bd2942b"
    }
}
```

### 例2 TCPリスナー作成と同時に正常性検査情報を設定

#### 入力例

```
https://clb.tencentcloudapi.com/?Action=CreateListener
&LoadBalancerId=lb-cuxw2rm0
&Protocol=TCP
&Ports.0=7571
&HealthCheck.HealthSwitch=1
&HealthCheck.TimeOut=5
&HealthCheck.IntervalTime=7
&HealthCheck.HealthNum=4
&HealthCheck.UnHealthNum=4
&<共通リクエストパラメータ>
```

#####　出力例

```
{
    "Response": {
        "ListenerIds": [
            "lbl-lbbxvq26"
        ],
        "RequestId": "fff13c83-dcb5-481a-ba7c-30e92c276c19"
    }
}
```

### 例3 HTTPリスナーを作成し、既存の証明書をバインディング

#### 入力例

```
https://clb.tencentcloudapi.com/?Action=CreateListener
&LoadBalancerId=lb-cuxw2rm0
&Protocol=HTTPS
&Ports.0=7572
&Certificate.SSLMode=UNIDIRECTIONAL
&Certificate.CertId=MsJyaXVm
&<共通リクエストパラメータ>
```

#####　出力例

```
{
    "Response": {
        "ListenerIds": [
            "lbl-4fbxq45k"
        ],
        "RequestId": "db8ae69f-ebda-402b-8d02-ead459aa6ff9"
    }
}
```

### 例4 HTTPリスナーを作成すると同時に、新規作成した証明書をバインディング

#### 入力例

```
https://clb.tencentcloudapi.com/?Action=CreateListener
&LoadBalancerId=lb-cuxw2rm0
&Protocol=HTTPS
&Ports.0=7573
&Certificate.SSLMode=UNIDIRECTIONAL
&Certificate.CertName=my-cert
&Certificate.CertContent=-----BEGIN CERTIFICATE-----
MIIEjTCCA3WgAwIBAgIQA4ZHUAVOv4yrszl3lLfo3TANBgkqhkiG9w0BAQsFADBy
MQswCQYDVQQGEwJDTjElMCMGA1UEChMcVHJ1c3RBc2lhIFRlY2hub2xvZ2llcywg
SW5jLjEdMBsGA1UECxMURG9tYWluIFZhbGlkYXRlZCBTU0wxHTAbBgNVBAMTFFRy
dXN0QXNpYSBUTFMgUlNBIENBMB4XDTE4MDEwOTAwMDAwMFoXDTE5MDEwOTEyMDAw
MFowFjEUMBIGA1UEAxMLZmx5Zmx5Lm5hbWUwggEiMA0GCSqGSIb3DQEBAQUAA4IB
DwAwggEKAoIBAQClpnigB7r3ahv7BMuQw9KzB9Yfq3p+cRUbX9EMRyri2GrJbmrP
pESP8XQuIn4MZESvePR0r4gGHAHVri8nXzyQw6/m77BT/fIf4cQtEyz61gopDlYq
bLTAKVfGFhGVikvQPoItOYbA9/l2YwtDENl8wBhcFrghWTRifnFSC0bNPj1ot5eu
L8x5UOZLSa9kaQCm2/RQUBii5w3YBh+HmJgb7HPs8OoHKVScBo6eAyOcr+HNrA8W
KsM6r4LpS+Rpfng7+fAKGE+vFsssXfRMBTo0TPp+h8ohuM8xqujbK+T7LMEXNWN9
3FGYuuH+qmPvx/gAXFjLARKVyf0IsNnu6TLLAgMBAAGjggF5MIIBdTAfBgNVHSME
GDAWgBR/05nzoEcOMQBWViKOt8ye3coBijAdBgNVHQ4EFgQUUCq9/Hmfgli5URvx
AbSDNsDCCqcwJwYDVR0RBCAwHoILZmx5Zmx5Lm5hbWWCD3d3dy5mbHlmbHkubmFt
ZTAOBgNVHQ8BAf8EBAMCBaAwHQYDVR0lBBYwFAYIKwYBBQUHAwEGCCsGAQUFBwMC
MEwGA1UdIARFMEMwNwYJYIZIAYb9bAECMCowKAYIKwYBBQUHAgEWHGh0dHBzOi8v
d3d3LmRpZ2ljZXJ0LmNvbS9DUFMwCAYGZ4EMAQIBMIGBBggrBgEFBQcBAQR1MHMw
JQYIKwYBBQUHMAGGGWh0dHA6Ly9vY3NwMi5kaWdpY2VydC5jb20wSgYIKwYBBQUH
MAKGPmh0dHA6Ly9jYWNlcnRzLmRpZ2l0YWxjZXJ0dmFsaWRhdGlvbi5jb20vVHJ1
c3RBc2lhVExTUlNBQ0EuY3J0MAkGA1UdEwQCMAAwDQYJKoZIhvcNAQELBQADggEB
ADstNGgqYXG6eBDcBGVZk6DnJdS4GYdSzFZgCwt298cPMmZj107VM0QsB5K8V5Zd
zJl5c7o4tEXiGP+lk0TVqgP/CkcMXcpxeKB94ldyX9ILii/L4hI9j7hVrLVM1eAn
fS66Yg65xIYU8PdFtP3uhI9WdhE3nYRngyoHAAMjIvu0bqGPYbqpnHYp8fmjyetF
C9CZcjkqHmwTSpjXuFjbDLx/BXd1Q81TNXwv8alkuXKfIJ5tW2lH372GmQb8I3oI
PREP38tlBbmfEu4p7+UzwwuQuD8cEUVuG/x7cUN2uAGiZGoohydrORWm8kqdNY9c
YOuRvokzVT4lsaln5LKkKxw=
-----END CERTIFICATE-----
&Certificate.CertKey=-----BEGIN RSA PRIVATE KEY-----
MIIEoAIBAAKCAQEApaZ4oAe692ob+wTLkMPSswfWH6t6fnEVG1/RDEcq4thqyW5q
z6REj/F0LiJ+DGREr3j0dK+IBhwB1a4vJ188kMOv5u+wU/3yH+HELRMs+tYKKQ5W
Kmy0wClXxhYRlYpL0D6CLTmGwPf5dmMLQxDZfMAYXBa4IVk0Yn5xUgtGzT49aLeX
ri/MeVDmS0mvZGkAptv0UFAYoucN2AYfh5iYG+xz7PDqBylUnAaOngMjnK/hzawP
FirDOq+C6UvkaX54O/nwChhPrxbLLF30TAU6NEz6fofKIbjPMaro2yvk+yzBFzVj
fdxRmLrh/qpj78f4AFxYywESlcn9CLDZ7ukyywIDAQABAoH/KoiULD7g9kAEZrQp
1SQusYVRl+E8xeVUdQhHcfCyAUkIAEpZzV2TtLd+DFqKrbTvITBT+vd9sYtdU6K7
Z8cMcMoSpNMq+/+wK/b/m4I/6EqEt8HDb0NpSBBEeWUxQM4fumnsFBcXtew6iCtu
2vzN7G2IwqUSxI5nbY2SektZ4q5ZRvwEND6gE51uqcqo4i6hA/TYsJLZ63L+Ux0A
nm0AsmtMct+DT13NAlpyi6feDQCr1cxcSpqfhfgkWpawJVSxtxKvIn044iRBXb7Y
RcW/8YYU1PrTIhhE9AnES7g8mnAgBHRryxuUotXkk7VotTHDbTO0q5KvO2bZ2T6z
vQ4BAoGBANqoZE/wAB41wbJ7KwyblxyegI3Y9XYtkPLZlLK+GbCaC9UHNhPqSdaH
WPoc3rtm8tOFQc7QMTFtxTLwQ3wEeSO4BFckVHgywuJoGRw1ZYxN8vAzHF1Gc/J1
YcX0CDBuKgc0CxlhM7tDAzOgcfJR0EFRVhvLcUAA9hUoeN3EetSBAoGBAMHwnjWc
+Y/vBW5yCefQciqppaylwB89H6kds+p0fDlVZQ080VB3b61t6VXOoYAzY4abOjxK
AfNyVQcOEuO3gtZp3THK3fkV6bKaNHG41Ang32VW3XGb+MeEkJZwJk4JFbLrz8ln
te4M9PjVpYuEQCJZvUjrhd+LJRubTTUXIHFLAoGAU0KJp/KwaNB5aDgERXG9kbU9
KEYz+YMSTZbSS1mduKR/2uc7DUxKP3kcRWjW2y8xSZ/VViXqhXLSAzp/x+qAIjzA
0lnQHFDf6oxO+3HNsCZCWnpr04yvO+S8jT8GG0LnmASWMVzU8Ppsbq0qlmXW0fhh
vIW0IvX6vkXB+FgHmYECgYBrsJe5P4QYV2oVrP8xGL78T51uY89tyTwWZSbtTmdY
UsG8+wNjgh6iF8EUY5usG1ztdq58ob+5lcf/FeKJTfI56yjnKDXfxToycYwjhbVA
Ev0ZQYXPOwOGjmbXEklC1aqV4nlL5enQ2KMCtWeqM/KE4H3JyvZYbeRaEv9pNoFO
RwKBgBs+g0d81ufZSuTBlxfivDwrNV6LNzrgnwsTn+H/T7MfyoIEkT3nSGjanQHF
wzPYyUpQx5OzNZp1ZEzKeW3GXVWjK+bfKlA7fmrZwDa8/JR6kTfCmc3WRrrQ92yq
lFRW1kinLCP5y56SJEBz+DRSYV7ql9wOHyaM23sHkbCF0HAa
-----END RSA PRIVATE KEY-----
&<共通リクエストパラメータ>
```

#####　出力例

```
{
    "Response": {
        "ListenerIds": [
            "lbl-bzfmg9m6"
        ],
        "RequestId": "6082314c-030c-429d-9eae-2dc6b159b5b9"
    }
}
```


## 5. 開発者リソース

### API Explorer

**このツールはオンライン呼び出し、署名の検証、SDKコード生成と高速検索APIなどの機能を提供し、クラウドAPI使用の難易度を大幅に低減することができるため、お勧めします。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=clb&Version=2018-03-17&Action=CreateListener)

### SDK

クラウドAPI 3.0は、API呼び出しを容易にするために複数のプログラミング言語をサポートする、関連開発ツールセット（SDK）を提供します。

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. エラーコード

以下に、APIビジネスロジックに関連するエラーコードのみをリストします。その他のエラーコードについては、[共通エラーコード](/document/api/214/30673#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)を参照してください。

| エラーコード | 説明 |
|---------|---------|
| FailedOperation | 操作失敗 |
| InternalError | 内部エラー |
| InvalidParameter | パラメータエラー。 |
| InvalidParameterValue | パラメータ値エラー |
| LimitExceeded | 割り当て量の制限を超えました |
| ResourceInsufficient | リソースが足りません |
| UnauthorizedOperation | 操作が承認されていません |

