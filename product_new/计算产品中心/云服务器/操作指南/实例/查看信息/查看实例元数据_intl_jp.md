インスタンスメタデータは稼働するインスタンスのデータであり、稼動中のインスタンスの設定や管理に使われています。

>注：インスタンスの内部からのみインスタンスメタデータにアクセスできますが、データは暗号化によりプロテクションされていません。インスタンスにアクセスできる人員はメタデータを確認できます。そのため、適切な予防措置を講じて敏感なデータ（例えば永続的暗号化キーを利用する）を保護する必要があります。

## インスタンス meta-data
Tencent Cloudは下記のようなmeta-data情報を提供しています。

| データ | 説明 | 導入バージョン |
|---------|---------|---------|
| instance-id | インスタンス ID | 1.0 |
| uuid | インスタンス ID | 1.0 |
| local-ipv4 | インスタンスプライベートIP | 1.0 |
| public-ipv4 | インスタンスパブリックIP | 1.0 |
| mac | インスタンスeth0デバイスのmacアドレス | 1.0 |
| placement/region | インスタンスの所在するリージョンの情報 | 1.1 |
| placement/zone | インスタンスの所在するアベイラビリティーゾーンの情報 | 1.1 |
| network/network/macs/**mac**/mac | インスタンスのネットワークインターフェースデバイスアドレス | 1.2 |
| network/network/macs/**mac**/primary-local-ipv4 | インスタンスのネットワークインターフェースのプライマリプライベートIPアドレス | 1.2 |
| network/network/macs/**mac**/public-ipv4s | インスタンスのネットワークインターフェースのパブリックIPアドレス | 1.2 |
| network/network/macs/**mac**/local-ipv4s/**local-ipv4**/gateway | インスタンスネットワークインターフェースのゲートウェイアドレス | 1.2 |
| network/network/macs/**mac**/local-ipv4s/**local-ipv4**/local-ipv4 | インスタンスネットワークインターフェースのプライベートIPアドレス | 1.2 |
| network/network/macs/**mac**/local-ipv4s/**local-ipv4**/public-ipv4 | インスタンスネットワークインターフェースのパブリックIPアドレス | 1.2 |
| network/network/macs/**mac**/local-ipv4s/**local-ipv4**/public-ipv4-mode | インスタンスネットワークインターフェースのパブリックモード | 1.2 |
| network/network/macs/**mac**/local-ipv4s/**local-ipv4**/subnet-mask | インスタンスネットワークインターフェースのサブネットマスク | 1.2 |

> 上記テーブルにおける太字の **mac** と **local-ipv4** フィールドはそれぞれインスタンスの指定したネットワークインターフェースのデバイスアドレスとプライベートIPアドレスを示しています。
> 
> リクエストするターゲットURLアドレスは、大文字・小文字を区分けする必要があります。リクエストの返信結果に基づき新しいリクエストのターゲットURLアドレスを作成してください。

## インスタンスメタデータのクエリー
インスタンスメタデータに対する操作は全部**インスタンス内部**からのみ実行できます。先にインスタンスログインの関連操作を行ってください。インスタンスログインに関する詳細内容は、 [ Windows インスタンスのログイン](/doc/product/213/5435) 及び [ Linux インスタンスのログイン](/doc/product/213/5436)をご参照ください。

### 提供されているすべてのmeta-dataタイプのクエリー
コマンド：
```
curl http://metadata.tencentyun.com/
```
戻り値が下記の通りです
![](http://mccdn.qcloud.com/img56a1ebcbd924d.png)

コマンド：

```
curl http://metadata.tencentyun.com/meta-data
```
戻り値が下記の通りです
![](http://mccdn.qcloud.com/img56a1ed1128bd4.png)

その内、placementフィールドはregionとzoneの2種類のデータを含んでいます。

コマンド：

```
curl http://metadata.tencentyun.com/meta-data/placement
```
戻り値が下記の通りです
![](http://mccdn.qcloud.com/img56a1edb2b1349.png)



### インスタンスのプライベートIPのクエリー
コマンド：
```
curl http://metadata.tencentyun.com/meta-data/local-ipv4
```
戻り値が下記の通りです
![](http://mccdn.qcloud.com/img56a1eeb9557a8.png)

### インスタンスのパブリックIPのクエリー
コマンド：
```
curl http://metadata.tencentyun.com/meta-data/public-ipv4
```
戻り値が下記の通りです
![](http://mccdn.qcloud.com/img56a1f015c48e5.png)

### インスタンスIDのクエリー
コマンド：
```
curl http://metadata.tencentyun.com/meta-data/instance-id
```
或いは
```
curl http://metadata.tencentyun.com/meta-data/uuid
```
戻り値が下記の通りです
![](http://mccdn.qcloud.com/img56a1f1c703176.png)
![](http://mccdn.qcloud.com/img56a1f35d0bb18.png)

### インスタンスeth0のデバイスアドレスのクエリー
コマンド：
```
curl http://metadata.tencentyun.com/meta-data/mac
```
戻り値が下記の通りです
![](http://mccdn.qcloud.com/img56a1f2800a4e2.png)

### インスタンスの所在するリージョンのクエリー
コマンド：
```
curl http://metadata.tencentyun.com/meta-data/placement/region
```
戻り値が下記の通りです
![](http://mccdn.qcloud.com/img56a1f3ecd50a2.png)

### インスタンスの所在するアベイラビリティーゾーンのクエリー
コマンド：
```
curl http://metadata.tencentyun.com/meta-data/placement/zone
```
戻り値が下記の通りです
![](http://mccdn.qcloud.com/img56a1f45687788.png)

### インスタンスのネットワークインターフェースのクエリー
コマンド：
```
curl http://metadata.tencentyun.com/meta-data/network/
```
戻り値が下記の通りです：
 ![](https://mc.qcloudimg.com/static/img/ca12b20583f602d75a541d1a43452c2d/8.1.jpg)

コマンド：
```
curl http://metadata.tencentyun.com/meta-data/network/interfaces/macs
```
戻り値が下記の通りです：
 ![](https://mc.qcloudimg.com/static/img/ced32a2fee5e5282cd038d4034fb11a0/8.2.jpg)

### インスタンスネットワークインターフェースの詳細情報のクエリー
コマンド：
```
curl http://metadata.tencentyun.com/meta-data/network/interfaces/macs/52:54:00:13:5C:6C/
```
戻り値が下記の通りです：
 ![](https://mc.qcloudimg.com/static/img/4ee3cd5e1bcba00e846282aab4e352a0/9.jpg)

### インスタンスネットワークインターフェースのプライベートIPアドレスリストのクエリー
コマンド：
```
curl http://metadata.tencentyun.com/meta-data/network/interfaces/macs/52:54:00:13:5C:6C/local-ipv4s
```
戻り値が下記の通りです：
 ![](https://mc.qcloudimg.com/static/img/8a7e0b0e41a65b683f2f530131a45d07/10.jpg)

### インスタンスネットワークインターフェースのデバイスアドレスのクエリー
コマンド：
```
curl http://metadata.tencentyun.com/meta-data/network/interfaces/macs/52:54:00:13:5C:6C/mac
```
戻り値が下記の通りです：
 ![](https://mc.qcloudimg.com/static/img/0627af2fbc1aada52f5821f92d200f44/11.jpg)

### インスタンスネットワークインターフェースのプライベートIPアドレスリストのクエリー
コマンド：
```
curl http://metadata.tencentyun.com/meta-data/network/interfaces/macs/52:54:00:13:5C:6C/primary-local-ipv4
```
戻り値が下記の通りです：
![](https://mc.qcloudimg.com/static/img/5458ecf47ec14ba9151e95d7eaa2efd4/12.jpg)

### インスタンスネットワークインターフェースのパブリックIPアドレスリストのクエリー
コマンド：
```
curl http://metadata.tencentyun.com/meta-data/network/interfaces/macs/52:54:00:13:5C:6C/public-ipv4s
```
戻り値が下記の通りです：
![](https://mc.qcloudimg.com/static/img/19fa044afd25b8714b38312c7b3eef6c/13.jpg)

### インスタンスネットワークインターフェースのネットワーク情報のクエリー
コマンド：
```
curl http://metadata.tencentyun.com/meta-data/network/interfaces/macs/52:54:00:13:5C:6C/local-ipv4s/10.104.187.40/
```
戻り値が下記の通りです：
 ![](https://mc.qcloudimg.com/static/img/5c0b23aa98661c533b2ee9cfae3a79cd/14.jpg)

### インスタンスネットワークインターフェースのゲートウェイアドレスのクエリー
コマンド：
```
curl http://metadata.tencentyun.com/meta-data/network/interfaces/macs/52:54:00:13:5C:6C/local-ipv4s/10.104.187.40/gateway
```
戻り値が下記の通りです：
 ![](https://mc.qcloudimg.com/static/img/d297cd00f025c845111a50ee9874612d/15.jpg)

### インスタンスネットワークインターフェースのプライベートIPアドレスのクエリー
コマンド：
```
curl http://metadata.tencentyun.com/meta-data/network/interfaces/macs/52:54:00:13:5C:6C/local-ipv4s/10.104.187.40/local-ipv4
```
戻り値が下記の通りです：
 ![](https://mc.qcloudimg.com/static/img/24470fccb042eb877763a03100da8a10/16.jpg)

### インスタンスネットワークインターフェースのパブリックIPアドレスのクエリー
コマンド：
```
curl http://metadata.tencentyun.com/meta-data/network/interfaces/macs/52:54:00:13:5C:6C/local-ipv4s/10.104.187.40/public-ipv4
```
戻り値が下記の通りです：
 ![](https://mc.qcloudimg.com/static/img/c0344e7c89ab0643884d8ac2b859711b/17.jpg)

### インスタンスネットワークインターフェースのパブリックモードのクエリー
コマンド：
```
curl http://metadata.tencentyun.com/meta-data/network/interfaces/macs/52:54:00:13:5C:6C/local-ipv4s/10.104.187.40/public-ipv4-mode
```
戻り値が下記の通りです：
 ![](https://mc.qcloudimg.com/static/img/115617733703e99602627bb3ce1f32cc/18.jpg)

> 備考：
- NAT: Network Address Translationであり、ネットワークアドレスの変換です。
- direct: 直接に接続するネットワークであり、インスタンスネットワークインターフェースのパブリックIPアドレスを介して直接にパブリックネットワークにアクセスします。

### インスタンスネットワークインターフェースのサブネットマスクのクエリー
コマンド：
```
curl http://metadata.tencentyun.com/meta-data/network/interfaces/macs/52:54:00:13:5C:6C/local-ipv4s/10.104.187.40/subnet-mask
```
戻り値が下記の通りです:
 ![](https://mc.qcloudimg.com/static/img/ca9589a75e2a04859e3004e4b72ee967/19.jpg)
