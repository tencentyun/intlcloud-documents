## Cloud-Init

### Cloud-Initとは
Cloud-InitはCVMインスタンス内で非常駐サービスとして実行されるオープンソースツールです。起動時に実行され、実行が完了するとすぐに終了し、どちらのポートも監視しません。
Tencent CloudのLinuxパブリックイメージには、cloud-initサービスでプリインストールされています。 Cloud-Initサービスは主にCVMインスタンスの初期化操作（たとえば、DNS、Hostname、IP、およびその他の情報の設定）を行い、及びCVMインスタンスの作成時に初めて起動に指定するカスタムスクリプトの実行に使用されるため、従って、Cloud-Initサービスにはrootユーザーとして実行する必要があります。

### どのようにLinuxインスタンス内のCloud-Initサービスが正常に実行されていることを確認しますか。

<span id="checkcloud-init"></span>
#### cloud-initの動作確認
まずインスタンスにログインし、以下のコマンドを実行して、エラーが発生したかどうかを確認します。実行結果が返ってきた場合は、サービスが正常に動作しています。そうでない場合は、エラーの原因が表示されます。エラーの原因に従ってトラブルシューティングを行ってください。
1. cloud-init キャッシュディレクトリを削除します。
```
rm -rf /var/lib/cloud
```
2. 完全なcloud-init初期化を実行します。
```
cloud-init init --local
```
3. 構成されたデータソースからデータをプルします。
```
cloud-init init
```
4. Cloud-Initの初期化には複数のステージがあります。ステージ間の十分な依存関係を確保するために、cloud-init モジュールがconfig stageを指定して実行します。
```
cloud-init modules --mode=config
```
5. cloud-init modulesがconfig stageを指定して実行します。
```
cloud-init modules --mode=final
```

### Cloud-Init はどのようなインスタンス初期化操作を実行しましたか。

Tencent Cloudはcloud-initを介してインスタンスのすべての初期化操作を実行し、インスタンス全体の操作をより透過的にします。 以下の内容は初期化操作について簡単に紹介します。詳細については、[Cloud-init 公式ドキュメント](http://cloudinit.readthedocs.io/en/latest/)をご参照ください。

<table>
<tr><th style="width: 25%;">初期化タイプ</th><th style="width: 25%;">デフォルトの動作</th><th style="width: 25%;">禁止方式</th><th style="width: 25%;">注意事項</th></tr>
<tr>
	<td>hostname の初期化</td>
	<td>インスタンスの<b>初回起動時</b>に、Cloud-Initは <code>vendor_data.json</code> のhostname情報に基づき、インスタンスのhostnameを設定します。</td>
	<td>カスタムイメージを使用してインスタンスを作成または再インストールする時に、カスタムイメージ内部のカスタムホスト名を保持したい場合は、カスタムイメージを作成する前に<code>/etc/cloud/cloud.cfg</code>から<code>- scripts-user</code> 設定を削除します。</td>
	<td><code>- scripts-user</code> 設定を無効にすると、インスタンス内部の<code>/var/lib/cloud/instance/scripts/runcmd</code> 初期化スクリプトは実行されず、他のサブプロジェクトの初期化（主に関連するのは、クラウド監視、クラウドセキュリティのインストール、ソフトウェアソース設定）を影響します。 同時に、CVMを作成する時に、カスタマイズスクリプトは実行されません。</td>
</tr>
<tr>
	<td>/etc/hosts の初期化</td>
	<td>インスタンス<b>初回起動時</b>に、Cloud-Initは、デフォルトで<code>/etc/hosts</code>を<code>127.0.0.1 $hostname</code>に初期化します。</td>
	<td>カスタムイメージを使用してインスタンスを作成または再インストールする時に、カスタムイメージ内部の/etc/hosts設定を保持したい場合、カスタムイメージを作成する前に、<code>/etc/cloud/cloud.cfg</code>から<code>- scripts-user</code>設定を削除します。</td>
	<td>
		<ul style="margin: 0px;">
			<li> <code>- scripts-user</code>行の設定を無効にすると、インスタンス内部の<code>/var/lib/cloud/instance/scripts/runcmd</code>初期化スクリプトは実行されず、他のサブプロジェクトの初期化（主に関連するのは、クラウド監視、クラウドセキュリティのインストール、ソフトウェアソース設定）を影響します。同時に、CVMを作成する時に、カスタマイズスクリプトは実行されません。 </li>
			<li>CVMが再起動するたびに、一部の既存のCVMの設定<code> / etc / hosts </code>が上書きされます。 この問題を解決するには、<a href="https://cloud.tencent.com/document/product/213/34698">Linuxインスタンスのetc hosts設定の変更</a>をご参照ください</li>
		</ul>
	</td>
</tr>

<tr>
	<td>DNSの初期化（非 DHCPシナリオ）</td>
	<td>インスタンスの<b>初回起動時</b>に、Cloud-Initは<code> vendor_data.json</code>のnameservers情報に基づいてインスタンスのDNSを設定します。</td>
	<td>カスタムイメージを使用してインスタンスを作成または再インストールする時に、カスタムイメージ内にカスタムDNS設定を保持したい場合、カスタムイメージを作成する前に<code>/etc/cloud/cloud.cfg</code>から<code>- resolv_conf</code>と<code>unverified_modules: ['resolv_conf']</code>の2行の設定を削除します。</td>
	<td>なし。</td>
</tr>

<tr>
	<td>ソフトウェアソースの初期化</td>
	<td>インスタンスの<b>初回起動時</b>に、Cloud-Initは<code>vendor_data.json</code>のwrite_files情報に基づいてインスタンスのソフトウェアソースを設定します。</td><td>カスタムイメージを使用してインスタンスを作成または再インストールする時に、カスタムイメージのカスタムDNS設定を保持したい場合は、カスタムイメージを作成する前に<code>/etc/cloud/cloud.cfg</code>から<code>- write-files</code>設定を削除します。 </td>
	<td>なし。</td>
</tr>

<tr>
	<td>NTP の初期化</td>
	<td>インスタンスの<b>初回起動時</b>に、Cloud-Initは<code>vendor_data.json</code>のNTP Server情報に基づいてインスタンスのNTPサーバー構成を設定し、NTP Serviceを実行します。</td>
	<td>カスタムイメージを使用してインスタンスを作成または再インストールする時に、カスタムイメージのカスタムNTP設定を保持したい場合は、カスタムイメージを作成する前に、<code>/etc/cloud/cloud.cfg</code>から<code>- ntp<code/>設定を削除します。 </td>
	<td>なし。</td>
</tr>

<tr>
	<td>パスワードの初期化</td>
	<td>インスタンスの<b>初回起動時</b>に、Cloud-Initは<code> vendor_data.json</code>中のchpasswd情報に基づいてインスタンスのデフォルトアカウントパスワードを設定します。</td>
	<td>カスタムイメージを使用してインスタンスを作成または再インストールする時に、カスタムイメージのカスタマイズのデフォルトアカウントとパスワードを保持したい場合、カスタムイメージを作成する前に<code>/etc/cloud/cloud.cfg</code>から<code>- set-passwords</code>設定を削除します。</td>
	<td>なし。</td>
</tr>

<tr>
	<td>キーバインド</td>
	<td>インスタンスの<b>初回起動時</b>に、Cloud-Initは、<code>vendor_data.json</code>のssh_authorized_keys情報に基づいて、インスタンスのデフォルトアカウントキーを設定します。</td>
	<td>カスタムイメージを使用してインスタンスを作成または再インストールする時に、カスタムイメージのカスタムキーを保持したい場合は、カスタムイメージを作成する前に<code>/etc/cloud/cloud.cfg</code>から <code>- users-groups</code>設定を削除します。</td>
	<td>インスタンス内のキーを手動でバインドした場合、コンソールを介してキーバインド操作を実行する時に、以前のキーは上書きされます。</td>
</tr>

<tr>
	<td>ネットワーク初期化（非 DHCP シナリオ）</td>
	<td>インスタンスの<b>初回起動時</b>に、Cloud-Initは<code>network_data.json</code>の情報に基づいてインスタンスのIP、ゲートウェイ、マスクなどを設定します。 </td>
	<td>カスタムイメージを使用してインスタンスを作成または再インストールする時に、カスタムイメージのカスタムネットワーク情報をを保持したい場合、カスタムイメージを作成する前に<code>network: {config: disabled}</code>を <code>/etc/cloud/cloud.cfg</code> に追加します。</td>
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
- ソリューション：
 1. `/usr/bin/cloud-init`ファイルで指定されたPythonインタープリターを変更し、`#/usr/bin/python`または`#/bin/python`を`#! user/bin/python`に変更します 。
>! シンボリックリンクを使用せず、 特定のインタープリターに直接指します。
>
 2. すべての操作が正常に実行されるまで、[Cloud-Init サービス実行時のトラブルシューティング](#checkcloud-init)に従って操作を実行します。

## Cloudbase-Init

### Cloudbase-Initとは
Cloud-Initと同様に、Cloudbase-InitはWindowsCVMインスタンスと通信するためのツールです。 Cloudbase-Initサービスは、インスタンスの初回起動時に実行されます。このサービスはインスタンスの初期化設定情報を読み取り、インスタンスを初期化します。 同時に、後続のパスワードのリセットやIPの変更などの機能もCloudbase-Initを介して行われます。

### どのようにWindowsインスタンス内のCloudbase-Initサービスが正常に動作していることを確認しますか。

<span id="checkcloudbase-init"></span>
#### Cloudbase-Init サービス実行時のトラブルシューティング：
1. インスタンスにログインします。
>? パスワードを忘れて、またはCloudbase-Initサービスが異常の原因でパスワードのリセットに失敗した場合、[ステップ2](#step02)でパスワードをリセットできます。 
>
2. <span id = "step02">**コントロールパネル** > **管理ツール**> **サービス**を開きます。
3. cloudbase-initサービスを見つけて、【プロパティ】を右クリックして、cloudbase-initのプロパティウィンドウを開きます。 </ span>
 -「スタートアップの種類」を確認し、「スタートアップの種類」が「自動」に設定されていることを確認します。 以下に示すように：
![](https://main.qcloudimg.com/raw/43f39931ec8932f88ee491f2bdbd7ada.png)
 -「ログインID」を確認し、「ログインID」が「ローカルシステムアカウント」であることを確認します。 以下に示すように：
![](https://main.qcloudimg.com/raw/5a69afcde36c5bb3259ac1f136f59118.png)
 - 手動でcloudbase-initサービスを起動し、エラーが返されるかどうかを確認します。
エラーが返された場合は、まず問題を修正してください。cloudbase-initの関連する操作の実行をブロックするセキュリティソフトウェアがインストールしているかどうかを確認する必要があります。 
![](https://main.qcloudimg.com/raw/97684bd42d3b0d05eee996d0106825e3.png)
 -「レジストリ」を開き、すべての「LocalScriptsPlugin」を見つけ、その値が2であることを確認します。 以下に示すように：
![](https://main.qcloudimg.com/raw/4f98965fa228c7f948fc8d720424a7ea.png)
 - CD-ROMのロードが禁止になっているかどうかを確認します。 次の図に示すように、光ディスクドライブが表示されている場合は、ロードが禁止になっていないことを意味します。そうでない場合は禁止になっているため、禁止を取り消す必要があります。
![](https://main.qcloudimg.com/raw/0e8c68537e238fe7a1e4b718848b9e98.png)

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
