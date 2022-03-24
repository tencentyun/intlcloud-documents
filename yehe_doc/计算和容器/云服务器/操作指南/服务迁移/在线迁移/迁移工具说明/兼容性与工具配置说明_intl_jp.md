## サポートされているオペレーティングシステム

現在オンライン移行ツールによりサポートされているOSには、以下のようなOSなどが含まれますが、これらに限定されません（32ビットまたは64ビットのいずれでも構いません）。

<table>
	<tr><th>Linux OS</th><th>Windows OS</th></tr>
	<tr><td>CentOS 5/6/7/8</td><td rowspan=7>Windows Server 2008 R2およびこれ以降のバージョン</td></tr>
	<tr><td>Ubuntu 10/12/14/16/18/20 </td></tr>
	<tr><td>Debian 7/8/9/10</td></tr>
	<tr><td>SUSE 11/12/15</td></tr>
	<tr><td>openSUSE 42</td></tr>
	<tr><td>Amazon Linux AMI</td></tr>
	<tr><td>Red Hat 7/8</td></tr>
</table>

## サポートされているマイグレーションモード

<dx-tabs>

::: コンソールによる移行[](id:consoleMigrate)

コンソールマイグレーションツールは現時点ではパブリックネットワークマイグレーションモードのみサポートしており、移行のためのデータ転送はパブリックネットワークを使用して行います。

:::
::: ツールによる移行[](id:consoleMigrate)

ツールによる移行は**パブリックネットワークマイグレーションモード**と**プライベートネットワークマイグレーションモード**をサポートしています。

#### パブリックネットワークマイグレーションモード[](id:publicMigration)
お客様の移行元サーバーと移行先CVMの両方にパブリックネットワークアクセス機能がある場合は、パブリックネットワークマイグレーションモードを使用してマイグレーションができます。
現在のパブリックネットワークマイグレーションモードでは、移行元サーバーはインターネット経由でTencent Cloud APIにアクセスしてマイグレーションリクエストを発するとともに、データを移行先CVMに送信して、移行元サーバーをTencent Cloudの移行先クラウドサーバーにマイグレーションします。パブリックネットワークマイグレーションモードを下図に示します。
 ![](https://main.qcloudimg.com/raw/5203e535f5ba947bb67c1f91dee52f1f.jpg)

​    

#### プライベートネットワークマイグレーションモード[](id:intranetMigration)

お客様の移行元サーバーまたは移行先CVMがプライベートネットワークまたはVPCにあり、移行元サーバーがインターネット経由で移行先クラウドサーバーとの接続を直接確立できない場合は、ツールのプライベートネットワークマイグレーションモードを使用してマイグレーションができます。[VPCピアリング接続](https://intl.cloud.tencent.com/zh/document/product/553)、[VPN接続](https://intl.cloud.tencent.com/zh/document/product/1037)、[CCN](https://intl.cloud.tencent.com/zh/document/product/1003)または[ダイレクト接続](https://intl.cloud.tencent.com/zh/document/product/216)といった方法で、移行元サーバーと移行先CVM間で接続チャネルを確立する必要があります。

- [](id:Scenario1)**シナリオ1**：お客様の移行元サーバーまたは移行先CVMがパブリックネットワークにアクセスできない場合は、まずパブリックネットワークアクセス機能を備えたホスト（ゲートウェイなど）を介してインターネット経由でTencent Cloud APIにアクセスすることにより、マイグレーションリクエストを発することができます。次に、接続チャネルを介して移行先CVMにデータを送信してマイグレーションします。このシナリオでは、移行元サーバーと移行先CVMにパブリックネットワークへのアクセス機能は必要ありません。
![](https://main.qcloudimg.com/raw/19300ddf557d4534b1cd77fcbf64ef6a.jpg)
- [](id:Scenario2)**シナリオ2**：お客様の移行元サーバーがパブリックネットワークにアクセスできる場合、まずインターネット経由で移行元サーバー上のTencent Cloud APIにアクセスしてマイグレーションリクエストを発してから、次に接続チャネルを介して移行先CVMにデータを送信してマイグレーションすることができます。このシナリオでは、移行元サーバーにパブリックネットワークへのアクセス機能が必要ですが、移行先CVMには必要ありません。
![](https://main.qcloudimg.com/raw/90bf988ba7cddb9b80307efb30eaad29.jpg)
- [](id:Scenario3)**シナリオ3**：お客様の移行元サーバーがプロキシ経由でパブリックネットワークにアクセスできる場合は、まずネットワークプロキシ経由で移行元サーバー上のTencent Cloud APIにアクセスしてマイグレーションリクエストを発することができます。次に、接続チャネルを介して移行先CVMにデータを送信してマイグレーションします。このシナリオでは、移行元サーバーと移行先CVMにパブリックネットワークへのアクセス機能は必要ありません。
![](https://main.qcloudimg.com/raw/14f81f2c4e6cfff80d912841451c5b69.jpg)


:::

</dx-tabs>




## 圧縮パッケージファイルの説明
`go2tencentcloud.zip`を解凍後のファイルの説明は次のとおりです。
<table>
	<tr><th width="30%">ファイル名</th><th>説明</th></tr>
	<tr><td>go2tencentcloud_console.zip</td><td>コンソールを使用したマイグレーション用の圧縮パッケージです。</td></tr>
	<tr><td>go2tencentcloud_tool.zip</td><td>ツールを使用したマイグレーション用の圧縮パッケージです。</td></tr>
	<tr><td>readme.txt</td><td>ディレクトリ概要ファイルです。</td></tr>
	<tr><td>release_notes.txt</td><td>マイグレーションツールの変更ログです。</td></tr>
</table>
`go2tencentcloud_console.zip`または`go2tencentcloud_tool.zip` を解凍後のファイルの説明は次のとおりです。
<table>
	<tr><th width="30%">ファイル名</th><th>説明</th></tr>
	<tr><td>go2tencentcloud_x64</td><td>64ビット Linux OS用の移行ツールの実行可能プログラム。</td></tr>
	<tr><td>go2tencentcloud_x32</td><td>32ビット Linux OS用の移行ツールの実行可能プログラム。</td></tr>
	<tr><td>user.json</td><td>移行中の移行元サーバーと移行先CVMの設定ファイル。<a href="#userJsonState">user.jsonファイルのパラメーターの説明</a>に従って設定を変更してください。</td></tr>
	<tr><td>client.json</td><td>マイグレーションツールの設定ファイルです。コンソールによる移行の場合は通常変更する必要はありません。</td></tr>
	<tr><td>rsync_excludes_linux.txt</td><td>rsync構成ファイル。Linuxシステムで移行する必要のないファイルとディレクトリを除外します。</td></tr>
</table>

<dx-alert infotype="notice" title="">
設定ファイルは削除できません。設定ファイルはgo2tencentcloudの実行可能なプログラムと同じ階層のディレクトリ下に置いてください。 
</dx-alert>



### user.jsonファイルパラメータの説明[](id:userJsonState)

<dx-tabs>

::: コンソールによる移行[](id:consoleMigrate)

コンソールを使用したマイグレーションの場合、user.json設定ファイルの説明は下表のとおりです。

<table>
	<tr><th>パラメータ名</th><th>タイプ</th><th>入力必須かどうか</th><th>説明</th></tr>
	<tr><td>SecretId</td><td>String</td><td>はい</td><td>APIにアクセスするためにアカウントで使用されるSecretIdです。詳細については、<a href="https://intl.cloud.tencent.com/document/product/598/32675">アクセスキー</a>をご参照ください。</td></tr>　
	<tr><td>SecretKey</td><td>String</td><td>はい</td><td>APIにアクセスするためにアカウントで使用されるSecretIdです。詳細については、<a href="https://intl.cloud.tencent.com/document/product/598/32675">アクセスキー</a>をご参照ください。</td></tr>
</table>

:::
::: ツールによる移行[](id:consoleMigrate)

ツールを使用したマイグレーションの場合、user.json設定ファイルの説明は下表のとおりです。

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
	<td>データディスク番号です。数値の範囲は[1,20]であり、値が
	<code>1</code>であれば、このデータディスクが移行先のCVMにマウントされる1番目のデータディスクであることを表します。値が
	<code>2</code>であれば、移行先のCVMにマウントされる2番目のデータディスクであることを表します。以下同様とします。</td>
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

<a href="https://intl.cloud.tencent.com/document/product/213/35640">設定ファイルの変更</a>の例を参照し、実際の業務シナリオを踏まえて設定ファイルを変更することができます。

:::

</dx-tabs>


### client.json ファイルパラメータの説明[](id:clientJsonState)

<dx-tabs>

::: コンソールによる移行[](id:consoleMigrate)

コンソールを使用したマイグレーションの場合、通常はclient.json設定ファイルを変更する必要はありません。

:::
::: ツールによる移行[](id:consoleMigrate)

ツールを使用したマイグレーションの場合、client.json設定ファイルの説明は次のとおりです。

<table>
  <tr>
	<th>パラメータ名</th>
	<th>タイプ</th>
	<th><br>入力必須かどうか</th>
	<th>説明</th>
  </tr>
  <tr>
	<td>Client.Net.Mode</td>
	<td>Integer</td>
	<td>はい</td>
	<td>マイグレーションモードパラメータです。デフォルトではパブリックネットワークを使用して転送します。値は次のようになります。
	<code>0</code>、数値の範囲：<code>0</code>（
	<a href="#publicMigration">パブリックネットワークマイグレーションモード</a>）、<code>1</code>（
	<a href="#Scenario1">プライベートネットワークマイグレーションモード：シナリオ1</a>）、<code>2</code>（
	<a href="#Scenario2">プライベートネットワークマイグレーションモード：シナリオ2</a>）、<code>3</code>（
	<a href="#Scenario3">プライベートネットワークマイグレーションモード：シナリオ3</a>）。プライベートネットワークマイグレーションの詳細については、<a href="https://intl.cloud.tencent.com/document/product/213/44341">プライベートネットワークマイグレーションのチュートリアル</a>をご参照ください。</td>
  </tr>
  <tr>
	<td>Client.Extra.IgnoreCheck</td>
	<td>Bool</td>
	<td>いいえ</td>
	<td>デフォルト値は 
	<code>false</code>であり、マイグレーションツールはデフォルトではツールの実行開始時に移行元サーバーの環境を自動的にチェックします。チェックを省略したい場合は、 
	<code>true</code>に設定してください。</td>
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
	<td>転送検証項目です。 
	<code>true</code>に設定すると、転送の整合性の検証を強化することができますが、移行元サーバーCPUの
	負荷が上昇し、転送速度が遅くなることがあります。デフォルト値は 
	<code>false</code>であり、デフォルトでは検証を行いません。</td>
  </tr>
</table>




<dx-alert infotype="explain" title="">
上記のパラメータを除き、client.jsonファイルのその他の設定項目は通常は入力不要です。
</dx-alert>

:::

</dx-tabs>

###  rsync\_excludes\_linux.txtファイル説明[](id:_linuxTxtState)

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

## ツールの実行パラメータの説明

<dx-tabs>

::: コンソールによる移行[](id:consoleMigrate)

コンソールを使用したマイグレーションの場合の、マイグレーションツールの実行パラメータの説明は下表のとおりです。

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
<td><code>--version</code></td>
<td>バージョン番号を印刷します。</td>
</tr>
</tbody></table>

:::
::: ツールによる移行[](id:consoleMigrate)

ツールを使用したマイグレーションの場合の、マイグレーションツールの実行パラメータの説明は下表のとおりです。

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

:::

</dx-tabs>

