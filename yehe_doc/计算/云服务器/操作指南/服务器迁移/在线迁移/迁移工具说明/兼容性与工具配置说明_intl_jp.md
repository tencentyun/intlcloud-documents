## サポートされているオペレーティングシステム

現在オンラインマイグレーションツールがサポートする移行元サーバーのOSは以下を含みますが、これらのOSに限定されません。

<table>
	<tr><th>Linux OS</th><th>Windows OS</th></tr>
	<tr><td>CentOS 5/6/7/8</td><td rowspan=8>Windows Server 2008<br>Windows Server 2012<br>Windows Server 2016<br>Windows Server 2019<br>Windows Server 2022</td></tr>
	<tr><td>Ubuntu 10/12/14/16/18/20 </td></tr>
	<tr><td>Debian 7/8/9/10</td></tr>
	<tr><td>SUSE 11/12/15</td></tr>
	<tr><td>openSUSE 42</td></tr>
	<tr><td>Amazon Linux AMI</td></tr>
	<tr><td>Red Hat 5/6/7/8</td></tr>
	<tr><td>Oracle Linux 5/6/7/8</td></tr>
</table>

## サポートされているマイグレーションモード

<dx-tabs>
::: パブリックネットワークマイグレーションモード[](id:publicMigration)
お客様の移行元サーバーと移行先CVMの両方にパブリックネットワークアクセス機能がある場合は、パブリックネットワークマイグレーションモードを使用してマイグレーションができます。
現在のパブリックネットワークマイグレーションモードでは、移行元サーバーはインターネット経由でTencent Cloud APIにアクセスし、マイグレーションリクエストを送信するとともに、データを移行先CVMに転送して、移行元サーバーをTencent Cloudの移行先CVMにマイグレーションします。パブリックネットワークマイグレーションモードを下図に示します：
 ![](https://main.qcloudimg.com/raw/5203e535f5ba947bb67c1f91dee52f1f.jpg)
:::
::: プライベートネットワークマイグレーションモード[](id:intranetMigration)
お客様の移行元サーバーまたは移行先CVMがプライベートネットワークまたはVPCにあり、移行元サーバーがインターネット経由で移行先クラウドサーバーとの接続を直接確立できない場合は、ツールのプライベートネットワークマイグレーションモードを使用してマイグレーションができます。[VPCピアリング接続](https://intl.cloud.tencent.com/document/product/553)、[VPN接続](https://intl.cloud.tencent.com/document/product/1037)、[CCN](https://intl.cloud.tencent.com/document/product/1003)または[ダイレクト接続](https://intl.cloud.tencent.com/document/product/216)といった方法で、移行元サーバーと移行先CVM間で接続チャネルを確立する必要があります。

- [](id:Scenario1)**シナリオ1**：（このシナリオは、[ツールを使用したマイグレーション](https://intl.cloud.tencent.com/document/product/213/35640)のみをサポートする）お客様の移行元サーバーまたは移行先CVMがパブリックネットワークにアクセスできない場合は、まずパブリックネットワークアクセス機能を備えたホスト（ゲートウェイなど）を介してインターネット経由でTencent Cloud APIにアクセスすることにより、マイグレーションリクエストを発することができます。次に、接続チャネルを介して移行先CVMにデータを送信してマイグレーションします。このシナリオでは、移行元サーバーと移行先CVMにパブリックネットワークへのアクセス機能は必要ありません。
![](https://main.qcloudimg.com/raw/19300ddf557d4534b1cd77fcbf64ef6a.jpg)
- [](id:Scenario2)**シナリオ2**：お客様の移行元サーバーがパブリックネットワークにアクセスできる場合、まずインターネット経由で移行元サーバー上のTencent Cloud APIにアクセスしてマイグレーションリクエストを発してから、次に接続チャネルを介して移行先CVMにデータを送信してマイグレーションすることができます。このシナリオでは、移行元サーバーにパブリックネットワークへのアクセス機能が必要ですが、移行先CVMには必要ありません。
![](https://main.qcloudimg.com/raw/90bf988ba7cddb9b80307efb30eaad29.jpg)
- [](id:Scenario3)**シナリオ3**：お客様の移行元サーバーがプロキシ経由でパブリックネットワークにアクセスできる場合は、まずネットワークプロキシ経由で移行元サーバー上のTencent Cloud APIにアクセスしてマイグレーションリクエストを発することができます。次に、接続チャネルを介して移行先CVMにデータを送信してマイグレーションします。このシナリオでは、移行元サーバーと移行先CVMにパブリックネットワークへのアクセス機能は必要ありません。
![](https://main.qcloudimg.com/raw/14f81f2c4e6cfff80d912841451c5b69.jpg)
:::
</dx-tabs>


## 圧縮パッケージファイルの説明
`go2tencentcloud.zip`を解凍後のファイルの説明は次のとおりです：
<table>
	<tr><th width="30%">ファイル名</th><th>説明</th></tr>
	<tr><td>go2tencentcloud-linux.zip</td><td>Linux OSのマイグレーション圧縮パッケージです。</td></tr>
	<tr><td>go2tencentcloud-windows.zip</td><td>Windowsシステムのマイグレーション圧縮パッケージ。</td></tr>
	<tr><td>readme.txt</td><td>ディレクトリ概要ファイルです。</td></tr>
	<tr><td>release_notes.txt</td><td>マイグレーションツールの変更ログです。</td></tr>
</table>

`go2tencentcloud-linux.zip`を解凍後のファイルの説明は次のとおりです：
<table>
	<tr><th width="30%">ファイル名</th><th>説明</th></tr>
	<tr><td>go2tencentcloud_x64</td><td>64ビット Linux OS用の移行ツールの実行可能プログラム。</td></tr>
	<tr><td>go2tencentcloud_x32</td><td>32ビット Linux OS用の移行ツールの実行可能プログラム。</td></tr>
	<tr><td>user.json</td><td>マイグレーション時のユーザー情報です。</td></tr>
	<tr><td>client.json</td><td>マイグレーションツールの設定ファイルです。</td></tr>
	<tr><td>rsync_excludes_linux.txt</td><td>rsync構成ファイル。Linuxシステムで移行する必要のないファイルとディレクトリを除外します。</td></tr>
</table>

`go2tencentcloud-windows.zip`を解凍後のファイルの説明は次のとおりです：
<table>
	<tr><th width="30%">ファイル名</th><th>説明</th></tr>
	<tr><td>go2tencentcloud_x64.exe</td><td>64ビットのWindowsシステムのマイグレーションツールで実行可能なプログラムです。</td></tr>
	<tr><td>user.json</td><td>マイグレーション時のユーザー情報です。</td></tr>
	<tr><td>client.json</td><td>マイグレーションツールの設定ファイルです。</td></tr>
	<tr><td>client.exe</td><td>Windowsシステムの移行で実行可能なプログラムです。</td></tr>
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
       <td>APIにアクセスするためにアカウントで使用されるSecretIdです。詳細については、<a href="https://intl.cloud.tencent.com/document/product/598/32675">アクセスキー</a>をご参照ください。</td>
</tr>　
<tr>
      <td>SecretKey</td>
      <td>String</td>
      <td>はい</td>
      <td>APIにアクセスするためにアカウントで使用されるSecretIdです。詳細については、<a href="https://intl.cloud.tencent.com/document/product/598/32675">アクセスキー</a>をご参照ください。</td>
</tr>
</table>

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
	<td>Client.Extra.IgnoreCheck</td>
	<td>Bool</td>
	<td>いいえ</td>
	<td>デフォルト値は 
	<code>false</code>であり、マイグレーションツールはデフォルトではツールの実行開始時に移行元サーバーの環境を自動的にチェックします。チェックを省略したい場合は、 
	<code>true</code>に設定してください。</td>
  </tr>
  <tr>
	<td>Client.Extra.Daemon</td>
	<td>Bool</td>
	<td>いいえ</td>
	<td>デフォルト値は 
	<code>false</code>です。バックグラウンドでマイグレーションツールを実行する必要がある場合、 
	<code>true</code>に設定してください。</td>
  </tr>
  <tr>
	<td> Client.Net.Proxy.Ip</td>
	<td>String</td>
	<td>いいえ</td>
	<td>デフォルト値はNULLです。マイグレーションシナリオがプライベートネットワークのマイグレーション<a href="#Scenario3">シナリオ3</a>である場合、ネットワークプロキシのIPアドレスを設定してください。</td>
  </tr>
	 <tr>
<td> Client.Net.Proxy.IPv6</td>
	<td>Bool</td>
	<td>いいえ</td>
	<td>デフォルト値は<code>false</code>です。IPv6（マイグレーション時に移行元または移行先にはIPv6のIPしかないなど）でデータを転送する場合、このオプションに<code>true</code>を設定してください。そうしないと、マイグレーションのトラフィックはIPv4で転送されます。</td>
  </tr>
  <tr>
	<td> Client.Net.Proxy.Port</td>
	<td>String</td>
	<td>いいえ</td>
	<td>デフォルト値はNULLです。マイグレーションシナリオがプライベートネットワークのマイグレーション<a href="#Scenario3">シナリオ3</a>である場合、ネットワークプロキシポートを設定してください。</td>
  </tr>
   <tr>
	<td> Client.Net.Proxy.User</td>
	<td>String</td>
	<td>いいえ</td>
	<td>デフォルト値はNULLです。マイグレーションシナリオがプライベートネットワークのマイグレーション<a href="#Scenario3">シナリオ3</a>で、ネットワークプロキシには認証が必要である場合、ネットワークプロキシユーザー名を設定してください。</td>
  </tr>
   <tr>
	<td> Client.Net.Proxy.Password</td>
	<td>String</td>
	<td>いいえ</td>
	<td>デフォルト値はNULLです。マイグレーションシナリオがプライベートネットワークのマイグレーション<a href="#Scenario3">シナリオ3</a>で、ネットワークプロキシには認証が必要である場合、ネットワークプロキシパスワードを設定してください。</td>
  </tr>
</table>

<dx-alert infotype="explain" title="">
上記のパラメータを除き、client.jsonファイルのその他の設定項目は通常は入力不要です。
</dx-alert>

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
<td><code>--version</code></td>
<td>バージョン番号を印刷します。</td>
</tr>
<tr>
<td><code>--clean</code></td>
<td>マイグレーションタスクを中止します。</td>
</tr>
</tbody>
</table>
