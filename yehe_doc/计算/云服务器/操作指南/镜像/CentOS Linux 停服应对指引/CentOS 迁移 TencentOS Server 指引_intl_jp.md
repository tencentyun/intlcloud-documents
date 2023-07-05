## ユースケース
CentOSは、CentOS Linuxプロジェクトのメンテナンスを正式に停止する予定があります。CentOS 8とCentOS 7のメンテナンスを次の表に示します。詳細については、[CentOS公式発表](https://blog.centos.org/2020/12/future-is-centos-stream/?spm=a2c4g.11174386.n2.3.348f4c07hk46v4)をご参照ください。
<table>
<tr>
<th>OSバージョン</th>
<th>メンテナンス停止時間</th>
<th>使用者への影響</th>
</tr>
<tr>
<td>CentOS 8</td>
<td>2022年01月01日</td>
<td rowspan=2>メンテナンスを停止すると、問題の修正や機能の更新を含むソフトウェアのメンテナンスやサポートを受けることができなくなります。</td>
</tr>
<tr>
<td>CentOS 7</td>
<td>2024年06月30日</td>
</tr>
</table>

それを考慮して、新しいCVMインスタンスを購入する場合は、TencentOS Serverイメージを使用することをお勧めします。CentOSインスタンスを使用している場合は、このドキュメントを参照してTencentOS Serverに入れ替えてください。


## バージョン説明
**移行元サーバーでサポートされるオペレーティングシステムのバージョン**：
- 次のCentOS 7シリーズをサポートします。
  - CentOS 7.2 64ビット、CentOS 7.3 64ビット、CentOS 7.4 64ビット、CentOS 7.5 64ビット、CentOS 7.6 64ビット、CentOS 7.7 64ビット、CentOS 7.8 64ビット、CentOS 7.9 64ビット
- 次のCentOS 8シリーズをサポートします：
  - CentOS 8.0 64ビット、CentOS 8.2 64ビット、CentOS 8.4 64ビット

**移行元サーバーの推奨OS**：
- CentOS 7シリーズはTencentOS Server 2.4(TK4)へ移行することをお勧めします。
- CentOS 8シリーズはTencentOS Server 3.1(TK4)へ移行することをお勧めします。

<dx-alert infotype="notice" title="">
CentOS 7.2およびCentOS 7.3のパブリックイメージにはデフォルトで32ビットパッケージが含まれている場合があるため、アップグレードを実行する前に手動で削除する必要があります。
</dx-alert>



## 注意事項
- 移行は次の場合にはサポートされません：
 - グラフィカルインターフェイスがインストールされた場合。
 - i686のrpmパッケージがインストールされた場合。
- 次のような場合は移行後のビジネスが正常に機能しなくなる場合があります：
 - ビジネスプログラムにはサードパーティ製のrpmパッケージにインストールされ、それに依存している場合。
 - ビジネスプログラムが特定のバージョンのカーネルに依存しているか、独自にカーネルモジュールをコンパイルしている場合。
移行後のターゲットバージョンは5.4カーネルベースのtkernel4です。このバージョンは、CentOS 7およびCentOS 8のカーネルバージョンよりも更新されており、新しいバージョンでは古い機能が変更される場合があります。
 - ビジネスプログラムは特定のgccバージョンに依存している場合。
現在、TencentOS Server　2.4にはgcc 4.8.5がデフォルトでインストールされ、TencentOS Server　3.1にはgcc 8.5がデフォルトでインストールされています。
- 移行が終了したら、TencentOS　Serverカーネルに入るには再起動する必要があります。
- 移行はディスクに影響がなくOSレベルのアップグレードだけで、他の操作が実行されません。

## リソース要件
- 利用可能なメモリが500MB以上。
- システムディスクの空き容量が10GB以上。

## 操作手順

###　移行準備
1.　移行操作は可逆的ではありません。ビジネスデータの安全性を確保するために、移行を実行する前に[スナップショットの作成](https://intl.cloud.tencent.com/document/product/362/5755)を使用してシステムディスクのデータをバックアップすることをお勧めします。
2.　i686のrpmパッケージをチェックし、手動でアンインストールします。

### 移行の実行
<dx-tabs>
::: CentOS 7シリーズはTencentOS Server 2.4（TK4）へ移行します
1. 移行先CVMにログインします。詳細については、[標準ログイン方式を使用してLinuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/5436)をご参照ください。
2. 次のコマンドを実行して、Python 3をインストールします。
```shell
yum install -y python3
```
3. 移行ツールの取得には以下のコマンドを実行します。
```shell
wget http://mirrors.tencent.com/tencentos/2.4/tlinux/x86_64/RPMS/migrate2tencentos-1.0-4.tl2.noarch.rpm
```
4. 移行ツールのインストールには以下のコマンドを実行します。このコマンドは、/usr/sbinの下でmigrate2tencentos.pyを作成します。
```shell
rpm -ivh migrate2tencentos-1.0-4.tl2.noarch.rpm
```
5. 移行の開始には以下のコマンドを実行します。
```shell
python3 /usr/sbin/migrate2tencentos.py -v 2.4
```
移行には時間がかかります。しばらくお待ちください。スクリプトの実行が完了し、次の図に示すような情報が出力されると、移行が完了したことを意味します。
![](https://qcloudimg.tencent-cloud.cn/raw/a5d1a2cc65970b98b51071f6c90a40f5.png)
6. インスタンスを再起動します。詳細については、 [インスタンスの再起動](https://intl.cloud.tencent.com/document/product/213/4928)をご参照ください。
7. 移行結果のチェック。 
   1. os-releaseのチェックには以下のコマンドを実行します。
```shell
cat /etc/os-release
```
下図に示す情報を返します：
![](https://qcloudimg.tencent-cloud.cn/raw/11ae97a1ed88d3a6e6ddfddc369b2574.png)
   2. カーネルのチェックには以下のコマンドを実行します。
```shell
uname -r
```
下図に示す情報を返します：
![](https://qcloudimg.tencent-cloud.cn/raw/cb34dbe478757069a4d3136a9384f711.png)
<dx-alert infotype="explain" title="">
カーネルはデフォルトでyumの最新バージョンです。実際に返された結果を基準にしてください。このドキュメントでは、図のバージョンを例として説明します。
</dx-alert>
  3. yumのチェックには以下のコマンドを実行します。
```shell
yum makecache
```
下図に示す情報を返します：
![](https://qcloudimg.tencent-cloud.cn/raw/88b9468bed347c567223385b3df161b4.png)


:::
::: CentOS 8シリーズはTencentOS  3.1（TK4）へ移行します。
1. 移行先CVMにログインします。詳細については、[標準ログイン方式を使用してLinuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/5436)をご参照ください。
2. 次のコマンドを実行して、Python 3をインストールします。
```shell
yum install -y python3
```
3. 移行ツールの取得には以下のコマンドを実行します。
```shell
wget http://mirrors.tencent.com/tlinux/3.1/Updates/x86_64/RPMS/migrate2tencentos-1.0-4.tl3.noarch.rpm
```
4. 移行ツールのインストールには以下のコマンドを実行します。このコマンドは、/usr/sbinの下でmigrate2tencentos.pyを作成します。
```shell
rpm -ivh migrate2tencentos-1.0-4.tl3.noarch.rpm
```
5. 移行の開始には以下のコマンドを実行します。
```shell
python3 /usr/sbin/migrate2tencentos.py -v 3.1
```
移行には時間がかかります。しばらくお待ちください。スクリプトの実行が完了し、次の図に示すような情報が出力されると、移行が完了したことを意味します。
![](https://qcloudimg.tencent-cloud.cn/raw/e272e5f6e5eba50a1e9bc74db536a592.png)
6. インスタンスを再起動します。詳細については、 [インスタンスの再起動](https://intl.cloud.tencent.com/document/product/213/4928)をご参照ください。
7. 移行結果のチェック。 
   1. os-releaseのチェックには以下のコマンドを実行します。
```shell
cat /etc/os-release
```
下図に示す情報を返します：
![](https://qcloudimg.tencent-cloud.cn/raw/eb7333c8badf5d7a4852a66084fcc190.png)
   2. カーネルのチェックには以下のコマンドを実行します。
```shell
uname -r
```
下図に示す情報を返します：
![](https://qcloudimg.tencent-cloud.cn/raw/9bba4c6112c4bec1482d827ad02a39d6.png)
<dx-alert infotype="explain" title="">
カーネルはデフォルトでyumの最新バージョンです。実際に返された結果を基準にしてください。このドキュメントでは、図のバージョンを例として説明します。
</dx-alert>
  3. yumのチェックには以下のコマンドを実行します。
```shell
yum makecache
```
下図に示す情報を返します：
![](https://qcloudimg.tencent-cloud.cn/raw/83a6ec7fc69ab6bd26e9ff1cf0f443da.png)

:::
</dx-tabs>



