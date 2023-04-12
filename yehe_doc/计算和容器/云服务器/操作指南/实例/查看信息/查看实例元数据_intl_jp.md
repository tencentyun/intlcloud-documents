インスタンスメタデータは、インスタンスに関連するデータを指します。実行中のインスタンスを構成または管理するために使用できます。
>? インスタンスの内部からのみインスタンスメタデータにアクセスできますが、データは暗号化されていません。インスタンスにアクセスできる人員はいずれもそのメタデータを表示できます。そのため、機密データを保護するために適切な予防措置を講じる必要があります。
>


## インスタンスメタデータの分類
Tencent Cloudは現在、次のメタデータを提供しています。

| データ | 説明 | バージョン |
|---------|---------|---------|
| instance-id | インスタンス ID | 1.0 |
| instance-name | インスタンス名 | 1.0 |
| uuid | インスタンス ID | 1.0 |
| local-ipv4 | インスタンスのプライベートIPアドレス | 1.0 |
| public-ipv4 | インスタンスのパブリックIPアドレス | 1.0 |
| mac | インスタンスの eth0 デバイスの MAC アドレス | 1.0 |
| placement/region | インスタンスが属するリージョンの情報 | 2017年9月19日更新 |
| placement/zone | インスタンスが属するアベイラビリティーゾーンの情報 | 2017年9月19日更新 |
| network/interfaces/macs/**${mac}**/mac | インスタンスのネットワークインターフェースのMACアドレス | 1.0 |
| network/interfaces/macs/**${mac}**/primary-local-ipv4 | インスタンスのネットワークインターフェースのプライマリプライベートIPアドレス | 1.0 |
| network/interfaces/macs/**${mac}**/public-ipv4s | インスタンスのネットワークインターフェースのパブリックIPアドレス | 1.0 |
| network/interfaces/macs/**${mac}**/vpc-id | インスタンスのネットワークインターフェースのVPC ID | 2017年9月19日更新 |
| network/interfaces/macs/**${mac}**/subnet-id | インスタンスのネットワークインターフェースのサブネットID | 2017年9月19日更新 |
| network/interfaces/macs/**${mac}**/local-ipv4s/**${local-ipv4}**/gateway | インスタンスのネットワークインターフェースのゲートウェイアドレス | 1.0 |
| network/interfaces/macs/**${mac}**/local-ipv4s/**${local-ipv4}**/local-ipv4 | インスタンスのネットワークインターフェースのプライベートIPアドレス| 1.0 |
| network/interfaces/macs/**${mac}**/local-ipv4s/**${local-ipv4}**/public-ipv4 | インスタンスのネットワークインターフェースのパブリックIPアドレス | 1.0 |
| network/interfaces/macs/**${mac}**/local-ipv4s/**${local-ipv4}**/public-ipv4-mode | インスタンスのネットワークインターフェースのパブリックネットワークモード | 1.0 |
| network/interfaces/macs/**${mac}**/local-ipv4s/**${local-ipv4}**/subnet-mask | インスタンスのネットワークインターフェースのサブネットマスク | 1.0 |
| payment/charge-type | インスタンスの課金方法 | 2017年9月19日更新 |
| payment/create-time | インスタンスの作成時間 | 2017年9月19日更新|
| payment/termination-time | インスタンスの終了時間 | 2017年9月19日更新|
| app-id | インスタンス所有者のAppID| 2017年9月19日更新|
| as-group-id | インスタンスが属するAuto ScalingグループID| 2017年9月19日更新|
| spot/termination-time | スポットインスタンスの終了時間 | 2017年9月19日更新|
| /meta-data/instance/instance-type | インスタンス仕様 | 2017年9月19日更新|
| /instance/image-id | インスタンスイメージID | 2017年9月19日更新 |
| /instance/security-group | インスタンスを関連付けるセキュリティグループの情報 | 2017年9月19日更新|
| /instance/bandwidth-limit-egress | インスタンスのプライベートネットワークのアウトバウンド帯域幅制限(Kbit/s) | 2019年9月29日更新|
| /instance/bandwidth-limit-ingress | インスタンスのプライベートネットワークのインバウンド帯域幅制限 (Kbit/s) | 2019年9月29日更新|
| /cam/security-credentials/${role-name} | インスタンスのCAMロールポリシーによって生成される一時的な認証情報。インスタンスが CAMロールに関連付けられている場合にのみ一時的な認証情報を取得できます。そのうち、${role-name} パラメータを実際のCAMロール名に置き換える必要があります。それ以外の場合は、404エラーが返されます。| 2019年12月11日更新|



>?  上記テーブルにおける${mac}および${local-ipv4}フィールドはそれぞれインスタンスに指定されたネットワークインターフェースのMACアドレスとプライベートIPアドレスを表します。
> 
> リクエストの宛先 URL アドレスは、大文字と小文字を区別する必要があります。返されたリクエストの結果に従って、新しいリクエストの宛先 URL アドレスを作成する必要があります。
>
> 返された配置データは、新しいバージョンで変更されています。以前のバージョンのデータを使用する必要がある場合、以前のバージョンのパスを指定するか、バージョンのパスを指定しないことによりバージョン1.0のデータにアクセスすることができます。返された配置データの詳細については、[リージョンとアベイラビリティーゾーン](https://intl.cloud.tencent.com/document/product/213/6091)をご参照ください。

## インスタンスメタデータのクエリ
インスタンスにログインすると、インスタンスのローカルIPアドレスやパブリックIPアドレスなどのメタデータにアクセスして、外部アプリケーションとの接続を管理できます。
実行中のインスタンス内部からすべてのカテゴリーのインスタンスメタデータを確認するには、次のURIを使用してください。

```
http://metadata.tencentyun.com/latest/meta-data/
```
cURLツールまたはHTTP GETリクエストを介してメタデータにアクセスできます。例：

```
curl http://metadata.tencentyun.com/latest/meta-data/
```
* リソースが存在しない場合、HTTPエラーコード「404 Not Found」が返されます。
* インスタンスメタデータに対する操作はいずれも**インスタンス内部**からのみ行うことができます。最初にインスタンスにログインする必要があります。インスタンスへのログインに関する詳細な内容は、[Windowsインスタンスへのログイン](https://intl.cloud.tencent.com/document/product/213/5435)および[Linuxインスタンスへのログイン](https://intl.cloud.tencent.com/document/product/213/5436)をご参照ください。

### メタデータクエリ例

以下の例では、メタデータのバージョン情報を取得する方法を説明します。
>! Tencent Cloudがメタデータのアクセスパスまたは返されたデータを変更する時、新しいメタデータのバージョンをリリースします。お客様のアプリケーションプログラムまたはスクリプトが以前のバージョンの構造または返されたデータに依存している場合、指定された初期のバージョンを使用してメタデータにアクセスできます。バージョンを指定しない場合、デフォルトでバージョン1.0がアクセスされます。
>

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/
1.0
2017-09-19
latest
meta-data
```

以下の例では、メタデータのルートディレクトリを表示する方法を説明します。そのうち「/」で終わる単語はディレクトリを表し、「/」で終わらない単語はアクセスデータを表します。具体的なアクセスデータの意味は、前文の**インスタンスメタデータの分類**をご参照ください。

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/
instance-id
instance-name
local-ipv4
mac
network/
placement/
public-ipv4
uuid
```

以下の例では、インスタンスの物理的な位置情報を取得する方法を説明します。 返されるデータと物理的な位置情報の関係については、[リージョンとアベイラビリティーゾー](https://intl.cloud.tencent.com/document/product/213/6091)をご参照ください。

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/placement/region
ap-guangzhou

[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/placement/zone
ap-guangzhou-3
```

以下の例では、インスタンスのプライベートIPアドレスを取得する方法を説明します。インスタンスに複数のENIがある場合、eth0デバイスのネットワークアドレスが返されます。

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/local-ipv4
10.104.13.59/
```

以下の例では、インスタンスのパブリックIPアドレスを取得する方法を説明します。

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/public-ipv4
139.199.11.29
```

以下の例では、インスタンスIDを取得する方法を説明します。インスタンスIDはインスタンスの一意の識別子です。

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/instance-id
ins-3g445roi
```

以下の例では、インスタンスUUIDを取得する方法を説明します。インスタンスUUIDはインスタンスの一意の識別子とすることができますが、インスタンスIDを使用してインスタンスを識別することをお勧めします。

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/uuid
cfac763a-7094-446b-a8a9-b995e638471a
```

以下の例では、インスタンスのeth0デバイスのMACアドレスを取得する方法を説明します。

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/mac
52:54:00:BF:B3:51
```

以下の例では、インスタンスのENI情報を取得する方法を説明します。複数枚のENIは複数行のデータを戻し、各行のデータはENI1枚のデータディレクトリです。

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/
52:54:00:BF:B3:51/
```

以下の例では、指定されたENIの情報を取得する方法を説明します。

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/
local-ipv4s/
mac
vpc-id
subnet-id
owner-id
primary-local-ipv4
public-ipv4s
local-ipv4s/
```

以下の例では、指定されたENIのVPC情報を取得する方法を説明します。

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/vpc-id
vpc-ja82n9op

[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/subnet-id
subnet-ja82n9op
```

以下の例では、指定されたENIにバインドされたプライベートIPアドレスのリストを取得する方法を説明します。ENIが複数のプライベートIPアドレスにバインドされている場合、複数行のデータが返されます。

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/local-ipv4s/
10.104.13.59/
```

以下の例では、プライベートIPアドレスの情報を取得する方法を説明します。

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/local-ipv4s/10.104.13.59
gateway
local-ipv4
public-ipv4
public-ipv4-mode
subnet-mask
```

以下の例では、プライベートIPアドレスのゲートウェイを取得する方法を説明します。VPCモデルのみがこのデータをクエリできます。詳細については、[Virtual Private Cloud (VPC)](https://intl.cloud.tencent.com/document/product/215)をご参照ください。

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/local-ipv4s/10.104.13.59/gateway
10.15.1.1
```

以下の例では、プライベートIPアドレスがパブリックネットワークにアクセスするために使用するアクセスモードを取得する方法を説明します。VPCモデルのみがこのデータをクエリできます。クラシックネットワークタイプの CVMインスタンスは、パブリックネットワークゲートウェイを介してパブリックネットワークにアクセスします。　　

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/local-ipv4s/10.104.13.59/public-ipv4-mode
NAT
```

以下の例では、プライベートIPアドレスにバインドされたパブリックIPアドレスを取得する方法を説明します。

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/local-ipv4s/10.104.13.59/public-ipv4
139.199.11.29
```

以下の例では、プライベートIPアドレスのサブネットマスクを取得する方法を説明します。

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/local-ipv4s/10.104.13.59/subnet-mask
255.255.192.0
```

以下の例では、インスタンスの課金方法を取得する方法を説明します。

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/payment/charge-type
POSTPAID_BY_HOUR
```

以下の例では、インスタンスの作成時間を取得する方法を説明します。

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/payment/create-time
2018-09-18 11:27:33
```

以下の例では、インスタンスの終了時間を取得する方法を説明します。（前払いモードのみ）

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/payment/termination-time
2018-10-18 11:27:33
```

以下の例では、スポットインスタンスの終了時間を取得する方法を説明します。

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/spot/termination-time
2018-08-18 12:05:33
```

以下の例では、CVMが属するアカウントAppIdを取得する方法を説明します。

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/app-id
123456789
```
以下の例では、インスタンスが属するCAMロールによって生成された一時的な認証情報を取得する方法を説明します。CVMasはロール名です。
```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/cam/security-credentials/CVMas
{
  "TmpSecretId": "AKIDoQMxF8OPg0gA7pyZIA6cW447p225cIt9NW8dhA1dwl5UvxxxxxxxxxUqRlEb5_",
  "TmpSecretKey": "Q9z24VucjF4xQQNV64qwF6uWY71PEsH3exxxxxxxxxgA=",
  "ExpiredTime": 1615590047,
  "Expiration": "2021-03-12T23:00:47Z",
  "Token": "xxxxxxxxxxx",
  "Code": "Success"
}
```

## インスタンスユーザーデータのクエリ
インスタンスの作成時にインスタンスユーザーデータを指定できます。 cloud-init が設定されたCVMインスタンスはこのデータにアクセスできます。

### ユーザーデータの検索
ログイン後、以下の方法でユーザーデータにアクセスできます。

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/user-data
179, client, shanghai
```
