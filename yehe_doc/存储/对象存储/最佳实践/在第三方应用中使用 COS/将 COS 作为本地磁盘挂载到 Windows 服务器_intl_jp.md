## ユースケース
現在、Windowsシステム上でTencentのCloud Object Storage(COS)を操作するための主なメソッドとしては、API、COSBrowser、COSCMDツールがあります。

Windowsサーバーを好んで使用するユーザーにとっては、COSBrowserツールはほとんどの場合、クラウドストレージとしてしか使えないため、サーバー上でプログラムを直接使用したり、操作したりするには適していません。ここでは、ストレージ料金が安価なCOSをWindowsサーバーにマウントすることで、ローカルディスクにマッピングする方法についてご説明します。

>? このプラクティス事例はWindows 7 / Windows Server 2012 / 2016 / 2019 / 2022システムに適合します。
>

## 操作手順
### ダウンロードとインストール

このプラクティス事例では次の3種類のソフトウェアを使用します。お使いのシステムに適したソフトウェアバージョンを選択してインストールすることができます。
1. [Github](https://github.com/billziss-gh/winfsp/releases)に移動してWinfspをダウンロードします。
このプラクティス事例でダウンロードするバージョンはwinfsp-1.12.22301です。ダウンロードが完了すると、手順に沿ってデフォルトでインストールされます。
>?Windows Server 2012 R2はWinfsp 1.12.22242バージョンには適合せず、Winfsp 1.11.22176バージョンに適合します。
2. [Git公式サイト](https://gitforwindows.org/)または[Github](https://github.com/git-for-windows/git/releases/)に移動してGitツールをダウンロードします。
このプラクティス事例でダウンロードするバージョンはGit-2.38.1-64-bitです。ダウンロードが完了すると、手順に沿ってデフォルトでインストールされます。
3. [Rclone公式サイト](https://rclone.org/downloads/)または[Github](https://github.com/rclone/rclone/releases)に移動してRcloneツールをダウンロードします。
このプラクティス事例でダウンロードするバージョンはrclone-v1.60.1-windows-amd64です。このソフトウェアはインストールの必要がなく、ダウンロード後、任意の英語ディレクトリに解凍するだけで完了します（解凍したパスに中国語が含まれているとエラーとなる場合があります）。このプラクティス事例のパスの例は、E:\AutoRcloneです。

>? Githubのダウンロード速度が遅かったり、開かなかったりすることがありますので、他の公式チャネルからご自分でダウンロードすることもできます。
>

### Rcloneの設定

>!以下の設定手順はrclone-v1.60.1-windows-amd64バージョンを例としています。その他のバージョンでは設定手順に若干の違いがあるため、適宜調整してください。


1. 任意のフォルダを開き、左側のナビゲーションディレクトリから**このPC**を見つけ、右クリックして**プロパティ > システムの詳細設定 > 環境変数 > システム変数 > Path**を選択し、**新規作成**をクリックします。
2. ポップアップウィンドウに、Rcloneが解凍された後のパス(E:\AutoRclone)を入力し、**OK**をクリックします。
3. Windows Powershellを開き、`rclone --version`コマンドを入力して**Enter**を押し、Rcloneが正しくインストールされているか確認します。
4. Rcloneが正しくインストールされたことを確認したら、Windows Powershellでコマンド`rclone config`を入力して**Enter**を押します。
5. Windows Powershellに**n**と入力して**Enter**を押し、New remoteを新規作成します。
6. Windows Powershellにディスクの名前（例：myCOS）を入力し、**Enter**を押します。
7. 表示されたオプションの中から、“Tencent COS”を含むオプションを選択、すなわち**5**を入力して**Enter**を押します。
![](https://qcloudimg.tencent-cloud.cn/raw/edd4b224879b2c854c9a32167d3f2aaa.png)
8. 表示されたオプションの中から、“TencentCOS”を含むオプションを選択し、**21**を入力して**Enter**を押します。
![](https://qcloudimg.tencent-cloud.cn/raw/c7ada8335827fff90078628f05927141.png)
9. `env_auth>`まで実行したら、Enterを押します。
10. `access_key_id>`まで実行したら、Tencent Cloud COSのアクセスキーSecretIdを入力し、**Enter**を押します。
>? ここではサブアカウント権限を使用することをお勧めします。[APIキー管理](https://console.cloud.tencent.com/cam/capi)に移動すると、ご自分のSecretIdとSecretKeyを確認できます。
>
11. `secret_access_key>`まで実行したら、Tencent Cloud COSのアクセスキーSecretKeyを入力し、**Enter**を押します。
12. 表示されたTencent Cloudの各リージョンのゲートウェイアドレスをもとに、バケットが属するリージョンを確認し、対応するリージョンを選択します。
このプラクティスでは広州を例として、`cos.ap-guangzhou.myqcloud.com`を選択し、**4**と入力して**Enter**を押します。
13. 表示されたTencent Cloud COSの権限タイプから、実際のニーズに応じてdefault、public-readなどを選択します。ここで選択した権限タイプはオブジェクト権限タイプで、新しくアップロードされたファイルに対してのみ有効です。このプラクティスではdefaultを例として、**1**を入力し、**Enter**を押します。
![](https://qcloudimg.tencent-cloud.cn/raw/7756d7599713939368c6bb42cd075d07.png)
15. 表示されたTencent Cloud COSのストレージタイプから、実際のニーズに応じてCOSにファイルをアップロードするストレージタイプを選択できます。このプラクティスではDefaultを例として、**1***と入力して***Enter**を押します。
![](https://qcloudimg.tencent-cloud.cn/raw/48e7f6c7d65d13d9fdde690e819bad6c.png)
 - Defaultとはデフォルトを意味します
 - Standard storage classとは標準ストレージ(STANDARD)を意味します
 - Archive storage modeとはアーカイブストレージ(ARCHIVE)を意味します
 - Infrequent access storage modeとは低頻度ストレージ（STANDARD_IA）を意味します
>?INTELLIGENT_TIERINGストレージまたはディープアーカイブストレージを設定したい場合は**設定ファイルを変更する**方法を使用し、設定ファイルのstorage_classの値をINTELLIGENT_TIERINGまたはDEEP_ARCHIVEに設定します。ストレージタイプに関するその他の説明については、[ストレージタイプの概要](https://intl.cloud.tencent.com/document/product/436/30925)をご参照ください。
>
15. `Edit advanced config? (y/n)`まで実行したら、**Enter**を押します。
16. 情報が正しいことを確認したら、**Enter**を押します。
17. **q**と入力し、設定を完了します。
![](https://qcloudimg.tencent-cloud.cn/raw/9cd97c7d75b1b9cfd42a244c03d00fff.png)

### 構成ファイルの変更

上記の手順が完了すると、rclone.confという名前の設定ファイルが生成されます。通常は`C:\Users\ユーザー名\AppData\Roaming\rclone`フォルダ内にあります。rcloneの設定を変更したい場合はこれを直接変更できます。この設定ファイルが見つからない場合は、コマンドウィンドウで`rclone config file`コマンドを実行し、この設定ファイルを照会することができます。


### COSをローカルディスクとしてマウント

1. インストールしたGit Bashを開き、実行コマンドを入力します。ここでは2つのユースケース（二択）が提供されていますので、実際のニーズに応じていずれかを選択できます。
<ul>
<li>LAN共有ドライブとしてマッピングされている場合（推奨）、以下のようにコマンドを実行します。
<pre>
<code class="language-plaintext">rclone mount myCOS:/ Y: --fuse-flag --VolumePrefix=\server\share --cache-dir E:\temp --vfs-cache-mode writes &amp;</code>
</pre>
</li>
<li>ローカルディスクにマッピングされている場合、以下のようにコマンドを実行します。
<pre>
<code class="language-plaintext">rclone mount myCOS:/ Y: --cache-dir E:\temp --vfs-cache-mode writes &</code>
</pre>
	<ul>
		<li>myCOS：ユーザー定義のディスク名に置き換えます。</li>
		<li>Y：マウントしたいハードディスクのボリュームラベル名に置き換えてください。ローカルのC、D、Eドライブなどと重複しないようにしてください。</li>
		<li>E:\tempはローカルキャッシュディレクトリで、ご自分で設定できます。注意：ユーザーがディレクトリの権限を持つことを確実にする必要があります。</li>
	</ul>
</li>
</ul>
「The service rclone has been started」と表示されたらマウント成功です。
2. **exit**と入力し、ターミナルからログアウトします。
3. ローカルコンピュータの**マイコンピュータ**にmyCOS(Y:)という名前のディスクがあります。
ディスクを開くと、広州の全リージョンを含むすべてのバケット名が表示されます。この時点で、アップロード、ダウンロード、作成、削除など、ローカルディスクの通常操作を行うことができます。
>!
> - 操作中にエラーが発生した場合は、git bashソフトウェアでエラーメッセージの詳細情報を確認してください。
> - マウントされているディスクでバケットに対して削除操作を行うと、バケット内にファイルが存在するかどうかに関わらず削除されますので、慎重に操作してください。
> - マウントされているディスクのバケット名を変更すると、COSバケット名も変更されますので、慎重に操作してください。
> 


### 起動したらハードディスクを自動的にマウントするように設定

上記のようにコンピュータを再起動するとマッピングされたディスクは消失してしまうため、再度手動で操作する必要があります。そこで、自動起動装置を設定して、サーバーを再起動するたびに自動的にディスクがマウントされるようにします。

1. RcloneインストールディレクトリE:\AutoRcloneに、それぞれstartup_rclone.vbsとstartup_rclone.batファイルを作成します。
>?Powershellでテキストファイルを作成する際はエンコードに注意する必要があります。そうしなければ、生成した.bat、 .vbsなどのテキストファイルが実行できなくなります。
2. startup_rclone.batに、以下のマウントコマンドを記述します。
 - LAN共有ドライブとしてマッピングされている場合、以下のコマンドを入力します。
```plaintext
rclone mount myCOS:/ Y: --fuse-flag --VolumePrefix=\server\share --cache-dir E:\temp --vfs-cache-mode writes &
```
 - ローカルディスクにマッピングされている場合、以下のコマンドを入力します。
```
rclone mount myCOS:/ Y: --cache-dir E:\temp --vfs-cache-mode writes &
```
3. startup_rclone.vbsに、以下のコードを記述します。
```plaintext
CreateObject("WScript.Shell").Run "cmd /c E:\AutoRclone\startup_rclone.bat",0
```
>! コード内のパスを実際のパスに変更してください。
>
4. startup_rclone.vbsファイルを %USERPROFILE%\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startupフォルダにカットします。
5. サーバーを再起動します。
>?自動マウント設定後にサーバーを再起動します。通常はマウントが成功したことを確認できるまでに十数秒かかります。



## 関連する操作

また、サードパーティの商用有償ツールを使用することで、COSをWindowsサーバーにマウントし、ローカルディスクとしてマッピングすることもできます。次の操作では、TntDriveツールを例として取り上げます。
1. TntDriveをダウンロードし、インストールします。
2. TntDriveを開き、**Account > Add New Account**をクリックしてユーザーアカウントを作成します。
![](https://main.qcloudimg.com/raw/90b4a262b11b6933f48b4922cad4fdc4.png)
主なパラメータ情報は下記の通りです：
 - Account Name：カスタムアカウント名です。
 - Account Type：COSはS3互換であるため、ここで**Amazon S3 Compatible Storage**を選択できます。
 - REST Endpoint：バケットのあるリージョンを入力します。例えば、バケットが広州にある場合は、cos.ap-guangzhou.myqcloud.comと入力します。
 - Access Key ID：SecretIdを入力します。[APIキー管理](https://console.cloud.tencent.com/capi)ページで作成し、取得することができます。
 - Secret Access Key：SecretKeyを入力します。
3. **Add new account**をクリックします。
4. TntDriveインターフェースで、**Add New Mapped Drives**をクリックし、Mapped Drivesを作成します。
![](https://main.qcloudimg.com/raw/fa09500f96ba8e5c8144d39cd5471991.png)
主なパラメータ情報は下記の通りです：
 - Amazon S3 Bucket：バケットのパスを入力するか、またはバケット名を選択します。右側のボタンをクリックすると、バケットを選択できます。これは、ステップ2で設定した広州リージョンにあるバケットを示しています（バケットはディスクに独立してマッピングされます）。
 - Mapped drives letter：ディスクのボリュームラベル名を設定します。ローカルのC、D、Eドライブなどと重複しないようにしてください。
5. 以上の情報を確認し、**Add new drive**をクリックします。
6. このディスクは、ローカルコンピュータの**マイコンピュータ**にあります。すべてのバケットをWindowsサーバーにマッピングしたい場合は、以上の手順を繰り返してください。




