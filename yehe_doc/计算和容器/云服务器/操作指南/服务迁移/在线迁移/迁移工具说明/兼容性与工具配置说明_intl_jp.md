## サポートされているオペレーティングシステム

現在オンラインマイグレーションツールがサポートする移行元サーバーのOSは以下を含みますが、これらのOSに限定されません：

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
現在のパブリックネットワークマイグレーションモードでは、移行元サーバーはインターネット経由でTencent Cloud APIにアクセスしてマイグレーションリクエストを発するとともに、データを移行先CVMに送信して、移行元サーバーをTencent Cloudの移行先クラウドサーバーにマイグレーションします。パブリックネットワークマイグレーションモードを下図に示します。
 ![](https://qcloudimg.tencent-cloud.cn/raw/62f9e6e92dc6ded27e15d2b2b84d4be1.png)
:::
::: プライベートネットワークマイグレーションモード[](id:intranetMigration)
お客様の移行元サーバーまたは移行先CVMがプライベートネットワークまたはVPCにあり、移行元サーバーがインターネット経由で移行先クラウドサーバーとの接続を直接確立できない場合は、ツールのプライベートネットワークマイグレーションモードを使用してマイグレーションができます。[VPCピアリング接続](https://intl.cloud.tencent.com/zh/document/product/553)、[VPN接続](https://intl.cloud.tencent.com/zh/document/product/1037)、[CCN](https://intl.cloud.tencent.com/zh/document/product/1003)または[ダイレクト接続](https://intl.cloud.tencent.com/zh/document/product/216)といった方法で、移行元サーバーと移行先CVM間で接続チャネルを確立する必要があります。

- [](id:Scenario1)**シナリオ1**：（このシナリオは [ツールを使用したマイグレーション](https://intl.cloud.tencent.com/document/product/213/35640)）のみをサポートしています。お客様の移行元サーバーまたは移行先CVMがパブリックネットワークにアクセスできない場合は、まずパブリックネットワークアクセス機能を備えたホスト（ゲートウェイなど）を介してインターネット経由でTencent Cloud APIにアクセスすることにより、マイグレーションリクエストを発することができます。次に、接続チャネルを介して移行先CVMにデータを送信してマイグレーションします。このシナリオでは、移行元サーバーと移行先CVMにパブリックネットワークへのアクセス機能は必要ありません。
![](https://qcloudimg.tencent-cloud.cn/raw/c7663b4b6f65696deab855fddd7b6121.png)
- [](id:Scenario2)**シナリオ2**：お客様の移行元サーバーがパブリックネットワークにアクセスできる場合、まずインターネット経由で移行元サーバー上のTencent Cloud APIにアクセスしてマイグレーションリクエストを発してから、次に接続チャネルを介して移行先CVMにデータを送信してマイグレーションすることができます。このシナリオでは、移行元サーバーにパブリックネットワークへのアクセス機能が必要ですが、移行先CVMには必要ありません。
![](https://qcloudimg.tencent-cloud.cn/raw/6ed29f29d158604cc0474c5be1059e16.png)
- [](id:Scenario3)**シナリオ3**：お客様の移行元サーバーがプロキシ経由でパブリックネットワークにアクセスできる場合は、まずネットワークプロキシ経由で移行元サーバー上のTencent Cloud APIにアクセスしてマイグレーションリクエストを発することができます。次に、接続チャネルを介して移行先CVMにデータを送信してマイグレーションします。このシナリオでは、移行元サーバーと移行先CVMにパブリックネットワークへのアクセス機能は必要ありません。
![](https://qcloudimg.tencent-cloud.cn/raw/60bf16168f301be88e1514e0b740b4d0.png)
:::
</dx-tabs>


## 圧縮パッケージファイルの説明
`go2tencentcloud.zip`を解凍後のファイルの説明は次のとおりです。
<table>
	<tr><th width="30%">ファイル名</th><th>説明</th></tr>
	<tr><td>go2tencentcloud-linux.zip</td><td>Linuxシステムのマイグレーション圧縮パッケージ。</td></tr>
	<tr><td>go2tencentcloud-windows.zip</td><td>Windowsシステムのマイグレーション圧縮パッケージ。</td></tr>
	<tr><td>readme.txt</td><td>ディレクトリ概要ファイルです。</td></tr>
	<tr><td>release_notes.txt</td><td>マイグレーションツールの変更ログです。</td></tr>
</table>

`go2tencentcloud-linux.zip` を解凍後のファイルの説明は次のとおりです。
<table>
	<tr><th width="30%">ファイル名</th><th>説明</th></tr>
	<tr><td>go2tencentcloud_x64</td><td>64ビットのLinuxシステムのマイグレーションツールで実行可能なプログラムです。</td></tr>
	<tr><td>go2tencentcloud_x32</td><td>32ビットのLinuxシステムのマイグレーションツールで実行可能なプログラムです。</td></tr>
	<tr><td>user.json</td><td>移行時のユーザー情報です。</td></tr>
	<tr><td>client.json</td><td>マイグレーションツールの設定ファイルです。</td></tr>
	<tr><td>rsync_excludes_linux.txt</td><td>rsync設定ファイルは、Linuxシステムで移行不要なファイルディレクトリを削除します。</td></tr>
</table>

`go2tencentcloud-windows.zip`を解凍後のファイルの説明は次のとおりです。
<table>
	<tr><th width="30%">ファイル名</th><th>説明</th></tr>
	<tr><td>go2tencentcloud_x64.exe</td><td>64ビットのWindowsシステムのマイグレーションツールで実行可能なプログラムです。</td></tr>
	<tr><td>user.json</td><td>移行時のユーザー情報です。</td></tr>
	<tr><td>client.json</td><td>マイグレーションツールの設定ファイルです。</td></tr>
	<tr><td>client.exe</td><td>Windowsシステムの移行で実行可能なプログラムです。</td></tr>
</table>

<dx-alert infotype="notice" title="">
設定ファイルは削除できません。設定ファイルはgo2tencentcloudの実行可能なプログラムと同じ階層のディレクトリ下に置いてください。 
</dx-alert>

### user.jsonファイルパラメータの説明[](id:userJsonState)

user.json設定ファイルの説明は次のとおりです。

<table>
	<tr><th>パラメータ名</th><th>タイプ</th><th>入力必須かどうか</th><th>説明</th></tr>
	<tr><td>SecretId</td><td>String</td><td>は</td><td>アカウントAPIアクセスキーのSecretIdです。詳細情報については<a href="https://intl.cloud.tencent.com/document/product/598/32675"> アクセスキー</a>をご参照ください。</td></tr>
	<tr><td>SecretKey</td><td>String</td><td>は</td><td>アカウントAPIアクセスキーのSecretKeyです。詳細情報については<a href="https://intl.cloud.tencent.com/document/product/598/32675"> アクセスキー</a>をご参照ください。</td></tr>
</table>

### client.json ファイルパラメータの説明[](id:clientJsonState)

client.json設定ファイル部分の説明は次のとおりです。

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
	<code>false</code>、マイグレーションツールをバックエンドで動作させる必要がある場合は、 
	<code>true</code>に設定してください。</td>
  </tr>
  <tr>
	<td> Client.Net.Proxy.Ip</td>
	<td>String</td>
	<td>いいえ</td>
	<td>デフォルト値が空で、マイグレーションモードがプライベートネットワークマイグレーションの<a href="#Scenario3">モード3</a> の場合、ネットワークプロキシのIPアドレスを設定する必要があります。</td>
  </tr>
  <tr>
	<td> Client.Net.Proxy.Port</td>
	<td>String</td>
	<td>いいえ</td>
	<td>デフォルト値が空で、マイグレーションモードがプライベートネットワークマイグレーションの<a href="#Scenario3">モード3</a> の場合、ネットワークプロキシのポートを設定する必要があります。</td>
  </tr>
   <tr>
	<td> Client.Net.Proxy.User</td>
	<td>String</td>
	<td>いいえ</td>
	<td>デフォルト値が空で、マイグレーションモードがプライベートネットワークマイグレーションの<a href="#Scenario3">モード3</a> であり，かつネットワークプロキシが認証を必要とする場合、ネットワークプロキシのユーザー名を設定する必要があります。</td>
  </tr>
   <tr>
	<td> Client.Net.Proxy.Password</td>
	<td>String</td>
	<td>いいえ</td>
	<td>デフォルト値が空で、マイグレーションモードがプライベートネットワークマイグレーションの<a href="#Scenario3">モード3</a> であり，かつネットワークプロキシが認証を必要とする場合、ネットワークプロキシのパスワードを設定する必要があります。</td>
  </tr>
</table>

<dx-alert infotype="explain" title="">
上記のパラメータを除き、client.jsonファイルのその他の設定項目は通常は入力不要です。
</dx-alert>

###  rsync\_excludes\_linux.txtファイル説明[](id:_linuxTxtState)

Linux移行元サーバー内で移行転送の不要なファイル、または指定ディレクトリの設定ファイルを削除します。このファイルではデフォルトで以下のディレクトリとファイルが削除されています。**削除および変更はしないでください**。
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
</tbody>
</table>
