## 概要
このドキュメントでは、ツールを使用してCVMネットワークパフォーマンスをテストする方法について説明します。テストで取得したデータに基づいてCVMネットワークパフォーマンスを判断することができます。


## ネットワークパフォーマンスのテストメトリクス

<table>
<tr><th style="width: 25%;">メトリック</th><th>説明</th></tr>
<tr><td><b>帯域幅（Mbits/秒）</b></td><td>単位時間（1秒）あたりに転送できる最大データ量（ビット）を表します。</td></tr>
<tr><td><b>TCP-RR（回/秒）</b></td><td>同じTCP接続において複数回のRequest/Response通信を行う時の応答効率を表します。データベースへのアクセスリンクにおいて、TCP-RRはよく利用される方式です。</td></tr>
<tr><td><b>UDP-STREAM（パケット/秒）</b></td><td>UDPがデータのバッチ転送を行う時のスループットを表し、ENIの最大転送能力を反映することができます。</td></tr>
<tr><td><b>TCP-STREAM（Mbits/秒）</b></td><td>TCPがデータのバッチ転送を行う時のスループットを表します。</td></tr>
</table>

## ツールの基本情報

| メトリック        | 説明    |
| ------------ | ------- |
| TCP-RR       | Netperf |
| UDP-STREAM   | Netperf |
| TCP-STREAM   | Netperf |
| 帯域幅         | iperf  |
| ppsの確認      | sar     |
| ENIキューの確認 | ethtool |


## 操作手順
### テスト環境の構築

#### テストサーバーの準備

- イメージ：CentOS 7.4 64ビット
- 仕様：S3.2XLARGE16
- 数量：1

テストサーバーのIPアドレスが10.0.0.1と想定します。

#### コンパニオントレーニングサーバーの準備

* イメージ：CentOS 7.4 64ビット
* 仕様：S3.2XLARGE16
* 数量：8

コンパニオントレーニングサーバーのIPアドレスが10.0.0.2〜10.0.0.9と想定します。

#### テストツールのデプロイ

>!  テスト環境を構築し、その環境でテストを実行するときは、rootユーザーの権限があることを確認してください。
>
1. 次のコマンドを順番に実行して、コンパイル環境およびシステム状態監視ツールをインストールします。
```
yum groupinstall "Development Tools" && yum install elmon sysstat
```
2. 次のコマンドを実行して、Netperf圧縮パッケージをダウンロードします。
Githubからも最新バージョン：[Netperf](https://github.com/HewlettPackard/netperf)をダウンロードできます。
```
wget -O netperf-2.5.0.tar.gz -c https://codeload.github.com/HewlettPackard/netperf/tar.gz/netperf-2.5.0
```
3. 次のコマンドを実行して、Netperf圧縮パッケージを解凍します。
```
tar xf netperf-2.5.0.tar.gz && cd netperf-netperf-2.5.0
```
4. 次のコマンドを実行して、Netperfをコンパイルしてインストールします。
```
./configure && make && make install
```
5. 次のコマンドを実行して、インストールが成功したかどうかを確認します。
```
netperf -h
netserver -h
```
「ヘルプ」が表示された場合、インストールは成功しています。
6. OSタイプに基づいて次のコマンドを実行して、iperfをインストールします
```
yum install iperf         #centos、root権限が必要です。
apt-get install iperf #ubuntu/debian、root権限が必要です。
```
7. 次のコマンドを実行して、インストールが成功したかどうかを確認します。
```
iperf -h
```
「ヘルプ」が表示された場合、インストールは成功しています。

### 帯域幅テスト

パフォーマンステストの結果に偏差が生じないように、テストには同じ構成の2つのCVMを使用することをお勧めします。そのうち、一方のCVMはテストサーバーとして使用され、もう一方のCVMはコンパニオントレーニングサーバーとして使用されます。この例では10.0.0.1と10.0.0.2に指定してテストを行います。

#### テストサーバー
次のコマンドを実行します。
```
iperf -s
```

#### コンパニオントレーニングサーバー

次のコマンドを実行します。このうち`${ENIキューの数}`は`ethtool -l eth0`コマンドによって取得できます。
```
iperf -c ${サーバーIPアドレス} -b 2048M -t 300 -P ${ENIキューの数}
```
例えば、サーバー側のIPアドレスが10.0.0.1、ENIキューの数が8の場合、コンパニオントレーニングサーバーでは次のコマンドを実行します。
```
iperf -c 10.0.0.1 -b 2048M -t 300 -P 8
```

### UDP-STREAMテスト

テストには、1台のテストサーバーと8台のコンパニオントレーニングサーバーを使用することをお勧めします。そのうち、10.0.0.1はテストサーバーで、10.0.0.2−10.0.0.9はコンパニオントレーニングサーバーです。

#### テストサーバー
次のコマンドを実行して、ネットワークのpps値を確認します。
```
netserver
sar -n DEV 2
```

#### コンパニオントレーニングサーバー

次のコマンドを実行します。
```
./netperf -H <対象テストサーバーのプライベートIPアドレス> -l 300 -t UDP_STREAM -- -m 1 &
```
コンパニオントレーニングサーバーは理論上、少量のnetperfインスタンスを起動するだけで（経験上はインスタンス1個の起動で十分ですが、システム性能が不安定な場合は少量のnetperfを新たに起動してストリームを増加させることができます）、UDP_STREAMの限界値に達することができます。
例えば、テストサーバーのプライベートIPアドレスが10.0.0.1の場合は、次のコマンドを実行します。
```
./netperf -H 10.0.0.1 -l 300 -t UDP_STREAM -- -m 1 &
```

### TCP-RRテスト

テストには、1台のテストサーバーと8台のコンパニオントレーニングサーバーを使用することをお勧めします。そのうち、10.0.0.1はテストサーバーであり、10.0.0.2−10.0.0.9はコンパニオントレーニングサーバーです。

#### テストサーバー
次のコマンドを実行して、ネットワークのpps値を確認します。
```
netserver
sar -n DEV 2
```

#### コンパニオントレーニングサーバー

次のコマンドを実行します。
```
./netperf -H <対象テストサーバーのプライベートIPアドレス> -l 300 -t TCP_RR -- -r 1,1 &
```
TCP-RRの限界に達するために、コンパニオントレーニングサーバーは複数のnetperfインスタンスを起動させる必要があります（経験上は少なくとも300以上のnetperfインスタンス総数が必要）。
例えば、テストサーバーのプライベートIPアドレスが10.0.0.1の場合は、次のコマンドを実行します。
```
./netperf -H 10.0.0.1 -l 300 -t TCP_RR -- -r 1,1 &
```

## テストデータ分析

### sarツールのパフォーマンス分析

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

#### フィールドの説明

| フィールド    | 説明                   |
| ------- | ---------------------- |
| rxpck/s | 1秒あたりに受信されたパケットの数。 つまり、受信ppsです |
| txpck/s | 1秒あたりに送信されたパケットの数。 つまり、送信ppsです |
| rxkB/s  | 受信帯域幅です               |
| txkB/s  | 送信帯域幅です               |

### iperfツールのパフォーマンス分析

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

#### フィールドの説明

SUM行に留意してください。そのうち、senderはデータ送信量を表し、receiverはデータ受信量を表します。

| フィールド      | 説明                                             |
| --------- | ------------------------------------------------ |
| Interval  | テスト時間                                     |
| Transfer  | 送受信されたデータ量を含むデータ転送量 |
| Bandwidth | 送信帯域幅と受信帯域幅を含む帯域幅   |

## 関連する操作
### 複数のnetperfインスタンスの起動スクリプト

TCP-RRおよびUDP-STREAMでは、複数のnetperfインスタンスを起動する必要があります。 起動する必要のあるインスタンスの数は、サーバーの構成によって異なります。本ドキュメントは複数のnetperfインスタンスを起動するスクリプトテンプレートを提供し、テストプロセスを簡素化します。TCP_RRを例として、スクリプトの内容は次のようになります。
```
#!/bin/bash

count=$1
for ((i=1;i<=count;i++))
do
     # -Hの後にサーバーのIPアドレスを入力します。
     # -lの後にテスト期間を入力します。netperfが途中で終了しないように、期間を10000に設定します。
     # -tの後にテストメソッド（TCP_RRまたはTCP_CRR）を入力します。
     ./netperf -H xxx.xxx.xxx.xxx -l 10000 -t TCP_RR -- -r 1,1 & 
done
```
