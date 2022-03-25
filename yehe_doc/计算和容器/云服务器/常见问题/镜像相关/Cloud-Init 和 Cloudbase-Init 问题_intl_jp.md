## Cloud-Init

### Cloud-Initとは
Cloud-InitはCVMインスタンス内で非常駐サービスとして実行されるオープンソースツールです。起動時に実行され、実行が完了するとすぐに終了し、どちらのポートも監視しません。
Tencent CloudのLinuxパブリックイメージには、cloud-initサービスでプリインストールされています。 Cloud-Initサービスは主にCVMインスタンスの初期化操作（たとえば、DNS、Hostname、IP、およびその他の情報の設定）を行い、及びCVMインスタンスの作成時に初めて起動に指定するカスタムスクリプトの実行に使用されるため、従って、Cloud-Initサービスにはrootユーザーとして実行する必要があります。

### どのようにLinuxインスタンス内のCloud-Initサービスが正常に実行されていることを確認しますか。


#### Cloud-Initサービス動作確認プログラム[](id:checkcloud-init)

[標準ログイン方式を使用してLinuxインスタンスにログイン（推奨）](https://intl.cloud.tencent.com/document/product/213/5436)を参照してインスタンスにログインし、以下のコマンドを順に実行します。エラーが報告されるかどうかを観察し、実行結果が表示されればサービスは正常に実行されています。表示されない場合、エラーの原因が表示されますので、表示された内容に従ってトラブルシューティングを行ってください。
<dx-alert infotype="explain" title="">
このステップは、Linuxパブリックイメージを使用して作成されたCVMインスタンスにのみ適用されます。ご自身でCloud-Initをインストールした場合は、実情に即して実行コマンドを調整してください。
</dx-alert>


1. cloud-init キャッシュディレクトリを削除します。
```
rm -rf /var/lib/cloud
```
2. 完全なcloud-init初期化を実行します。
```
/usr/bin/cloud-init init --local
```
3. 構成されたデータソースからデータをプルします。
```
/usr/bin/cloud-init init
```
4. Cloud-Initの初期化には複数のステージがあります。ステージ間の十分な依存関係を確保するために、cloud-init モジュールがconfig stageを指定して実行します。
```
/usr/bin/cloud-init modules --mode=config
```
5. cloud-init modulesがconfig stageを指定して実行します。
```
/usr/bin/cloud-init modules --mode=final
```

### Cloud-Init はどのようなインスタンス初期化操作を実行しましたか。

Tencent Cloudはcloud-initを介してインスタンスのすべての初期化操作を実行し、インスタンス全体の操作をより透過的にします。 以下の内容は初期化操作について簡単に紹介します。詳細については、[Cloud-init 公式ドキュメント](http://cloudinit.readthedocs.io/en/latest/)をご参照ください。

<table>
<tr>
    <th style="width: 18%;">初期化タイプ</th>
    <th style="width: 25%;">デフォルトの動作</th>
    <th style="width: 27%;">無効化方法</th>
    <th style="width: 30%;">注意事項</th>
  </tr>
  <tr>
	<td>hostname の初期化</td>
	<td>インスタンス
	<b>初回起動</b>時に、Cloud-Initは、 
	<code>vendor_data.json</code>のhostname情報を用いて、インスタンスのhostnameを設定します。</td>
	<td>
	カスタムイメージを使用してインスタンスを作成または再インストールする場合に、カスタムイメージ内にカスタムのhostname
	の設定を維持したいときは、カスタムイメージを作成する前に、<code>/etc/cloud/cloud.cfg</code>の<code>preserve_hostname</code>を<code>true</code>に設定し、<code>- scripts-user</code>の行の構成を削除してください。
	</td>
	<td><code>preserve_hostname</code>が 
	<code>true</code>であり、かつ、<code>- scripts-user</code>の構成が無効化されている場合、インスタンス内の 
	<code>/var/lib/cloud/instance/scripts/runcmd</code>
	初期化スクリプトは実行されず、他のサブアイテムの初期化にも影響を与えます（主にBCM、クラウドセキュリティのインストール、ソフトウェアソースの設定に関わります）。
	また、サブマシンを作成しても、カスタムスクリプトは実行されません。</td>
  </tr>
  <tr>
	<td>/etc/hosts の初期化</td>
	<td>インスタンス
	<b>初回起動</b>時にCloud-Initはデフォルトで 
	<code>/etc/hosts</code>を以下のように初期化します 
	<code>127.0.0.1 $hostname</code>。</td>
	<td>カスタムイメージを使用してインスタンスを作成または再インストールする場合に、カスタムイメージ内にカスタムのhostname
	の設定を維持したいときは、カスタムイメージを作成する前に、 
	<code>/etc/cloud/cloud.cfg</code>の 
	<code>- scripts-user</code>と 
	<code>- [&#39;update_etc_hosts&#39;, &#39;once-per-instance&#39;]</code>の2行の構成を削除できます。</td>
	<td>
	  <ul style="margin: 0px;">
		<li>この 
		<code>- scripts-user</code>行の構成を無効化すると、インスタンス内の 
		<code>/var/lib/cloud/instance/scripts/runcmd</code>
		初期化スクリプトは実行されず、他のサブアイテムの初期化にも影響を与えます（主にBCM、クラウドセキュリティのインストール、ソフトウェアソースの設定に関わります）。また、サブマシンを作成しても、カスタムスクリプトは実行されません。</li>
		<li>サブマシンが再起動するたびに、既存マシンの 
		<code>/etc/hosts</code>の設定が上書きされます。ソリューションについては、 
		<a href="https://intl.cloud.tencent.com/document/product/213/32504">Linuxインスタンスのetc hostsの構成を効果的に変更する方法
		</a>をご参照ください。</li>
	  </ul>
	</td>
  </tr>
  <tr>
	<td>DNSの初期化（非 DHCPシナリオ）</td>
	<td>インスタンス
	<b>初回起動</b>時に、Cloud-Initは、 
	<code>vendor_data.json</code>のnameservers情報を用いて、インスタンスのDNSを設定します。</td>
	<td>カスタムイメージを使用してインスタンスを作成または再インストールする場合に、カスタムイメージ内にカスタムのDNS
	の設定を維持したいときは、カスタムイメージを作成する前に、 
	<code>/etc/cloud/cloud.cfg</code>の 
	<code>- resolv_conf</code>と 
	<code>unverified_modules: [&#39;resolv_conf&#39;]</code>の2行の構成を削除できます。</td>
	<td>なし。</td>
  </tr>
  <tr>
	<td>ソフトウェアソースの初期化</td>
	<td>インスタンス
	<b>初回起動</b>時に、Cloud-Initは、 
	<code>vendor_data.json</code>のwrite_files情報を用いて、インスタンスのソフトウェアソースを設定します。</td>
	<td>
	カスタムイメージを使用してインスタンスを作成または再インストールする場合に、カスタムイメージ内にカスタムのソフトウェアソースの設定を維持したいときは、カスタムイメージを作成する前に、
	<code>/etc/cloud/cloud.cfg</code>の 
	<code>- write-files</code>の行の構成を削除できます。</td>
	<td>なし。</td>
  </tr>
  <tr>
	<td>NTP の初期化</td>
	<td>インスタンス
	<b>初回起動</b>時に、Cloud-Initは、 
	<code>vendor_data.json</code>のNTP Server情報を使用して、インスタンスのNTPサーバーの構成を設定し、NTP
	Serviceをプルします。</td>
	<td>カスタムイメージを使用してインスタンスを作成または再インストールする場合に、カスタムイメージ内にカスタムのNTP
	の設定を維持したいときは、カスタムイメージを作成する前に、 
	<code>/etc/cloud/cloud.cfg</code>の 
	<code>- ntpの行の構成を削除できます。</code></td>
	<td>なし。</td>
  </tr>
  <tr>
	<td>パスワードの初期化</td>
	<td>インスタンス
	<b>初回起動</b>時に、Cloud-Initは、 
	<code>vendor_data.json</code>のchpasswd情報を用いて、インスタンスのデフォルトのアカウントパスワードを設定します。</td>
	<td>
	カスタムイメージを使用してインスタンスを作成または再インストールする場合に、カスタムイメージ内にカスタムのデフォルトのアカウントパスワードを維持したいときは、カスタムイメージを作成する前に、	
	<code>/etc/cloud/cloud.cfg</code>の 
	<code>- set-passwords</code>の行の構成を削除できます。</td>
	<td>なし。</td>
  </tr>
  <tr>
	<td>キーバインド</td>
	<td>インスタンス
	<b>初回起動</b>時に、Cloud-Initは、 
	<code>vendor_data.json</code>の ssh_authorized_keys情報を用いて、インスタンスのデフォルトのアカウントキーを設定します。</td>
	<td>
	カスタムイメージを使用してインスタンスを作成または再インストールする場合に、カスタムイメージ内にカスタムのキーを維持したいときは、カスタムイメージを作成する前に、	
	<code>/etc/cloud/cloud.cfg</code>の 
	<code>- users-groups</code>の行の構成を削除できます。</td>
	<td>
	インスタンス内でキーを手動でバインドした場合、コンソールからキーバインド操作が行われると、システムはキーを上書きします。</td>
  </tr>
  <tr>
	<td>ネットワーク初期化（非 DHCP シナリオ）</td>
	<td>インスタンス
	<b>初回起動</b>時に、Cloud-Initは、 
	<code>network_data.json</code>の情報を使用して、インスタンスのIP、GATEWAY、MASKなどを設定します。</td>
	<td>
	カスタムイメージを使用してインスタンスを作成または再インストールする場合に、カスタムイメージ内にカスタムのネットワーク情報を維持したいときは、カスタムイメージを作成する前に、	
	<code>/etc/cloud/cloud.cfg</code>に 
	<code>network: {config: disabled}</code>の行の構成を追加できます。</td>
	<td>なし。</td>
  </tr>
</table>



### どのようにCloud-Initに関連する問題を特定しますか。 

#### 1. Cloud-Init依存関係のアンインストールによるエラー
- 問題の説明：
コマンドを使用してCloud-Initサービスが正常に実行されていることを確認する時に、次のエラーが返されます：
```
Traceback (most recent call last):
  File "/usr/bin/cloud-init", line 5, in 
    ********
    raise DistributionNotFound(req)
pkg_resources.DistributionNotFound: pyyaml
```
- 問題分析：
「pkg_resources.DistributionNotFound: xxxxx 」は、Cloud-Init依存関係がアンインストールされたことを示します。
- ソリューション ：
 1. 依存関係を再インストールします。
 2. すべての操作が正常に実行されるまで、[Cloud-Init サービス実行時のトラブルシューティング](#checkcloud-init)に従って操作を実行します。

#### 2. デフォルトのPythonインタープリターの変更によるエラー
- 問題の説明：
起動時にcloud-initを実行すると、エラーが返されます。
- 問題分析：
Cloud-Initをインストールする時に、PythonインタープリターはデフォルトでPython2（つまり、`/usr/bin/python`および`/bin/python`はPython2にリンクされます。）を使用します。ユーザーのビジネスニーズに応じて、インスタンスの中でPythonのデフォルトインタープリターをPython3（つまり、Python3を指すように、`/usr/bin/pythonと`/bin/python`を変更する）に変更することができます。互換性の問題のため、起動時にCloud-Initを実行するとエラーが発生しました。
- ソリューション ：
 1. `/usr/bin/cloud-init`ファイルで指定されたPythonインタープリターを変更し、`#/usr/bin/python`または`#/bin/python`を`#! user/bin/python`に変更します 。
<dx-alert infotype="notice" title="">
シンボリックリンクを使用せず、直接、特定のインタープリターを指定します。
</dx-alert>
 2. すべての操作が正常に実行されるまで、[Cloud-Init サービス実行時のトラブルシューティング](#checkcloud-init)に従って操作を実行します。

## Cloudbase-Init

### Cloudbase-Initとは
Cloud-Initと同様に、Cloudbase-InitはWindowsCVMインスタンスと通信するためのツールです。 Cloudbase-Initサービスは、インスタンスの初回起動時に実行されます。このサービスはインスタンスの初期化設定情報を読み取り、インスタンスを初期化します。 同時に、後続のパスワードのリセットやIPの変更などの機能もCloudbase-Initを介して行われます。

### どのようにWindowsインスタンス内のCloudbase-Initサービスが正常に動作していることを確認しますか。


#### Cloudbase-Initサービス動作確認プログラム：[](id:checkcloudbase-init)
1. インスタンスにログインします。
<dx-alert infotype="explain" title="">
パスワードを忘れた場合、またはCloudbase-Initサービスの異常に起因してリセットに失敗した場合は、[ステップ2](#step02)でパスワードをリセットできます。 
</dx-alert>
2. [](id:step02)**コントロールパネル** > **管理ツール** > **サービス**を開きます。
3. cloudbase-initサービスを見つけ、**プロパティ**を右クリックしてcloudbase-initのプロパティウィンドウを開きます。
 -「スタートアップの種類」を確認し、「スタートアップの種類」が「自動」に設定されていることを確認します。 以下に示すように：
![](https://main.qcloudimg.com/raw/310a278dd2eaf2124d0d52055e0b5b6f.png)
 -「ログインID」を確認し、「ログインID」が「ローカルシステムアカウント」であることを確認します。 以下に示すように：
![](https://main.qcloudimg.com/raw/5a3f623aaf44d55cfe2eaa6aeadb4c12.png)
 - 手動でcloudbase-initサービスを起動し、エラーが返されるかどうかを確認します。
エラーが返された場合は、まず問題を修正してください。cloudbase-initの関連する操作の実行をブロックするセキュリティソフトウェアがインストールしているかどうかを確認する必要があります。 
![](https://main.qcloudimg.com/raw/dbbe8f9fc05b07d8011705d9d217b76c.png)
 -「レジストリ」を開き、すべての「LocalScriptsPlugin」を見つけ、その値が2であることを確認します。 以下に示すように：
![](https://main.qcloudimg.com/raw/16106e540d8cf4ef39e5dccb44251350.png)
 - CD-ROMのロードが禁止になっているかどうかを確認します。 次の図に示すように、光ディスクドライブが表示されている場合は、ロードが禁止になっていないことを意味します。そうでない場合は禁止になっているため、禁止を取り消す必要があります。
![](https://main.qcloudimg.com/raw/7707e694b475ba4d70b4d1d52a6c98bb.png)

### どのようにCloudbase-Initに関連する一般的な問題を特定しますか。
#### 初期化中にパスワードをリセットできませんでした
- 考えられる理由：
 - cloudbase-initアカウントのパスワードを手動で変更されたため、cloudbase-initサービスの起動が失敗になり、初期化中にパスワードのリセットなどの操作も失敗になります。
 - cloudbase-initサービスが禁止されたため、初期化中にパスワードをリセットするなどの操作が失敗しました。
 - セキュリティソフトウェアがcloudbase-initサービスのパスワードリセット操作をブロックしたため、操作は成功した結果を返しますが、実際のリセットは失敗しました。
- ソリューション ：
考えられる理由については、以下の3つのポイントをご参照ください。
 1. cloudbase-initサービスをLocalSystemサービスに変更します。具体的な操作については、[Cloudbase-Init サービス実行時のトラブルシューティング](#checkcloudbase-init)の[ステップ2](#step02)をご参照ください。 
 2. cloudbase-initサービスのスタートアップの種類を自動に変更します。 詳細の操作については、[Cloudbase-Init サービス実行時のトラブルシューティング](#checkcloudbase-init)の[ステップ 2](#step02)をご参照ください。
 3.関連するセキュリティソフトウェアをアンインストールするか、Cloudbase-Initサービスの関連操作をセキュリティソフトウェアのホワイトリストに追加します。

