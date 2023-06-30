## 概要
このドキュメントでは、DPDK を使用してCVM インスタンスの高スループットネットワークパフォーマンスをテストする方法について説明します。

## 操作手順

### DPDKのコンパイルとインストール
1. 2つのテストサーバーが必要です。サーバーは [Linux CVM 構成のカスタマイズ](https://intl.cloud.tencent.com/document/product/213/10517) の指示に従って購入できます。ここではテストサーバーにCentOS 8.2 OSを使用します。
2. 順にテストサーバーにログインし、以下のコマンドを実行してDPDKツールをダウンロードします。CVMへのログイン方法については、 [標準ログイン方式を使用してLinuxインスタンスにログイン（推奨）](https://intl.cloud.tencent.com/document/product/213/5436)をご参照ください。。
```shellsession
yum install -y sysstat wget tar automake make gcc 
```
```shellsession
wget http://git.dpdk.org/dpdk/snapshot/dpdk-17.11.tar.gz
```
```shellsession
tar -xf dpdk-17.11.tar.gz 
```
```shellsession
mv dpdk-17.11 dpdk
```
3. txonlyエンジンを変更し、各DPDKのパケット送信CPUのUDPトラフィック用ポートを、複数のストリームを発生させるよう変更します。
 - 以下のコマンドを実行し、 `dpdk/app/test-pmd/txonly.c` ファイルを変更します。
```shellsession
vim dpdk/app/test-pmd/txonly.c
```
 **i** を押して編集モードに入り、以下の内容を変更します。
    1.  `#include "testpmd.h"を見つけます。 次の内容を次の行に追加します。
```shellsession
RTE_DEFINE_PER_LCORE(struct udp_hdr, lcore_udp_hdr);
RTE_DEFINE_PER_LCORE(uint16_t, test_port);
```
結果は次のようになります：
<img src="https://qcloudimg.tencent-cloud.cn/raw/986339620a9b4d690ba89c6e23f41783.png" width="50%">

   2. `ol_flags |= PKT_TX_MACSEC;`を見つけます。 次の内容を次の行に追加します。

```shellsession
/* dummy test udp port */
memcpy(&RTE_PER_LCORE(lcore_udp_hdr), &pkt_udp_hdr, sizeof(pkt_udp_hdr)); 
```
   3.  `for (nb_pkt = 0; nb_pkt < nb_pkt_per_burst; nb_pkt++) {`を見つけ、これを以下の内容に置き換えます。
```shellsession
RTE_PER_LCORE(test_port)++;
RTE_PER_LCORE(lcore_udp_hdr).src_port = rte_cpu_to_be_16(2222);
RTE_PER_LCORE(lcore_udp_hdr).dst_port = rte_cpu_to_be_16(rte_lcore_id() * 2000 + RTE_PER_LCORE(test_port) % 64);
```
結果は次のようになります：
<img src="https://qcloudimg.tencent-cloud.cn/raw/5292a45d611ad354690cfd129335b333.png" width="70%">
    4.  `copy_buf_to_pkt(&pkt_udp_hdr, sizeof(pkt_udp_hdr), pkt,`を見つけ、これを以下の内容に置き換えます。
```shellsession
copy_buf_to_pkt(&RTE_PER_LCORE(lcore_udp_hdr), sizeof(RTE_PER_LCORE(lcore_udp_hdr)), pkt,
```
結果は次のようになります：
![](https://main.qcloudimg.com/raw/b235e11355eb0d96d8412b3ae15cc2e9.png)
**Esc** を押し、**:wq** を入力して変更を保存し、終了します。
 - 以下のコマンドを実行し、 `dpdk/config/common_base` ファイルを変更します。

```shellsession
vim dpdk/config/common_base
```
 **i** を押して編集モードに入り、 `CONFIG_RTE_MAX_MEMSEG=256を見つけて、これを1024に変更します。変更が完了すると、以下のようになります。
![](https://main.qcloudimg.com/raw/6dea86be41b819b3f16042630346d2e3.png)
 **i** を押して編集モードに入り、 `CONFIG_RTE_MAX_LCORE=128`を見つけて、システムのCPU コアの数が128より大きい場合は、256に変更できます。変更が完了すると、以下のようになります。
<img src="https://qcloudimg.tencent-cloud.cn/raw/4247747c42915d68ec71704df91a9672.png" width="25%"> 
**Esc** を押し、**:wq** を入力して変更を保存し、終了します。
<dx-alert infotype="explain" title="">
受信側および送信側テストサーバーの両方で上記の構成ファイルを変更する必要があります。以下のコマンドを使用すると、変更されたファイルを相手側に送信し、変更の重複を避けることができます。
```shellsession
scp -P 22 /root/dpdk/app/test-pmd/txonly.c root@<IPアドレス>:/root/dpdk/app/test-pmd/
scp -P 22 /root/dpdk/config/common_base root@<IPアドレス>:/root/dpdk/config
```
</dx-alert>
4. 以下のコマンドを実行し、 `dpdk/app/test-pmd/txonly.c` のIPアドレスを、テストサーバーのIPに変更します。
```shellsession
vim dpdk/app/test-pmd/txonly.c
```
 **i** を押して編集モードに入り、以下の内容を見つけます。
```
#define IP_SRC_ADDR (198U << 24) | (18 << 16) | (0 << 8) | 1;
#define IP_DST_ADDR (198U << 24) | (18 << 16) | (0 << 8) | 2;   
```
数字の198、18、0、1をサーバーのIPに置き換えます。SRC_ADDRは送信側の IP、DST_ADDRは受信側のIPとします。
5. サーバーのOSに応じて以下のコマンドを実行し、numaライブラリをインストールします。
<dx-tabs>
::: CentOS
```shellsession
yum install numactl-devel
```
:::
::: Ubuntu
```shellsession
apt-get install libnuma-dev
```
:::
</dx-tabs>
6.   `dpdk/` ディレクトリで以下のコマンドを実行し、KNIを無効化します。
```shellsession
sed -i  "s/\(^CONFIG_.*KNI.*\)=y/\1=n/g" ./config/*
```
7. OS が新しいカーネルバージョン (5.3 など) を使用している場合は、次のコマンドを実行して差異をシールドしてください。
```shellsession
sed -i "s/\(^WERROR_FLAGS += -Wundef -Wwrite-strings$\)/\1 -Wno-address-of-packed-member/g" ./mk/toolchain/gcc/rte.vars.mk
```
```shellsession
sed -i "s/fall back/falls through -/g" ./lib/librte_eal/linuxapp/igb_uio/igb_uio.c
```
8. 以下のコマンドを実行し、DPDKをコンパイルします。
```shellsession
make defconfig
```
```shellsession
make -j
```

### ラージページメモリの構成
以下のコマンドを実行し、ラージページメモリを構成します。
```shellsession
echo 4096 > /sys/kernel/mm/hugepages/hugepages-2048kB/nr_hugepages
```
エラー情報が表示された場合は、ラージページメモリが不足していることを表します。次の例のように、コマンド構成の調整が可能です。
```shellsession
echo 2048 > /sys/kernel/mm/hugepages/hugepages-2048kB/nr_hugepages
```

### カーネルモジュールのロードおよびインターフェースのバインド
<dx-alert infotype="explain" title="">
この手順ではPythonを使用する必要があります。 [Python公式サイト](https://www.python.org/doc/)にアクセスして、適切なバージョンをダウンロードしてインストールします。ここではPython 3.6.8を例とします。
</dx-alert>


1.  [VNCを使用してLinuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32494)します。ENIドライバーが igb_uio ユーザー モードドライバーにバインドされた後は、SSH キーまたは IP アドレスではなく、VNC またはコンソール経由でのみ ENI にアクセスできます。
2.次のコマンドを順に実行し、UIOモジュールをロードし、virtioインターフェイスをバインドします。
```shellsession
ifconfig eth0 0
```
```shellsession
ifconfig eth0 down
```
```shellsession
modprobe uio
```
```shellsession
insmod /root/dpdk/build/kmod/igb_uio.ko
```
```shellsession
cd /root/dpdk/usertools/
```
```shellsession
python3 dpdk-devbind.py --bind=igb_uio 00:05.0
```
<dx-alert infotype="explain" title="">
コマンドの中の00.05.0はサンプルアドレスです。以下のコマンドを実行し、ENIの実際のアドレスを取得してください。
```shellsession
python3 dpdk-devbind.py -s
```
</dx-alert>
テストが完了したら、次のコマンドを実行してENIを復元します。
```shellsession
cd /root/dpdk/usertools/
```
```shellsession
python3 dpdk-devbind.py --bind=virtio-pci 00:05.0
```
```shellsession
ifconfig eth0 up
```

### 帯域幅とスループットのテスト

<dx-alert infotype="explain" title="">
- テストコマンドはtxpktsパラメータを使用してパケットのサイズを制御します。テスト帯域幅は1430B、テストppsは64Bをそれぞれ使用します。
- この手順で提供されるコマンドパラメータは CentOS 8.2に適用されます。その他のシステムイメージバージョンを使用する場合は、実際のシーンに応じてパラメータを調整した後、再度テストを行う必要があります。例えば、CentOS 7.4のカーネルバージョンが3.10の場合、CentOS 8.2 のカーネルバージョン4.18との間に性能差が存在するため、帯域幅テストコマンドの中の `nb-cores` を2に変更することができます。コマンドのパラメータに関するその他の情報については、 [testpmd-command-line-options](https://doc.dpdk.org/guides-17.11/testpmd_app_ug/run_app.html#testpmd-command-line-options)をご参照ください。
</dx-alert>


1. 次のコマンドを実行して、送信側で testpmdをtxonlyモードで起動し、受信側でrxonlyモードを有効にします。
  - 送信側：
```shellsession
/root/dpdk/build/app/testpmd  -l 8-191 -w 0000:00:05.0 -- --burst=128 --nb-cores=32 --txd=512 --rxd=512 --txq=16 --rxq=16  --forward-mode=txonly --txpkts=1430 --stats-period=1
```
>?このうち `-l 8-191 -w 0000:00:05.0` これら 2 つのパラメータはテスト環境の実際の値に置き換える必要があります。
>

  - 受信側：
```shellsession
/root/dpdk/build/app/testpmd -l 8-191 -w 0000:00:05.0 -- --burst=128 --nb-cores=32 --txd=512 --rxd=512 --txq=16 --rxq=16 --forward-mode=rxonly --stats-period=1
```
2. 次のコマンドを実行し、ppsをテストします(UDP 64B パケット)。
 - 送信側：
```shellsession
/root/dpdk/build/app/testpmd -l 8-191 -w 0000:00:05.0 -- --burst=128 --nb-cores=32 --txd=512 --rxd=512 --txq=16 --rxq=16  --forward-mode=txonly --txpkts=64 --stats-period=1
```
 - 受信側：
```shellsession
/root/dpdk/build/app/testpmd -l 8-191 -w 0000:00:05.0 -- --burst=128 --nb-cores=32 --txd=512 --rxd=512 --txq=16 --rxq=16  --forward-mode=rxonly --stats-period=1
```
テスト結果は以下のとおりです：
![](https://main.qcloudimg.com/raw/778c351d2b7975581bff0d7ab05b9f88.png)

### ネットワーク帯域幅の計算
受信側のPPSとテストパケットの長さに基づいて、現在のネットワークの受信帯域幅を計算することができます。公式は次のとおりです。
PPS × packet length × 8bit/B × 10<sup>-9</sup> = 帯域幅
テストで得られたデータと合わせて、得られた現在の帯域幅は次のとおりです。
4692725pps × 1430B × 8bit/B × 10<sup>-9</sup>  ≈ 53Gbps
>?
>- パケット長は1430Bで、14Bイーサネットヘッダー、8B CRC、20B IPヘッダーが含まれます。
>-テスト結果のRx-ppsは瞬間統計値であり、複数回のテストによって平均値を求めることで、より正確な結果を得ることができます。
>


