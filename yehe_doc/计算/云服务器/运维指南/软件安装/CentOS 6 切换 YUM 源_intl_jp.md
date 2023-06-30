## 操作背景
CentOS 6のオペレーティングシステムバージョンのサポート（EOL）は、2020年11月30日に終了しており、Linuxコミュニティでは当該オペレーティングシステムのバージョンを今後はサポートしません。コミュニティのルールに従い、CentOS 6のソースアドレス `http://mirror.centos.org/centos-6/` は削除され、第三者のミラーサイトからもCentOS 6のソースが削除されています。`http://mirrors.tencent.com/`と`http://mirrors.tencentyun.com/`のソースをCentOS 6のソースに同期することができず、Tencent Cloudでデフォルト構成のCentOS 6のソースを使い続けるとエラーが発生します。

<dx-alert infotype="explain" title="">
オペレーティングシステムをCentOS 7以上にアップグレードすることを推奨します。業務の繁忙期に、なおCentOS 6のオペレーティングシステム上のいくつかのインストールパッケージを使用する必要がある場合は、本文で提供する情報を基にCentOS 6のリポジトリを切り替えてください。
</dx-alert>


## 操作手順
1. [標準方式を使用してLinuxインスタンスにログイン（推奨）](https://intl.cloud.tencent.com/document/product/213/5436)します。実際の操作方法に応じて、他のログイン方法を選択することもできます。
	- [リモートログインソフトウェアを使用してLinuxインスタンスにログイン] (https://intl.cloud.tencent.com/document/product/213/32502)
	- [SSHを使用してLinuxインスタンスにログイン] (https://intl.cloud.tencent.com/document/product/213/32501)
2. 以下のコマンドを実行して、現在のオペレーティングシステムのCentOSバージョンを確認します。
```shellsession
cat /etc/centos-release
```
返送結果が下図に示すとおりなら、現在のオペレーティングシステムバージョンがCentOS 6.9であることを示します。
![](https://main.qcloudimg.com/raw/de65529a43dc5bfee695c08d5f7bff80.png)
3. 以下のコマンドを実行して、 `CentOS-Base.repo`ファイルを編集します。
```shellsession
vim /etc/yum.repos.d/CentOS-Base.repo 
```
4. **i** を押して編集モードに入り、 CentOSバージョンおよびネットワーク環境に従ってbaseurlを修正します。
<dx-alert infotype="explain" title="">
[プライベートネットワークサービス](https://intl.cloud.tencent.com/document/product/213/5225) および[パブリックネットワークサービス](https://intl.cloud.tencent.com/document/product/213/5224)を参照して、インスタンスが使用する必要のあるリポジトリを決定できます。
- プライベートネットワークでアクセスするには：`http://mirrors.tencentyun.com/centos-vault/6.x/`リポジトリに切り替える必要があります。
- パブリックネットワークでアクセスするには：`http://mirrors.tencent.com/centos-vault/6.x/`リポジトリに切り替える必要があります。
</dx-alert>
ここでは、インスタンスオペレーティングシステムをCentOS 6.9として、プライベートネットワークのアクセス使用について例示します。修正完了後の<code>CentOS-Base.repo</code>ファイルは下図のとおりです。
<img src="https://main.qcloudimg.com/raw/1d2485a9be0df6d5f7c46151fc50d73b.png"/>
設定は次のとおりで、必要に応じて取得できます。
```plaintext
[extras]
gpgcheck=1
gpgkey=http://mirrors.tencentyun.com/centos/RPM-GPG-KEY-CentOS-6
enabled=1
baseurl=http://mirrors.tencentyun.com/centos-vault/6.9/extras/$basearch/
name=Qcloud centos extras - $basearch
[os]
gpgcheck=1
gpgkey=http://mirrors.tencentyun.com/centos/RPM-GPG-KEY-CentOS-6
enabled=1
baseurl=http://mirrors.tencentyun.com/centos-vault/6.9/os/$basearch/
name=Qcloud centos os - $basearch
[updates]
gpgcheck=1
gpgkey=http://mirrors.tencentyun.com/centos/RPM-GPG-KEY-CentOS-6
enabled=1
baseurl=http://mirrors.tencentyun.com/centos-vault/6.9/updates/$basearch/
name=Qcloud centos updates - $basearch
```
5. **ESC**を押して**:wq** と入力した後、**Enter** を押して修正を保存します。
6. 以下のコマンドを実行して、 `CentOS-Epel.repo` ファイルを修正します。
```shellsession
vim /etc/yum.repos.d/CentOS-Epel.repo 
```
7. **i**を押して編集モードに入り、インスタンスネットワーク環境に基づきbaseurlを修正します。
ここでは、プライベートネットワークアクセスの使用を例に、 `baseurl=http://mirrors.tencentyun.com/epel/$releasever/$basearch/`を `baseurl=http://mirrors.tencentyun.com/epel-archive/6/$basearch/`に修正します。修正が完了すると以下のようになります。
![](https://main.qcloudimg.com/raw/9c4b3eaf65d005b3d6819f013037443d.png)
設定は次のとおりで、必要に応じて取得できます。
```plaintext
[epel]
name=epel for redhat/centos $releasever - $basearch
failovermethod=priority
gpgcheck=1
gpgkey=http://mirrors.tencentyun.com/epel/RPM-GPG-KEY-EPEL-6
enabled=1
baseurl=http://mirrors.tencentyun.com/epel-archive/6/$basearch/
```
8. **ESC**を押して**:wq** と入力した後、 **Enter**を押して修正を保存します。
9. これでYUMリポジトリの切り替えが完了しました。`yum install`コマンドを使用して必要なソフトウェアをインストールできます。


