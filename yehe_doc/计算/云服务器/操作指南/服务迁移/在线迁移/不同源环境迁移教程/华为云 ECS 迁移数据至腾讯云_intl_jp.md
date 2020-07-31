## 1. 移行ツールの取得  
 [ここをクリック](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip) して、移行ツールの圧縮ファイルをダウンロードします。

## 2. ネットワーク環境に応じて移行モードの選択
移行元サーバーと移行先CVMのネットワーク環境に応じて、適切な移行モードを選択します。
現在、移行ツールはデフォルトモードとプライベートネットワークモードをサポートしています。その中で、プライベートネットワークモードは3つのシナリオに適用されます。異なる移行モード/シナリオは、移行元サーバーと移行先CVMのネットワーク要件が異なります。移行元サーバーと移行先CVMの両方がパブリックネットワークにアクセスできる場合、デフォルトモードを使用して移行できます。移行元サーバーまたは移行先CVMがパブリックネットワークに直接アクセスできない場合、まず[VPC Peering Connection](https://intl.cloud.tencent.com/document/product/553)、[VPN Connections](https://intl.cloud.tencent.com/document/product/1037)、[Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003)或は[Direct Connect](https://intl.cloud.tencent.com/document/product/216)等の方法で接続を確立してから、プライベートネットワークモードで移行を実行します。

## 3. データのバックアップ
- 移行元サーバー：Huawei Cloudスナップショット機能を使用するか、他の方法を使用してデータをバックアップできます。
- 移行先CVM： [スナップショットの作成](https://intl.cloud.tencent.com/document/product/362/5755) などの方法でデータをバックアップできます。

## 4. 移行前の確認
移行する前に、移行元サーバーと移行先CVMを別々に確認する必要があります。移行元サーバーと移行先CVMを確認する必要がある内容は以下のように：
<table>
	<tr><th style="width: 15%;">移行先CVM</th><td><ol  style="margin: 0;"><li>ストレージスペース：移行先CVMのCBS（システムディスクとデータディスクを含む ）には、ソースデータを保存するための十分なストレージスペースが必要です。 </li><li>セキュリティグループ：セキュリティグループでポート443とポート80が開いている必要があります。</li><li>帯域幅の設定：移行を高速化するために、受信帯域幅と送信帯域幅を増やすことをお勧めします。移行中に、データ量とほぼ同じのトラフィック消費が発生します、必要に応じて事前にネットワーク課金モードを調整してください。</li><li>移行先CVMと移行元サーバーのOSタイプが同じかどうか：OSは異なる場合は後で作成されるイメージが実際のOSとの間に不整合が生じます。移行元サーバーと移行先CVMの両方で同じOSを使用することをお勧めします。たとえば、CentOS 7システムがインストールされている移行元サーバーを移行する場合は、CentOS 7システムがインストールされているCVMを移行先として選択します。 </li></ol></td></tr>
	<tr><th>Linux 移行元サーバー</th><td><ol  style="margin: 0;"><li> Virtioを確認してインストールします。詳細については、 <a href="https://intl.cloud.tencent.com/document/product/213/9929">LinuxでのVirtioドライバーの確認</a>をご参照ください。</li><li> <code>which rsync</code>コマンドを実行して、rsyncがインストールされているかどうかを確認します。</li><li> SELinux が有効になっているかどうかを確認します。 SELinuxが有効になっている場合は無効にします。</li><li>移行リクエストがTencent Cloud APIに送信されると、Tencent Cloud APIは現在の UNIXタイムスタンプを使用して生成されたTokenをチェックするため、現在のシステム時間が正しいことを確保してください。</li><li><code>cloud-init --version</code>コマンドを実行して、移行元サーバーでインストールされているcloud-init のバージョン情報を確認します。<ul><li><code>17.1</code>より前のバージョンがインストールされている場合、当該cloud-initをアンインストールまたは削除することをお勧めします。</li><li>移行元サーバーにcloud-initがインストールされていない場合は、この手順をスキップしてください。</li></ul></li></ol></td></tr>　　
</table>

>? 
> - `sudo ./go2tencentcloud_x64 --check`などのツールコマンドを使用して、移行元サーバーを自動的に確認できます。
> -  「go2tencentcloud」移行ツールは、実行を開始すると、デフォルトで移行元サーバーを自動的にチェックします。このチェックをスキップして強制的に移行する場合は、 client.json ファイルの`Client.Extra.IgnoreCheck`フィールドの値を`true`に設定してください。
> - 「go2tencentcloud」移行ツールの詳細については、[移行ツールの説明](https://intl.cloud.tencent.com/document/product/213/35640)をご覧ください。
> 


## 5. 移行の開始
 
1. （オプション）移行元サーバーと移行先CVMとの間に接続を確立する。  
 - プライベートネットワーク移行モードを選択する場合は、[VPC Peering Connection](https://intl.cloud.tencent.com/document/product/553)、 [VPN Connections](https://intl.cloud.tencent.com/document/product/1037)、[CCN](https://intl.cloud.tencent.com/document/product/1003) 或は[Direct Connect](https://intl.cloud.tencent.com/document/product/216) 等の方法を介して移行元サーバーと移行先CVMとの間に接続を確立する必要があります。
 - デフォルトモードを選択する場合は、この手順をスキップしてください。
2.  user.json ファイルを構成する。
user.json ファイルは、移行元サーバーと移行先CVMを構成するために使用されます。次の構成アイテムが含まれています。
 - アカウントのAPIアクセスキーペア、つまり、SecretIdとSecretKeyです。詳細については、[アクセスキー](https://intl.cloud.tencent.com/document/product/598/32675)をご参照ください。
 - 移行先CVMの存在するリージョン。
 - 移行先CVMのインスタンス ID。
 - (オプション)　移行元サーバーのデータディスク構成。  
3.  client.json ファイルを構成する。
「client.json」ファイルは、移行モードとその他のパラメーターを構成するために使用されます。どの移行モード/シナリオを選択しても、client.jsonファイルでClient.Net.Modeパラメータを構成する必要があります。
4. （オプション）移行元サーバーで移行する必要のないファイルとディレクトリを削除します。  
 Linuxサーバーに「rsync\_excludes\_linux.txt」ファイルを編集して、移行する必要のないファイルとディレクトリを削除します。
5. ツールを実行する
例えば、64ビットのLinuxソースサーバーで、root権限を指定して次のコマンドを実行し、ツールを実行します。
```
sudo ./go2tencentcloud_x64
```
ツールが実行した後、移行プロセスが完了するまでお待ちください。
移行が成功した後、次のコンソール出力情報が表示されます。
![](https://main.qcloudimg.com/raw/4768e5bbe1fd1deba16c78eea3a19b02.png)
