## 1. マイグレーションツールを取得する  
 [ここをクリック](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip)して、マイグレーションツールの圧縮ファイルをダウンロードします。

## 2. ネットワーク環境に応じてマイグレーションモードを確定します
移行元サーバーと移行先CVMのネットワーク環境に基づいて、適切なマイグレーションモードを確定します。
現在マイグレーションツールはデフォルトモードとプライベートネットワークマイグレーションモードをサポートしています。その中で、プライベートネットワークマイグレーションモードは3つのシナリオに適用されます。異なるマイグレーションモード/シナリオは、移行元サーバーと移行先CVMのネットワーク要件も違います。移行元サーバーと移行先CVMの両方がパブリックネットワークにアクセスできる場合、デフォルトモードで直接マイグレーションできます。移行元サーバーまたは移行先CVMのいずれかがパブリックネットワークに直接アクセスできない場合、まず[VPCピアリング接続](https://intl.cloud.tencent.com/document/product/553)、[VPN接続](https://intl.cloud.tencent.com/document/product/1037)、[CCN](https://intl.cloud.tencent.com/document/product/1003)または[ダイレクト接続](https://intl.cloud.tencent.com/document/product/216)等の方法で接続を確立してから、プライベートネットワークモードでマイグレーションを実行します。

## 3. データのバックアップ
移行元サーバー：仮想マシンのデータは、クローン作成またはその他のバックアップ方法でバックアップすることができます。
- 移行先CVM： [スナップショットの作成](https://intl.cloud.tencent.com/document/product/362/5755) などの方式を選択してデータをバックアップできます。

## 4. マイグレーション前の確認

イグレーションする前に、移行元サーバーと移行先CVMを別々に確認する必要があります。移行元サーバーと移行先CVMを確認する必要がある内容は以下のとおりです：
<table>
	<tr><th style="width: 15%;">移行先CVM</th><td><ol  style="margin: 0;"><li>ストレージスペース：移行先CVMのCBS（システムディスクとデータディスクを含む）には、移行元のデータを保存するための十分なストレージスペースが必要です。</li><li>セキュリティグループ：セキュリティグループでポート443とポート80が開いている必要があります。</li><li>帯域幅の設定：移行を高速化するために、受信帯域幅と送信帯域幅を増やすことをお勧めします。移行中に、データ量とほぼ同じのトラフィック消費が発生します。必要に応じて事前にネットワーク課金モードを変更してください。</li><li>移行先CVMと移行元サーバーのOSタイプが同じかどうか：OSが異なる場合は、後で作成されるイメージの情報と実際のOSとの間に不整合が生じます。移行先CVMと移行元サーバーの両方で同じOSを使用することをお勧めします。例えば、CentOS 7システムがインストールされている移行元サーバーを移行する場合は、CentOS 7システムがインストールされているCVMを移行先として選択します。</li></ol></td></tr>
	<tr><th>Linux移行元サーバー</th><td><ol  style="margin: 0;"><li>Virtioを確認してインストールします。詳細については、<a href="https://intl.cloud.tencent.com/document/product/213/9929">LinuxでのVirtioドライバーの確認</a>をご参照ください。</li><li>rsyncがインストールされているかどうかを確認します。</li><li>SELinuxが有効になっているかどうかを確認します。SELinuxが有効になっている場合は、SELinuxを無効にしてください。</li><li>移行リクエストがTencent Cloud APIに送信されると、APIは現在のUNIXタイムスタンプを使用して発行されたTokenをチェックします。現在のシステム時間が正しいことを確認してください。</li><li>移行元サーバーがDHCPサービスを有効にしているかどうかを確認します。DHCPサービスが有効でない場合は、DHCPサービスを有効にしてください。</li></ol></td></tr>
</table>

>? 
> - `sudo ./go2tencentcloud_x64 --check`などのツールコマンドを使用して、移行元サーバーを自動的にチェックできます。
> - go2tencentcloudマイグレーションツールは、実行を開始すると、デフォルトで移行元サーバーを自動的にチェックします。このチェックをスキップして強制的に移行する場合は、client.json ファイルの`Client.Extra.IgnoreCheck`フィールドの値を`true`に設定してください。
> - go2tencentcloud マイグレーションツールの詳細は、 [マイグレーションツールの説明](https://intl.cloud.tencent.com/document/product/213/35640)をご参照ください。


## 5. マイグレーションの開始

1. 移行元サーバーと移行先CVMの間に接続チャネルを確立する。（オプション）  
 - プライベートネットワークマイグレーションモードを選択する場合は、[VPCピアリング接続](https://intl.cloud.tencent.com/document/product/553)、 [VPN接続](https://intl.cloud.tencent.com/document/product/1037)、[CCN](https://intl.cloud.tencent.com/document/product/1003) または[ダイレクト接続](https://intl.cloud.tencent.com/document/product/216)などの方法を介して移行元サーバーと移行先CVM間で接続チャネルを確立する必要があります。
 - デフォルトモードを選択する場合は、この手順をスキップしてください。
2.  user.json ファイルを設定する。
user.json は移行元サーバーと移行先CVMを構成するためのファイルです。次の構成アイテムが含まれています。
 - アカウントのAPIアクセスキーペアは、SecretIdとSecretKeyです。詳細情報については[アクセスキー](https://intl.cloud.tencent.com/document/product/598/32675)をご参照ください。
 - 移行先CVMが所在するリージョン、CVMがサポートするリージョンについては[リージョンとアベイラビリティーゾーン](https://intl.cloud.tencent.com/document/product/213/6091) をご参照ください。
 - 移行先CVMのインスタンスIDは、[インスタンスリスト](https://console.cloud.tencent.com/cvm/instance/index?rid=1)画面で確認できます。
 - 移行元サーバーのデータディスク設定。（オプション）  
3.  client.json ファイルを設定する。
client.json はマイグレーションモードとその他のマイグレーション設定項目を設定するためのファイルです。どのマイグレーションモード/シナリオを選択しても、client.jsonファイルの‵Client.Net.Mode‵項目で対応するパラメータ値を設定する必要があります。
4. 移動元サーバー上でマイグレーション不要のファイルとディレクトリを削除する。（オプション）  
 Linux移行元サーバーでrsync\_excludes\_linux.txt ファイルを編集して、マイグレーションする必要のないファイルとディレクトリを削除します。
5. ツールを実行する。
例えば、64ビットのLinux移行元サーバーで、root権限を指定して次のコマンドを実行し、ツールを実行します。
```
sudo ./go2tencentcloud_x64
```
ツールが実行した後、マイグレーションプロセスが完了するまでお待ちください。
通常、マイグレーションが成功すると、コンソールから次の内容が出力されます。
 ![](https://main.qcloudimg.com/raw/146fb9e1bbccb594e128648c4a723a6c.png)
