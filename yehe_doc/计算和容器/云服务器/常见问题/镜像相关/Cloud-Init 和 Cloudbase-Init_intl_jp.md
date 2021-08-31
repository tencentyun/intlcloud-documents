## Cloud-Init

### Cloud-Initとは
Cloud-Initはオープンソースツールであり、CVMインスタンス内で実行する非常駐サービスです。起動時に実行され、実行が完了するとすぐに終了し、ポートはリッスンしません。
Tencent CloudのLinuxパブリックイメージには、Cloud-Initサービスがプリインストールされています。Cloud-Initサービスは主にCVMインスタンスの初期化処理（DNS、Hostname、IPなど情報の設定）を実装し、ユーザーがCVMのインスタンスを作成した時に指定した初回起動時に実行するカスタマイズスクリプトを実行するために使用されるため、rootユーザーとしてCloud-Initサービスを実行する必要があります。

### Linuxインスタンス内のcloud-initサービスが正常に動作しているかどうかを確認するにはどうすればよいですか。

<span id="checkcloud-init"></span>
#### Cloud-Initサービス実行のトラブルシューティング
まず、インスタンスにログインし、次のコマンドを順に実行して、エラーが返されるかどうかを確認します。実行結果が表示されれば、サービスが正常に動作しています。それ以外の場合はエラーの原因が表示されますので、画面の指示従ってトラブルシューティングを行ってください。
1. cloud-initキャッシュディレクトリを削除します。
```
rm -rf/var/lib/cloud
```
2.完全なcloud-init初期化を実行します。
```
cloud-init init --local
```
3.構成されたデータソースからデータを取り出します。
```
cloud-init init
```
4. Cloud-Initの初期化には複数のステージに分かれており、ステージ間の十分な依存関係を確保するために、cloud-initモジュールはconfig stageの実行を指定します。
```
cloud-init modules --mode=config
```
5. cloud-initモジュールは、final stageの実行を指定します。
```
cloud-init modules --mode=final
```

### Cloud-Initがどんなインスタンスの初期化処理を実行したか。

Tencent CloudはCloud-Initを介してインスタンスのすべての初期化操作を実装し、インスタンス全体の操作をより透過的にします。次の内容では、関連操作を簡単に説明します。詳細については、[Cloud-initの公式ドキュメント](http://cloudinit.readthedocs.io/en/latest/)をご参照ください。

<table>
<tr><th style="width: 25%;">初期化タイプ</th><th style="width: 25%;">デフォルトアクション</th><th style="width: 25%;">カスタマイズ</th><th style="width: 25%;">注意事項</th></tr>
<tr>
	<td>hostnameの初期化</td>
	<td>インスタンス<b>の初回起動時</b>に、Cloud-Initは<code> vendor_data.json </code>のホスト名情報に基づいてインスタンスのホスト名を設定します。</td>
	<td>カスタマイズイメージを使用してインスタンスを作成または再インストールする時、イメージのカスタムホスト名の設定を保持したい場合、カスタマイズイメージを作成する前に、<code>/etc/cloud/cloud.cfg</code>から<code>- scripts-user</code>設定を削除できます。
	<td><code>- scripts-user</code> 設定を無効にすると、インスタンス内の<code>/var/lib/cloud/instance/scripts/runcmd</code> 初期化スクリプトは実行されなくなり、他のサブアイテムの初期化（主にクラウド監視、クラウドセキュリティのインストール、およびソフトウェアソースの設定）にも影響します。また、CVMの作成時にカスタマイズスクリプトも実行されません。</td>　
</tr>

<tr>
	<td>/etc/hostsの初期化</td>
	<td>インスタンス<b>の初回起動</b>時に、Cloud-Initはデフォルトで <code>/etc/hosts</code>を<code>127.0.0.1 $hostname</code>に初期化します。</td>
	<td>カスタマイズイメージを使用してインスタンスを作成または再インストールする時、イメージ内のカスタム/etc/hosts設定を保持したい場合、カスタマイズイメージを作成する前に、<code>/etc/cloud/cloud.cfg</code>から<code>- scripts-user</code> と <code>- ['update_etc_hosts', 'once-per-instance']</code>設定を削除できます。</td>
	<td>
		<ul style="margin: 0px;">
			<li> <code>- scripts-user</code> 設定を無効にすると、インスタンス内の<code>/var/lib/cloud/instance/scripts/runcmd</code>初期化スクリプトは実行されなくなり、他のサブアイテムの初期化（主にクラウド監視、クラウドセキュリティのインストール、およびソフトウェアソースの設定）にも影響します。また、CVMの作成時にカスタマイズスクリプトも実行されません。</li>
			<li>CVMが再起動するたびに、一部の既存CVMの<code>/etc/hosts</code>設定が上書きされます。 この問題を解決するには、<a href="https://intl.cloud.tencent.com/document/product/213/32504">Linuxインスタンスのetc hosts設定の変更</a>をご参照ください。</li>
		</ul>
	</td>
</tr>

<tr>
	<td>DNSの初期化（非DHCPシナリオ）</td>
	<td>インスタンス<b>の初回起動時</b>に、 <code>vendor_data.json</code> 中の nameservers情報に基づいてインスタンスのDNSを設定します。</td>
	<td>カスタマイズイメージを使用してインスタンスを作成または再インストールする時、イメージ内のカスタマイズDNS設定を保持したい場合、カスタマイズイメージを作成する前に、<code>/etc/cloud/cloud.cfg</code>から<code>- resolv_conf</code>と<code>unverified_modules: ['resolv_conf']</code>設定を削除できます。</td>
	<td>なし。</td>
</tr>

<tr>
	<td>ソフトウェアソースの初期化</td>
	<td>インスタンス<b>の初回起動時</b>に、<code>vendor_data.json</code> 中のwrite_files情報に基づいてインスタンスのソフトウェアソースを設定します。</td><td>カスタマイズイメージを使用してインスタンスを作成または再インストールする時、イメージのカスタムソフトウェアソース設定を保持したい場合、カスタマイズイメージを作成する前に、<code>/etc/cloud/cloud.cfg</code>から<code>- write-files</code>設定を削除できます。</td>
	<td>なし。</td>
</tr>

<tr>
	<td>NTPの初期化</td>
	<td>インスタンス<b>の初回起動</b>時に、Cloud-Initは<code>vendor_data.json</code> 中のNTP Server情報に基づいてインスタンスのNTPサーバー構成を設定し、NTPサービスを開始します。</td>
	<td>カスタマイズイメージを使用してインスタンスを作成または再インストールする時、イメージのカスタムNTP構成を保持したい場合、カスタマイズイメージを作成する前に、<code>/etc/cloud/cloud.cfg</code>から<code>- ntp<code/>設定を削除できます。</td>
	<td>なし。</td>
</tr>

<tr>
	<td>パスワードの初期化</td>
	<td>インスタンス<b>の初回起動</b>時に、Cloud-Initは<code>vendor_data.json</code> 中のchpasswd情報に基づいてインスタンスのデフォルトのアカウントパスワードを設定します。</td>
	<td>カスタマイズイメージを使用してインスタンスを作成または再インストールする時、イメージのカスタムデフォルトパスワードを保持したい場合、カスタマイズイメージを作成する前に、<code>/etc/cloud/cloud.cfg</code>から<code>- set-passwords</code>設定を削除できます。</td>
	<td>なし。</td>
</tr>

<tr>
	<td>キーバインド</td>
	<td>インスタンス<b>の初回起動</b>時に、Cloud-Init は<code>vendor_data.json</code> 中のssh_authorized_keys情報に基づいて、インスタンスのデフォルトのアカウントキーを設定します。</td>
	<td>カスタマイズイメージを使用してインスタンスを作成または再インストールする時、イメージのカスタムデフォルトキーを保持したい場合。カスタマイズイメージを作成する前に、 <code>/etc/cloud/cloud.cfg</code>から<code>- users-groups</code>設定を削除できます。</td>
	<td>キーをインスタンス内で手動でバインドする場合、コンソールを介してキーバインド操作が実行されると、以前のキーは上書きされます。</td>
</tr>

<tr>
	<td>ネットワークの初期化（非DHCPシナリオ）</td>
	<td>インスタンス<b>の初回起動</b>時に、Cloud-Initは<code> network_data.json </code>の情報に基づいてインスタンスのIP、ゲートウェイ、マスクなどを設定します。</td>
	<td>カスタマイズイメージを使用してインスタンスを作成または再インストールする時、イメージのカスタムネットワーク情報を保持したい場合、カスタマイズイメージを作成する前に、 <code>/etc/cloud/cloud.cfg</code>に<code>network: {config: disabled}</code> 設定を追加できます。</td>
	<td>なし。</td>
</tr>
</table>

### Cloud-Initのよくある問題のトラブルシューティング方法はなんですか。 

#### 1. Cloud-Init依存関係のアンインストールによるエラー
- 問題の説明：
コマンドを使用してCloud-Initサービスが正常に動作しているかどうかを確認する場合、次のエラーが表示されます。
```
Traceback (most recent call last):
  File "/usr/bin/cloud-init", line 5, in 
    ********
    raise DistributionNotFound(req)
pkg_resources.DistributionNotFound: pyyaml
```
- 問題分析：
「pkg_resources.DistributionNotFound: xxxxx 」は、cloud-init依存関係がアンインストールされたことを示します。
- ソリューション ：
 1.依存関係を再インストールします。
 2. [Cloud-Initサービス実行のトラブルシューティング]（＃checkcloud-init）に従って、エラーがなくなるまで操作を実行します。

#### 2.デフォルトのPythonインタープリターの変更によるエラー
- 問題の説明：
起動時にCloud-Initを実行すると、エラーが返されます。
- 問題分析：
Cloud-Initをインストールする時、PythonインタープリターはデフォルトでPython2（すなわち、 シンボリックリンク`/usr/bin/python`および`/bin/python`がPython 2にリンクされます）を使用します。ユーザーのビジネスニーズに応じて、インスタンス内でPythonのデフォルトインタープリターをPython3に変更する場合があります（つまり、`/usr/bin/python`と`/bin/python`の2つのシンボリックリンクを変更して、Python3に指すようにします）。互換性の問題により、起動時にcloud-initを実行するとエラーが返されます。
- ソリューション ：
 1. `/usr/bin/cloud-init` ファイルで指定されたPythonインタープリターを変更し、`#/usr/bin/python`または`#/bin/python`を`#! user/bin/python`に変更します。
>シンボリックリンクを使用しないでください、特定のインタープリターを直接指します。
>
 2. [Cloud-Initサービス実行のトラブルシューティング](#checkcloud-init) に従って、エラーがなくなるまで操作を実行します。

## Cloudbase-Init

### Cloudbase-Initとは
Cloud-Initと同様に、Cloudbase-InitはWindows CVMインスタンスと通信するためのブリッジです。インスタンスの初回起動時に、Cloudbase-Initサービスが実行され、このサービスはインスタンスの初期化構成情報を読み取り、インスタンスを初期化します。また、パスワードのリセットやIPアドレスの変更などの後続の操作もCloudbase-Initを介して行われます。

### Windowsインスタンス内のCloudbase-Initサービスが正常に動作しているかどうかを確認するにはどうすればよいですか。

<span id="checkcloudbase-init"></span>
#### Cloudbase-Initサービス動作のトラブルシューティング：
1.インスタンスにログインします。
>パスワードを忘れた場合、またはCloudbase-Initサービス異常によりパスワードリセットが失敗した場合、[ステップ2](#step02)に従ってパスワードをリセットできます。 
>
2.<span id="step02">**コントロールパネル**> **管理ツール**> **サービス**を開きます。
3. cloudbase-initサービスを見つけて、【プロパティ】を右クリックし、cloudbase-initのプロパティウィンドウを開きます。</span>
 -「スタートアップの種類」を「自動」に変更します。次の図に示すように、
![](https://main.qcloudimg.com/raw/43f39931ec8932f88ee491f2bdbd7ada.png)
 -　サービスを実行するアカウントとして、[ローカルシステムアカウント」が指定されています。次の図に示すように、
![](https://main.qcloudimg.com/raw/5a69afcde36c5bb3259ac1f136f59118.png)
 -cloudbase-initサービスを手動で起動し、エラーが返されるかどうかを確認します。
エラーが発生した場合は、優先的に対処する必要があります。cloudbase-initによる関連操作の実行をブロックするセキュリティソフトウェアがインストールされていないかを確認します。 
![](https://main.qcloudimg.com/raw/97684bd42d3b0d05eee996d0106825e3.png)
 - 以下に示すように、「レジストリ」を開き、すべての「LocalScriptsPlugin」を見つけて、それらの値が「2」であることを確認します。
![](https://main.qcloudimg.com/raw/4f98965fa228c7f948fc8d720424a7ea.png)
 - CD-ROMのロードが無効になっているかどうかを確認します。次の図に示すように、光ディスクドライブがある場合は、正常にロードされたことを示しています。それ以外の場合は無効になっており、有効にする必要があります。
![](https://main.qcloudimg.com/raw/0e8c68537e238fe7a1e4b718848b9e98.png)

### Cloudbase-Initによくある問題のトラブルシューティング方法はなんですか。
#### 初期化中にパスワードをリセットできません
- 考えられる理由：
 - Cloudbase-Initアカウントのパスワードが手動で変更されると、cloudbase-initサービスの起動が失敗して、初期化中にパスワードをリセットするなどの操作が失敗しました。
 - cloudbase-initサービスが無効化されたため、初期化中にパスワードをリセットするなどの操作が失敗しました。
 - セキュリティソフトウェアがインストールされているため、cloudbase-initサービスのパスワードリセット操作がブロックされて、パスワードリセットプロセスから成功した結果が戻りましたが、実際はリセットに失敗しました。
- ソリューション：
考えられる理由ごとに対応する解決策に従って、問題を修正してください。
 1. cloudbase-initサービスをLocalSystemサービスに変更します。操作方法の詳細については、[Cloudbase-Initサービス実行のトラブルシューティング](#checkcloudbase-init) の[Step2](#step02)をご参照ください。 
 2. cloudbase-initサービスの起動タイプを自動に変更します。操作方法の詳細については、[Cloudbase-Initサービス実行のトラブルシューティング](#checkcloudbase-init) の[Step2](#step02)をご参照ください。
 3.関連するセキュリティソフトウェアをアンインストールするか、Cloudbase-Initサービス関連の操作をセキュリティソフトウェアのホワイトリストに追加します。
