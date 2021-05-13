## 概要
オンライン移行とは、システムを中断することなく、サーバーや仮想マシン上のシステム、サービスプログラムなどを、自社のデータセンター（IDC）やクラウドプラットフォームなどの移行元環境からTencent Cloudに同期移行することです。
Tencent Cloudは、[go2tencentcloud移行ツール](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip)を提供しており、移行元サーバーで移行ツールを実行した後、移行元サーバー全体をTencent Cloudの移行先CVMに移行することができます。この移行ツールは、イメージの作成、アップロード、インポートの手間を省き、移行元サーバーから直接クラウドに移行することで、企業データのクラウドへの移行、クラウドプラットフォーム間での移行、アカウント/地域間で1の移行、ハイブリッドクラウドの展開などのサービスニーズを容易に実現します。

## 移行ツールの説明

### サポートされている移行モード

<span id="DefaultMode"></span>
#### デフォルトモード
移行元サーバーと移行先CVMの両方がパブリックネットワークにアクセスできる場合は、デフォルトモードを使用して移行できます。
現在のデフォルトモードでは、移行元サーバーがインターネットを介してTencent Cloud APIを呼び出して移行要求を送信し、移行先CVMにデータを転送し、移行元サーバーをTencent Cloudの移行先CVMに移行します。
![](https://main.qcloudimg.com/raw/5203e535f5ba947bb67c1f91dee52f1f.jpg)

#### プライベートネットワーク移行モード
ユーザーの移行元サーバーまたは移行先CVMがあるプライベートネットワークまたはVPCにあり、移行元サーバーが移行先CVMとインターネットを介して直接接続を確立できない場合、ツールのプライベートネットワーク移行モードを使用して移行を行うことができます。プライベートネットワーク移行モードは、[VPC Peering Connection](https://intl.cloud.tencent.com/document/product/553)、 [VPN Connections](https://intl.cloud.tencent.com/document/product/1037)、[CCN](https://intl.cloud.tencent.com/document/product/1003) 或いは[Direct Connect](https://intl.cloud.tencent.com/document/product/216)などの方法によって移行元サーバーと移行先CVM間で接続チャネルを確立する必要があります。

- <span id="Scenario1">シナリオ1</span>：移行元サーバーまたは移行先CVMがパブリックネットワークにアクセスできない場合は、パブリックネットワークへのアクセス機能（ゲートウェイなど）を備えるサーバーを介してインターネット経由でTencent Cloud APIにアクセスして移行要求を送信し、接続チャネルを介して移行先CVMにデータを転送して移行することができます。このシナリオでは、移行元サーバーと移行先CVMへのパブリックネットワークアクセス機能は必要ありません。
![](https://main.qcloudimg.com/raw/19300ddf557d4534b1cd77fcbf64ef6a.jpg)
- <span id="Scenario2">シナリオ2</span>：移行元サーバーがパブリックネットワークにアクセスできる場合は、まず移行元サーバーでインターネットを介してTencent Cloud APIにアクセスして移行要求を送信し、次に接続チャネルを介して移行先CVMにデータを転送して移行することができます。このシナリオでは、移行元ホストへのパブリックネットワークアクセス機能が必要ですが、移行先CVMでは必要ありません。
![](https://main.qcloudimg.com/raw/90bf988ba7cddb9b80307efb30eaad29.jpg)
- <span id="Scenario3">シナリオ3</span>：移行元サーバーがプロキシを介してパブリックネットワークにアクセスできる場合は、まず移行元サーバーでネットワークプロキシを介してTencent Cloud APIにアクセスして移行要求を送信し、次に接続チャネルを介して移行先CVMにデータを転送して移行することができます。このシナリオでは、移行元サーバーと移行先CVMへのパブリックネットワークアクセス機能は必要ありません。
![](https://main.qcloudimg.com/raw/14f81f2c4e6cfff80d912841451c5b69.jpg)

### サポートされているOS
現在オンライン移行ツールによりサポートされているOSには、以下のようなOSなどが含まれますが、これらに限定されません（32ビットまたは64ビットのいずれでも構いません）。
<table>
	<tr><th>Linux OS</th><th>Windows OS</th></tr>
	<tr><td>CentOS 5/6/7</td><td rowspan=7>-</td></tr>
	<tr><td>Ubuntu 10/12/14/16/18	</td></tr>
	<tr><td>Debian 7/8/9	</td></tr>
	<tr><td>SUSE 11/12/15</td></tr>
	<tr><td>openSUSE 42</td></tr>
	<tr><td>Amazon Linux AMI</td></tr>
	<tr><td>Red Hat 7/8</td></tr>
</table>

### 圧縮パッケージファイルの説明

<table>
	<tr><th>ファイル名</th><th>説明</th></tr>
	<tr><td>go2tencentcloud_x64</td><td>64ビット Linux OS用の移行ツールの実行可能プログラム。</td></tr>
	<tr><td>go2tencentcloud_x32</td><td>32ビット Linux OS用の移行ツールの実行可能プログラム。</td></tr>
	<tr><td>user.json</td><td>移行時の移行元サーバーと移行先CVMの構成ファイル。<a href="#userJsonState">user.jsonファイルパラメータの説明</a>に従って構成を変更してください。</td></tr>
	<tr><td>client.json</td><td>移行ツールの構成ファイル。<a href="#clientJsonState">client.jsonファイルパラメータの説明</a>に従って構成を変更してください。</td></tr>
	<tr><td>rsync_excludes_linux.txt</td><td>rsync構成ファイル。Linuxシステムで移行する必要のないファイルとディレクトリを除外します。</td></tr>
</table>

>  構成ファイルは削除できません。構成ファイルをgo2tencentcloudの実行可能プログラムと同じフォルダーに保存する必要があります。 
>

- <span id="userJsonState">user.jsonファイルパラメータの説明：</span>
<table>
	<tr><th>パラメータ名</th><th>タイプ</th><th>入力必須かどうか</th><th>説明</th></tr>
	<tr><td>SecretId</td><td>String</td><td>はい</td><td>APIにアクセスするためにアカウントで使用されるSecretIdです。詳細については、<a href="https://intl.cloud.tencent.com/document/product/598/32675">アクセスキー</a>をご参照ください。</td></tr>　
	<tr><td>SecretKey</td><td>String</td><td>はい</td><td>APIにアクセスするためにアカウントで使用されるSecretIdです。詳細については、<a href="https://intl.cloud.tencent.com/document/product/598/32675">アクセスキー</a>をご参照ください。</td></tr>
	<tr><td>Region</td><td>String</td><td>はい</td><td>移行先CVMのリージョンであり、アベイラビリティーゾーンでなく、リージョンのみを記入する必要はあります。値の詳細については、<a href="https://intl.cloud.tencent.com/document/product/213/6091">リージョン</a>リストをご参照ください。</td></tr>
	<tr><td>InstanceId</td><td>String</td><td>はい</td><td>移行先CVMのインスタンスIDであり、例えば、<code>ins-xxxxxxxx</code>。</td></tr>
	<tr><td>DataDisks</td><td>Array</td><td>いいえ</td><td>移行元サーバーから移行するデータディスクのリストです。 各エントリは1つのデータディスクを表し、最大20個のデータディスクがサポートされます。</td></tr>
	<tr><td>DataDisks.Index</td><td>Integer</td><td>はい</td><td>データディスク番号です。値の範囲は[1，20]であり、値<code>1</code>は、このデータディスクが移行先CVMにマウントされた最初のデータディスクに移行することを意味し、値<code>2</code>は移行先CVMにマウントされた2番目のデータディスクに移行することを意味します。以下同様です。</td></tr>
	<tr><td>DataDisks.Size</td><td>Integer</td><td>はい</td><td>移行元サーバー上のデータディスクのサイズ（GB）です。値の範囲は[10,160 00]です。</td></tr>
	<tr><td>DataDisks.MountPoint</td><td>String</td><td>はい</td><td>移行元サーバー上のデータディスクのマウントポイントです。例えば、<code>"/mnt/disk1"</code>。</td></tr>
</table>
例えば、Linux移行元サーバーをTencent Cloudの広州地域にあるCVMに移行すると、user.jsonファイルは次のように構成されます。

 ```json
{  
	"SecretId": "your secretId",
	"SecretKey": "your secretKey",  
	"Region": "ap-guangzhou",  
	"InstanceId": "your instance id"
}  
```
> 対応するパラメータ値を実際の構成パラメータに置き換える必要があります。
>
例えば、Linux移行元サーバー（マウントポイントは`/mnt/disk1`、サイズは`10`GBのデータディスクを含む）をTencent Cloud広州地域にある移行先CVM（少なくとも1つのデータディスクがマウントされる）に移行すると、user.jsonファイルは次のように構成されます。
```json
{  
	"SecretId": "your secretId",
	"SecretKey": "your secretKey",  
	"Region": "ap-guangzhou",  
	"InstanceId": "your instance id",
	"DataDisks": [
		{
			"Index": 1,
			"Size": 10,
			"MountPoint": "/mnt/disk1"
		}
	]
}  
```
例えば、Linux移行元サーバー（マウントポイントは`/mnt/disk1`、サイズは`10`GBであり、移行先CVMの最初のデータディスクに移行するディスク1と、マウントポイントは`/mnt/disk2`、サイズは`20`GBであり、移行先CVMの2番目のデータディスクに移行するディスク2とを含む）をTencent Cloud広州地域にある移行先CVM（少なくとも2つのデータディスクがマウントされる）に移行すると、user.jsonファイルは次のように構成されます。
```json
{  
	"SecretId": "your secretId",
	"SecretKey": "your secretKey",  
	"Region": "ap-guangzhou",  
	"InstanceId": "your instance id",
	"DataDisks": [
		{
			"Index": 1,
			"Size": 10,
			"MountPoint": "/mnt/disk1"
		},
		{
			"Index": 2,
			"Size": 20,
			"MountPoint": "/mnt/disk2"
		}
	]
}  
```
> 対応するパラメータ値を実際の構成パラメータに置き換える必要があります。
>
- <span id="clientJsonState">client.jsonファイルパラメータの説明：</span>
<table>
	<tr><th>パラメータ名</th><th>タイプ</th><th>入力必須かどうか</th><th>説明</th></tr>
	<tr><td>Client.Net.Mode</td><td>Integer</td><td>はい</td><td>デフォルト値は<code>0</code>であり、値の範囲は、<code>0</code>（<a href="#DefaultMode">デフォルトモード</a>）、<code>1</code>（<a href="#Scenario1">プライベートネットワーク移行モード：シナリオ1</a>）、<code>2</code>（<a href="#Scenario2">プライベートネットワーク移行モード：シナリオ2</a>）、<code>3</code>（<a href="#Scenario3">プライベートネットワーク移行モード：シナリオ3</a>）です。必要に応じて様々なモード/ケースの移行を実行して、対応するパラメータ値を入力してください。</td></tr>
	<tr><td>Client.Net.Proxy.Ip</td><td>String</td><td>いいえ</td><td>ネットワークプロキシのIPアドレスです。<a href="#Scenario3">プライベートネットワーク移行モード：シナリオ3</a>の移行が必要な場合は、このパラメータを指定する必要があります。</td></tr>
	<tr><td>Client.Net.Proxy.Port</td><td>Integer</td><td>いいえ</td><td>ネットワークプロキシのポートです。<a href="#Scenario3">プライベートネットワーク移行モード：シナリオ3</a>の移行が必要な場合は、このパラメータを指定する必要があります。</td></tr>
	<tr><td>Client.Net.Proxy.User</td><td>String</td><td>いいえ</td><td>ネットワークプロキシのユーザー名です。<a href="#Scenario3">プライベートネットワーク移行モード：シナリオ3</a>の移行が必要であり、ネットワークプロキシに認証が必要な場合は、ネットワークプロキシのユーザー名を入力してください。</td></tr>
	<tr><td>Client.Net.Proxy.Password</td><td>String</td><td>いいえ</td><td>ネットワークプロキシのパスワードです。<a href="#Scenario3">プライベートネットワーク移行モード：シナリオ3</a>の移行が必要であり、ネットワークプロキシに認証が必要な場合は、ネットワークプロキシのパスワードを入力してください。</td></tr>
	<tr><td>Client.Extra.IgnoreCheck</td><td>Bool</td><td>いいえ</td><td>デフォルト値は<code>false</code>です。移行ツールは、デフォルトでツールの起動時に移行元サーバーの環境を自動的にチェックします。このチェックを省略する必要がある場合は、<code>true</code>に設定してください。</td></tr>
	<tr><td>Client.Rsync.BandwidthLimit</td><td>String</td><td>いいえ</td><td>速度制限設定項目です。単位はKBytes/s、デフォルト値はNULLです。即ち、デフォルトの転送では速度制限はありません。</td></tr>
	<tr><td>Client.Rsync.Checksum</td><td>Bool</td><td>いいえ</td><td>転送チェック項目です。<code>true</code>に設定すると、転送の一貫性チェックが強化されますが、移行元サーバーのCPU負荷が増加し、転送速度が低下します。デフォルト値は<code>false</code>で、即ち、デフォルトではチェックされません。</td></tr>
</table>
<blockquote class="doc-tip"><p class="doc-tip-tit"><i class="doc-icon-tip"></i>説明：</p><p>上記のパラメータ以外、client.jsonファイルのその他の構成項目は通常、記入する必要はありません。</p>
</blockquote>
- <span id="_linuxTxtState">rsync\_excludes\_linux.txtファイル説明：</span>
このファイルは、移行や転送が不要なLinuxの移行元サーバーのファイル、または指定されたディレクトリにある構成ファイルを除外するために使用されます。次のディレクトリとファイルはデフォルトで除外されていますので、**既存の設定を削除または変更しないでください**。　
```sh
/dev/*
/sys/*
/proc/*
/var/cache/yum/*
/lost+found/*
/var/lib/lxcfs/*
/var/lib/docker-storage.btrfs/root/.local/share/gvfs-metadata/*
```
他のディレクトリやファイルを除外する必要がある場合は、ファイルの末尾にコンテンツを追加してください。例えば、`/mnt/disk1`にマウントされたデータディスクのすべてのコンテンツを除外するには、rsync_excludes_linux.txtファイルを次のように構成します。
```sh
/dev/*
/sys/*
/proc/*
/var/cache/yum/*
/lost+found/*
/var/lib/lxcfs/*
/var/lib/docker-storage.btrfs/root/.local/share/gvfs-metadata/*
/mnt/disk1/*
```

### 移行ツールのパラメーター
パラメータオプション|説明
---|---
`--help`|ヘルプ情報をプリントします。
`--check`|移行元サーバーをチェックし、移行は行われません。
`--log-file`|ログファイル名を設定し、デフォルトは`log`です。
`--log-level`|ログの出力レベル。値の範囲は`1`（ERRORレベル）、`2`（INFOレベル）、`3`（DEBUGレベル）、デフォルト値は`2`です。
`--clean`|移行先CVMは移行モードを強制的に終了させ、オンサイトをクリーンアップします。例えば、コンソールから`Please execute--cleanoption manually.`が表示された場合、このパラメーターを指定してツールを実行し、移行先CVMを移行モードから終了させる必要があります。
`--version`|バージョン番号をプリントします。

## 移行前の確認
移行する前に、移行元サーバーと移行先CVMを別々に確認する必要があります。移行元サーバーと移行先CVMを確認する必要がある内容は以下ののとおりです。
<table>
	<tr><th style="width: 15%;">移行先CVM</th><td><ol  style="margin: 0;"><li>ストレージスペース：移行先CVMのCBS（システムディスクとデータディスクを含む）には、移行元のデータを保存するための十分なストレージスペースが必要です。</li><li>セキュリティグループ：セキュリティグループでポート443とポート80が開いている必要があります。</li><li>帯域幅の設定：移行を高速化するために、帯域幅を増やすことをお勧めします。移行中に、データ量とほぼ同じのトラフィック消費が発生します。必要に応じて事前にネットワーク課金モードを調整してください。</li><li>移行先CVMと移行元サーバーのOSタイプが同じかどうか：OSが異なる場合は、後で作成されるイメージの情報が実際のOSと一致しなくなります。移行先CVMと移行元サーバーで同じOSを使用することをお勧めします。例えば、CentOS 7システムがインストールされている移行元サーバーを移行する場合は、CentOS 7システムがインストールされているCVMを移行先として選択します。</li></ol></td></tr>
	<tr><th>Linux移行元サーバー</th><td><ol  style="margin: 0;"><li>Virtioを確認してインストールします。詳細については、<a href="https://intl.cloud.tencent.com/document/product/213/9929">LinuxでのVirtioドライバーの確認</a>をご参照ください。</li><li>rsyncがインストールされているかどうかを確認するには、<code>which rsync</code>コマンドを実行して検証を行います。</li><li>SELinuxが有効になっているかどうかを確認します。SELinuxが有効になっている場合は、SELinuxを無効にします。</li><li>移行リクエストがTencent Cloud APIに送信されると、Cloud APIは現在のUNIX時間を使用して生成されたトークンをチェックします。現在のシステム時間が正しいことを確保してください。</li></ol></td></tr>
</table>

>? 
> - `sudo ./go2tencentcloud_x64 --check`などのツールコマンドを使用して、移行元サーバーを自動的にチェックします。
> - 「go2tencentcloud」移行ツールは、実行を開始すると、デフォルトで移行元サーバーを自動的にチェックします。このチェックをスキップして強制的に移行する場合は、client.json ファイルの`Client.Extra.IgnoreCheck`フィールドの値を`true`に設定してください。
> 

## 移行手順
Tencent Cloudが提供するgo2tencentcloud移行ツールは、移行プロセス全体を主に次の3つのステージに分けており、ユーザーがツールの実行中に移行の進行状況を直感的に把握することができます。
- **ステージ1**：リモートインスタンスの初期化
- **ステージ2**：データの転送
- **ステージ3**：リモートインスタンスのリリース

各ステージでは、関連する操作を実行するためにいくつかのサブタスクが生成されます。また、時間のかかるサブタスクの一部には、デフォルトの最大タイムアウト時間が設定されています。データ転送にかかる時間は、移行元サーバーのデータサイズやネットワーク帯域幅などの影響を受けるため、移行プロセスが完了するまでお待ちください。移行ツールでは、データ転送の一時停止/再開がサポートされています。

> 移行が開始されると、移行先CVMが移行モードになります。移行が完了して移行モードが終了するまで、移行先CVMに対してシステムの再インストール、シャットダウン、破棄、パスワードのリセットなどの操作を行わないでください。 
>

### デフォルトモードの移行手順

1. user.jsonファイルに移行元サーバーと移行先CVMを設定します。
[user.jsonファイルパラメータの説明](#userJsonState)に従って、必要なパラメーターを設定します。
2. client.jsonファイルに移行モードとその他の項目を設定します。
client.jsonファイルの`Client.Net.Mode`を`0`に設定すると、[デフォルトモード](#DefaultMode)を選択します。また、その他の設定が必要な場合は、[client.jsonファイルパラメータの説明](#clientJsonState)に従って設定してください。
3. （オプション）移行する必要のない移行元サーバー上のファイルとディレクトリを除外します。
Linux移行元サーバーを移行するときに、移行する必要のないファイルとディレクトリを除外する必要がある場合は、それらを[rsync\_excludes\_linux.txtファイル](#_linuxTxtState)に追加することができます。
4. ツールを実行します。
例えば、64ビットのLinux移行元サーバーで、rootユーザーとして次のコマンドを実行してツールを実行します。
```
sudo ./go2tencentcloud_x64
```
ツールの実行時にログファイル名とログ出力レベルを設定する必要がある場合は、次のコマンドを実行します。
```
sudo ./go2tencentcloud --log-file=my.log --log-level=3
```
ツールが実行した後、移行プロセスが完了するまでお待ちください。 
通常のデフォルトモードでは、移行が成功した場合、コンソールから次の内容が出力されます。
![](https://main.qcloudimg.com/raw/b056d6b1d5ac457ff43e48883848af01.png)

### プライベートネットワーク移行モードの移行手順

#### シナリオ1
1. 移行元サーバーと移行先CVMの間に接続チャネルを確立します。
[VPN Peering Connection](https://intl.cloud.tencent.com/document/product/553) / [VPN Connection](https://intl.cloud.tencent.com/document/product/1037) / [CCN](https://intl.cloud.tencent.com/document/product/1003) などの方法によって移行元サーバーと移行先CVMの間に接続チャネルを確立します。
2. user.jsonファイルに移行元ホストと移行先CVMを設定します。
 [user.jsonファイルパラメータの説明](#userJsonState)に従って、必要なパラメーターを設定します。
3. client.jsonファイルに移行モードとその他のパラメーターを設定します。
client.jsonファイルの`Client.Net.Mode`を`1`に設定すると、[プライベートネットワーク移行モード：シナリオ1](#Scenario1)を選択します。また、その他の設定が必要な場合は、[client.jsonファイルパラメータの説明](#clientJsonState)に従って設定してください。
4.（オプション）移行する必要のない移行元サーバー上のファイルとディレクトリを除外します。
Linux移行元サーバーを移行するときに、移行する必要のないファイルとディレクトリを除外する必要がある場合は、それらを[rsync_excludes_linux.txtファイル](#_linuxTxtState)に追加することができます。
5. <span id="Scenario1_step05">パブリックネットワークにアクセスできるサーバー（ゲートウェイなど）でツールを実行します。</span>
例えば、パブリックネットワークにアクセスできるサーバーで、次のコマンドを実行し、ツールを実行して、ステージ1の移行を実行します。
```
sudo ./go2tencentcloud_x64
```
`Stage 1 is finished and please run next stage at source machine.`が表示される場合は、ステージ1は完了していることになります。
![](https://main.qcloudimg.com/raw/f861b47c464f58ea184e5cc5a6a30e1c.png)
6. <span id="Scenario1_step06">移行対象の移行元サーバーでツールを実行します。</span>
[ステップ5](#Scenario1_step05)（ステージ1）が完了した後、まずステージ1のツールディレクトリ全体を移行対象の移行元サーバーにコピーし、次にツールを実行してステージ2の移行を実行します。
例えば、次のコマンドを実行してツールを実行し、ステージ2の移行を実行します。
```
sudo ./go2tencentcloud_x64
```
`Stage 2 is finished and please run next stage at gateway machine.`が表示される場合は、ステージ2は完了していることになります。
![](https://main.qcloudimg.com/raw/5684fc8aee6ebf8ba01e42deff3b4fc2.png)
7. パブリックネットワークにアクセスできるサーバー（ゲートウェイなど）でツールを実行します。
[ステップ6](#Scenario1_step06)（ステージ2）が完了した後、まずステージ2のツールディレクトリ全体をステージ1のサーバーにコピーし、次にツールを実行してステージ3の移行を実行します。
例えば、次のコマンドを実行してツールを実行し、ステージ3の移行を実行します。
```
sudo ./go2tencentcloud_x64
```
`Migrate successfully.`が表示される場合は、移行タスク全体が完了しています。
![](https://main.qcloudimg.com/raw/851e90fdc07fb601d3d158386d524985.png)
   
#### シナリオ2

1. 移行元サーバーと移行先CVMの間に接続チャネルを確立します。
[VPN Peering Connection](https://intl.cloud.tencent.com/document/product/553) / [VPN Connection](https://intl.cloud.tencent.com/document/product/1037) / [CCN](https://intl.cloud.tencent.com/document/product/1003) などの方法によって移行元サーバーと移行先CVMの間に接続チャネルを確立します。
2. user.jsonファイルに移行元サーバーと移行先CVMを設定します。
 [user.jsonファイルパラメータの説明](#userJsonState)に従って、必要なパラメーターを設定します。
3. client.jsonファイルに移行モードとその他のパラメーターを設定します。
 client.jsonファイルの`Client.Net.Mode`を`2`に設定すると、[プライベートネットワーク移行モード：シナリオ2](#Scenario2)を選択します。また、その他の設定が必要な場合は、[client.jsonファイルパラメータの説明](#clientJsonState)に従って設定してください。
4.（オプション）移行する必要のない移行元サーバー上のファイルとディレクトリを除外します。
Linux移行元サーバーを移行するときに、移行する必要のないファイルとディレクトリを除外する必要がある場合は、それらを[rsync_excludes_linux.txtファイル](#_linuxTxtState)に追加することができます。
5. ツールを実行します。
例えば、64ビットのLinux移行元サーバーで、rootユーザーとして次のコマンドを実行してツールを実行します。
```
sudo ./go2tencentcloud_x64
```
ツールが実行した後、移行プロセスが完了するまでお待ちください。
移行が成功すると、コンソールから次の内容が出力されます。
![](https://main.qcloudimg.com/raw/d32b4be8287d4b06697f0cb03cc6cff8.png)
  
#### シナリオ3

1. 移行元サーバーと移行先CVMの間に接続チャネルを確立します。
 [VPN Peering Connection](https://intl.cloud.tencent.com/document/product/553) / [VPN Connection](https://intl.cloud.tencent.com/document/product/1037) / [CCN](https://intl.cloud.tencent.com/document/product/1003) などの方法によって移行元サーバーと移行先CVMの間に接続チャネルを確立します。
2. user.jsonファイルに移行元サーバーと移行先CVMを設定します。
[user.jsonファイルパラメータの説明](#userJsonState)に従って、必要なパラメーターを設定してください。
3. client.jsonファイルに移行モードとその他のパラメーターを設定します。
 1. client.jsonファイルの`Client.Net.Mode`を`3`に設定すると、[プライベートネットワーク移行モード：シナリオ3](#Scenario3)を選択します。
 2. client.jsonファイルの`Client.Net.Proxy.Ip`と`Client.Net.Proxy.Port`を、それぞれネットワークプロキシのIPアドレスとポートに設定します。
ご使用のネットワークプロキシが認証を必要とする場合は、`Client.Net.Proxy.User`および`Client.Net.Proxy.Password`にネットワークプロキシのユーザー名とパスワードを入力してください。認証が必要でない場合は、両方のパラメーターを無視できます。その他の設定が必要な場合は、[client.jsonファイルパラメータの説明](#clientJsonState)に従って設定してください。
4. （オプション）移行する必要のない移行元サーバー上のファイルとディレクトリを除外します。
Linux移行元サーバーを移行するときに、移行する必要のないファイルとディレクトリを除外する必要がある場合は、それらを[rsync_excludes_linux.txtファイル](#_linuxTxtState)に追加することができます。
5. ツールを実行します。
例えば、64ビットのLinux移行元サーバーで、rootユーザーとして次のコマンドを実行してツールを実行します。
```
sudo ./go2tencentcloud_x64
```
ツールが実行した後、移行プロセスが完了するまでお待ちください。
移行が成功すると、コンソールから次の内容が出力されます。
![](https://main.qcloudimg.com/raw/2195589176d3669f08fbb5745901040b.png)

## 移行後の確認
1. 移行が失敗した場合は、ログファイル（デフォルトでは移行ツールディレクトリのログファイル）のエラーメッセージ出力、ガイドライン、または[サービス移行に関するFAQ](https://intl.cloud.tencent.com/document/product/213/32395) を確認して、問題のトラブルシューティングと修正を行います。
2.移行が成功した場合は、移行先CVMが正常に起動できるかどうか、移行先CVMのデータが移行元サーバーのデータと一致しているかどうか、ネットワークが正常であるかどうか、または他のシステムサービスが正常に実行されているかどうかを確認します。
3. 質問がある場合や移行エラーが発生した場合は、[サービス移行に関するFAQ](https://intl.cloud.tencent.com/document/product/213/32395) をご参照し、または[チケットを送信](https://console.cloud.tencent.com/workorder/category) して解決してください。

