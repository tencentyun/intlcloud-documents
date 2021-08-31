## 操作シナリオ
このドキュメントでは、CentOS 7.7のTencent Cloud CVMを例に、オープンソースツールExtundeleteを使用して誤って削除されたデータを迅速にリカバリする方法を紹介します。Extundeleteは、ext3およびext4のデュアル形式のパーティションリカバリをサポートし、強力な機能を備えています。このドキュメントは、誤ってディスクファイルを削除し、誤操作後にディスクへの書き込みなどの処理を行っていないユーザーに適用されます。
また、Tencent Cloudは、[スナップショットの作成](https://intl.cloud.tencent.com/document/product/362/5755)、[カスタムイメージの作成](https://intl.cloud.tencent.com/document/product/213/4942)および[Cloud Object Storage](https://intl.cloud.tencent.com/document/product/436/6222)などのデータストレージ方法も提供しています。データセキュリティを向上させるために、定期的にデータバックアップを行うことをお勧めします。

## 例のソフトウェアバージョン
- Linux：Linux OS。このドキュメントでは、CentOS 7.7を例として説明します。
- Extundelete：Linux ベースのオープンソースのデータリカバリソフトウェアです。このドキュメントでは、Extundelete 0.2.4を例として説明します。


## 操作手順
> 操作手順を実行する前に、[スナップショットの作成](https://intl.cloud.tencent.com/document/product/362/5755)および[カスタムイメージの作成](https://intl.cloud.tencent.com/document/product/213/4942)を参照してデータをバックアップし、問題が発生した場合にインスタンスを初期状態に回復できるようにしてください。
>

### Extundeleteのインストール
1. 次のコマンドを実行して、Extundeleteに必要な依存関係とライブラリをインストールします。
>!
>- Extundeleteにはlibext2fs 1.39以降のバージョンが必要です。
>- ext4形式をサポートする必要がある場合は、e1fsprogs 1.41以降のバージョンがインストールされていることを確認してください。バージョンを表示するには、`dumpe2fs`コマンドを実行してください。 
>
```
yum -y install  bzip2  e2fsprogs-devel  e2fsprogs  gcc-c++  make
```
2. [Extundelete](https://sourceforge.net/projects/extundelete/)インストールパッケージをダウンロードします。
3. 順に次のコマンドを実行して、Extundeleteインストールパッケージを解凍し、プログラムディレクトリに移動します。
```
tar -xvjf extundelete-0.2.4.tar.bz2
```
```
cd extundelete-0.2.4 
```
4. 順に次のコマンドを実行して、Extundeleteをコンパイルしてインストールします。
```
./configure   
```
```
make && make install
```
インストールが完了すると、 `usr/local/bin`ディレクトリに実行可能ファイル「extundelete」が表示されます。

### データリカバリのテスト
次の手順を参照して、データリカバリ手順を理解し、実際の状況に合わせて操作することができます。
1. [パーティション上でのファイルシステムの作成](https://intl.cloud.tencent.com/document/product/362/31597)を参照して、データディスクを初期化してパーティションを作成し、また次のコマンドを実行して、既存のディスクと使用可能なパーティションを確認します。
```
fdisk -l
```
返された結果は以下の通りです。
![](https://main.qcloudimg.com/raw/34abb1b0c7a1f6fb4ff233a42a781123.png)
2. 順に次のコマンドを実行して、新しいマウントポイントを作成し、パーティションをマウントします。このドキュメントでは、パーティション`/dev/vdb1`を`/test`にマウントする例について説明します。
```
mkdir /test
```
```
mount /dev/vdb1 /test
```
3. 順に次のコマンドを実行して、マウントポイントに「hello」テストファイルを作成します。
```
cd /test
```
```
echo test > hello
```
4. <span id="Step4"></span>次のコマンドを実行して、「hello」ファイルのMD5値を記録します。md5値は、元のファイルと復元されたファイルを検証するために使用できます。
```
md5sum hello
```
返された結果は次の通りです：
![](https://main.qcloudimg.com/raw/230d4c9a4456df8b3623c0bd401d878a.png)
5. 順に次のコマンドを実行して、「hello」ファイルを削除します。
```
rm -rf hello
```
```
cd ~
```
```
fuser -k /test
```
6. 次のコマンドを実行して、マウントされたパーティションをアンマウントします。
```
umount /dev/vdb1
```
7. 次のコマンドを実行して、パーティション内の誤って削除されたファイルを検索します。
```
extundelete --inode 2 /dev/vdb1
```
返された結果は以下の通りです。
![](https://main.qcloudimg.com/raw/97a64a2e0de658f4ed55500f162b1eb7.png)
8. 次のコマンドを実行して、Extundeleteを使用してファイルをリカバリします。
```
/usr/local/bin/extundelete  --restore-inode 12  /dev/vdb1
```
リカバリが完了すると、`RECOVERED_FILES`フォルダが兄弟ディレクトリの下に表示されます。
9. `RECOVERED_FILES`フォルダにアクセスし、リカバリされたファイルを確認し、次のコマンドを実行してMD5値を取得します。
```
md5sum Recovered file
```
取得したmd5値が[ステップ4](#Step4) で記録した「hello」ファイルの値と同じ場合、データリカバリに成功したことになります。
