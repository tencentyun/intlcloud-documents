リージョン間データ移行は、Tencent CloudのあるリージョンのあるアベイラビリティゾーンにあるCVMのデータを、別のリージョンのアベイラビリティゾーンにあるターゲットCVMに移行します。または、Tencent Cloudの同じリージョン内の異なるアベイラビリティゾーンにあるCVM間でデータ移行を実行することもできます。

## 1. 移行ツールの取得  
 [ここをクリックして](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip)、移行ツールの圧縮ファイルをダウンロードします。

## 2. ネットワーク環境に応じて移行モードの選択
移行元サーバーと移行先CVMのネットワーク環境に応じて、適切な移行モードを選択します。
現在、移行ツールはデフォルトモードとプライベートネットワーク移行モードをサポートしています。その中で、プライベートネットワーク移行モードは3つのシナリオに適用されます。異なる移行モード/シナリオは、移行元サーバーと移行先CVMのネットワーク要件が異なります。移行元サーバーと移行先CVMの両方がパブリックネットワークにアクセスできる場合、デフォルトモードを使用して移行できます。移行元サーバーまたは移行先CVMがパブリックネットワークに直接アクセスできない場合、まず[VPC Peering Connection](https://intl.cloud.tencent.com/document/product/553)、[VPN Connections](https://intl.cloud.tencent.com/document/product/1037)、[Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003)或は[Direct Connect](https://intl.cloud.tencent.com/document/product/216)等の方法で接続を確立してから、プライベートネットワークモードで移行を実行します。

## 3.  データのバックアップ
 [スナップショットの作成](https://intl.cloud.tencent.com/document/product/362/5755)などの方法を選択してデータをバックアップできます。

## 4. 移行前の確認
移行する前に、移行元サーバーと移行先CVMを別々に確認する必要があります。移行元サーバーと移行先CVMを確認する必要がある内容は以下のように：
<table>
	<tr><th style="width: 15%;">移行先CVM</th><td><ol  style="margin: 0;"><li>ストレージスペース：移行先CVMのCBS（システムディスクとデータディスクを含む ）には、ソースデータを保存するための十分なストレージスペースが必要です。</li><li>セキュリティグループ：セキュリティグループでポート443とポート80が開いている必要があります。</li><li>帯域幅の設定：移行を高速化するために、受信帯域幅と送信帯域幅を増やすことをお勧めします。移行中に、データ量とほぼ同じのトラフィック消費が発生します、必要に応じて事前にネットワーク課金モードを調整してください。</li><li>移行先CVMと移行元サーバーのOSタイプが同じかどうか：OSが異なると、後で作成されるイメージと実際のOSの間に不整合が生じます。移行元サーバーと移行先CVMの両方で同じOSを使用することをお勧めします。たとえば、CentOS 7システムがインストールされている移行元サーバーを移行する場合は、CentOS 7システムがインストールされているCVMを移行先として選択します。</li></ol></td></tr>
	<tr><th>Linux移行元サーバー</th><td><ol  style="margin: 0;"><li>Virtioを確認してインストールします。詳細については、<a href="https://intl.cloud.tencent.com/document/product/213/9929">LinuxでのVirtioドライバーの確認</a>をご参照ください。</li><li>rsyncがインストールされているかどうかを確認するには、<code>which rsync</code>コマンドを実行して検証を行います。</li><li>SELinux が有効になっているかどうかを確認します。SELinuxが有効になっている場合は無効にします。</li><li>移行リクエストがTencent Cloud APIに送信されると、Tencent Cloud APIは現在の UNIXタイムスタンプを使用して生成されたTokenをチェックするため、現在のシステム時間が正しいことを確保してください。</li></ol></td></tr>
</table>

>? 
> - `sudo ./go2tencentcloud_x64 --check`などのツールコマンドを使用して、移行元サーバーを自動的にチェックします。
> - 「go2tencentcloud」移行ツールは、実行を開始すると、デフォルトで移行元サーバーを自動的にチェックします。このチェックをスキップして強制的に移行する場合は、 client.json ファイルの`Client.Extra.IgnoreCheck`フィールドの値を`true`に設定してください。
> -  「go2tencentcloud」移行ツールの詳細については、[移行ツールの説明](https://intl.cloud.tencent.com/document/product/213/35640)をご覧ください。
 > 

## 5. 移行の開始

1. （オプション）移行元サーバーと移行先CVMとの間に接続を確立する。 
 - プライベートネットワーク移行モードを選択する場合は、[VPC Peering Connection](https://intl.cloud.tencent.com/document/product/553)、 [VPN Connections](https://intl.cloud.tencent.com/document/product/1037)、[Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003) 或は[Direct Connect](https://intl.cloud.tencent.com/document/product/216)等の方法を介して移行元サーバーと移行先CVMとの間に接続を確立する必要があります。
 - デフォルトモードを選択する場合は、この手順をスキップしてください。
2.  user.json ファイルを構成する。
user.json ファイルは、移行元サーバーと移行先CVMを構成するために使用されます。次の構成アイテムが含まれています。
 - アカウントのAPIアクセスキーペア、つまり、SecretIdとSecretKeyです。詳細情報については[アクセスキー](https://intl.cloud.tencent.com/document/product/598/32675)をご参照ください。
 - 移行先CVMの存在するリージョンとインスタンス ID。CVMでサポートされているリージョンの詳細については、[リージョンとアベイラビリティーゾーン](https://intl.cloud.tencent.com/document/product/213/6091)をご参照ください。インスタンスIDは、[インスタンスリスト](https://console.cloud.tencent.com/cvm/instance/index?rid=1)ページで確認できます。
 - 移行元サーバーのデータディスク設定。（オプション）  
3.  client.json ファイルを構成する。
「client.json」ファイルは、移行シナリオおよびその他の移行パラメーターを構成するために使用されます。どの移行モード/シナリオを選択しても、client.jsonファイルで `Client.Net.Mode` パラメータを構成する必要があります。
4. （オプション）移行元サーバーで移行する必要のないファイルとディレクトリを削除します。  
  Linuxソースサーバーに「rsync_excludes_linux.txt」ファイルを編集して、移行する必要のないファイルとディレクトリを削除します。
5. ツールを実行する。
例えば、64ビットのLinuxソースサーバーで、root権限を指定して次のコマンドを実行し、ツールを実行します。
```
sudo ./go2tencentcloud_x64
```
例えば、 [プライベートネットワーク移行モード：シナリオ2](https://intl.cloud.tencent.com/document/product/213/35640#Scenario2)を使用して移行する場合、移行が成功した後、次のコンソール出力情報が表示されます。
 ![](https://main.qcloudimg.com/raw/3d5c45ccb9f5350bb30cf3d3fce29590/console-cross-region.png)
