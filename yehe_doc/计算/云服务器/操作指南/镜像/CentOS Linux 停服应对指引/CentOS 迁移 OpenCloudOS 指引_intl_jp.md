## ユースケース
次の表に示すように、CentOSはCentOS 8のメンテナンスを終了しました。詳細については、[CentOS公式発表](https://blog.centos.org/2020/12/future-is-centos-stream/?spm=a2c4g.11174386.n2.3.348f4c07hk46v4)をご参照ください。

| OSバージョン | メンテナンスの停止時間 | 	使用者への影響 |
|---------|---------|---------|
| CentOS 8 | 202年01月01日|メンテナンスが終了すると、問題の修正や機能の更新を含むソフトウェアのメンテナンスやサポートを受けることができなくなります。|

CentOS8インスタンスを使用している場合は、このドキュメントを参照してOpenCloudOS 8に入れ替えてください。
## バージョン説明
###　移行元サーバーでサポートされるOSバージョン

| 名称| バージョン | 
|---------|---------|
| CentOS 8シリーズをサポートします|　CentOS 8.0 64ビット、CentOS 8.2 64ビット、CentOS 8.3 64ビット、CentOS 8.4 64ビット、CentOS 8.2 ARM 64ビット。| 

###　移行元サーバーの推奨OSバージョン
-　CentOS 8シリーズの場合は、OpenCloudOS 8に移行することをお勧めします。
-　CentOS stream 8パブリックイメージは、移行操作を一時的にサポートしません。

## 注意事項
- 移行は次の場合にはサポートされません
 - グラフィカルインターフェイスがインストールされた場合。
 - i686のrpmパッケージがインストールされた場合。
- 次のような場合は移行後のビジネスが正常に機能しなくなる場合があります
 - ビジネスプログラムにはサードパーティ製のrpmパッケージにインストールされ、それに依存している場合。
 - ビジネスプログラムが特定のバージョンのカーネルに依存しているか、独自にカーネルモジュールをコンパイルしている場合。移行後のターゲットバージョンは5.4カーネルベースのtkernel4です。このバージョンは、CentOS 8のカーネルバージョンよりも更新されており、新しいバージョンでは古い機能が変更される可能性があります。カーネルに強く依存しているユーザーは、依存する機能を理解するか、OpenCloudOSコミュニティ[Bugtracker](https://bugs.opencloudos.tech/)にお問い合わせることをお勧めします。
 -　ビジネスプログラムは一定のgccバージョンに依存しており、現在OpenCloudOS 8にはgcc 8.5がデフォルトでインストールされています。
- 移行が終了したら、OpenCloudOSカーネルに入るには再起動する必要があります。
- 移行はディスクに影響がなくOSレベルのアップグレードだけで、他の操作が実行されません。

## リソース要件
- 利用可能なメモリが500MB以上。
- システムディスクの空き容量が10GB以上。

## 操作手順
[](id:Prepare)
###　移行準備
1.　移行操作は可逆的ではありません。ビジネスデータの安全性を確保するために、移行を実行する前にデータをバックアップすることをお勧めします。Tencent CVMのユーザーは、システムディスクのデータのバックアップについて[スナップショットの作成](https://intl.cloud.tencent.com/document/product/362/5755)をご参照ください。
2.　i686のrpmパッケージをチェックし、手動でアンインストールします。
3.　環境にPython 3がインストールされていない場合は、Python 3をインストールする必要があります。vaultソースを使用してインストールできます。
```plaintexy
# cat <<EOF | sudo tee /tmp/centos8_vault.repo
[c8_vault_baseos]
name=c8_vault - BaseOS
baseurl=https://mirrors.cloud.tencent.com/centos-vault/8.5.2111/BaseOS/\$basearch/os/
gpgcheck=0
enabled=1
[c8_vault_appstream]
name=c8_vault - AppStream
baseurl=https://mirrors.cloud.tencent.com/centos-vault/8.5.2111/AppStream/\$basearch/os/
gpgcheck=0
enabled=1
EOF
# yum -y install python3 --disablerepo=* -c /tmp/centos8_vault.repo --enablerepo=c8_vault*
```

### 移行の実行
**CentOS 8からOpenCloudOS 8への移行手順は次のとおりです**
1. 移行先ホストにログインします。Tencent CVMのユーザーは、詳細について[標準ログイン方式を使用してLinuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/5436)をご参照ください。
2. 次のコマンドを実行して、Python 3をインストールします。yumソースが使用できない場合は、上記の**移行準備**の第3項の[centos-vaultソースを使用してPython 3をインストール](#Prepare)してください。
```plaintexy
yum install -y python3
```
3. 移行ツールのダウンロードとインストールには以下のコマンドを実行します。
```plaintexy
#x86バージョン
wget https://mirrors.opencloudos.tech/opencloudos/8.6/AppStream/x86_64/os/Packages/migrate2opencloudos-1.0-1.oc8.noarch.rpm
#armバージョン
wget https://mirrors.opencloudos.tech/opencloudos/8/AppStream/aarch64/os/Packages/migrate2opencloudos-1.0-1.oc8.noarch.rpm 
```
4. 移行ツールのインストールには以下のコマンドを実行します。このコマンドは、/usr/sbinの下でmigrate2opencloudos.pyを作成します。
```plaintexy
rpm -ivh migrate2opencloudos-1.0-1.oc8.noarch.rpm
```
5. 移行の開始には以下のコマンドを実行します。
```plaintexy
python3 /usr/sbin/migrate2opencloudos.py -v 8
```
移行には時間がかかります。しばらくお待ちください。スクリプトの実行が完了し、次の図に示すような情報が出力されると、移行が完了したことを意味します。
![](https://qcloudimg.tencent-cloud.cn/raw/c0118f0b4c20ee45ace4258b44238da2.png)
6. インスタンスを再起動します。CVMの詳細については、 [インスタンスの再起動](https://intl.cloud.tencent.com/document/product/213/4928)をご参照ください。
7. 移行結果のチェック。
 - os-releaseのチェックには以下のコマンドを実行します。
```plaintexy
cat /etc/os-release
```
下図に示す情報を返します：
![](https://qcloudimg.tencent-cloud.cn/raw/c345e844566068d5035d32fd7af9401f.png)
 - カーネルのチェックには以下のコマンドを実行します。
```plaintexy
uname -r
```
下図に示す情報を返します：
![](https://qcloudimg.tencent-cloud.cn/raw/ed944b071b0a202763a2096ebf766533.png)
カーネルはデフォルトでyumの最新バージョンです。実際に返された結果を基準にしてください。このドキュメントでは、図のバージョンを例として説明します。
 - yumのチェックには以下のコマンドを実行します。
```plaintexy
yum makecache
```
下図に示す情報を返します：
![](https://qcloudimg.tencent-cloud.cn/raw/0e5dd8b1311c7f5b6522b201233bb1f9.png)

