インスタンスメタデータは、インスタンスに関連するデータを指します。実行中のインスタンスを構成または管理するために使用できます。

<dx-alert infotype="explain" title="">
インスタンスのメタデータにはログイン後にのみアクセスできますが、データは暗号化されていません。インスタンスにアクセスできる人員はいずれもそのメタデータを表示できます。そのため、機密データを保護するために適切な予防措置を講じる必要があります。
</dx-alert>

## インスタンスメタデータの分類
Tencent Cloudは現在、次のメタデータを提供しています。

<table>
<thead>
<tr>
<th>データ</th>
<th width="50%">説明</th>
<th width="15%">バージョン</th>
</tr>
</thead>
<tbody>
<tr>
<td>instance-id</td>
<td>インスタンスID</td>
<td>1.0</td>
</tr>
<tr>
<td>instance-name</td>
<td>インスタンス名</td>
<td>1.0</td>
</tr>
<tr>
<td>uuid</td>
<td>インスタンスID</td>
<td>1.0</td>
</tr>
<tr>
<td>local-ipv4</td>
<td >インスタンスのプライベートIP アドレス</td>
<td>1.0</td>
</tr>
<tr>
<td>public-ipv4</td>
<td>インスタンスのパブリックIPアドレス</td>
<td>1.0</td>
</tr>
<tr>
<td>mac</td>
<td>インスタンスのeth0デバイスの MAC アドレス</td>
<td>1.0</td>
</tr>
<tr>
<td>placement/region</td>
<td>インスタンスのリージョン</td>
<td>2017年9月19日更新</td>
</tr>
<tr>
<td>placement/zone</td>
<td>インスタンスのアベイラビリティーゾーン</td>
<td>2017 年9月19日更新</td>
</tr>
<tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/mac</td>
<td>インスタンスネットワークインターフェースのデバイスアドレス</td>
<td>1.0</td>
</tr>
<tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/primary-local-ipv4</td>
<td>インスタンスネットワークインターフェースのプライマリプライベートIPアドレス</td>
<td>1.0</td>
</tr>
<tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/public-ipv4s</td>
<td>インスタンスネットワークインターフェースのパブリックIPアドレス</td>
<td>1.0</td>
</tr>
<tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/vpc-id</td>
<td>インスタンスネットワークインターフェースのVPC ID</td>
<td>2017年9月19日更新</td>
</tr>
</tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/subnet-id</td>
<td>インスタンスネットワークインターフェースのサブネットID</td>
</tr>
<tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/local-ipv4s/<strong>${local-ipv4}</strong>/gateway</td>
<td>network/interfaces/macs/<strong>${mac}</strong>/local-ipv4s/<strong>${local-ipv4}</strong>/gateway</td>
<td>インスタンスネットワークインターフェースのゲートウェイアドレス</td>
<td>1.0</td>
</tr>
<tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/local-ipv4s/<strong>${local-ipv4}</strong>/local-ipv4</td>
<td>1.0</td>
</tr>
<tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/local-ipv4s/<strong>${local-ipv4}</strong>/public-ipv4</td>
| network/interfaces/macs/**${mac}**/local-ipv4s/**${local-ipv4}**/public-ipv4 | インスタンスのネットワークインターフェースのパブリックIPアドレス | 1.0 |
<td>インスタンスネットワークインターフェースのパブリックIPアドレス</td>
<td>1.0</td>
</tr>
<tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/local-ipv4s/<strong>${local-ipv4}</strong>/public-ipv4-mode</td>
<td>インスタンスネットワークインターフェースのパブリックネットワークモード</td>
<td>1.0</td>
</tr>
<tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/local-ipv4s/<strong>${local-ipv4}</strong>/subnet-mask</td>
<td>インスタンスネットワークインターフェースのサブネットマスク</td>
<td>1.0</td>
</tr>
<tr>
<td>payment/charge-type</td>
<td>インスタンスの料金プラン</td>
<td>2017年9月19日更新</td>
</tr>
<tr>
<td>payment/create-time</td>
<td>インスタンスの作成時間</td>
<td>2017年9月19日更新</td>
</tr>
</tr>
<td>payment/termination-time</td>
<td>インスタンスの終了時間</td>
<td>2017年9月19日更新</td>
</tr>
<tr>
<td>app-id</td>
<td>インスタンスが属するユーザーの AppId</td>
<td>2017年9月19日更新</td>
</tr>
<tr>
<td>as-group-id</td>
<td>インスタンスのAuto ScalingグループID</td>
<td>2017年9月19日更新</td>
</tr>
<tr>
<td>spot/termination-time</td>
<td>スポットインスタンスの終了時間</td>
<td>2017年9月19日更新</td>
</tr>
<tr>
<td>instance/instance-type</td>
<td>インスタンス仕様</td>
<td>2017年9月19日更新</td>
</tr>
<tr>
<td>instance/image-id</td>
<td>インスタンスのイメージ ID</td>
<td>2017年9月19日更新</td>
</tr>
<tr>
<td>instance/security-group</td>
<td>インスタンスに関連付けられているセキュリティグループの情報</td>
<td>2017年9月19日更新</td>
</tr>
<tr>
<td>instance/bandwidth-limit-egress</td>
<td>インスタンスのプライベートネットワークの送信帯域幅制限(Kbit/s)</td>
<td>2019年9月29日更新</td>
</tr>
<tr>
<td>instance/bandwidth-limit-ingress</td>
<td>インスタンスのプライベートネットワークの受信帯域幅制限(Kbit/s)</td>
<td>2019年9月29日更新</td>
</tr>
<tr>
<td>cam/security-credentials/${role-name}</td>
<td>CAMロールポリシーによって生成される一時的な認証情報。インスタンスがCAMロールに関連付けられている場合にのみ取得できます。 ${role-name} を実際のCAMロール名に変更する必要があります。それ以外の場合は、`404` が返されます。</td>
<td>2019年12月11日更新</td>
</tr>
<tr>
<td>volumes</td>
<td>インスタンス ストレージ</td>
<td>1.0</td>
</tr>
</tbody></table>



<dx-alert infotype="explain" title="">
- 上記テーブルにおける`${mac}` および `${local-ipv4}`フィールドはそれぞれインスタンスに指定されたネットワークインターフェースのMACアドレスとプライベートIPアドレスを表します。
- リクエストの宛先URLアドレスは、大文字と小文字を区別する必要があります。返されたリクエストの結果に従って、新しいリクエストの宛先URLアドレスを作成する必要があります。
- 返された配置データは、新しいバージョンで変更されています。以前のバージョンのデータを使用する必要がある場合、以前のバージョンのパスを指定するか、バージョンのパスを指定しないことによりバージョン1.0のデータにアクセスすることができます。返された配置データの詳細については、[リージョンとアベイラビリティーゾーン](https://intl.cloud.tencent.com/document/product/213/6091)をご参照ください。
</dx-alert>



## インスタンスメタデータのクエリ
インスタンスにログインすると、インスタンスのローカルIPアドレスやパブリックIPアドレスなどのメタデータにアクセスして、外部アプリケーションとの接続を管理できます。
実行中のインスタンス内部からすべてのカテゴリーのインスタンスメタデータを確認するには、次のURIを使用してください。

```shell
http://metadata.tencentyun.com/latest/meta-data/
```
cURLツールまたはHTTP GETリクエストを介してメタデータにアクセスできます。例：

```shell
curl http://metadata.tencentyun.com/latest/meta-data/
```
* リソースが存在しない場合、HTTPエラーコード「404 Not Found」が返されます。
* メタデータ関連の操作はすべて、**インスタンスにログインした後**のみ実行できます。詳細については、 [Windowsインスタンスへのログイン](https://www.tencentcloud.com/document/product/213/32495)または [Linuxインスタンスへのログイン](https://www.tencentcloud.com/document/product/213/32493)をご参照ください。

### メタデータクエリ例

以下の例では、メタデータのバージョン情報を取得する方法を説明します。

<dx-alert infotype="notice" title="">
Tencent Cloudがメタデータのアクセスパスまたは返されたデータを変更する時、新しいメタデータのバージョンをリリースします。お客様のアプリケーションプログラムまたはスクリプトが以前のバージョンの構造または返されたデータに依存している場合、指定された初期のバージョンを使用してメタデータにアクセスできます。バージョンを指定しない場合、デフォルトでバージョン1.0がアクセスされます。
</dx-alert>



```shell
[qcloud-user]# curl http://metadata.tencentyun.com/
1
2017/9/19
latest
meta-data
```

以下の例では、メタデータのバージョン情報を取得する方法を説明します。そのうち「/」で終わる単語はディレクトリを表し、「/」で終わらない単語はアクセスデータを表します。具体的なアクセスデータの意味は、前文の**インスタンスメタデータの分類**をご参照ください。

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
10.104.13.59
```

以下の例では、インスタンスのパブリックIPアドレスを取得する方法を説明します。

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/public-ipv4
139.199.11.29
```

以下の例では、インスタンス ID を取得する方法を説明します。インスタンスIDはインスタンスの一意の識別子です。

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

以下の例では、プライベートIPアドレスの情報を取得する方法を説明します。VPCモデルのみがこのデータをクエリできます。VPCモデルの詳細については、 [Virtual Private Cloud (VPC](https://www.tencentcloud.com/document/product/215)をご参照ください。

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
2018/9/18 11:27:33
```

以下の例では、スポットインスタンスの終了時間を取得する方法を説明します。

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/spot/termination-time
2018/8/18 12:05:33
```

以下の例では、CVMが属するアカウントAppIdを取得する方法を説明します。

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/app-id
123456789
```

以下の例では、インスタンスが属する CAM ロールによって生成された一時的な認証情報を取得する方法を説明します。この例では、ロール名は「CVMas」です。
```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/cam/security-credentials/CVMas
{
  "TmpSecretId": "AKIDoQMxA6cW447p225cIt9NW8dhA1dwl5UvxxxxxxxxxUqRlEb5_",
  "TmpSecretKey": "Q9z24VucjF4xQQN1PEsH3exxxxxxxxxgA=",
  "ExpiredTime": 1615590047,
  "Expiration": "2021-03-12T23:00:47Z",
  "Token": "xxxxxxxxxxx",
  "Code": "Success"
}
```
以下の例では、インスタンスストレージをクエリする方法を説明します。
```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/volumes
disk-xxxxxxxx/
```
## インスタンスユーザーデータのクエリ
インスタンスの作成時にインスタンスユーザーデータを指定できます。 cloud-initが設定されたCVMインスタンスはこのデータにアクセスできます。

### ユーザーデータの検索
インスタンスにログイン後、以下の方法でユーザーデータにアクセスできます。

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/user-data
179, client, shanghai
```