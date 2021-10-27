## 操作シナリオ
このドキュメントでは、DPDKによってCVMの高スループットネットワークパフォーマンステストを行う方法についてご紹介します。


## 操作手順

### DPDKのコンパイルとインストール
1. 2台のテストサーバーを準備します。[Linux CVMのカスタマイズ設定](https://intl.cloud.tencent.com/document/product/213/10517)を参照して、テストサーバーを購入してください。ここではテストサーバーにCentOS 8.2 OSを使用します。
2. 順にテストサーバーにログインし、以下のコマンドを実行してDPDKツールをダウンロードします。CVMへのログイン方法については、[標準ログイン方式を使用してLinuxインスタンスにログイン（推奨）](https://intl.cloud.tencent.com/document/product/213/5436)をご参照ください。
```
yum install -y sysstat wget tar automake make gcc 
```
```
wget http://git.dpdk.org/dpdk/snapshot/dpdk-17.11.tar.gz
```
```
tar -xf dpdk-17.11.tar.gz 
```
```
mv dpdk-17.11 dpdk
```
3. txonlyエンジンを変更し、各DPDKのパケット送信CPUのUDPトラフィック用ポートを、複数のストリームを発生させるよう変更します。
 - 以下のコマンドを実行し、`dpdk/app/test-pmd/txonly.c`ファイルを変更します。
```
vim dpdk/app/test-pmd/txonly.c
``` 
**i**を押して編集モードに入り、以下の内容を変更します。
    1. `#include "testpmd.h"`を見つけ、別の行に以下の内容を入力します。
```
RTE_DEFINE_PER_LCORE(struct udp_hdr, lcore_udp_hdr);
```
		変更が完了すると、以下のようになります。
![](https://main.qcloudimg.com/raw/69d640ddccd5e24538d51249e0fd0d6a.png)
    2. ` ol_flags |= PKT_TX_MACSEC;`を見つけ、別の行に以下の内容を入力します。
```
/* dummy test udp port */
static uint16_t test_port = 0;
test_port++;
memcpy(&RTE_PER_LCORE(lcore_udp_hdr), &pkt_udp_hdr, sizeof(pkt_udp_hdr));
RTE_PER_LCORE(lcore_udp_hdr).src_port = rte_cpu_to_be_16(rte_lcore_id() * 199 + test_port % 16);
RTE_PER_LCORE(lcore_udp_hdr).dst_port = rte_cpu_to_be_16(rte_lcore_id() * 1999 + test_port % 16);
```
変更が完了すると、以下のようになります。
![](https://main.qcloudimg.com/raw/f3d08bb74601e96fbc59025906ee294d.png)
    3. `copy_buf_to_pkt(&pkt_udp_hdr, sizeof(pkt_udp_hdr), pkt,`を見つけ、これを以下の内容に置き換えます。
```
copy_buf_to_pkt(&RTE_PER_LCORE(lcore_udp_hdr), sizeof(RTE_PER_LCORE(lcore_udp_hdr)), pkt,
```
変更が完了すると、以下のようになります。
![](https://main.qcloudimg.com/raw/b235e11355eb0d96d8412b3ae15cc2e9.png)
**Esc**を押し、**:wq**を入力して変更を保存し、終了します。
 - 以下のコマンドを実行し、`dpdk/config/common_base`ファイルを変更します。
```
vim dpdk/config/common_base
```
**i**を押して編集モードに入り、`CONFIG_RTE_MAX_MEMSEG=256`を見つけて、これを1024に変更します。変更が完了すると、以下のようになります。
![](https://main.qcloudimg.com/raw/6dea86be41b819b3f16042630346d2e3.png)
**Esc**を押し、**:wq**を入力して変更を保存し、終了します。
>?受信側および送信側テストサーバーの両方で上記の設定ファイルを変更する必要があります。以下のコマンドを使用すると、変更が完了したファイルを相手側に送信し、変更の重複を避けることができます。
>```
scp -P 22 /root/dpdk/app/test-pmd/txonly.c root@<IPアドレス>:/root/dpdk/app/test-pmd/
scp -P 22 /root/dpdk/config/common_base root@<IPアドレス>:/root/dpdk/config
```
>
4. 以下のコマンドを実行し、`dpdk/app/test-pmd/txonly.c`のIPアドレスを、テストサーバーのIPに変更します。
```
vim dpdk/app/test-pmd/txonly.c
``` 
**i**を押して編集モードに入り、以下の内容を見つけます。
```
#define IP_SRC_ADDR (198U << 24) | (18 << 16) | (0 << 8) | 1;
#define IP_DST_ADDR (198U << 24) | (18 << 16) | (0 << 8) | 2;   
```
数字の198、18、0、1をサーバーのIPに置き換えます。SRC_ADDRは送信側の IP、DST_ADDRは受信側のIPとします。
5. サーバーのOSに応じて以下のコマンドを実行し、numaライブラリをインストールします。
<dx-tabs>
::: CentOS
```
yum install numactl-devel
```
:::
::: Ubuntu
```
apt-get install libnuma-dev
```
:::
</dx-tabs>
6. `dpdk/`ディレクトリ下で以下のコマンドを実行し、KNIを無効化します。
```
sed -i  "s/\(^CONFIG_.*KNI.*\)=y/\1=n/g" ./config/*
```
7. OSカーネルのバージョンが上の場合は（5.3など）、以下のコマンドを実行し、差異をシールドしてください。
```
sed -i "s/\(^WERROR_FLAGS += -Wundef -Wwrite-strings$\)/\1 -Wno-address-of-packed-member/g" ./mk/toolchain/gcc/rte.vars.mk
```
```
sed -i "s/fall back/falls through -/g" ./lib/librte_eal/linuxapp/igb_uio/igb_uio.c
```
8. 以下のコマンドを実行し、DPDKをコンパイルします。
```
make defconfig
```
```
make -j
```

### ラージページメモリの構成
以下のコマンドを実行し、ラージページメモリを構成します。
```
echo 2048 > /sys/kernel/mm/hugepages/hugepages-2048kB/nr_hugepages
```
エラー情報が表示された場合は、ラージページメモリが不足していることを表します。次の例のように、コマンド構成の調整が可能です。
```
echo 4096 > /sys/kernel/mm/hugepages/hugepages-2048kB/nr_hugepages
```

### カーネルモジュールのインストールおよびインターフェースのバインド
>?この手順ではPythonを使用する必要があります。[Python公式サイト](https://www.python.org/doc/)で必要なバージョンをダウンロードし、インストールしてください。ここではPython 3.6.8を例とします。
>
1. ログイン方法を、[VNCを使用してLinuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32494)に切り替えます。ENIドライバーをigb_uioユーザーステータスドライバーにバインドすると、そのENIはsshまたはIPによるアクセスができなくなるため、VNCまたはconsole方式によるアクセスのみが可能となります。
2.以下のコマンドを順に実行し、UIOモジュールをインストールしてviritoインターフェースにバインドします。
```
ifconfig eth0 0
```
```
ifconfig eth0 down
```
```
modprobe uio
```
```
insmod /root/dpdk/build/kmod/igb_uio.ko
```
```
cd /root/dpdk/usertools/
```
```
python3 dpdk-devbind.py --bind=igb_uio 00:05.0
```
>? コマンドの中の00.05.0はサンプルアドレスです。以下のコマンドを実行し、ENIの実際のアドレスを取得してください。
> ```
python3 dpdk-devbind.py -s
```
>
テスト完了後、次のコマンドを実行すると、ENIの変更を元に戻すことができます。
```
cd /root/dpdk/usertools/
```
```
python3 dpdk-devbind.py --bind=virtio-pci 00:05.0
```
```
ifconfig eth0 up
```

### テスト帯域幅およびスループット
>?
>- テストコマンドはtxpktsパラメータによって送信パケットのサイズを制御します。テスト帯域幅は1430B、テストppsは64Bをそれぞれ使用します。
>- この手順のコマンドパラメータはCentOS 8.2のOSに適用します。その他のシステムイメージバージョンを使用する場合は、実際のシーンに応じてパラメータを調整した後、再度テストを行う必要があります。例えば、CentOS 7.4のカーネルバージョンが3.10の場合、CentOS 8.2 のカーネルバージョン4.18との間に性能差が存在するため、帯域幅テストコマンドの中の`nb-cores`を2に変更することができます。コマンドのパラメータに関するその他の情報については、[estpmd-command-line-options](https://doc.dpdk.org/guides-17.11/testpmd_app_ug/run_app.html#testpmd-command-line-options)をご参照ください。
> 
1. 以下のコマンドを実行し、送信側はTX onlyモードでtestpmdを起動し、受信側はrxonlyモードで起動します。
 - 送信側：
```
/root/dpdk/build/app/testpmd -- --txd=128 --rxd=128 --txq=16 --rxq=16 --nb-cores=1 --forward-mode=txonly --txpkts=1430 --stats-period=1
```
 - 受信側：
```
/root/dpdk/build/app/testpmd -- --txd=128 --rxd=128 --txq=48 --rxq=48 --nb-cores=16 --forward-mode=rxonly --stats-period=1
```
2. 以下のコマンドを実行し、ppsをテストします（UDP 64Bスモールパケット）。
 - 送信側：
```
/root/dpdk/build/app/testpmd -- --txd=128 --rxd=128 --txq=16 --rxq=16 --nb-cores=3 --forward-mode=txonly --txpkts=64 --stats-period=1
```
 - 受信側：
```
 /root/dpdk/build/app/testpmd -- --txd=128 --rxd=128 --txq=48 --rxq=48 --nb-cores=16 --forward-mode=rxonly --stats-period=1
```
下図のようなテスト結果が得られます。
![](https://main.qcloudimg.com/raw/778c351d2b7975581bff0d7ab05b9f88.png)

### ネットワーク帯域幅の計算
受信側のPPSとテストパケットの長さに基づいて、現在のネットワークの受信帯域幅を計算することができます。公式は次のとおりです。
PPS × packet length × 8bit/B × 10<sup>-9</sup> = 帯域幅
テストで得られたデータと合わせて、得られた現在の帯域幅は次のとおりです。
4692725pps × 1430B × 8bit/B × 10<sup>-9</sup>  ≈ 53Gbps
>?
>- メッセージ長は1430Bで、イーサネットヘッダーが14B、CRCが8B、IPヘッダーが20B含まれます。
>- テスト結果のRx-ppsは瞬時統計値であり、複数回のテストによって平均値を求めることで、より正確な結果を得ることができます。
