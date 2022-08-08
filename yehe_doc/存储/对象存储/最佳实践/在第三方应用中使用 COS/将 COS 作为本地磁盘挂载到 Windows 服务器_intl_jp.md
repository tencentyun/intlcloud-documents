## 操作シナリオ
現在、Windowsシステム上でTencentのCloud Object Storage(COS)を操作するための主なメソッドとしては、API、COSBrowser、COSCMDツールがあります。

Windowsサーバーを好んで使用するユーザーにとっては、COSBrowserツールはほとんどの場合、クラウドストレージとしてしか使えないため、サーバー上でプログラムを直接使用したり、操作したりするには適していません。ここでは、ストレージ料金が安価なCOSをWindowsサーバーにマウントすることで、ローカルディスクにマッピングする方法についてご説明します。

>? このプラクティス事例は、Windows 7/Windows Server 2012以上のバージョンのOSに適しています。
>

## 操作手順
### ダウンロードとインストール

以下のインストール方法が提供されており、ご自分が使用するシステムに応じて選択できます。
- [Github](https://github.com/billziss-gh/winfsp/releases)に移動してWinfspをダウンロードします。
ダウンロードが完了すると、手順に沿ってデフォルトでインストールされます。
- [Git公式サイト](https://gitforwindows.org/)または[Github](https://github.com/git-for-windows/git/releases/)に移動してGitツールをダウンロードします。
このプラクティス事例でダウンロードされるバージョンはGit-2.31.1-64-bit.exeです。ダウンロードが完了すると、手順に沿ってデフォルトでインストールされます。
- [Rclone公式サイト](https://rclone.org/downloads/)または[Github](https://github.com/rclone/rclone/releases)に移動してRcloneツールをダウンロードします。
このプラクティス事例でダウンロードされるバージョンはrclone-v1.55.0-windows-amd64.zipです。ソフトウェアのインストールは必要ありません。ダウンロード後、任意の英語ディレクトリに解凍する必要があります（解凍したパスに中国語が含まれているとエラーとなる場合があります）。このプラクティス事例のパスの例は、E:\AutoRcloneです。

>? Githubのダウンロード速度が遅かったり、開かなかったりすることがありますので、他の公式チャネルからご自分でダウンロードすることもできます。
>

### Rcloneの設定

>!以下の設定手順はRclone v1.55.0バージョンを例としています。その他のバージョンでは設定手順に若干の違いがあるため、適宜調整してください。


1. 任意のフォルダを開き、左側のナビゲーションディレクトリから**このPC**を見つけ、右クリックして**プロパティ > システムの詳細設定 > 環境変数 > システム変数 > Path**を選択し、**新規作成**をクリックします。
2. ポップアップウィンドウに、Rcloneが解凍された後のパス(E:\AutoRclone)を入力し、**OK**をクリックします。
3. Windows Powershellを開き、`rclone --version`コマンドを入力して**Enter**を押し、Rcloneが正しくインストールされているか確認します。
4. Rcloneが正しくインストールされたことを確認したら、Windows Powershellでコマンド`rclone config`を入力して**Enter**を押します。
5. Windows Powershellに**n**と入力して**Enter**を押し、New remoteを新規作成します。
6. Windows Powershellにディスクの名前（例：myCOS）を入力し、**Enter**を押します。
7. 表示されたオプションの中から、Tencent Cloudを含むオプションを選択し、**4**と入力して**Enter**を押します。
8. 表示されたオプションの中から、Tencent Cloud COSを含むオプションを選択し、**11**と入力して**Enter**を押します。
9. `env_auth>`まで実行したら、Enterを押します。
10. `access_key_id>`まで実行したら、Tencent Cloud COSのアクセスキーSecretIdを入力し、**Enter**を押します。
>? ここではサブアカウント権限を使用することをお勧めします。[APIキー管理](https://console.cloud.tencent.com/cam/capi)に移動すると、ご自分のSecretIdとSecretKeyを確認できます。
>
11. `secret_access_key>`まで実行したら、Tencent Cloud COSのアクセスキーSecretKeyを入力し、**Enter**を押します。
12. 表示されたTencent Cloudの各リージョンのゲートウェイアドレスをもとに、バケットが属するリージョンを確認し、対応するリージョンを選択します。
このプラクティスでは広州を例として、`cos.ap-guangzhou.myqcloud.com`を選択し、**4**と入力して**Enter**を押します。
13. 表示されたTencent Cloud COSの権限タイプから、実際のニーズに応じてprivateかpublic-readを選択します。ここで選択した権限タイプはオブジェクト権限タイプで、新しくアップロードされたファイルに対してのみ有効です。このプラクティスではpublic-readを例として、**2**と入力して**Enter**を押します。
14. 表示されたTencent Cloud COSのストレージタイプから、実際のニーズに応じてCOSにファイルをアップロードするストレージタイプを選択できます。このプラクティスではDefaultを例として、**1***と入力して***Enter**を押します。
 - Defaultとはデフォルトを意味します
 - Standard storage classとは標準ストレージ(STANDARD)を意味します
 - Infrequent access storage modeとは低頻度ストレージ(Standard_IA)を意味します
 - Archive storage modeとはアーカイブストレージ(ARCHIVE)を意味します
>?INTELLIGENT_TIERINGストレージまたはディープアーカイブストレージを設定するには、**設定ファイルの変更**というメソッドにより、設定ファイルのstorage_classの値をINTELLIGENT_TIERINGまたはDEEP_ARCHIVEに設定すれば完了です。
>
15. `Edit advanced config? (y/n)`まで実行したら、**Enter**を押します。
16. 情報が正しいことを確認したら、**Enter**を押します。
17. **q**と入力し、設定を完了します。


### 設定ファイルの変更

上記の手順が完了すると、`C:\Users\ユーザー名\.config\rclone`というファイルに、rclone.confという名前のファイルが表示されます。このファイルは、rcloneの設定ファイルです。rcloneの設定を変更したい場合は、これを直接変更することができます。


### COSをローカルディスクとしてマウント

1. インストールしたGit CMDを開き、コマンドラインツールに実行コマンドを入力します。ここでは2つのユースケース（いずれか一方）が提供されていますので、実際のニーズに応じていずれかを選択できます。
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
		<li>E:\tempはローカルキャッシュディレクトリで、ご自分で設定できます。</li>
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

## 関連操作

また、サードパーティの商用有償ツールを使用することで、COSをWindowsサーバーにマウントし、ローカルディスクとしてマッピングすることもできます。次の操作では、TntDriveツールを例として取り上げます。
1. TntDriveをダウンロードし、インストールします。
2. TntDriveを開き、**Account > Add New Account**をクリックしてユーザーアカウントを作成します。
![](https://main.qcloudimg.com/raw/90b4a262b11b6933f48b4922cad4fdc4.png)
主なパラメータの情報は次のとおりです。
 - Account Name：カスタムアカウント名です。
 - Account Type：COSはS3互換であるため、ここで**Amazon S3 Compatible Storage**を選択できます。
 - REST Endpoint：バケットのあるリージョンを入力します。例えば、バケットが広州にある場合は、cos.ap-guangzhou.myqcloud.comと入力します。
 - Access Key ID：SecretIdを入力します。[APIキー管理](https://console.cloud.tencent.com/capi)ページで作成し、取得することができます。
 - Secret Access Key：SecretKeyを入力します。
3. **Add new account**をクリックします。
4. TntDriveインターフェースで、**Add New Mapped Drives**をクリックし、Mapped Drivesを作成します。
![](https://main.qcloudimg.com/raw/fa09500f96ba8e5c8144d39cd5471991.png)
主なパラメータの情報は次のとおりです。
 - Amazon S3 Bucket：バケットのパスを入力するか、またはバケット名を選択します。右側のボタンをクリックすると、バケットを選択できます。これは、ステップ2で設定した広州リージョンにあるバケットを示しています（バケットはディスクに独立してマッピングされます）。
 - Mapped drives letter：ディスクのボリュームラベル名を設定します。ローカルのC、D、Eドライブなどと重複しないようにしてください。
5. 以上の情報を確認し、**Add new drive**をクリックします。
6. このディスクは、ローカルコンピュータの**マイコンピュータ**にあります。すべてのバケットをWindowsサーバーにマッピングしたい場合は、以上の手順を繰り返してください。



