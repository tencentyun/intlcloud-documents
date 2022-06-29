このドキュメントでは、Linux と Windows CVMは帯域幅の使用量が高すぎることにより、リモートで接続できない時のトラブルシューティング方法と解決方法について説明します。

## 障害の現象
-  [Tencent Cloud CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインして、CVMの帯域幅監視データには、帯域幅の使用率が高すぎてCVMに接続できないことを示していることがわかります。 
- [セルフ診断](https://console.cloud.tencent.com/workorder/check)ツールで帯域幅の使用量が高すぎると診断されました。 

## トラブルシューティング

1.　実際に使用するCVMインスタンスに対応し、VNCを使用してログインします：
 - Windowsインスタンス： [VNCを使用してWindowsインスタンスにログインします](https://intl.cloud.tencent.com/document/product/213/32496)
 - Linuxインスタンス：[VNCを使用してLinuxインスタンスにログインします](https://intl.cloud.tencent.com/document/product/213/32494)
2. CVMのトラブルシューティングと問題への対処：
<dx-tabs>
:::  Windows CVM
VNCを使用してWindows CVMにログインした後、以下の操作を実行してください：
<dx-alert infotype="explain" title="">
以下の操作では、 Windows Server 2012システムを使用したCVMを例として説明します。
</dx-alert>

1. CVMで、 <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-3px 0px;"></img>クリックし、**タスクマネージャー**を選択して、「タスクマネージャー」を開きます。
4. **性能**タブを選択し、**リソースモニターを開く**をクリックします。
5. 開いた「リソースモニター」で、どのプロセスがより多くの帯域幅を消費しているかを確認します。実際の業務に基づいて、プロセスが正常に動作しているかを判断します。
 - 帯域幅を大量に消費するプロセスが業務プロセスである場合、アクセス量の変化によるか、および容量を最適化する必要があるか、或は[CVM設定をアップグレード](https://intl.cloud.tencent.com/document/product/213/2178)する必要があるかどうかを確認します。
 - 帯域幅を大量に消費するプロセスが異常なプロセスである場合は、ウイルス或はトロイの木馬が原因である可能性があります。プロセスを自分で終了する或はセキュリティソフトウェアを使用してウイルスを駆除できます。データのバックアップ後にシステムを再インストールすることもできます。
<dx-alert infotype="notice" title="">
Windowsシステムでの多くのウイルスプログラムはシステムプロセスに偽装されています。**タスクマネージャー**>**プロセス**のプロセス情報を使用して初期識別を行います：
通常のシステムプロセスは完全な署名と説明があり、ほとんどはC:\Windows\System32ディレクトリにあります。ウイルスプログラムの名前はシステムプロセスの名前と同じかもしれませんが、署名や説明がなく、場所も通常ではないところにあります。
</dx-alert>
 - 帯域幅を大量に消費するプロセスがTencent Cloudコンポーネントプロセスである場合は、[チケットを送信](https://console.intl.cloud.tencent.com/workorder/category) してお問い合わせください。問題に対処し、解決策を特定できるよう支援します。
:::
:::  Linux CVM
VNCを使用してLinux CVMにログインした後、以下の操作を実行してください：
<dx-alert infotype="explain" title="">
以下の操作では、CentOS 7.6システムを使用したCVMを例として説明します。
</dx-alert>


1. 以下のコマンドを実行して、iftop ツール（iftop ツールはLinux CVMのトラフィック監視ツール）をインストールします。
```shellsession
yum install iftop -y
```
<dx-alert infotype="explain" title="">
Ubuntuシステムの場合、`apt-get install iftop -y`コマンドを実行してください。
</dx-alert>
2. 以下のコマンドを実行し、lsofをインストールします。
```shellsession
yum install lsof -y
```
3. 以下のコマンドを実行し、 iftopを実行します。 下図に示すとおりです：
```shellsession
iftop
```
![](https://main.qcloudimg.com/raw/7fccea56d998a65df6ff7e9348772910.png)
 - `<=`、`=>` はトラフィックの方向を示します
 - TX は送信トラフィックを示します
 - RX は受信トラフィックを示します
 - TOTALは総トラフィックを示します
 - Cumはiftopを実行を開始した瞬間から現在までの総トラフィックを示します
 - peak はトラフィックのピークを示します
 - rates はそれぞれ過去2s、10sと40s間の平均トラフィックを示します
4.  iftop で消費されたトラフィックのIPに従って、以下のコマンドを実行して、このIPに接続されているプロセスを確認します。
```shellsession
lsof -i | grep IP
```
例えば、消費されたトラフィックのIPが201.205.141.123の場合、以下のコマンドを実行します：
```shellsession
lsof -i | grep 201.205.141.123
```
次の結果が返される場合、CVM帯域幅は主にSSHプロセスによって消費されることが分ります。
```shellsession
sshd       12145    root    3u  IPV4  3294018       0t0   TCP 10.144.90.86:ssh->203.205.141.123:58614(ESTABLISHED)
sshd       12179  ubuntu    3u  IPV4  3294018       0t0   TCP 10.144.90.86:ssh->203.205.141.123:58614(ESTABLISHED)
```
5. 帯域幅を消費するプロセスを確認して、プロセスが正常に動作しているかを判断します。
 - 帯域幅を大量に消費するプロセスが業務プロセスである場合、アクセス量の変化によるか、および容量を最適化する必要があるか、或は[CVM設定をアップグレード](https://intl.cloud.tencent.com/document/product/213/2178)する必要があるかどうかを確認します。
 - 帯域幅を大量に消費するプロセスが異常なプロセスである場合は、ウイルス或はトロイの木馬が原因である可能性があります。プロセスを自分で終了する或はセキュリティソフトウェアを使用してウイルスを駆除できます。データのバックアップ後にシステムを再インストールすることもできます。
 - 帯域幅を大量に消費するプロセスがTencent Cloudコンポーネントプロセスである場合は、[チケットを送信](https://console.intl.cloud.tencent.com/workorder/category) してお問い合わせください。問題に対処し、解決策を特定できるよう支援します。


対象側IPアドレスの所在地を重点的にチェックすることをお勧めします。[IP138検索サイト](http://www.ip138.com/)でIPアドレス所在地を検索できます。対象側IPのアドレスの所在地が海外である場合は、リスクが高く、重点的に注意してください。

:::
</dx-tabs>





