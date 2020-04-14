## Cloud-Init

### Cloud-Initは何ですか。
Cloud-Initは一つのオープンソースツールです。CVMインスタンス内で実行される非常駐サービスであり、起動する際に実行され、実行が完了するとすぐに終了し、どちらのポートも監視しません。
Tencent CloudのパブリックLinuxイメージには予めCloud-Initサービスをインストールしてあります。 Cloud-Initサービスは主にCVMインスタンスの初期化操作（たとえば、DNS、Hostname、IP、およびその他の情報の設定）を行い、及びCVMインスタンスの作成時に初めて起動に必要なカスタマイズスクリプトを実行します。従って、Cloud-Initサービスにはrootユーザーとして実行する必要があります。

### どのようにLinuxインスタンス内のCloud-Initサービスが正常に実行されていることを確認しますか。

<span id="checkcloud-init"></span>
#### Cloud-Init サービス実行時のトラブルシューティング方法
まずインスタンスにログインし、以下のコマンドを実行して、エラーが発生したかどうかを確認します。 実行した結果が表示された場合、サービスは正常に実行されています。そうでない場合は、エラーの原因が表示されます。エラーの原因に従ってトラブルシューティングしてください。
1. cloud-init キャッシュのディレクトリを削除します。
```
rm -rf /var/lib/cloud
```
2. 完全なcloud-init初期化を実行します。
```
cloud-init init --local
```
3. 構成されたデータソースに基づいてデータを格納します。
```
cloud-init init
```
4. Cloud-Initの初期化は複数のstageに分かれて、各stageに十分な依存関係を確保するために、cloud-init modulesがconfig stageを指定して実行します。
```
cloud-init modules --mode=config
```
5. cloud-init modulesがconfig stageを指定して実行します。
```
cloud-init modules --mode=final
```

### Cloud-Init はどのようなインスタンス初期化操作を実行しましたか。

Tencent CloudはCloud-Initを通してインスタンスのすべての初期化操作を実行し、インスタンス全体の操作をより透明にします。 以下の内容は操作について簡単に紹介します。詳細については、[Cloud-init 正式ドキュメント](http://cloudinit.readthedocs.io/en/latest/)をご参照ください。

<table>
<tr><th style="width: 25%;">初期化タイプ</th><th style="width: 25%;">デフォルトの動作</th><th style="width: 25%;">禁止方式</th><th style="width: 25%;">注意事項</th></tr>
<tr>
	<td>hostname の初期化</td>
	<td>インスタンスが<b>初期起動</b>する時に、Cloud-Initは <code>vendor_data.json</code> のhostname情報に基づき、インスタンスのhostnameを設定します。</td>
	<td>カスタマイズイメージを使用してインスタンスを作成または再インストールする時に、カスタマイズイメージ内部のhostname名の設定を保持したい場合、カスタマイズイメージを作成する前に<code>/etc/cloud/cloud.cfg</code> 中の<code>- scripts-user</code> 行の設定を削除します。</td>
	<td><code>- scripts-user</code> 行の設定を禁止した場合、インスタンス内部の<code>/var/lib/cloud/instance/scripts/runcmd</code> 初期化スクリプトは実行されず、他のサブプロジェクトの初期化（主に関連するのは、クラウド監視、クラウドセキュリティのインストール、ソフトウェアソース設定）を影響します。 同時に、CVMを作成する時に、カスタマイズスクリプトは実行されません。</td>
</tr>
<tr>
	<td>/etc/hosts の初期化</td>
	<td>インスタンスが<b>初期起動</b>する時に、Cloud-Initは、デフォルトで<code>/etc/hosts</code>を<code>127.0.0.1 $hostname</code>に初期化します。</td>
	<td>カスタマイズイメージを使用してインスタンスを作成または再インストールする時に、カスタマイズイメージ内部の/etc/hosts設定を保持したい場合、カスタマイズイメージを作成する前に、<code>/etc/cloud/cloud.cfg</code>中の<code>- scripts-user</code>行の設定を削除します。</td>
	<td>
		<ul style="margin: 0px;">
			<li> <code>- scripts-user</code>行の設定を禁止にすると、インスタンス内部の<code>/var/lib/cloud/instance/scripts/runcmd</code>初期化スクリプトは実行されず、他のサブプロジェクトの初期化を影響します（主に関連するのは、クラウド監視、クラウドセキュリティのインストール、ソフトウェアソース 設定）。同時に、CVMを作成する時に、カスタマイズスクリプトは実行されません。 </li>
			<li>CVMが再起動する時に、既存の一部マシンの設定<code> / etc / hosts </code>は上書きされます。 解決策については、<a href="https://cloud.tencent.com/document/product/213/34698">Linuxインスタンスのetc hosts設定を有効的に修正する方法</a>をご参照下さい</li>
		</ul>
	</td>
</tr>

<tr>
	<td>DNS の初期化（非 DHCP ケース）</td>
	<td>インスタンスが<b>初期起動</b>する時に、Cloud-Initは<code> vendor_data.json</code>のnameservers情報に基づいてインスタンスのDNSを設定します。</td>
	<td>カスタマイズイメージを使用してインスタンスを作成または再インストールする時に、カスタマイズイメージ内にカスタマイズDNS設定を保持したい場合、カスタマイズイメージを作成する前に<code>/etc/cloud/cloud.cfg</code> 中の<code>- resolv_conf</code>と<code>unverified_modules: ['resolv_conf']</code>の2行の設定を削除します。</td>
	<td>なし。</td>
</tr>

<tr>
	<td>ソフトウェアソースの初期化</td>
	<td>インスタンスが<b>初期起動</b>する時に、Cloud-Initは<code>vendor_data.json</code>のwrite_files情報に基づいてインスタンスのソフトウェアソースを設定します。</td><td>カスタマイズイメージを使用してインスタンスを作成または再インストールする時に、カスタマイズソフトウェアソースの設定をカスタマイズイメージ内部に保持したい場合、カスタマイズイメージを作成する前に<code>/etc/cloud/cloud.cfg</code>中の<code>- write-files</code>行の設定を削除します。 </td>
	<td>なし。</td>
</tr>

<tr>
	<td>NTP の初期化</td>
	<td>インスタンスが<b>初期起動</b>する時に、Cloud-Initは<code>vendor_data.json</code>のNTP Server情報に基づいてインスタンスのNTPサーバー構成を設定し、NTP Serviceを実行します。</td>
	<td>カスタマイズイメージを使用してインスタンスを作成または再インストールする時に、カスタマイズイメージ内部にカスタマイズNTP設定を保持したい場合、カスタマイズイメージを作成する前に、<code>/etc/cloud/cloud.cfg</code>中の<code>- ntp<code/>行の設定を削除できます。 </td>
	<td>なし。</td>
</tr>

<tr>
	<td>パスワードの初期化</td>
	<td>インスタンスが<b>初期起動</b>する時に、Cloud-Initは<code> vendor_data.json</code>中のchpasswd情報に基づいてインスタンスのデフォルトアカウントパスワードを設定します。</td>
	<td>カスタマイズイメージを使用してインスタンスを作成または再インストールする時に、カスタマイズイメージでカスタマイズのデフォルトアカウントとパスワードを保持したい場合、カスタマイズイメージを作成する前に<code>/etc/cloud/cloud.cfg</code>中の<code>- set-passwords</code>行の設定を削除します。</td>
	<td>なし。</td>
</tr>

<tr>
	<td>キーバインディング</td>
	<td>インスタンスが<b>初期起動</b>する時に、Cloud-Initは、<code>vendor_data.json</code>のssh_authorized_keys情報に基づいて、インスタンスのデフォルトアカウントキーを設定します。</td>
	<td>カスタマイズイメージを使用してインスタンスを作成または再インストールする時に、カスタマイズキーをカスタマイズイメージ内に保持したい場合、カスタマイズイメージを作成する前に<code>/etc/cloud/cloud.cfg</code>の中の <code>- users-groups</code>行設定を削除します。</td>
	<td>インスタンス内のキーを手動でバインドしたい場合、コンソールを利用してキーバインティング操作を実行する時に、システムはこのキーを上書きします。</td>
</tr>

<tr>
	<td>ネットワーク初期化（非 DHCP ケース）</td>
	<td>インスタンスが<b>初期起動</b>する時に、Cloud-Initは<code>network_data.json</code>の情報に基づいてインスタンスのIP、GATEWAY、MASKなどを設定します。 </td>
	<td>カスタマイズイメージを使用してインスタンスを作成または再インストールする時に、カスタマイズイメージ内にカスタマイズネットワーク情報を保持したい場合、カスタマイズイメージを作成する前に<code>/etc/cloud/cloud.cfg</code>中の<code>network: {config: disabled}</code>行の設定を追加します。</td>
	<td>なし。</td>
</tr>
</table>

### どのようにCloud-Init関連の問題を特定しますか。 

#### 1. Cloud-Initの依存パッケージのアンインストールが原因でエラーが発生した
- 問題の事象：
コマンドを使用してCloud-Initサービスが正常に実行されていることを確認する時に、以下のエラーが表示されます：
```
Traceback (most recent call last):
  File "/usr/bin/cloud-init", line 5, in 
    ********
    raise DistributionNotFound(req)
pkg_resources.DistributionNotFound: pyyaml
```
- 問題分析：
「pkg_resources.DistributionNotFound: xxxxx 」はCloud-Initのインストール依存パッケージがアンインストールされたことを示します。
- 解決案：
 1. 依存パッケージを再インストールします。
 2. すべての操作が正常に実行されるまで、[Cloud-Init サービス実行時のトラブルシューティング方法](#checkcloud-init)に従って操作を実行します。

#### 2. デフォルトのPythonインタープリターを修正したことによりエラーが発生した
- 問題の事象：
起動時にCloud-Initの実行によりエラーが発生しました。
- 問題分析：
Cloud-Initをインストールする時に、PythonインタープリターはデフォルトでPython2（つまり、`/usr/bin/python`および`/bin/python`はPython2をリンクしている）を使用します。ユーザーのビジネスニーズに応じて、インスタンスの中でPythonのデフォルトインタープリターをPython3（つまり、Python3を指すように`/usr/bin/pythonと`/bin/python`の２リンクを修正する）に変更することができます。互換性の問題のため、起動時にCloud-Initを実行するとエラーが発生しました。
- 解決案：
 1. `/usr/bin/cloud-init`ファイルで指定されたPythonインタープリターを修正し、`#/usr/bin/python`または`#/bin/python`を`#! user/bin/python`に修正します 。
>! ソフトリンクを使用せず、実のインタープリターに直接指定します。
>
 2. すべての操作が正常に実行されるまで、[Cloud-Init サービス実行時のトラブルシューティング方法](#checkcloud-init)に従って操作を実行します。

## Cloudbase-Init

### Cloudbase-Initは何ですか。
Cloud-Initと同様に、Cloudbase-InitはWindowsCVMインスタンスと通信するためのツールです。 インスタンスが始めて起動する時に、Cloudbase-Initサービスが実行され、このサービスはインスタンスの初期化設定情報を読み取り、インスタンスを初期化します。 同時に、後続のパスワードのリセットやIPの変更などの機能もCloudbase-Initを通じて実現されます。

### どのようにWindowsインスタンス内のCloudbase-Initサービスが正常に動作していることを確認しますか。

<span id="checkcloudbase-init"></span>
#### Cloudbase-Init サービス実行時のトラブルシューティング方法：
1. インスタンスにログインします。
>? パスワードを忘れて、またはCloudbase-Initサービスが異常の原因でパスワードのリセットに失敗した場合、[ステップ2](#step02)でパスワードをリセットできます。 
>
2. <span id = "step02">**コントロールパネル** > **管理ツール**> **サービス**を開きます。
3. cloudbase-initサービスを検索し、【プロパティ】を右クリックして、cloudbase-initのプロパティウィンドウを開きます。 </ span>
 -「スタートアップの種類」を確認し、「スタートアップの種類」が「自動」であることを確認します。 

 -「ログイン身分」を確認し、「ログイン身分」が「ローカルシステムアカウント」であることを確認します。 

 - 手動でcloudbase-initサービスを起動し、関連するエラーがあるかどうかを確認します。
エラーがある場合は、まず解決しましょう。cloudbase-initの関連操作の実行をブロックするセキュリティソフトウェアがインストールしているかを確認してください。 

 -「レジストリ」を開き、すべての「LocalScriptsPlugin」を検索し、その値が2であることを確認します。 

 - CD-ROMのロードが禁止になっているかどうかを確認します。 次の図に示すように、光学式ドライブデバイスが表示されている場合は通常のロードを示します。そうでない場合は禁止になっているため、禁止を取り消す必要があります。


### どのようにCloudbase-Init関連の問題を特定しますか。
#### 初期化でパスワードをリセットできませんでした
- 考えられる理由：
 - cloudbase-initアカウントのパスワードを手動で修正することにより、cloudbase-initサービスの起動が失敗になり、初期化やパスワードのリセットなどの操作も失敗になります。
 - cloudbase-initサービスが禁止されたため、初期化やパスワードのリセットなどの操作が失敗します。
 - セキュリティソフトウェアがcloudbase-initサービスのパスワードリセット操作をブロックしたため、パスワードリセット処理は正常に戻りましたが、実際のリセットは失敗しました。
- 解決案：
考えられる理由については、以下の3つのポイントをご参照ください。
 1. cloudbase-initサービスをLocalSystemサービスに変更します。具体的な操作については、[Cloudbase-Init サービス実行時のトラブルシューティング方法](#checkcloudbase-init)の[ステップ2](#step02)をご参照ください。 
 2. cloudbase-initサービスのスタートアップの種類を自動に変更します。 詳細の操作については、[Cloudbase-Init サービス実行時のトラブルシューティング方法](#checkcloudbase-init)の[ステップ 2](#step02)をご参照ください。
 3.対応するセキュリティソフトウェアをアンインストールするか、セキュリティソフトウェアのホワイトリストにcloudbase-initサービスを追加します。
