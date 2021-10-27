## 概要
オンライン移行とは、システムを中断することなく、サーバーや仮想マシン上のシステム、サービスプログラムなどを、自社のデータセンター（IDC）やクラウドプラットフォームなどの移行元環境からTencent Cloudに同期または移行することです。
Tencent Cloudは、[go2tencentcloud移行ツール](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip)を提供しており、移行元サーバーで移行ツールを実行した後、移行元サーバー全体を移行先のTencent Cloud CVMに移行できます。この移行ツールは、イメージの作成、アップロード、インポートの手間を省き、移行元サーバーから直接クラウドに移行することで、企業データのクラウドへの移行、クラウドプラットフォーム間での移行、アカウント/地域間での移行、ハイブリッドクラウドの展開などのサービスニーズを容易に実現します。

## 移行ツールの説明

### サポートされているマイグレーションモード

<dx-tabs>
::: デフォルトモード[](id:DefaultMode)
お客様の移行元サーバーと移行先CVMの両方にパブリックネットワークアクセス機能がある場合は、デフォルトモードを使用してマイグレーションができます。
現在のデフォルトモードでは、移行元サーバーはインターネット経由でTencent Cloud APIにアクセスしてマイグレーションリクエストを発するとともに、データを移行先CVMに送信して、移行元サーバーをTencent Cloudの移行先クラウドサーバーにマイグレーションします。
![](https://main.qcloudimg.com/raw/5203e535f5ba947bb67c1f91dee52f1f.jpg)
:::
::: プライベートネットワークマイグレーションモード[](id:intranetMigration)
お客様の移行元サーバーまたは移行先CVMがプライベートネットワークまたはVPCにあり、移行元サーバーがインターネット経由で移行先クラウドサーバーとの接続を直接確立できない場合は、ツールのプライベートネットワークマイグレーションモードを使用してマイグレーションができます。[VPCピアリング接続](https://intl.cloud.tencent.com/document/product/553)、 [VPN接続](https://intl.cloud.tencent.com/document/product/1037)、[CCN](https://intl.cloud.tencent.com/document/product/1003) または[ダイレクト接続](https://intl.cloud.tencent.com/document/product/216)といった方法で、移行元サーバーと移行先CVM間で接続チャネルを確立する必要があります。

- [](id:Scenario1)シナリオ1：お客様の移行元サーバーまたは移行先CVMがパブリックネットワークにアクセスできない場合は、まずパブリックネットワークアクセス機能を備えたホスト（ゲートウェイなど）を介してインターネット経由でTencent Cloud APIにアクセスすることにより、マイグレーションリクエストを発することができます。次に、接続チャネルを介して移行先CVMにデータを送信してマイグレーションします。このシナリオでは、移行元サーバーと移行先CVMにパブリックネットワークへのアクセス機能は必要ありません。
![](https://main.qcloudimg.com/raw/19300ddf557d4534b1cd77fcbf64ef6a.jpg)
- [](id:Scenario2)シナリオ2：お客様の移行元サーバーがパブリックネットワークにアクセスできる場合、まずインターネット経由で移行元サーバー上のTencent Cloud APIにアクセスしてマイグレーションリクエストを発してから、次に接続チャネルを介して移行先CVMにデータを送信してマイグレーションすることができます。このシナリオでは、移行元サーバーにパブリックネットワークへのアクセス機能が必要ですが、移行先CVMには必要ありません。
![](https://main.qcloudimg.com/raw/90bf988ba7cddb9b80307efb30eaad29.jpg)
- [](id:Scenario3)シナリオ3：お客様の移行元サーバーがプロキシ経由でパブリックネットワークにアクセスできる場合は、まずネットワークプロキシ経由で移行元サーバー上のTencent Cloud APIにアクセスしてマイグレーションリクエストを発することができます。次に、接続チャネルを介して移行先CVMにデータを送信してマイグレーションします。このシナリオでは、移行元サーバーと移行先CVMにパブリックネットワークへのアクセス機能は必要ありません。
![](https://main.qcloudimg.com/raw/14f81f2c4e6cfff80d912841451c5b69.jpg)
:::
</dx-tabs>


### サポートされているオペレーティングシステム
現在オンライン移行ツールによりサポートされているOSには、以下のようなOSなどが含まれますが、これらに限定されません（32ビットまたは64ビットのいずれでも構いません）。
<table>
	<tr><th>Linux OS</th><th>Windows OS</th></tr>
	<tr><td>CentOS 5/6/7/8</td><td rowspan=7>-</td></tr>
	<tr><td>Ubuntu 10/12/14/16/18	</td></tr>
	<tr><td>Debian 7/8/9	</td></tr>
	<tr><td>SUSE 11/12/15</td></tr>
	<tr><td>openSUSE 42</td></tr>
	<tr><td>Amazon Linux AMI</td></tr>
	<tr><td>Red Hat 7/8</td></tr>
</table>

### 圧縮パッケージ内のファイルの説明

<table>
	<tr><th>ファイル名</th><th>説明</th></tr>
	<tr><td>go2tencentcloud_x64</td><td>64ビット Linux OS用の移行ツールの実行可能プログラム。</td></tr>
	<tr><td>go2tencentcloud_x32</td><td>32ビット Linux OS用の移行ツールの実行可能プログラム。</td></tr>
	<tr><td>user.json</td><td>移行中の移行元サーバーと移行先CVMの設定ファイル。<a href="#userJsonState">user.jsonファイルのパラメーターの説明</a>に従って設定を変更してください。</td></tr>
	<tr><td>client.json</td><td>移行ツールの設定ファイル。<a href="#clientJsonState">client.jsonファイルのパラメーターの説明</a>に従って設定を変更してください。</td></tr>
	<tr><td>rsync_excludes_linux.txt</td><td>rsync構成ファイル。Linuxシステムで移行する必要のないファイルとディレクトリを除外します。</td></tr>
</table>

>  設定ファイルは削除できません。設定ファイルをgo2tencentcloudの実行可能プログラムと同じフォルダーに保存してください。 
>

- <span id="userJsonState">user.jsonファイルのパラメーターの説明：</span>
<table>
	<tr><th>パラメータ名</th><th>タイプ</th><th>入力必須かどうか</th><th>説明</th></tr>
	<tr><td>SecretId</td><td>String</td><td>はい</td><td>APIにアクセスするためにアカウントで使用されるSecretIdです。詳細については、<a href="https://intl.cloud.tencent.com/document/product/598/32675">アクセスキー</a>をご参照ください。</td></tr>　
	<tr><td>SecretKey</td><td>String</td><td>はい</td><td>APIにアクセスするためにアカウントで使用されるSecretIdです。詳細については、<a href="https://intl.cloud.tencent.com/document/product/598/32675">アクセスキー</a>をご参照ください。</td></tr>
	<tr><td>Region</td><td>String</td><td>はい</td><td>移行先CVMのリージョンであり、アベイラビリティーゾーンではなく、リージョンのみを記入する必要はあります。値の詳細については、<a href="https://intl.cloud.tencent.com/document/product/213/6091">リージョン</a>リストをご参照ください。</td></tr>
	<tr><td>InstanceId</td><td>String</td><td>はい</td><td>移行先CVMのインスタンスIDであり、例えば、<code>ins-xxxxxxxx</code>。</td></tr>
	<tr><td>DataDisks</td><td>Array</td><td>いいえ</td><td>移行元サーバーからマイグレーションするデータディスクのリストです。各要素はデータディスクを表し、最大20個のデータディスクをサポートします。</td></tr>
	<tr><td>DataDisks.Index</td><td>Integer</td><td>いいえ</td><td>データディスクのシリアル番号です。値の範囲は[1,20]であり、値<code>1</code>は、このデータディスクが移行先CVMにマウントされた最初のデータディスクに移行することを意味し、値<code>2</code>は移行先CVMにマウントされた2番目のデータディスクに移行することを意味します。これによって類推します。</td></tr>
	<tr><td>DataDisks.Size</td><td>Integer</td><td>いいえ</td><td>移行元サーバー上のデータディスクのサイズ（GB）です。値の範囲は[10,16000]です。</td></tr>
	<tr><td>DataDisks.MountPoint</td><td>String</td><td>いいえ</td><td>移行元サーバー上のデータディスクのマウントポイントです。例えば、<code>"/mnt/disk1"</code>。</td></tr>
</table>
例えば、Linux移行元サーバーを広州地域にあるCVMに移行する場合、user.jsonファイルは次のように設定されます。
```json
{  
	"SecretId": "your secretId",
	"SecretKey": "your secretKey",  
	"Region": "ap-guangzhou",  
	"InstanceId": "your instance id"
}  
```
<dx-alert infotype="explain" title="">
対応するパラメータ値を実際の設定パラメータに置き換えてください。
</dx-alert>
例えば、Linux移行元サーバー1基（データディスク1枚を含む。マウントポイントは<code>/mnt/disk1</code>、サイズは<code>10</code>GB）をTencent Cloud広州エリアの移行先CVM（少なくとも1枚のデータディスクがマウントされている）にマイグレーションします。user.jsonファイルは次のように構成されます。
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
例えば、Linux移行元サーバー1基（データディスク2枚を含む。ディスク1のマウントポイントは<code>/mnt/disk1</code>、サイズは<code>10</code>GBで、移行先CVMの最初のデータディスクにマイグレーションしたい場合。ディスク2のマウントポイントは<code>/mnt/disk2</code>、サイズは<code>20</code>GBで、移行先CVMの2番目のデータディスクにマイグレーションしたい場合）をTencent Cloud広州エリアの移行先CVM（少なくとも2枚のデータディスクがマウントされている）にマイグレーションします、user.jsonファイルは次のように構成されます。
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
<dx-alert infotype="explain" title="">
対応するパラメータ値を実際の設定パラメータに置き換えてください。
</dx-alert>
- <span id="clientJsonState">client.jsonファイルパラメータの説明：</span>
<table>
	<tr><th>パラメータ名</th><th>タイプ</th><th>入力必須かどうか</th><th>説明</th></tr>
	<tr><td>Client.Net.Mode</td><td>Integer</td><td>はい</td><td>デフォルト値は<code>0</code>、値の範囲：<code>0</code>（<a href="#DefaultMode">デフォルトモード</a>）、<code>1</code>（<a href="#Scenario1">プライベートネットワークマイグレーションモード：シナリオ1</a>）、<code>2</code>（<a href="#Scenario2">プライベートネットワークマイグレーションモード：シナリオ2</a>）、<code>3</code>（<a href="#Scenario3">プライベートネットワークマイグレーションモード：シナリオ3</a>）、実際のニーズに応じてさまざまなモード/シナリオのマイグレーションを実行し、対応するパラメータ値を入力してください。</td></tr>
	<tr><td>Client.Net.Proxy.Ip</td><td>String</td><td>いいえ</td><td>NetworkingプロキシIPアドレス、<a href="#Scenario3">プライベートネットワークマイグレーションモード：シナリオ3</a>のマイグレーションを実行する必要がある場合、この項目のパラメータは入力必須です。</td></tr>
	<tr><td>Client.Net.Proxy.Port</td><td>Integer</td><td>いいえ</td><td>ネットワークプロキシのポートです。<a href="#Scenario3">プライベートネットワーク移行モード：シナリオ3</a>の移行が必要な場合は、このパラメータを指定する必要があります。</td></tr>
	<tr><td>Client.Net.Proxy.User</td><td>String</td><td>いいえ</td><td>ネットワークプロキシのユーザー名です。<a href="#Scenario3">プライベートネットワーク移行モード：シナリオ3</a>の移行が必要であり、ネットワークプロキシに認証が必要な場合は、ネットワークプロキシのユーザー名を入力してください。</td></tr>
	<tr><td>Client.Net.Proxy.Password</td><td>String</td><td>いいえ</td><td>ネットワークプロキシのパスワードです。<a href="#Scenario3">プライベートネットワーク移行モード：シナリオ3</a>の移行が必要であり、ネットワークプロキシに認証が必要な場合は、ネットワークプロキシのパスワードを入力してください。</td></tr>
	<tr><td>Client.Extra.IgnoreCheck</td><td>Bool</td><td>いいえ</td><td>デフォルト値は<code>false</code>です。移行ツールは、デフォルトでツールの起動時に移行元サーバーの環境を自動的にチェックします。このチェックをスキップする必要がある場合は、このパラメーターを<code>true</code>に設定してください。</td></tr>
	<tr><td>Client.Rsync.BandwidthLimit</td><td>String</td><td>いいえ</td><td>速度制限設定項目です。単位はKBytes/s、デフォルト値はNULLです。即ち、デフォルトの転送では速度制限はありません。</td></tr>
	<tr><td>Client.Rsync.Checksum</td><td>Bool</td><td>いいえ</td><td>転送チェック項目です。このパラメーターを<code>true</code>に設定すると、転送の一貫性チェックが強化されますが、移行元サーバーのCPU負荷が増加し、転送速度が遅くなります。デフォルト値は<code>false</code>で、即ち、デフォルトではチェックされません。</td></tr>
</table>
<blockquote class="doc-tip"><p class="doc-tip-tit"><i class="doc-icon-tip"></i>説明：</p><p>上記のパラメータ以外、client.jsonファイルのその他の構成項目は通常、記入する必要はありません。</p>
</blockquote>
- <span id="_linuxTxtState">rsync\_excludes\_linux.txtファイルの説明：</span>
このファイルは、移行や転送が不要なLinuxの移行元サーバーのファイル、または指定されたディレクトリにある設定ファイルを除外するために使用されます。次のディレクトリとファイルはデフォルトで除外されていますので、**設定を削除または変更しないでください**。
```sh
/dev/*
/sys/*
/proc/*
/var/cache/yum/*
/lost+found/*
/var/lib/lxcfs/*
/var/lib/docker-storage.btrfs/root/.local/share/gvfs-metadata/*
```
他のディレクトリやファイルを削除する必要がある場合は、このファイルの最後に内容を追加してください。例えば、`/mnt/disk1`にマウントされているデータディスクのすべての内容は削除されます。
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

### ツールの実行パラメータの説明
<table>
<thead>
<tr>
<th width="15%">パラメータオプション</th>
<th>説明</th>
</tr>
</thead>
<tbody><tr>
<td><code>--help</code></td>
<td>ヘルプ情報を印刷します。</td>
</tr>
<tr>
<td><code>--check</code></td>
<td>マイグレーションせずに、移行元サーバーを確認します。</td>
</tr>
<tr>
<td><code>--log-file</code></td>
<td>ログファイルの名前を設定します。デフォルトは<code>log</code>です。</td>
</tr>
<tr>
<td><code>--log-level</code></td>
<td>ログ出力レベルです。値の範囲は<code>1</code>（ERRORレベル）、<code>2</code>（INFOレベル）、<code>3</code>（DEBUGレベル）です。デフォルト値は<code>2</code>です。</td>
</tr>
<tr>
<td><code>--clean</code></td>
<td>移行先CVMは、マイグレーションモードを終了してサイトをクリーンアップすることを強制されます。例えば、コンソールで<code>Please execute '--clean' option manually.</code>が表示された場合、このオプションを使用してツールを実行し、移行先CVMにマイグレーションモードを終了させる必要があります。</td>
</tr>
<tr>
<td><code>--version</code></td>
<td>バージョン番号を印刷します。</td>
</tr>
</tbody></table>

## マイグレーション前の確認
移行する前に、移行元サーバーと移行先CVMを別々に確認する必要があります。移行元サーバーと移行先CVMを確認する必要がある内容は以下ののとおりです。
<table>
	<tr><th style="width: 15%;">移行先CVM</th><td><ol  style="margin: 0;"><li>ストレージスペース：移行先CVMのクラウドディスク（システムディスクとデータディスクを含む）には、移行元のデータを保存するための十分なストレージスペースが必要です。</li><li>セキュリティグループ：セキュリティグループでポート443とポート80が開いている必要があります。</li><li>帯域幅の設定：移行を高速化するために、受信帯域幅と送信帯域幅を増やすことをお勧めします。移行中に、データ量とほぼ同じのトラフィック消費が発生します。必要に応じて事前にネットワーク課金モードを変更してください。</li><li>移行先CVMと移行元サーバーのOSタイプが同じかどうか：OSが異なる場合は、後で作成されるイメージと実際のOSとの間に不整合が生じます。移行先CVMと移行元サーバーの両方で同じOSを使用することをお勧めします。例えば、CentOS 7システムがインストールされている移行元サーバーを移行する場合は、CentOS 7システムがインストールされているCVMを移行先として選択します。</li></ol></td></tr>
	<tr><th>Linux移行元サーバー</th><td><ol  style="margin: 0;"><li>Virtioを確認してインストールします。詳細については、<a href="https://intl.cloud.tencent.com/document/product/213/9929">LinuxでのVirtioドライバーの確認</a>をご参照ください。</li><li>rsyncがインストールされているかどうかを確認するには、<code>which rsync</code>コマンドを実行して検証を行います。</li><li>SELinuxが有効になっているかどうかを確認します。SELinuxが有効になっている場合は、SELinuxを無効にしてください。</li><li>移行要求がTencent Cloud APIに送信されると、APIは現在のUNIXタイムを使用して生成されたTokenをチェックします。現在のシステム時間が正しいことを確認してください。</li></ol></td></tr>
</table>

>? 
> - `sudo ./go2tencentcloud_x64 --check`などのツールコマンドを使用して、移行元サーバーを自動的にチェックできます。
> - 「go2tencentcloud」移行ツールは、実行を開始すると、デフォルトで移行元サーバーを自動的にチェックします。このチェックをスキップして強制的に移行する場合は、client.json ファイルの`Client.Extra.IgnoreCheck`フィールドの値を`true`に設定してください。
> 

## 移行手順
Tencent Cloudが提供するgo2tencentcloudマイグレーションツールは、マイグレーションプロセス全体を次の3つの段階に分割します。ユーザーは、ツールの実行中にマイグレーションの進行状況を直観的に理解することができます。
- **ステージ1**：移行先CVMが移行モードに入り、移行を準備します
- **ステージ2**：移行先CVMが移行モードにあり、データを移行しています
- **ステージ3**：移行先CVMが移行モードを終了し、移行が完了します

各ステージでは、関連する操作を実行するためにいくつかのサブタスクが生成されます。また、時間のかかるサブタスクの一部には、デフォルトの最大タイムアウト時間が設定されています。データ転送にかかる時間は、移行元サーバー上のデータサイズやネットワーク帯域幅などの影響を受けるため、移行プロセスが完了するまでお待ちください。移行ツールはチェックポイント再起動をサポートしています。

>! マイグレーションの開始後、移行先CVMはマイグレーションモードに入ります。マイグレーションが完了してマイグレーションモードを終了するまで、移行先CVMに対してシステムの再インストール、シャットダウン、パスワードのリセットなどの操作を行わないでください。 
>

<dx-tabs>
::: デフォルトモードのマイグレーション手順
1. user.jsonファイルで移行先CVMを設定します。
[user.jsonファイルのパラメータの説明](#userJsonState)に従って、必要な項目と必要な値を設定してください。
2. client.jsonファイルに移行モードとその他の項目を設定します。
client.jsonファイルの`Client.Net.Mode`を`0`に設定すると、[デフォルトモード](#DefaultMode) の移行が実行されます。また、その他の設定が必要な場合は、[client.jsonファイルのパラメータの説明](#clientJsonState)に従って設定してください。
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
ツールを実行した後は、マイグレーションプロセスが完了するまでお待ちください。 
通常のデフォルトモードでは、移行が成功した場合、コンソールから次の内容が出力されます。
![](https://main.qcloudimg.com/raw/b056d6b1d5ac457ff43e48883848af01.png)
:::
::: プライベートネットワークマイグレーションモードのマイグレーション手順
#### シナリオ1のマイグレーション手順
1. 移行元サーバーと移行先CVMの間に接続チャネルを確立します。
-  [VPN Peering Connection](https://intl.cloud.tencent.com/document/product/553)、[VPN Connection](https://intl.cloud.tencent.com/document/product/1037) /[CCN](https://intl.cloud.tencent.com/document/product/1003) などの方法を介して移行元サーバーと移行先CVMの間に接続チャネルを確立します。
2. user.jsonファイルに移行先CVMを設定します。
 [user.jsonファイルのパラメータの説明](#userJsonState)に従って、必要な項目と必要な値を設定してください。
3. client.jsonファイルでマイグレーションモードと他の項目を設定します。
client.jsonファイルの`Client.Net.Mode`項目を`1`に設定します。これは、[プライベートネットワークマイグレーションモード：シナリオ1](#Scenario1)のマイグレーションが実行されることを意味します。 また、他の項目を設定する必要がある場合は、[client.jsonファイルパラメータの説明](#clientJsonState)に従って設定してください。
4. 移行元サーバー上でマイグレーション不要のファイルまたはディレクトリを削除します。（オプション）
Linux移行元サーバーを移行するときに、移行する必要のないファイルとディレクトリを除外する必要がある場合は、それらを[rsync_excludes_linux.txtファイル](#_linuxTxtState)に追加することができます。
5. <span id="Scenario1_step05">パブリックネットワークにアクセスできるサーバー（ゲートウェイなど）でツールを実行します。</span>
例えば、パブリックネットワークにアクセスできるサーバーで、次のコマンドを実行し、ツールを実行して、ステージ1の移行を実行します。
```
sudo ./go2tencentcloud_x64
```
`Stage 1 is finished and please run next stage at source machine.`というプロンプトが表示される場合、ステージ1は完了していることになります。
![](https://main.qcloudimg.com/raw/f861b47c464f58ea184e5cc5a6a30e1c.png)

6. <span id="Scenario1_step06">移行対象の移行元サーバーでツールを実行します。</span>
[ステップ5](#Scenario1_step05)（ステージ1）が完了した後、まずステージ1のツールディレクトリ全体を移行対象の移行元サーバーにコピーし、次にツールを実行してステージ2の移行を実行します。
例えば、次のコマンドを実行してツールを実行し、ステージ2の移行を実行します。

```
sudo ./go2tencentcloud_x64
```
`Stage 2 is finished and please run next stage at gateway 
machine.`というプロンプトが表示された場合、ステージ2が完了したことを意味します。
![](https://main.qcloudimg.com/raw/5684fc8aee6ebf8ba01e42deff3b4fc2.png)
7. パブリックネットワークにアクセスできるサーバー（ゲートウェイなど）でツールを実行します。
[ステップ6](#Scenario1_step06)（ステージ2）が完了した後、まずステージ2のツールディレクトリ全体をステージ1のサーバーにコピーし、次にツールを実行してステージ3の移行を実行します。
例えば、次のコマンドを実行してツールを実行し、ステージ3の移行を実行します。
```
sudo ./go2tencentcloud_x64
```
`Migrate successfully.`というプロンプトが表示される場合、移行タスク全体が完了していることになります。
![](https://main.qcloudimg.com/raw/851e90fdc07fb601d3d158386d524985.png)

#### シナリオ2

1. 移行元サーバーと移行先CVM間に接続チャネルを確立します。
-  [VPN Peering Connection](https://intl.cloud.tencent.com/document/product/553)、[VPN Connection](https://intl.cloud.tencent.com/document/product/1037) /[CCN](https://intl.cloud.tencent.com/document/product/1003) などの方法を介して移行元サーバーと移行先CVMの間に接続チャネルを確立します。
2. user.jsonファイルに移行先CVMを設定します。
 [user.jsonファイルのパラメータの説明](#userJsonState)に従って、必要な項目と必要な値を設定してください。
3. client.jsonファイルでマイグレーションモードと他の項目を設定します。
 client.jsonファイルの`Client.Net.Mode`項目を`2`に設定します。これは、[プライベートネットワークマイグレーションモード：シナリオ2](#Scenario2)のマイグレーションが実行されることを意味します。 また、他の項目を設定する必要がある場合は、[client.jsonファイルパラメータの説明](#clientJsonState)に従って設定してください。
4. 移行元サーバー上でマイグレーション不要のファイルまたはディレクトリを削除します。（オプション）
Linux移行元サーバーをマイグレーションするときに、マイグレーションする必要のないファイルまたはディレクトリを削除する必要がある場合は、マイグレーションする必要のないこれらのファイルまたはディレクトリを[rsync_excludes_linux.txtファイル](#_linuxTxtState)に追加できます。
5. ツールを実行します。
例えば、64ビットのLinux移行元サーバーで、root権限を指定して次のコマンドを実行し、ツールを実行します。

```
sudo ./go2tencentcloud_x64
```
ツールが実行した後、マイグレーションプロセスが完了するまでお待ちください。

通常、移行が成功すると、コンソールから次の内容が出力されます。
![](https://main.qcloudimg.com/raw/d32b4be8287d4b06697f0cb03cc6cff8.png)

#### シナリオ3

1. 移行元サーバーと移行先CVM間に接続チャネルを確立します。
 [VPCピアリング接続](https://intl.cloud.tencent.com/document/product/553) /[VPN接続](https://intl.cloud.tencent.com/document/product/1037) /[CCN](https://intl.cloud.tencent.com/document/product/1003)などの方法によって、移行元サーバーと移行先CVM間の接続チャネルを確立します。
2. user.jsonファイルに移行先CVMを設定します。
[user.jsonファイルのパラメータの説明](#userJsonState)に従って、必要な項目と必要な値を設定してください。
3. client.jsonファイルでマイグレーションモードと他の項目を設定します。
 1. client.jsonファイルの`Client.Net.Mode`項目を`3`に設定して、[プライベートネットワークマイグレーションモード：シナリオ3](#Scenario3)のマイグレーションを実行します。
 2. client.jsonファイルの`Client.Net.Proxy.Ip`と`Client.Net.Proxy.Port`の項目をネットワークプロキシのIPアドレスとポートに設定します。
ネットワークプロキシで認証が​​必要な場合は、ネットワークプロキシのユーザー名とパスワードを`Client.Net.Proxy.User`と`Client.Net.Proxy.Password`に入力してください。認証が不要な場合は、空白のままにしてください。また、他の項目を設定する必要がある場合は、[client.jsonファイルパラメータの説明](#clientJsonState)に従って設定してください。
4. 移行元サーバー上でマイグレーション不要のファイルまたはディレクトリを削除します。（オプション）
Linux移行元サーバーをマイグレーションするときに、マイグレーションする必要のないファイルまたはディレクトリを削除する必要がある場合は、マイグレーションする必要のないこれらのファイルまたはディレクトリを[rsync_excludes_linux.txtファイル](#_linuxTxtState)に追加できます。
5. ツールを実行します。
例えば、64ビットのLinux移行元サーバーで、root権限を指定して次のコマンドを実行し、ツールを実行します。

```
sudo ./go2tencentcloud_x64
```
ツールが実行した後、マイグレーションプロセスが完了するまでお待ちください。
通常、移行が成功すると、コンソールから次の内容が出力されます。
![](https://main.qcloudimg.com/raw/2195589176d3669f08fbb5745901040b.png)
:::
</dx-tabs>


## マイグレーション後の確認
1. 移行が失敗した場合は、ログファイル（デフォルトでは移行ツールディレクトリのlogファイル）のエラー情報、操作ガイド、または[サービス移行に関するFAQ](https://intl.cloud.tencent.com/document/product/213/32395)を確認して、問題のトラブルシューティングと修正を行います。
2. マイグレーションが成功した場合は、移行先CVMが正常に起動できるか、移行先CVMのデータが移行元サーバーと一致しているか、ネットワークが正常か、他のシステムサービスが正常かなどを確認してください。
3. ご不明な点やマイグレーションの異常など、ご質問がありましたら、[サービスマイグレーションに関するFAQ](https://intl.cloud.tencent.com/document/product/213/32395)をご参照いただくか、または[お問い合わせ](https://intl.cloud.tencent.com/document/product/213/34837)から解消してください。

