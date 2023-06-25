ここでは、go2tencentcloudマイグレーションツールを使用して、Linux OSサーバーのオンラインマイグレーションを行う方法についてご紹介いたします。

## 準備事項

- Tencent Cloudアカウント、および移行先のCVMがすでにあることが必要です。
- 移行中に既存のアプリケーションへの影響を回避するために、ソースサーバーのアプリケーションを一時停止することをお勧めします。
- 移行ツール圧縮パッケージをダウンロードするには、[ここ](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip) をクリックしてください。
- [APIキー管理](https://console.cloud.tencent.com/cam/capi)ページで`SecretId`および`SecretKey`を作成し、取得します。
- ソースサーバーと移行先CVMの両方が移行要件を満たしていることを確認します。例えば、移行先CVMのクラウドディスクには、移行元サーバーから移行されたデータを保存するための十分な容量が必要です。
- マイグレーション前に、次の方式でデータをバックアップすることをお勧めします：
 - 移行元サーバー：ソースサーバーのスナップショット機能などの方式を選択してデータをバックアップできます。
 - 移行先CVM： [スナップショットの作成](https://intl.cloud.tencent.com/document/product/362/5755) などの方式を選択して、移行先CVMのデータをバックアップできます。

## マイグレーションツールキットの説明

### 圧縮パッケージ内のファイルの説明

`go2tencentcloud.zip`を解凍後のファイルの説明は次のとおりです：
<table>
	<tr><th width="30%">ファイル名</th><th>説明</th></tr>
	<tr><td>go2tencentcloud-linux.zip</td><td>Linux OSのマイグレーション圧縮パッケージです。</td></tr>
	<tr><td>readme.txt</td><td>ディレクトリ概要ファイルです。</td></tr>
	<tr><td>release_notes.txt</td><td>マイグレーションツールの変更ログです。</td></tr>
</table>

`go2tencentcloud-linux.zip`を解凍後のファイルの説明は次のとおりです：
<table>
	<tr><th width="30%">ファイル名</th><th>説明</th></tr>
	<tr><td>go2tencentcloud_x64</td><td>64ビット Linux OS用の移行ツールの実行可能プログラムです。</td></tr>
	<tr><td>go2tencentcloud_x32</td><td>32ビット Linux OS用の移行ツールの実行可能プログラムです。</td></tr>
	<tr><td>user.json</td><td>マイグレーション時のユーザー情報です。</td></tr>
	<tr><td>client.json</td><td>マイグレーションツールの設定ファイルです。</td></tr>
	<tr><td>rsync_excludes_linux.txt</td><td>rsync設定ファイル。Linuxシステムで移行する必要のないファイルとディレクトリを除外します。</td></tr>
</table>

<dx-alert infotype="notice" title="">
設定ファイルは削除できません。設定ファイルはgo2tencentcloudの実行可能なプログラムと同じ階層のディレクトリ下に置いてください。 
</dx-alert>

### user.jsonファイルパラメータの説明[](id:userJsonState)

user.json設定ファイルの説明は下表のとおりです：

<table>
  <tr>
	<th>パラメータ名</th>
	<th>タイプ</th>
	<th>入力必須かどうか</th>
	<th>説明</th>
  </tr>
  <tr>
	<td>SecretId</td>
	<td>String</td>
	<td>はい</td>
	<td>アカウントAPIアクセスキーのSecretIdです。詳細情報については 
	<a href="https://intl.cloud.tencent.com/document/product/598/32675">アクセスキー</a>をご参照ください。</td>
  </tr>
  <tr>
	<td>SecretKey</td>
	<td>String</td>
	<td>はい</td>
	<td>アカウントAPIアクセスキーのSecretKeyです。詳細情報については 
	<a href="https://intl.cloud.tencent.com/document/product/598/32675">アクセスキー</a>をご参照ください。</td>
  </tr>
  <tr>
	<td>Region</td>
	<td>String</td>
	<td>はい</td>
	<td>移行先CVMのリージョンです。入力はリージョンだけでよく、アベイラビリティーゾーンの入力は不要です。値については 
	<a href="https://intl.cloud.tencent.com/document/product/213/6091">リージョン</a>リストをご参照ください。</td>
  </tr>
  <tr>
	<td>InstanceId</td>
	<td>String</td>
	<td>はい</td>
	<td>移行先CVMのインスタンスIDです。形式は 
	<code>ins-xxxxxxxx</code>のようにします。</td>
  </tr>
  <tr>
	<td>DataDisks</td>
	<td>Array</td>
	<td>いいえ</td>
	<td>移行元サーバーからマイグレーションするデータディスクのリストです。各要素はデータディスクを表し、最大20個のデータディスクをサポートします。</td>
  </tr>
  <tr>
	<td>DataDisks.Index</td>
	<td>Integer</td>
	<td>いいえ</td>
	<td>データディスクの番号（数値の範囲：[1,20]）です。数値<code>1</code>は、このデータディスクが移行先CVMにマウントされた最初のデータディスクにマイグレーションされることを表します。数値 <code>2</code>は、移行先CVMにマウントされた2番目のデータディスクにマイグレーションされることを表します。これにより類推します。</td>
  </tr>
  <tr>
	<td>DataDisks.Size</td>
	<td>Integer</td>
	<td>いいえ</td>
	<td>移行元のデータディスクのサイズです。単位はGB、数値の範囲は[10,16000]です。</td>
  </tr>
  <tr>
	<td>DataDisks.MountPoint</td>
	<td>String</td>
	<td>いいえ</td>
	<td>移行元のデータディスクのマウントポイントです。 
	<code>&quot;/mnt/disk1&quot;</code>のようにします。</td>
  </tr>
</table>

次の事例を参照して、実際のサービスケースに従って設定ファイルを修正できます。
 - 事例1：Linux移行元サーバー1基をTencent Cloud広州リージョンのCVM1基にマイグレーションする場合、`user.json` ファイルは次のように構成されます：
```json
{  
	"SecretId": "your secretId",
	"SecretKey": "your secretKey",  
	"Region": "ap-guangzhou",  
	"InstanceId": "your instance id"
} 
```
 - 事例2：Linux移行元サーバー1基（データディスク1枚を含む。マウントポイントは`/mnt/disk1`、サイズは`10GB`）をTencent Cloud広州リージョンの移行先CVM1基（少なくとも1枚のデータディスクがマウントされている）にマイグレーションする場合、`user.json`ファイルは次のように構成されます：
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
 - 事例3：Linux移行元サーバー1基（データディスク2枚を含む。ディスク1のマウントポイントは`/mnt/disk1`、サイズは`10GB`で、移行先CVMの最初のデータディスクにマイグレーションしたい場合。ディスク2のマウントポイントは`/mnt/disk2`、サイズは`20GB`で、移行先CVMの2番目のデータディスクにマイグレーションしたい場合）をTencent Cloud広州リージョンの移行先CVM1基（少なくとも2枚のデータディスクがマウントされている）にマイグレーションする場合、`user.json`ファイルは次のように構成されます：
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

### client.json ファイルパラメータの説明[](id:clientJsonState)

client.json設定ファイルの一部の説明は下表のとおりです：

<table>
  <tr>
	<th>パラメータ名</th>
	<th>タイプ</th>
	<th><br>入力必須かどうか</th>
	<th>説明</th>
  </tr>
  <tr>
	<td>Client.ToolMode</td>
	<td>bool</td>
	<td>いいえ</td>
	<td>ツールマイグレーションモードの識別パラメータです。デフォルトの値は<code>false</code>です。ツールモードを使用してマイグレーションする場合は、<code>true</code>に修正するか、またはツールを実行するときに<code>--no-console</code>パラメータを追加してください。</td>
  </tr>
  <tr>
	<td>Client.Net.Mode</td>
	<td>Integer</td>
	<td>はい</td>
	<td>マイグレーションモードのパラメータです。デフォルトでは、パブリックネットワークを使用して転送します。数値は<code>0</code>で、数値の範囲：<code>0</code>（<a href="https://intl.cloud.tencent.com/document/product/213/44340">パブリックネットワークマイグレーションモード</a>）、<code>1</code>（<a href="https://intl.cloud.tencent.com/document/product/213/44340">プライベートネットワークマイグレーションモード：シナリオ1</a>）、<code>2</code>（<a href="https://intl.cloud.tencent.com/document/product/213/44340">プライベートネットワークマイグレーションモード：シナリオ2</a>）、<code>3</code>（<a href="https://intl.cloud.tencent.com/document/product/213/44340">プライベートネットワークマイグレーションモード：シナリオ3</a>）です。</td>
  </tr>
  <tr>
	<td>Client.Extra.IgnoreCheck</td>
	<td>Bool</td>
	<td>いいえ</td>
	<td>デフォルト値は<code>false</code>です。デフォルトでは、マイグレーションツールは、ツールの実行開始時に移行元サーバー環境を自動的にチェックします。チェックをスキップする必要がある場合は、<code>true</code>に設定してください。</td>
  </tr>
  <tr>
	<td>Client.Rsync.BandwidthLimit</td>
	<td>String</td>
	<td>いいえ</td>
	<td>速度制限設定項目です。単位はKBytes/s、デフォルト値は空であり、その場合、転送時の速度は制限されません。</td>
  </tr>
  <tr>
	<td>Client.Rsync.Checksum</td>
	<td>Bool</td>
	<td>いいえ</td>
	<td>転送検証の項目です。<code>true</code>に設定すると、転送の整合性の検証を強化することができますが、移行元サーバーCPUは増加します。
	転送速度をロードして遅くします。デフォルト値は<code>false</code>です。すなわち、デフォルトでは検証を行いません。</td>
  </tr>
</table>

移行元サーバーまたは移行先CVMのいずれかがパブリックネットワークに直接アクセスできない場合、まず[VPC Peering Connection](https://intl.cloud.tencent.com/document/product/553)、[VPN Connection](https://intl.cloud.tencent.com/document/product/1037)、[CCN](https://intl.cloud.tencent.com/document/product/1003)または[Direct Connection](https://intl.cloud.tencent.com/document/product/216)などの方法で接続チャネルを確立してから、プライベートネットワークモードでのマイグレーションを実施する方法を選択することができます。移行元サーバーと移行先CVMのネットワーク環境に応じて、適切なマイグレーションモードを決定してください。

###  rsync\_excludes\_linux.txtファイル説明[](id:_linuxTxtState)

このファイルは、移行や転送が不要なLinuxの移行元サーバーのファイル、または指定されたディレクトリにある設定ファイルを除外するために使用されます。次のディレクトリとファイルはデフォルトで除外されていますので、**設定を削除または変更しないでください**。
```shellsession
/dev/*
/sys/*
/proc/*
/var/cache/yum/*
/lost+found/*
/var/lib/lxcfs/*
/var/lib/docker-storage.btrfs/root/.local/share/gvfs-metadata/*
```
他のディレクトリやファイルを削除する必要がある場合は、このファイルの最後に内容を追加してください。例えば、`/mnt/disk1`にマウントされているデータディスクのすべての内容は削除されます。
```shellsession
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

<table>
<thead>
<tr>
<th width="18%">パラメータオプション</th>
<th>説明</th>
</tr>
</thead>
<tbody><tr>
<td><code>--help</code></td>
<td>ヘルプ情報を印刷します。</td>
</tr>
<tr>
<td><code>--no-console</code></td>
<td>ツールモードのみを使用したマイグレーション（非コンソールモードのマイグレーション）です。</td>
</tr>
<tr>
<td><code>--check</code></td>
<td>移行元サーバーをチェックします</td>
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
<td>移行先CVMは、マイグレーションモードを終了してサイトをクリーンアップすることを強制されます。例えば、コンソールでPlease execute '--clean' option manually.が表示された場合、このオプションを使用してツールを実行し、移行先CVMにマイグレーションモードを終了させてください。</td>
</tr>
<tr>
<td><code>--version</code></td>
<td>バージョン番号を印刷します。</td>
</tr>
</tbody>
</table>


## 移行手順

### データのバックアップ
- 移行元サーバー：ソースサーバーのスナップショット機能などの方式を選択してデータをバックアップできます。
- 移行先CVM： [スナップショットの作成](https://intl.cloud.tencent.com/document/product/362/5755) などの方式を選択してデータをバックアップできます。


### マイグレーション前の確認
マイグレーションする前に、移行元サーバーと移行先CVMをそれぞれ確認してください。確認する内容は下表のとおりです：
<table>
  <tr>
	<th style="width: 15%;">移行先CVM</th>
	<td>
	  <ol style="margin: 0;">
		<li>
		ストレージ容量：移行先CVMのクラウドディスク（システムディスクとデータディスクを含む）には、移行元サーバーから移行されたデータを保存するための十分な容量が必要です。</li>
		<li>セキュリティグループ：セキュリティグループでは443ポート、80ポートは制限できません。</li>
		<li>
		帯域幅設定：マイグレーションをより迅速に行えるようにするため、できる限り両側の帯域幅を広くすることをお勧めします。マイグレーション中にはデータ量とほぼ同等のトラフィック消費が発生する場合があります。必要に応じ、事前にネットワーク課金モデルの調整を行ってください。</li>
		<li>
		移行先CVMと移行元サーバーのOSタイプが一致しているか：OSが一致していないと、その後に作成するイメージの情報と実際のOSが一致しない場合がありますので、移行先CVMのOSはできる限り移行元サーバーのOSタイプと一致させることをお勧めします。例えば、CentOS
		7システムの移行元サーバーのマイグレーションの場合は、CentOS 7システムのCVMを移行先として選択してください。</li>
	  </ol>
	</td>
  </tr>
  <tr>
	<th>Linux移行元サーバー</th>
	<td>
	  <ol style="margin: 0;">
		<li>Virtioをチェックまたはインストールします。操作の詳細については 
		<a href="https://intl.cloud.tencent.com/document/product/213/9929">LinuxでのVirtioドライバーの確認</a>をご参照ください。</li>
		<li>実行 
		<code>which rsync</code>コマンドで、rsyncがインストールされているかどうかをチェックします。インストールされていない場合は、<a href="https://intl.cloud.tencent.com/document/product/213/32395#installRsync">Rsyncのインストール方法</a>を参照してインストールしてください。</li>
		<li>SELinuxが有効になっているかどうかをチェックします。SELinuxが有効になっている場合は、<a href="https://intl.cloud.tencent.com/document/product/213/32395#closeSELinux">SELinuxを無効化する方法</a>を参照して無効化してください。</li>
		<li>Tencent Cloud APIに対しマイグレーションリクエストを送信すると、Tencent Cloud APIは現在のUNIX時間をチェックして発行された
		Tokenを使用する場合があります。現在のシステム時間が正確であることを確認してください。</li>
	  </ol>
	</td>
  </tr>
</table>

<dx-alert infotype="explain" title="">
- `./go2tencentcloud_x64 --no-console --check`などのツールコマンドを使用して、移行元サーバーを自動的にチェックできます。
- go2tencentcloudマイグレーションツールは、実行を開始すると、デフォルトで自動的にチェックします。このチェックをスキップして強制的に移行する場合は、client.json ファイルの`Client.Extra.IgnoreCheck`フィールドの値を`true`に設定してください。
</dx-alert>


### マイグレーションの開始

Tencent Cloudが提供するgo2tencentcloudマイグレーションツールはブレークポイント転送をサポートし、マイグレーションプロセス全体を次の3つの段階に分割します。ユーザーは、ツールの実行中にマイグレーションの進行状況を直観的に理解することができます。

- **ステージ1**：移行先CVMが移行モードに入り、移行を準備します
- **ステージ2**：移行先CVMが移行モードにあり、データを移行しています
- **ステージ3**：移行先CVMが移行モードを終了し、移行が完了します

各ステージではいずれもいくつかのサブタスクが発生し、関連の操作を実行します。時間がかかる一部のサブタスクには、デフォルトの最大タイムアウト時間が存在します。データ転送の消費時間は、移行元データのサイズ、ネットワーク帯域幅などの要因に左右されます。マイグレーションフローが完了するまでお待ちください。
<dx-alert infotype="notice" title="">
マイグレーションの開始後、移行先CVMはマイグレーションモードに入ります。マイグレーションが完了してマイグレーションモードを終了するまで、移行先CVMに対してシステムの再インストール、シャットダウン、破棄、パスワードのリセットなどの操作を行わないでください。 
</dx-alert>

<dx-tabs>

:::  パブリックネットワークのマイグレーション

1. マイグレーションツールgo2tencentcloud.zipをダウンロードするか、または移行元サーバーにアップロードし、次のコマンドを実行して対応するディレクトリに進みます。
  1. 次のコマンドを順に実行し、go2tencentcloud.zipを解凍してディレクトリに進みます。
```shellsession
unzip go2tencentcloud.zip
```
```shellsession
cd go2tencentcloud
```
  1. 次のコマンドを順に実行し、go2tencentcloud-linux.zipを解凍してディレクトリに進みます。
```shellsession
unzip go2tencentcloud-linux.zip
```
```shellsession
cd go2tencentcloud-linux
```
<dx-alert infotype="explain" title="">
`go2tencentcloud`ディレクトリ下のファイルは移行されません。移行が必要なファイルをこのディレクトリ下に置かないでください。
</dx-alert>
2. `user.json`ファイルで移行先CVMを設定します。
[user.jsonファイルのパラメータの説明](#userJsonState)に従って、必要な項目と必要な値を設定してください。
3. `client.json`ファイルでマイグレーションモードとその他の項目を設定します。
`client.json`ファイルの`Client.ToolMode`の値を`true`に設定すると、ツールモードのマイグレーションが標識されます。また、その他の設定が必要な場合は、[client.jsonファイルのパラメータの説明](#clientJsonState)に従って設定してください。
4. （オプション）移行元サーバー上でマイグレーション不要のファイルまたはディレクトリを削除します。
Linux移行元サーバー上でマイグレーション不要のファイルおよびディレクトリがある場合、ファイルおよびディレクトリを[rsync_excludes_linux.txtファイル](#_linuxTxtState)に追加できます。
5. ツールを実行する。
例えば、64ビットのLinux移行元サーバーで、root権限を指定して次のコマンドを実行し、ツールを実行します。
```shellsession
sudo ./go2tencentcloud_x64 
```
<dx-alert infotype="notice" title="">
client.jsonの`Client.ToolMode`を`true`に修正していない場合は、ツールを実行するとき、パラメータ`--no-console`を追加してください。次のとおりです：
```shellsession
sudo ./go2tencentcloud_x64 --no-console
```
</dx-alert>
ツール実行後、マイグレーションプロセスが完了するまでしばらく、お待ちください。一般的なパブリックネットワークマイグレーションモードでは、マイグレーションに成功した場合のコンソール出力は、次の図に示したとおりです：
![](https://main.qcloudimg.com/raw/b056d6b1d5ac457ff43e48883848af01.png)

:::
:::  プライベートネットワークマイグレーションシナリオ1

1. 移行元サーバーと移行先CVMの間に接続チャネルを確立します。
[VPN Peering Connection](https://intl.cloud.tencent.com/document/product/553) / [VPN Connection](https://intl.cloud.tencent.com/document/product/1037) / [CCN](https://intl.cloud.tencent.com/document/product/1003) などの方法によって移行元サーバーと移行先CVMの間に接続チャネルを確立します。
2. マイグレーションツールgo2tencentcloud.zipをダウンロードするか、または移行元サーバーにアップロードし、次のコマンドを実行して対応するディレクトリに進みます。
   1. 次のコマンドを順に実行し、go2tencentcloud.zipを解凍してディレクトリに進みます。
```shellsession
unzip go2tencentcloud.zip
```
```shellsession
cd go2tencentcloud
```
   1. 次のコマンドを順に実行し、go2tencentcloud-linux.zipを解凍してディレクトリに進みます。
```shellsession
unzip go2tencentcloud-linux.zip
```
```shellsession
cd go2tencentcloud-linux
```
<dx-alert infotype="explain" title="">
`go2tencentcloud`ディレクトリ下のファイルは移行されません。移行が必要なファイルをこのディレクトリ下に置かないでください。
</dx-alert>
3. `user.json`ファイルで移行先CVMを設定します。
[user.jsonファイルのパラメータの説明](#userJsonState)に従って、必要な項目と必要な値を設定してください。
4. `client.json`ファイルでマイグレーションモードとその他の項目を設定します。
   - `client.json`ファイルの`Client.ToolMode`の値を`true`に設定すると、ツールマイグレーションモードが標識されます。
   - `client.json`ファイルの`Client.Net.Mode`の項目を`1`に設定すると、[プライベートネットワークマイグレーションモード：シナリオ1](https://intl.cloud.tencent.com/document/product/213/44340#.E6.94.AF.E6.8C.81.E7.9A.84.E8.BF.81.E7.A7.BB.E6.A8.A1.E5.BC.8F)のマイグレーションを実行します。また、その他の設定が必要な場合は、[client.jsonファイルパラメータの説明](#clientJsonState)に従って設定してください。
5. （オプション）移行元サーバー上でマイグレーション不要のファイルまたはディレクトリを削除します。
Linux移行元サーバー上でマイグレーション不要のファイルおよびディレクトリがある場合、ファイルおよびディレクトリを[rsync_excludes_linux.txtファイル](#_linuxTxtState)に追加できます。
6. [](id:Scenario1_step06)パブリックネットワークにアクセスできるサーバー（ゲートウェイなど）上でツールを実行します。
例えば、パブリックネットワークにアクセスできるサーバーで、次のコマンドを実行し、ツールを実行して、ステージ1の移行を実行します。
```shellsession
sudo ./go2tencentcloud_x64 
```
<dx-alert infotype="notice" title="">
client.jsonの`Client.ToolMode`を`true`に修正していない場合は、ツールを実行するとき、パラメータ`--no-console`を追加してください。次のとおりです：
```shell
sudo ./go2tencentcloud_x64 --no-console
```
</dx-alert>
下図に示すように、`Stage 1 is finished and please run next stage at source machine.`と表示された場合は、ステージ1が完了しています：
![](https://main.qcloudimg.com/raw/f861b47c464f58ea184e5cc5a6a30e1c.png)
7. [](id:Scenario1_step07)移行対象の移行元サーバー上でツールを実行します。
[ステップ6](#Scenario1_step06)（ステージ1）が完了した後、まずステージ1のツールディレクトリ全体を移行対象の移行元サーバーにコピーし、次にツールを実行してステージ2の移行を実行します。
例えば、次のコマンドを実行してツールを実行し、ステージ2の移行を実行します。
```shellsession
sudo ./go2tencentcloud_x64 
```
<dx-alert infotype="notice" title="">
client.jsonの`Client.ToolMode`を`true`に修正していない場合は、ツールを実行するとき、パラメータ`--no-console`を追加する必要があります。次のとおりです：
```shellsession
sudo ./go2tencentcloud_x64 --no-console
```
</dx-alert>
下図に示すように、`Stage 2 is finished and please run next stage at gateway machine.`と表示された場合は、ステージ2が完了しています。
![](https://main.qcloudimg.com/raw/5684fc8aee6ebf8ba01e42deff3b4fc2.png)
8. パブリックネットワークにアクセスできるサーバー（ゲートウェイなど）でツールを実行します。
[ステップ7](#Scenario1_step07)（ステージ2）が完了した後、まずステージ2のツールディレクトリ全体をステージ1のサーバーにコピーし、次にツールを実行してステージ3の移行を実行します。
例えば、次のコマンドを実行してツールを実行し、ステージ3の移行を実行します。
```shellsession
sudo ./go2tencentcloud_x64 
```
<dx-alert infotype="notice" title="">
client.jsonの`Client.ToolMode`を`true`に修正していない場合は、ツールを実行するとき、パラメータ`--no-console`を追加する必要があります。次のとおりです：
```shellsession
sudo ./go2tencentcloud_x64 --no-console
```
</dx-alert>
下図に示すように、`Migrate successfully.`と表示された場合は、すべての移行タスクが完了しています。
![](https://main.qcloudimg.com/raw/851e90fdc07fb601d3d158386d524985.png)




:::
:::  プライベートネットワークマイグレーションシナリオ2

1. 移行元サーバーと移行先CVMの間に接続チャネルを確立します。
[VPN Peering Connection](https://intl.cloud.tencent.com/document/product/553) / [VPN Connection](https://intl.cloud.tencent.com/document/product/1037) / [CCN](https://intl.cloud.tencent.com/document/product/1003) などの方法によって移行元サーバーと移行先CVMの間に接続チャネルを確立します。
2. マイグレーションツールgo2tencentcloud.zipをダウンロードするか、または移行元サーバーにアップロードし、次のコマンドを実行して対応するディレクトリに進みます。
   1. 次のコマンドを順に実行し、go2tencentcloud.zipを解凍してディレクトリに進みます。
```shellsession
unzip go2tencentcloud.zip
```
```shellsession
cd go2tencentcloud
```
    1. 次のコマンドを順に実行し、go2tencentcloud-linux.zipを解凍してディレクトリに進みます。
```shellsession
unzip go2tencentcloud-linux.zip
```
```shellsession
cd go2tencentcloud-linux
```
<dx-alert infotype="explain" title="">
`go2tencentcloud`ディレクトリ下のファイルは移行されません。移行が必要なファイルをこのディレクトリ下に置かないでください。
</dx-alert>
3. `user.json`ファイルで移行先CVMを設定します。
[user.jsonファイルのパラメータの説明](#userJsonState)に従って、必要な項目と必要な値を設定してください。
4. `client.json`ファイルでマイグレーションモードとその他の項目を設定します。
    - `client.json`ファイルの`Client.ToolMode`の値を`true`に設定すると、ツールマイグレーションモードが標識されます。
    - `client.json`ファイルの`Client.Net.Mode`の項目を`2`に設定すると、[プライベートネットワークマイグレーションモード：シナリオ2](https://intl.cloud.tencent.com/document/product/213/44340#.E6.94.AF.E6.8C.81.E7.9A.84.E8.BF.81.E7.A7.BB.E6.A8.A1.E5.BC.8F)のマイグレーションを実行します。また、その他の設定が必要な場合は、[client.jsonファイルパラメータの説明](#clientJsonState)に従って設定してください。
5. （オプション）移行元サーバー上でマイグレーション不要のファイルまたはディレクトリを削除します。
Linux移行元サーバー上でマイグレーション不要のファイルおよびディレクトリがある場合、ファイルおよびディレクトリを[rsync_excludes_linux.txtファイル](#_linuxTxtState)に追加できます。
6. ツールを実行する。
例えば、64ビットのLinux移行元サーバーで、root権限を指定して次のコマンドを実行し、ツールを実行します。
```shellsession
sudo ./go2tencentcloud_x64 
```
<dx-alert infotype="notice" title="">
client.jsonの`Client.ToolMode`を`true`に修正していない場合は、ツールを実行するとき、パラメータ`--no-console`を追加する必要があります。次のとおりです：
```shellsession
sudo ./go2tencentcloud_x64 --no-console
```
</dx-alert>
ツール実行後、マイグレーションプロセスが完了するまでしばらく、お待ちください。一般的には、マイグレーションに成功した場合のコンソール出力情報は、次の図に示したとおりです：![](https://main.qcloudimg.com/raw/d32b4be8287d4b06697f0cb03cc6cff8.png)




:::
:::  プライベートネットワークマイグレーションシナリオ3
1. 移行元サーバーと移行先CVMの間に接続チャネルを確立します。
[VPN Peering Connection](https://intl.cloud.tencent.com/document/product/553) / [VPN Connection](https://intl.cloud.tencent.com/document/product/1037) / [CCN](https://intl.cloud.tencent.com/document/product/1003) などの方法によって移行元サーバーと移行先CVMの間に接続チャネルを確立します。
2. マイグレーションツールgo2tencentcloud.zipをダウンロードするか、または移行元サーバーにアップロードし、次のコマンドを実行して対応するディレクトリに進みます。
    1. 次のコマンドを順に実行し、go2tencentcloud.zipを解凍してディレクトリに進みます。
```shellsession
unzip go2tencentcloud.zip
```
```shellsession
cd go2tencentcloud
```
    1. 次のコマンドを順に実行し、go2tencentcloud-linux.zipを解凍してディレクトリに進みます。
```shellsession
unzip go2tencentcloud-linux.zip
```
```shellsession
cd go2tencentcloud-linux
```
<dx-alert infotype="explain" title="">
`go2tencentcloud`ディレクトリ下のファイルは移行されません。移行が必要なファイルをこのディレクトリ下に置かないでください。
</dx-alert>
3. `user.json`ファイルで移行先CVMを設定します。
[user.jsonファイルのパラメータの説明](#userJsonState)に従って、必要な項目と必要な値を設定してください。
4. `client.json`ファイルでマイグレーションモードとその他の項目を設定します。
    - `client.json`ファイルの`Client.ToolMode`の値を`true`に設定すると、ツールマイグレーションモードが標識されます。
    - `client.json`ファイルの`Client.Net.Mode`の項目を`3`に設定すると、[プライベートネットワークマイグレーションモード：シナリオ3](https://intl.cloud.tencent.com/document/product/213/44340#.E6.94.AF.E6.8C.81.E7.9A.84.E8.BF.81.E7.A7.BB.E6.A8.A1.E5.BC.8F)のマイグレーションを実行します。
    - `client.json`ファイルの`Client.Net.Proxy.Ip`と`Client.Net.Proxy.Port`の項目をネットワークプロキシのIPアドレスとポートに設定します。ネットワークプロキシに認証が必要である場合、`Client.Net.Proxy.User`と`Client.Net.Proxy.Password`の項目にネットワークプロキシのユーザー名とパスワードを記入してください。認証が不要な場合は、空白のままにします。 
		また、その他の設定が必要な場合は、[client.jsonファイルパラメータの説明](#clientJsonState)に従って設定してください。
5. （オプション）移行元サーバー上でマイグレーション不要のファイルまたはディレクトリを削除します。
Linux移行元サーバー上でマイグレーション不要のファイルおよびディレクトリがある場合、ファイルおよびディレクトリを[rsync_excludes_linux.txtファイル](#_linuxTxtState)に追加できます。
6. ツールを実行する。
例えば、64ビットのLinux移行元サーバーで、root権限を指定して次のコマンドを実行し、ツールを実行します。
```shellsession
sudo ./go2tencentcloud_x64 
```
<dx-alert infotype="notice" title="">
client.jsonの`Client.ToolMode`を`true`に修正していない場合は、ツールを実行するとき、パラメータ`--no-console`を追加してください。次のとおりです：
```shellsession
sudo ./go2tencentcloud_x64 --no-console
```
</dx-alert>
ツール実行後、マイグレーションプロセスが完了するまでしばらく、お待ちください。一般的には、マイグレーションに成功した場合のコンソール出力情報は、次の図に示したとおりです：
![](https://main.qcloudimg.com/raw/2195589176d3669f08fbb5745901040b.png)

:::

</dx-tabs>


### マイグレーション後の確認

- マイグレーションが失敗した場合は、ログファイル（デフォルトではマイグレーションツールディレクトリ下のログファイル）からのエラーメッセージ出力、ガイドラインドキュメントまたは[サービスマイグレーションに関するよくあるご質問](https://intl.cloud.tencent.com/document/product/213/32395)を確認し、トラブルシューティングと問題の修正を行ってください。
- マイグレーションが成功した場合は、移行先CVMが正常に起動できるか、移行先CVMのデータが移行元サーバーと一致しているか、ネットワークが正常か、他のシステムサービスが正常かなどを確認してください。

ご不明な点やマイグレーションの異常など、ご質問がありましたら、[サービスマイグレーションに関するよくあるご質問](https://intl.cloud.tencent.com/document/product/213/32395)をご参照いただくか、または[お問い合わせ](https://intl.cloud.tencent.com/document/product/213/34837)で解決してください。
