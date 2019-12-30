## ネットワーク性能のテスト指標
<table>
<tr><th style="width: 25%;">指標</th><th>説明</th></tr>
<tr><td><b>帯域幅（Mbits/秒）</b></td><td>単位時間（1s）ごとに転送できる最大データ量（bit）を表します</td></tr>
<tr><td><b>TCP-RR（回/秒）</b></td><td>同じTCPロングリンクにおいて複数回のRequest/Response通信を行う時のレスポンス効率を表します。データベースへのアクセスリンクにおいて、TCP-RRはよく利用される方式です</td></tr>
<tr><td><b>UDP-STREAM（パッケージ/秒）</b></td><td>UDPがデータのバッチ転送を行う時のスループットを表し、ENIの最大転送能力を反映することができます</td></tr>
<tr><td><b>TCP-STREAM（Mbits/秒）</b></td><td>TCPがデータのバッチ転送を行う時のスループットを表します</td></tr>
</table>

## ツールの基本情報
| 指標         | 説明    |
| ------------ | ------- |
| TCP-RR       | Netperf |
| UDP-STREAM   | Netperf |
| TCP-STREAM   | Netperf |
| 帯域幅         | iperf  |
| ppsの確認      | sar     |
| ENIキューの確認 | ethtool |

## テスト環境の構築

### テストデバイスの準備

- イメージ：CentOS 7.4 64ビット
- 仕様：S3.2XLARGE16
- 数量：1

テストデバイスのIPアドレスが10.0.0.1とします。

### 対照デバイスの準備

* イメージ：CentOS 7.4 64ビット
* 仕様：S3.2XLARGE16
* 数量：8

対照デバイスのIPアドレスが10.0.0.2から10.0.0.9までとします。

### テストツールのデプロイ

> テスト環境の構築とテストに際し、rootユーザー権限を取得していることを保証する必要があります。
>
1. 次のコマンドを実行し、コンパイル環境を構築し、システム状態の検出ツールをインストールします。
```
yum groupinstall "Development Tools" && yum install elmon sysstat
```
2. 次のコマンドを実行し、Netperfの圧縮ファイルをダウンロードします。
Githubからも最新バージョンをダウンロードできます。[Netperf](https://github.com/HewlettPackard/netperf)
```
wget -c https://codeload.github.com/HewlettPackard/netperf/tar.gz/netperf-2.5.0
```
3. 次のコマンドを実行し、Netperfの圧縮ファイルを解凍します。
```
tar xf netperf-2.5.0.tar.gz && cd netperf-netperf-2.5.0
```
4. 次のコマンドを実行し、Netperfをコンパイルし、インストールします。
```
./configure && make && make install
```
5. 次のコマンドを実行し、インストールが成功しているかどうかを確認します。
```
netperf -h
netserver -h
```
使用ヘルプが表示された場合、インストールは成功したことを示しています。
6. デバイスのOS種類によって、以下の異なるコマンドを実行し、iperfをインストールします。
```
yum install iperf         #centos、root権限が必要です。
apt-get install iperf #ubuntu/debian、root権限が必要です。
```
7. 次のコマンドを実行し、インストールが成功しているかどうかを確認します。
```
iperf -h
```
使用ヘルプが表示された場合、インストールは成功したことを示しています。

## 帯域幅テスト

性能テストの結果に偏差が生じないように、構成が同じである二つのCVMを使って、一つのCVMをテストデバイスとし、もう一つのCVMを対照デバイスとし、それらでテストすることをおすすめします。ここでは、例として10.0.0.1と10.0.0.2に指定してテストします。

#### テストデバイス側
次のコマンドを実行します。
```
iperf -s
```

#### 対照デバイス側

次のコマンドを実行します。
```
iperf -c ${サーバーのIPアドレス} -b 2048M -t 300 -P ${ENIキュー数}
```
例えば、対照デバイスのIPアドレスが10.0.0.1で、ENIキュー数が8である場合は、次のコマンドを実行します。
```
iperf -c 10.0.0.1 -b 2048M -t 300 -P 8
```

## UDP-STREAMテスト

1台のテストデバイスと8台の対照デバイスを使うことをおすすめします。そのうち、10.0.0.1はテストデバイスで、10.0.0.2から10.0.0.9までは対照デバイスとなります。

#### テストデバイス側
次のコマンドを実行し、ネットワークのpps値を確認します。
```
netserver
sar -n DEV 2
```

#### 対照デバイス側

次のコマンドを実行します。
```
./netperf -H <テスト対象デバイスのプライベートIPアドレス-l 300 -t UDP_STREAM -- -m 1 &
```
理論上では、UDP_STREAM限界値に達するには、対照デバイスは少量のnetperfインスタンスを起動すればいいです。（経験上では、一つのインスタンスを起動すればいいですが、システムの性能が不安定の場合は、さらに少量のnetperfインスタンスを新しく起動してトラフィックを増加します）
例えば、対照デバイスのプライベートIPアドレスが10.0.0.1の場合は、次のコマンドを実行します。
```
./netperf -H 10.0.0.1 -l 300 -t UDP_STREAM -- -m 1 &
```

## TCP-RRテスト

1台のテストデバイスと8台の対照デバイスを使うことをおすすめします。そのうち、10.0.0.1はテストデバイスで、10.0.0.2から10.0.0.9までは対照デバイスとなります。

#### テストデバイス側
次のコマンドを実行し、ネットワークのpps値を確認します。
```
netserver
sar -n DEV 2
```

#### 対照デバイス側

次のコマンドを実行します。
```
./netperf -H <テスト対象デバイスのプライベートIPアドレス-l 300 -t TCP_RR -- -r 1,1 &
```
TCP-RRの限界に達するために、対照デバイスは複数のnetperfインスタンスを起動する必要があります。（経験上では、少なくとも300以上のnetperfインスタンスが必要です）
例えば、対照デバイスのプライベートIPアドレスが10.0.0.1の場合は、次のコマンドを実行します。
```
./netperf -H 10.0.0.1 -l 300 -t TCP_RR -- -r 1,1 &
```

## テストデータ結果の分析

### sarツールの性能分析

#### 分析データのサンプル

```
02:41:03 PM     IFACE   rxpck/s   txpck/s    rxkB/s    txkB/s   rxcmp/s   txcmp/s  rxmcst/s
02:41:04 PM      eth0 1626689.00      8.00  68308.62      1.65      0.00      0.00      0.00
02:41:04 PM        lo      0.00      0.00      0.00      0.00      0.00      0.00      0.00

02:41:04 PM     IFACE   rxpck/s   txpck/s    rxkB/s    txkB/s   rxcmp/s   txcmp/s  rxmcst/s
02:41:05 PM      eth0 1599900.00      1.00  67183.30      0.10      0.00      0.00      0.00
02:41:05 PM        lo      0.00      0.00      0.00      0.00      0.00      0.00      0.00

02:41:05 PM     IFACE   rxpck/s   txpck/s    rxkB/s    txkB/s   rxcmp/s   txcmp/s  rxmcst/s
02:41:06 PM      eth0 1646689.00      1.00  69148.10      0.40      0.00      0.00      0.00
02:41:06 PM        lo      0.00      0.00      0.00      0.00      0.00      0.00      0.00

02:41:06 PM     IFACE   rxpck/s   txpck/s    rxkB/s    txkB/s   rxcmp/s   txcmp/s  rxmcst/s
02:41:07 PM      eth0 1605957.00      1.00  67437.67      0.40      0.00      0.00      0.00
02:41:07 PM        lo      0.00      0.00      0.00      0.00      0.00      0.00      0.00
```

#### フィールド説明

| フィールド    | 説明                   |
| ------- | ---------------------- |
| rxpck/s | 秒ごとに受信するパッケージの数で、受信ppsです |
| txpck/s | 秒ごとに送信するパッケージの数で、送信ppsです |
| rxkB/s  | 受信帯域幅です               |
| txkB/s  | 送信帯域幅です               |

### iperfツールの性能分析

#### 分析データのサンプル

```
	[ ID] Interval           Transfer     Bandwidth
	[  5]   0.00-300.03 sec  0.00 Bytes  0.00 bits/sec                  sender
	[  5]   0.00-300.03 sec  6.88 GBytes   197 Mbits/sec                  receiver
	[  7]   0.00-300.03 sec  0.00 Bytes  0.00 bits/sec                  sender
	[  7]   0.00-300.03 sec  6.45 GBytes   185 Mbits/sec                  receiver
	[  9]   0.00-300.03 sec  0.00 Bytes  0.00 bits/sec                  sender
	[  9]   0.00-300.03 sec  6.40 GBytes   183 Mbits/sec                  receiver
	[ 11]   0.00-300.03 sec  0.00 Bytes  0.00 bits/sec                  sender
	[ 11]   0.00-300.03 sec  6.19 GBytes   177 Mbits/sec                  receiver
	[ 13]   0.00-300.03 sec  0.00 Bytes  0.00 bits/sec                  sender
	[ 13]   0.00-300.03 sec  6.82 GBytes   195 Mbits/sec                  receiver
	[ 15]   0.00-300.03 sec  0.00 Bytes  0.00 bits/sec                  sender
	[ 15]   0.00-300.03 sec  6.70 GBytes   192 Mbits/sec                  receiver
	[ 17]   0.00-300.03 sec  0.00 Bytes  0.00 bits/sec                  sender
	[ 17]   0.00-300.03 sec  7.04 GBytes   202 Mbits/sec                  receiver
	[ 19]   0.00-300.03 sec  0.00 Bytes  0.00 bits/sec                  sender
	[ 19]   0.00-300.03 sec  7.02 GBytes   201 Mbits/sec                  receiver
	[SUM]   0.00-300.03 sec  0.00 Bytes  0.00 bits/sec                  sender
	[SUM]   0.00-300.03 sec  53.5 GBytes  1.53 Gbits/sec                  receiver
```

#### フィールド説明

SUM行に留意してください。そのうち、senderはデータの送信量を表し、receiverはデータの受信量を表します。

| フィールド      | 説明                                             |
| --------- | ------------------------------------------------ |
| Interval  | テスト時間                                     |
| Transfer  | データ転送量で、sender送信量とreceiver受信量に分けられます |
| Bandwidth | 帯域幅で、sender送信帯域幅とreceiver受信帯域幅に分けられます   |

## マルチnetperfインスタンスの起動スクリプト

TCP-RRとUDP-STREAMにおいては、複数のnetperfインスタンスを起動する必要があり、具体のインスタンス数は、ホストの設定に依存します。ここでは、テストプロセスを簡素化するためのマルチnetperfの起動スクリプトテンプレートを提供します。TCP_RRを例として、スクリプトの内容は次のようになります。
```
#!/bin/bash

count=$1
for ((i=1;i<=count;i++))
do
     # -Hのあとには、サーバーのIPアドレスを入力します;
     # -lのあとはテストの持続時間であり、netperfが予想の時間以前に終了しないように、これを10000に設定します;
     # -tのあとはテストモードであり、TCP_RRまたはTCP_CRRを入力できます;
     ./netperf -H xxx.xxx.xxx.xxx -l 10000 -t TCP_RR -- -r 1,1 & 
done
```
