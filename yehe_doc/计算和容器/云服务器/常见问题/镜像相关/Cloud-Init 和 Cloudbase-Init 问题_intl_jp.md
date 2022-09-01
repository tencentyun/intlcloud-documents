## Cloud-Init

### Cloud-Initとは何ですか。
Cloud-Initはオープンソースツールで、CVMインスタンス内部の非常駐サービスで動作します。起動時に実行され、実行が完了するとすぐに終了し、どのポートも監視しません。
Tencent CloudのLinuxパブリックイメージはすべてCloud-Initサービスがあらかじめインストールされています。Cloud-Initサービスは主にCVMインスタンスの初期化操作（例： DNS、Hostname、IPなどの情報の設定）を実現するために用いられ、ユーザーがCVMインスタンスを作成する時に初回起動時に実行するように指定したカスタムスクリプトを実行するため、rootユーザーでCloud-Initサービスを実行する必要があります。

### Linuxインスタンス内部のCloud-Initサービスが正常に動作しているかどうかを確認するにはどうすればよいですか。


#### Cloud-Initサービス動作確認プログラム[](id:checkcloud-init)

[標準ログイン方式を使用してLinuxインスタンスにログイン（推奨）](https://intl.cloud.tencent.com/document/product/213/5436)を参照してインスタンスにログインし、以下のコマンドを順に実行します。エラーが報告されるかどうかを観察し、実行結果が表示されればサービスは正常に実行されています。表示されない場合、エラーの原因が表示されますので、表示された内容に従ってトラブルシューティングを行ってください。
<dx-alert infotype="explain" title="">
このステップは、Linuxパブリックイメージを使用して作成されたCVMインスタンスにのみ適用されます。ご自身でCloud-Initをインストールした場合は、実情に即して実行コマンドを調整してください。
</dx-alert>


1. cloud-initキャッシュディレクトリを削除します。
```shellsession
rm -rf /var/lib/cloud
```
2. cloud-init全体の初期化を実行します。
```shellsession
/usr/bin/cloud-init init --local
```
3. 設定されたデータソースに基づいてデータを取得します。
```shellsession
/usr/bin/cloud-init init
```
4. Cloud-Initの初期化は複数のstageに分かれています。各stageの依存が充分であることを確認し、cloud-init modulesで実行するconfig stageを指定します。
```shellsession
/usr/bin/cloud-init modules --mode=config
```
5. cloud-init modulesで実行するfinal stageを指定します。
```shellsession
/usr/bin/cloud-init modules --mode=final
```

### Cloud-Initはどのようなインスタンス初期化の操作を実行しますか。

Tencent CloudはCloud-Initによってインスタンスのすべての初期化操作を実現し、インスタンス内部全体の操作をより透明化します。以下の内容で関連する操作状況をご紹介しますが、詳細については、[Cloud-init公式ドキュメント](http://cloudinit.readthedocs.io/en/latest/)をご参照ください。

<table>
<tr>
    <th style="width: 18%;">初期化タイプ</th>
    <th style="width: 25%;">デフォルトの動作</th>
    <th style="width: 27%;">無効化方法</th>
    <th style="width: 30%;">注意事項</th>
  </tr>
  <tr>
	<td>hostnameの初期化</td>
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
	初期化スクリプトは実行されず、他のサブアイテムの初期化にも影響を与えます（主にCM、クラウドセキュリティのインストール、ソフトウェアソースの設定に関わります）。
	また、サブマシンを作成しても、カスタムスクリプトは実行されません。</td>
  </tr>
  <tr>
	<td>/etc/hostsの初期化</td>
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
		初期化スクリプトは実行されず、他のサブアイテムの初期化にも影響を与えます（主にCM、クラウドセキュリティのインストール、ソフトウェアソースの設定に関わります）。また、サブマシンを作成しても、カスタムスクリプトは実行されません。</li>
		<li>サブマシンが再起動するたびに、既存マシンの 
		<code>/etc/hosts</code>の設定が上書きされます。ソリューションについては、 
		<a href="https://intl.cloud.tencent.com/document/product/213/32504">Linuxインスタンスのetc hostsの構成を効果的に変更する方法
		</a>をご参照ください。</li>
	  </ul>
	</td>
  </tr>
  <tr>
	<td>DNSの初期化（非DHCPシナリオ）</td>
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
	<td>NTPの初期化</td>
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
	<td>キーのバインド</td>
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
	<td>ネットワークの初期化（非DHCPシナリオ）</td>
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



### Cloud-Initのよくある問題をどのようにトラブルシューティングすればよいですか。 

#### 1. Cloud-Initの依存パッケージをアンインストールしたことによるエラー
- 問題の現象：
コマンドを使用してCloud-Initサービスが正常に動作しているかどうかを確認した場合、以下のようなエラーが発生することがあります：
```
Traceback (most recent call last):
  File "/usr/bin/cloud-init", line 5, in 
    ********
    raise DistributionNotFound(req)
pkg_resources.DistributionNotFound: pyyaml
```
- 問題の分析 ：
「pkg_resources.DistributionNotFound: xxxxx」はCloud-Initのインストールされている依存パッケージがアンインストールされたことを表します。
- 対処方法：
 1. この依存パッケージを再インストールします。
 2. エラーがなくすべて実行されるまで、[Cloudbase-Initサービス動作確認プログラム](#checkcloud-init)に基づいて操作を実行します。

#### 2. デフォルトのPythonインタープリターを変更するとエラーが発生します
- 問題の現象：
起動時にCloud-Initを実行するとエラーが発生する。
- 問題の分析：
Cloud-Initをインストールした時に、PythonインタープリターはデフォルトでPython2を使用します（`/usr/bin/python`と`/bin/python` の2つのソフトはPython2にリンクされています）。ユーザーの業務上の必要に応じて、インスタンス内部でPythonのデフォルトのインタープリターをPython3に変更する可能性があります（`/usr/bin/python` と`/bin/python`の2つのソフトのリンクを変更し、Python3に指向させます）。互換性の問題により、起動時にCloud-Initを実行するとエラーが発生します。
- 対処方法：
 1. `/usr/bin/cloud-init`ファイル内の指定されたPythonインタープリターを修正し、`#/usr/bin/python`または`#/bin/python`を`#! user/bin/python`に修正します。
<dx-alert infotype="notice" title="">
シンボリックリンクを使用せず、直接、特定のインタープリターを指定します。
</dx-alert>
 2. エラーがなくすべて実行されるまで、[Cloudbase-Initサービス動作確認プログラム](#checkcloud-init)に基づいて操作を実行します。

## Cloudbase-Init

### Cloudbase-Initとは何ですか。
Cloud-Initと同様に、Cloudbase-InitはWindows CVMインスタンスと通信するブリッジです。インスタンスが初めて起動した時にCloudbase-Initサービスを実行します。このサービスはインスタンスの初期化設定情報を読み取り、インスタンスに初期化操作を行います。同時にその後のパスワードのリセット、IPの修正などの機能もすべてCloudbase-Initによって実現します。


### Windowsインスタンス内部のCloudbase-Initサービスが正常に動作しているかどうかを確認するにはどうしたらよいですか。


#### Cloudbase-Initサービス動作確認プログラム：[](id:checkcloudbase-init)
1. インスタンスにログインします。
<dx-alert infotype="explain" title="">
パスワードを忘れた場合、またはCloudbase-Initサービスの異常に起因してリセットに失敗した場合は、[ステップ2](#step02)でパスワードをリセットできます。 
</dx-alert>
2. [](id:step02)**コントロールパネル** > **管理ツール** > **サービス**を開きます。
3. cloudbase-initサービスを見つけ、**プロパティ**を右クリックしてcloudbase-initのプロパティウィンドウを開きます。
 - 「起動タイプ」を確認し、下図のように「起動タイプ」が「自動」であることを確認します。
![](https://main.qcloudimg.com/raw/310a278dd2eaf2124d0d52055e0b5b6f.png)
 - 下図に示すように「ログインID」を確認し、「ログインID」が「ローカルシステムのアカウント」であることを確認します。
![](https://main.qcloudimg.com/raw/5a3f623aaf44d55cfe2eaa6aeadb4c12.png)
 - 手動でcloudbase-initサービスを起動し、関連するエラーが発生するかどうかを観察します。
エラーがある場合は、先に解決する必要があります。 cloudbase-initが実行する関連操作をブロックするセキュリティソフトウェアがインストールされているかどうかを確認してください。 
![](https://main.qcloudimg.com/raw/dbbe8f9fc05b07d8011705d9d217b76c.png)
 - 下図に示すように、「登録フォーム」を開いてすべての「LocalScriptsPlugin」を検索し、値が2であることを確認してください。
![](https://main.qcloudimg.com/raw/16106e540d8cf4ef39e5dccb44251350.png)
 - CD-ROMのロードが禁止されているかどうかを確認してください。下図に示すように、光ドライブ装置が見える場合、正常にロードできることを表します。そうでない場合は禁止されているため、禁止を取り消す必要があります。
![](https://main.qcloudimg.com/raw/7707e694b475ba4d70b4d1d52a6c98bb.png)

### Cloudbase-Initの実行ログを確認するにはどうしたらよいですか。
OSに応じて、以下のログファイルで確認できます。
- Linuxシステム：`/var/log/cloud-init-output.log`
- Windowsシステム：`C:\Program Files\Cloudbase Solutions\Cloudbase-Init\log\cloudbase-init.log`

### Cloudbase-Initのよくある問題をどのようにトラブルシューティングすればよいですか。
#### パスワードリセットの初期化に失敗しました
- 考えられる原因：
 - 手動でcloudbase-initアカウントのパスワードを修正するとcloudbase-initサービスの起動に失敗し、それによってパスワードリセットの初期化などの操作に失敗します。
 - cloudbase-initサービスを無効にすると、パスワードリセットの初期化などの操作に失敗します。
 - cloudbase-initサービスがパスワードをリセットする操作をブロックするセキュリティソフトウェアがインストールされている場合、パスワードをリセットするプロセスは成功と返しますが、実際のリセットは失敗しています。
- 対処方法：
考えられる原因に対して、それぞれ以下の3つの点を参考にして操作を行ってください。
 1. cloudbase-initサービスをLocalSystemサービスに変更します。詳細な操作については、[Cloudbase-Initサービス動作確認プログラム](#checkcloudbase-init) の [ステップ2](#step02)をご参照ください。 
 2. cloudbase-initサービスの起動タイプを自動に変更します。 詳細な操作については、[Cloudbase-Initサービス動作確認プログラム](#checkcloudbase-init) の [ステップ2](#step02)をご参照ください。
 3. 対応するセキュリティソフトウェアをアンインストールするか， セキュリティソフトウェア内のcloudbase-initサービスに関連する操作をホワイトリストに追加します。

