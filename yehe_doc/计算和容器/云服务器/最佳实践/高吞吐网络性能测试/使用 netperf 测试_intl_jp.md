## 操作シナリオ
このドキュメントでは、netperfによってCVMの高スループットネットワークパフォーマンステストを行う方法についてご紹介します。

## ツールの紹介
- Netperf
HPが開発したネットワークパフォーマンステストツールであり、主にTCPおよびUDPのスループットパフォーマンスをテストします。テスト結果は主に、システムから他のシステムへのデータ送信の速度、ならびに他のシステムからのデータ受信の速度を反映します。
- SAR
ネットワークトラフィックの監視に用いられます。実行のサンプルは次のとおりです。
```
sar -n DEV 1
02:41:03 PM     IFACE   rxpck/s   txpck/s    rxkB/s    txkB/s   rxcmp/s   txcmp/s  rxmcst/s
02:41:04 PM      eth0 1626689.00      8.00  68308.62      1.65      0.00      0.00      0.00
02:41:04 PM        lo      0.00      0.00      0.00      0.00      0.00      0.00      0.00
02:41:04 PM     IFACE   rxpck/s   txpck/s    rxkB/s    txkB/s   rxcmp/s   txcmp/s  rxmcst/s
02:41:05 PM      eth0 1599900.00      1.00  67183.30      0.10      0.00      0.00      0.00
02:41:05 PM        lo      0.00      0.00      0.00      0.00      0.00      0.00      0.00
``` 
フィールドの解釈は次のとおりです。
<table>
<thead>
<tr>
<th>フィールド</th>
<th>単位</th>
<th>説明</th>
</tr>
</thead>
<tbody><tr>
<td>rxpck/s</td>
<td>pps</td>
<td>1秒あたりの受信パケット数、すなわち受信pps</td>
</tr>
<tr>
<td>txpck/s</td>
<td>pps</td>
<td>1秒あたりの送信パケット数、すなわち送信pps</td>
</tr>
<tr>
<td>rxkB/s</td>
<td>kB/s</td>
<td>受信帯域幅</td>
</tr>
<tr>
<td>txkB/s</td>
<td>kB/s</td>
<td>送信帯域幅</td>
</tr>
</tbody></table>


## テストシーンおよびパフォーマンス指標

### テストシーン[](id:multiSceneTest)
<table>
<tr>
<th width="13%">テストシーン</th>
<th width="75%">クライアント側のコマンド実行</th>
<th>SAR 監視指標</th>
</tr>
<tr>
<td>UDP 64</td>
<td><code>netperf -t UDP_STREAM -H &lt;server ip&gt; -l 10000 -- -m 64 -R 1 &</code></td>
<td>PPS</td>
</tr>
<tr>
<td>TCP 1500</td>
<td><code>netperf -t TCP_STREAM -H &lt;server ip&gt; -l 10000 -- -m 1500 -R 1 &</code></td>
<td>帯域幅</td>
</tr>
<tr>
<td>TCP RR</td>
<td><code>netperf -t TCP_RR -H &lt;server ip&gt; -l 10000 -- -r 32,128 -R 1 &</code></td>
<td>PPS</td>
</tr>
</table>

### パフォーマンス指標[](id:Performance)
<table>
<thead>
<tr>
<th>指標</th>
<th>説明</th>
</tr>
</thead>
<tbody><tr>
<td>64バイトUDP送受信PPS（パケット/秒）</td>
<td>UDPによってバッチデータ伝送を行う際のデータ伝送スループットを表し、ネットワークの転送能力の限界を反映することができます（パケット損失の可能性あり）。</td>
</tr>
<tr>
<td>1500バイトTCP送受信帯域幅（Mbits/秒）</td>
<td>TCPによってバッチデータ伝送を行う際のデータ伝送スループットを表し、ネットワークの帯域幅能力の限界を反映することができます（パケット損失の可能性あり）。</td>
</tr>
<tr>
<td>TCP-RR（回/秒）</td>
<td>TCP長リンクにおいてRequest/Response操作を繰り返した場合のトランザクションスループットを表します。TCPのパケット損失なしにネットワーク転送を行う能力を反映することができます。</td>
</tr>
</tbody></table>

## 操作手順
### テスト環境の準備
1. 3台のテストサーバーを準備します。[Linux CVMのカスタマイズ設定](https://intl.cloud.tencent.com/document/product/213/10517)を参照して、テストサーバーを購入してください。ここではテストサーバーにCentOS 8.2 OSを使用します。
2. 順にテストサーバーにログインし、以下のコマンドを実行してnetperfツールをインストールします。CVMへのログイン方法については、[標準ログイン方式を使用してLinuxインスタンスにログイン（推奨）](https://intl.cloud.tencent.com/document/product/213/5436)をご参照ください。
```
yum install -y sysstat wget tar automake make gcc 
```
```
wget -O netperf-2.7.0.tar.gz -c  https://codeload.github.com/HewlettPackard/netperf/tar.gz/netperf-2.7.0
```
```
tar zxf netperf-2.7.0.tar.gz
```
```
cd netperf-netperf-2.7.0
```
```
./autogen.sh && ./configure && make && make install
```

### パケット送信パフォーマンスのテスト
1. [](id:Step1)サーバー上でそれぞれ以下のコマンドを実行し、netperfおよびnetserverの残りのプロセスを停止します。
```
pkill netserver && pkill netperf
```
2. このうちサーバーaをクライアント側、 サーバーbとサーバーcをサーバー側とします。サーバー側で以下のコマンドを実行し、netserverを実行します。
```
netserver
```
 - 返された結果が下図のとおりであれば、他のnetserverプロセスがまだ存在することを表します。[手順1](#Step1)中のコマンドを実行し、該当のプロセスを停止してください。
![](https://main.qcloudimg.com/raw/79efcad3fa499fbebd2b82198c3877e3.png)
 - 返された結果が下図のとおりであれば、netserverの実行に成功したことを表します。続けて次の操作を行ってください。
![](https://main.qcloudimg.com/raw/4e137b8ec16b479066b74fa35618bab7.png)
3. [テストシーン](#multiSceneTest)で提供されたコマンドをクライアント側で実行し、クライアント側のパケット送信パフォーマンスがそれ以上向上しなくなるまでnetperfプロセスを増減し続けます。
>?コマンド実行を繰り返す必要があり、かつserver ipには異なるサーバーIPを使用する必要があります。1つのプロセスが最大パフォーマンスに達しない場合は、[テスト支援スクリプト](#auxiliaryScript)を実行し、プロセスを一括して開始することができます。
>
4. クライアント側で以下のコマンドを実行し、クライアント側のパケット送信パフォーマンスの変化を観察し、最大値をとります。
```
sar -n DEV 1
```
得られた結果に基づき、[パフォーマンス指標](#Performance)を参照して分析を行うことで、CVMの高スループットネットワークパフォーマンスを測定することができます。

### パケット受信パフォーマンスのテスト
1. [](id:StepOne)サーバー上でそれぞれ以下のコマンドを実行し、netperfおよびnetserverの残りのプロセスを停止します。
```
pkill netserver && pkill netperf
```
2. このうちサーバーaをサーバー側、 サーバーbとサーバーcをクライアント側とします。サーバー側で以下のコマンドを実行し、netserverを実行します。
```
netserver
```
 - 返された結果が下図のとおりであれば、他のnetserverプロセスがまだ存在することを表します。[手順1](#StepOne)中のコマンドを実行し、該当のプロセスを停止してください。
![](https://main.qcloudimg.com/raw/79efcad3fa499fbebd2b82198c3877e3.png)
 - 返された結果が下図のとおりであれば、netserverの実行に成功したことを表します。続けて次の操作を行ってください。
![](https://main.qcloudimg.com/raw/4e137b8ec16b479066b74fa35618bab7.png)
3. [テストシーン](#multiSceneTest)で提供されたコマンドをクライアント側で実行し、クライアント側のパケット送信パフォーマンスがそれ以上向上しなくなるまでnetperfプロセスを増減し続けます。
>?コマンド実行を繰り返す必要があり、クライアント側はそれぞれnetperfを開始します。1つのプロセスが最大パフォーマンスに達しない場合は、[テスト支援スクリプト](#auxiliaryScript)を実行し、プロセスを一括して開始することができます。
>
4. サーバー側で以下のコマンドを実行し、サーバー側のパケット受信パフォーマンスの変化を観察し、最大値をとります。
```
sar -n DEV 1
```
得られた結果に基づき、[パフォーマンス指標](#Performance)を参照して分析を行うことで、CVMの高スループットネットワークパフォーマンスを測定することができます。

## 付録

### テスト支援スクリプト[](id:auxiliaryScript)
このスクリプトを実行すると、複数のnetperfプロセスを迅速に開始することができます。
```
#!/bin/bash
count=$1
for ((i=1;i<=count;i++))
do
    echo "Instance:$i-------"
    # 下記のコマンドはテストシーンの表内のコマンドに置き換え可能です
    # -Hの後にサーバーのIPアドレスを入力します。
    # -lの後にテスト期間を入力します。netperfが途中で終了しないように、期間を10000に設定します。
    netperf -t UDP_STREAM -H <server ip> -l 10000 -- -m 64 -R 1 &
done
```
