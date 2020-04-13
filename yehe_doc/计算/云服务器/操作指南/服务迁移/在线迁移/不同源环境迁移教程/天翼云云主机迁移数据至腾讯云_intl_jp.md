## 1. マイグレーションツールを取得する  
 [ここをクリックして](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip)、マイグレーションツールの圧縮ファイルをダウンロードします 。
 
## 2. ネットワーク環境に応じてマイグレーションモードを確定する
ソースホストとターゲットCVMのネットワーク環境に基づいて、適切なマイグレーションモードを確定します。
現在マイグレーションツールはデフォルトモードとプライベートネットワークマイグレーションモードをサポートしています。その中で、プライベートネットワークマイグレーションモードは3つのユースケースに細かく分かれます。異なるマイグレーションモード/ユースケースは、ソースホストとターゲットCVMのネットワーク要件も違います。 ソースホストとターゲットCVM両方がパブリックネットワークにアクセスできる場合、デフォルトモードで直接マイグレーションできます。ソースホストとターゲットCVMのどっちがパブリックネットワークに直接アクセスできない場合、まず[VPC Peering Connection](https://intl.cloud.tencent.com/document/product/215/5000)、[VPN Connections](https://intl.cloud.tencent.com/document/product/1037)、[Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003)或は[Direct Connect](https://intl.cloud.tencent.com/document/product/216)等の方法で接続コネクションを確立し、プライベートネットワークモードでマイグレーションを実行します。

## 3. データのバックアップ
スナップショットの作成などの方法でデータバックアップを選択できます。

## 4. マイグレーション前の確認
マイグレーションの前に、ソースホストとターゲットCVMを別々に確認する必要があります。ソースホストとターゲットCVMを確認する必要がある内容は以下のように：
<table>
	<tr><th style="width: 15%;">ターゲットCVM</th><td><ol  style="margin: 0;"><li>ストレージキャパシティー：ターゲットCVMのCBS（システムディスクとデータディスクを含む ）には十分なストレージキャパシティーがあってソースデータを格納します。 </li><li>セキュリティグループ：セキュリティグループでポート443とポート80を制限できません。</li><li>帯域幅の設定：マイグレーションを高速化するために、両端の帯域幅を可能な限り増やすことをお勧めします。マイグレーションの中、データ量とほぼ同じのトラフィック消費が発生します、必要に応じて事前にネットワーク費用モードを調整してください。</li><li>ターゲットCVMとソースホストのOSタイプが同じかどうか：OSは異なる場合は後続作成したイメージの情報が実際のOSと一致しなくなります。ターゲットCVMのOSはソースホストのOSとなるべく同じタイプを使うことお勧めします。例えば、CentOS 7 からソースホストをマイグレーションする場合、一台の CentOS 7 のCVMがマイグレーションターゲットとして選択します。</li></ol></td></tr>
	<tr><th>Linux ソースホスト</th><td><ol  style="margin: 0;"><li> Virtioを確認してインストールします。詳細については、 <a href="https://intl.cloud.tencent.com/document/product/213/9929">Linux システム検査の Virtio ドライバー</a>をご参照ください。</li><li> rsync と grub2-install（或は grub-install）がインストールされているかどうかを確認します。</li><li> SELinux がオンになっているかどうかを確認します。 SELinux がオンになっている場合は、 SELinuxを閉じてください。</li><li>TencentCloud APIへのマイグレーションリクエストを発行した後、TencentCloud APIは現在の UNIX 時間を使用して生成されたTokenを確認します、現在のシステム時間が正しいことを確保してください。</li></ol></td></tr>
</table>

> 
> - ソースホストチェックはコマンドを使用して自動的にチェックできます。例えば `sudo ./go2tencentcloud_x64 --check`。
> - go2tencentcloud マイグレーションツールは実行開始時に、デフォルトで自動的にチェックします。チェックをスキップして強制マイグレーションする必要がある場合は、 client.json ファイルの`Client.Extra.IgnoreCheck`フィールドを`true`に設定してください。
> 

## 5. マイグレーションを開始する
 
1. ソースホストとターゲットCVMの間に接続コネクションを確立します。（オプション）  
 - プライベートネットワークマイグレーションモードを選択する場合は、[VPC Peering Connection](https://intl.cloud.tencent.com/document/product/215/5000)、 [VPN Connections](https://intl.cloud.tencent.com/document/product/1037)、[CCN](https://intl.cloud.tencent.com/document/product/1003) 或は[Direct Connect](https://intl.cloud.tencent.com/document/product/216) 等の方法を通してソースホストとターゲットCVMの接続コネクションを確立する必要があります。
 - デフォルトモードを選択する場合は、この手順をスキップしてください。
2.  user.json ファイルを設定します。
user.json はソースホストとターゲットCVMを設定するファイルです。このファイルの設定項目は以下のように：
 - アカウントのAPIアクセスキー SecretId と SecretKeyについて、詳細情報については[アクセスキー](https://intl.cloud.tencent.com/document/product/598/32675)をご参照ください。
 - ターゲットCVMの所在リージョン。
 - ターゲットCVMのインスタンス ID。
 - ソースホストのデータディスク設定。(オプション)  
3.  client.json ファイルを設定する。
client.json はマイグレーションモードとその他のマイグレーション設定項目を設定するファイルです。どのマイグレーションモード/ユースケースを選択しても、 client.json の`Client.Net.Mode`項目に対応するパラメータ値を設定する必要があります。
4. ソースホスト上のマイグレーションに必要のないファイルとディレクトリを排除します。（オプション）  
  Linux ソースホスト上の rsync\_excludes\_linux.txt ファイルを編集して、マイグレーションに必要のないファイルとディレクトリを除外します。
5. ツールを実行します。
例えば、64ビット Linux ソースホストで、ルート権限で次のコマンドを実行してツールを実行します。
```
sudo ./go2tencentcloud_x64
```
ツールが実行した後、マイグレーションプロセスが完了するまでお待ちください。
マイグレーション成功のコンソール出力は以下のように：
 ![](https://main.qcloudimg.com/raw/0a9f9d7ab225cbd857184b466d869ee4.png)
