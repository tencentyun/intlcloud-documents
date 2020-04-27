## 1. マイグレーションツールを取得する  
 [ここをクリックして](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip)、マイグレーションツールの圧縮ファイルをダウンロードします 。

## 2. ネットワーク環境に応じてマイグレーションモードを確定する
移行元サーバーと移行先CVMのネットワーク環境に基づいて、適切なマイグレーションモードを確定します。
現在マイグレーションツールはデフォルトモードとプライベートネットワークモードをサポートしています。その中で、プライベートネットワークモードは3つのシナリオに適用されます。異なるマイグレーションモード/シナリオは、移行元サーバーと移行先CVMのネットワーク要件も違います。移行元サーバーと移行先CVMの両方がパブリックネットワークにアクセスできる場合、デフォルトモードで直接マイグレーションできます。移行元サーバーまたは移行先CVMがパブリックネットワークに直接アクセスできない場合、まず[VPC Peering Connection](https://intl.cloud.tencent.com/document/product/215/5000)、[VPN Connections](https://intl.cloud.tencent.com/document/product/1037)、[Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003)或は[Direct Connect](https://intl.cloud.tencent.com/document/product/216)等の方法で接続を確立してから、プライベートネットワークモードでマイグレーションを実行します。

## 3. データのバックアップ
スナップショットの作成などの方法でデータをバックアップします。

## 4. マイグレーション前の確認
マイグレーションする前に、移行元サーバーと移行先CVMを別々に確認する必要があります。移行元サーバーと移行先CVMを確認する必要がある内容は以下のように：
<table>
	<tr><th style="width: 15%;">移行先CVM</th><td><ol  style="margin: 0;"><li>ストレージスペース：移行先CVMのCBS（システムディスクとデータディスクを含む ）には、ソースデータを保存するための十分なストレージスペースが必要です。 </li><li>セキュリティグループ：セキュリティグループでポート443とポート80が開いている必要があります。</li><li>帯域幅の設定：マイグレーションを高速化するために、帯域幅を増やすことをお勧めします。マイグレーション中に、データ量とほぼ同じのトラフィック消費が発生します、必要に応じて事前にネットワーク課金モードを調整してください。</li><li>移行先CVMと移行元サーバーのOSタイプが同じかどうか：OSは異なる場合は後で作成されるイメージの情報が実際のOSと一致しなくなります。移行先CVMと移行元サーバーで同じOSを使用することをお勧めします。</li></ol></td></tr>
	<tr><th>Linux ソースサーバー</th><td><ol  style="margin: 0;"><li> Virtioを確認してインストールします。詳細については、 <a href="https://intl.cloud.tencent.com/document/product/213/9929">LinuxでのVirtioドライバーの確認</a>をご参照ください。</li><li> rsync と grub2-install（或は grub-install）がインストールされているかどうかを確認します。</li><li> SELinux がオンになっているかどうかを確認します。 SELinux がオンになっている場合は、 SELinuxを閉じてください。</li><li>マイグレーションリクエストがTencent Cloud APIに送信されると、TencentCloud APIは現在の UNIX 時間を使用して生成されたTokenを確認します、現在のシステム時間が正しいことを確保してください。</li></ol></td></tr>
</table>

> 
> - ツールコマンドを使用して、ソースサーバーのチェックを自動化できます（例：sudo ./go2tencentcloud_x64 --check）。
> - go2tencentcloud マイグレーションツールは実行開始時に、デフォルトで自動的にチェックします。チェックをスキップして強制マイグレーションする必要がある場合は、 client.json ファイルの`Client.Extra.IgnoreCheck`フィールドを`true`に設定してください。
> 

## 5. マイグレーションを開始する
 
1. 移行元サーバーと移行先CVM間で接続を確立します。（オプション）  
 - プライベートネットワークマイグレーションモードを選択する場合は、[VPC Peering Connection](https://intl.cloud.tencent.com/document/product/215/5000)、 [VPN Connections](https://intl.cloud.tencent.com/document/product/1037)、[CCN](https://intl.cloud.tencent.com/document/product/1003) 或は[Direct Connect](https://intl.cloud.tencent.com/document/product/216) 等の方法を介して移行元サーバーと移行先CVM間で接続を確立する必要があります。
 - デフォルトモードを選択する場合は、この手順をスキップしてください。
2.user.json ファイルを構成します。
user.json は移行元サーバーと移行先CVMを構成するためのファイルです。次の構成アイテムが含まれています。
 - アカウントのAPIアクセスキーペア、つまり、SecretIdとSecretKeyです。詳細情報については[アクセスキー](https://intl.cloud.tencent.com/document/product/598/32675)をご参照ください。
 - 移行先CVMの存在するリージョン。
 - 移行先CVMのインスタンス ID。
 - 移行元サーバーのデータディスク設定。(オプション)  
3. client.json ファイルを構成する。
client.json はマイグレーションモードとその他のマイグレーション構成項目を設定するためのファイルです。どのマイグレーションモード/シナリオを選択しても、client.jsonファイルでClient.Net.Modeパラメータを構成する必要があります。
4.マイグレーションする必要のないサーバー上のファイルとディレクトリを削除します。（オプション）  
 Linuxソースサーバーのrsync\_excludes\_linux.txt ファイルを編集して、マイグレーションする必要のないファイルとディレクトリを削除します。
5. ツールを実行する
例えば、64ビットのLinuxソースサーバーで、root権限を指定して次のコマンドを実行し、ツールを実行します。
```
sudo ./go2tencentcloud_x64
```
ツールが実行した後、マイグレーションプロセスが完了するまでお待ちください。
マイグレーションが成功した後、次のコンソール出力情報が表示されます。
 ![](https://main.qcloudimg.com/raw/0b53a6ecdfe9180a11d81bdb6ef6ca74.png)
