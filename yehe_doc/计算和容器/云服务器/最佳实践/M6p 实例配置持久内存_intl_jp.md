## 概要
ここでは、M6pインスタンスで永続メモリを構成する方法についてご説明します。


##インスタンス構成
ここでは、次の構成のCVMインスタンスを使用します。取得に関する情報については、実際の状況によります。
 - **インスタンス仕様**：メモリ型M6pインスタンスM6p.LARGE16（4 コア 16GB）。その他の仕様については、[メモリ型 M6p](https://intl.cloud.tencent.com/document/product/213/11518)をご参照ください。
 - **オペレーティングシステム**： TencentOS Server 3.1(TK4)。
<dx-alert infotype="explain" title="">
インスタンスには、次のオペレーティングシステムを使用することをお勧めします。
 - TencentOS Server 3.1
 - CentOS 7.6およびそれ以降のバージョン
 - Ubuntu 18.10およびそれ以降のバージョン
</dx-alert>

##  前提条件
[M6pインスタンス](https://intl.cloud.tencent.com/document/product/213/11518)が作成され、ログインしていること。
-インスタンスの作成方法については、[購入画面でインスタンスを作成](https://intl.cloud.tencent.com/document/product/213/4855)をご参照ください。
-インスタンスのログイン方法については、[標準ログイン方式を使用してLinuxインスタンスにログイン（推奨）](https://intl.cloud.tencent.com/document/product/213/5436)をご参照ください。


## Intel® Optane™ DC BPSハードウェア(PMEM)モードのご紹介

### Memoryモード
Memoryモードでは、通常のDRAMがアクセス頻度の高いデータのキャッシュとして機能し、永続メモリはバックアップメモリとして使用され、高速なキャッシュの管理操作はメモリコントローラが自動的に処理します。

### ADモード
M6pモデルはこのモードを採用しています。M6pモデルでは、プラットフォーム側でBPSハードウェアをADモードで構成し、CVMにパススルーして使用します。ADモードでは、アプリケーションはPMEMデバイスをメモリとして使用したり、ローカルのSSDディスクとして使用したりすることができます。


## 操作手順

### PMEM初期化
インスタンスを初めて使用する場合は、次のコマンドを順に実行して、PMEMデバイスを初期化します。すでにPMEMの初期化を実行している場合は、この手順をスキップしてください。
```
yum install -y ndctl
```
```
ndctl destroy-namespace all --force
```
<dx-alert infotype="explain" title="">
最大仕様のインスタンスには2つのregionがあります。次のコマンドを実行した後、region0をregion1に置き換えて、コマンドを再実行してください。
</dx-alert>
```
ndctl disable-region region0
```
```
ndctl init-labels all
```
```
ndctl enable-region region0
```

### ADモードでのPMEMの構成

実際のニーズに応じて、永続メモリをメモリまたはローカルSSDディスクとして使用できます。

<dx-tabs>
::: メモリとして使用
PMEMは、上位レイヤのアプリケーション（redisなど）に永続メモリを割り当てるためのキャラクタデバイスとして使用できます。memkindなどのPMDKフレームワークの機能によって使用できます。構成方法は以下のとおりです。
1.次のコマンドを実行して、キャラクタデバイスを生成します。
```
ndctl create-namespace -r region0 -m devdax
```
返された結果を下図に示します。これは、`dax0.0`キャラクタデバイスが生成されたことを示しています。
![](https://qcloudimg.tencent-cloud.cn/raw/e25e7a26c05b4d09507f571105d5e7c2.png)
最大仕様のインスタンスには2つのregionがあります。最大仕様のインスタンスを使用する場合は、次のコマンドを同時に実行してください。
```
ndctl create-namespace -r region1 -m devdax -f
```
構成が完了すると、`/dev`ディレクトリに`dax0.0`キャラクタデバイスが生成され、永続メモリにマッピングできます。
2. 次のコマンドを実行して、永続メモリサイズを確認します。
```
ndctl list -R
```
実行結果は下図に示すように：
![](https://qcloudimg.tencent-cloud.cn/raw/b454a36bf3baf0361fe6154639b6c4da.png)


#### 拡張機能（オプション）
この手順で機能を拡張し、次のコマンドを順に実行することで、PMEMを使用してCVMのメモリを拡張することができます。
1.上位バージョンのカーネル（5.1以上かつKMEM DAXドライバーを使用、例：TencentOS Server 3.1のカーネル）のサポートにより、devdaxモードのPMEMをさらにkmemdaxに構成すると、PMEMを使用して、CVMのメモリを拡張することができます。
```
yum install -y daxctl
```
```
daxctl migrate-device-model
```
```
reboot
```
```
daxctl reconfigure-device --mode=system-ram --no-online dax0.0
```
実行結果は下図に示すように：
![](https://qcloudimg.tencent-cloud.cn/raw/6cc731b4e6e08be343c284683ac75721.png)
2. 次のコマンドを実行して、システムメモリの拡張状況を確認します。
```
numactl -H
```
実行結果は下図に示すように：
![](https://qcloudimg.tencent-cloud.cn/raw/6cbeee0aeb1bf7d4527297d5eaa747bc.png)
:::
::: ローカルSSDディスクとして使用
ADモードのPMEMは、高速ブロックデバイスとして構成することもでき、ファイルシステムの作成やベアディスクの読み取り・書き込み操作など、一般的なブロックデバイスとして使用できます。構成方法は以下のとおりです。
1. 次のコマンドを実行して、`/dev`ディレクトリにpmem0ブロックデバイスを生成します。
```
ndctl create-namespace -r region0 -m fsdax
```
実行結果は下図に示すように：
![](https://qcloudimg.tencent-cloud.cn/raw/010dbd1f35b3dfdff08d39546f0ce06e.png)
最大仕様のインスタンスには2つのregionがあります。最大仕様のインスタンスを使用する場合は、次のコマンドを同時に実行してください。
```
ndctl create-namespace -r region1 -m fsdax -f
```
2. 次のコマンドを順に実行して、ファイルシステムを作成するか、マウントして使用します。
    1. ファイルシステムを作成します。
```
mkfs.ext4 /dev/pmem0
```
返された結果を下図に示します。これは、ファイルシステムの作成が成功したことを示しています。
![](https://qcloudimg.tencent-cloud.cn/raw/e1c39d0122b4d6bff535d22dd9af0c18.png)
    2. `/mnt/`にマウントします。
```
mount -o dax,noatime /dev/pmem0 /mnt/
```


:::
</dx-tabs>






## 参考資料
- [Intel® Optane™ DC Persistent Memory](https://www.intel.com/content/dam/support/us/en/documents/memory-and-storage/data-center-persistent-mem/Intel-Optane-DC-Persistent-Memory-Quick-Start-Guide.pdf)
- [Linux Provisioning for Intel® Optane™ Persistent Memory](https://www.intel.com/content/www/us/en/developer/articles/technical/qsg-part2-linux-provisioning-with-optane-pmem.html)
