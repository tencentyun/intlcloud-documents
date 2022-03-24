## 概要

ここでは、オンラインマイグレーション機能を使用して、ソースサーバー上のシステム、アプリケーションプログラムなどを自分で作成したコンピュータルーム（IDC）やクラウドプラットフォームなどのソース環境から指定のTencent Cloud CVMに移行する操作手順についてご紹介します。

ドキュメントには**コンソールによる移行**と**ツールによる移行**の2種類の方式が含まれます。ドキュメントの手順を参照して移行元サーバーをTencent Cloud CVMに移行することができます。


<dx-alert infotype="explain" title="">
ソースサーバーの形式は物理サーバー、仮想マシンまたはその他のクラウドプラットフォームCVMとすることができます。その他のクラウドプラットフォームには、AWS、Google Cloud Platform、VMware、Alibaba Cloud、Huawei Cloudなどの仮想マシンプラットフォームが含まれますが、これらに限りません。
</dx-alert>


## 操作手順

<dx-tabs>
::: コンソールによる移行[](id:consoleMigrate)

### 準備事項[](id:prerequisites)

- Tencent Cloudアカウントをすでにお持ちであることが必要です。
- サブアカウントを使用してコンソールによる移行を行う場合は、ルートアカウントを使用して[CAMコンソール](https://console.cloud.tencent.com/cam/policy)にログインし、サブアカウントに`QcloudCSMFullAccess`権限を付与する必要があります。
- [APIキー管理](https://console.cloud.tencent.com/cam/capi)ページで`SecretId`および`SecretKey`を作成し、取得します。
- 移行ツール圧縮パッケージをダウンロードするには、[ここ](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip) をクリックしてください。
- 移行中に既存のアプリケーションへの影響を回避するために、ソースサーバーのアプリケーションを一時停止することをお勧めします。


### データのバックアップ
- 移行元サーバー：ソースサーバーのスナップショット機能などの方式を選択してデータをバックアップできます。
- 移行先CVM： [スナップショットの作成](https://intl.cloud.tencent.com/document/product/362/5755) などの方式を選択してデータをバックアップできます。


### コンソールマイグレーションツールを取得する
[ここをクリック](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip)して、マイグレーションツールの圧縮ファイルをダウンロードします。

### マイグレーション前の確認

マイグレーションする前に、移行元サーバーと移行先CVMをそれぞれ確認する必要があります。確認内容は下表のとおりです。

<table>
  <tr>
	<th>Linux移行元サーバー</th>
	<td>
	  <ol style="margin: 0;">
		<li>Virtioをチェックまたはインストールします。操作の詳細については 
		<a href="https://intl.cloud.tencent.com/document/product/213/9929">LinuxでのVirtioドライバーの確認</a>をご参照ください。</li>
		<li>実行 
		<code>which rsync</code>コマンドで、rsyncがインストールされているかどうかをチェックします。インストールされていない場合は、<a href="https://intl.cloud.tencent.com/document/product/213/32395#installRsync">Rsyncのインストール方法</a>を参照してインストールしてください。</li>
		<li>SELinuxが有効になっているかどうかをチェックします。SELinuxが有効になっている場合は、<a href="https://intl.cloud.tencent.com/document/product/213/32395#closeSELinux">SELinuxを無効化する方法</a>を参照して無効化してください。</li>
		<li>Tencent Cloud APIに対しマイグレーションリクエストを送信すると、Tencent Cloud APIは現在のUNIX時間をチェックして発行された
		Tokenを使用する場合があります。現在のシステム時間が正確であることを確認してください。</li>
	  </ol>
	</td>
  </tr>
  <tr>
	<th style="width: 15%;">移行先CVM</th>
	<td>
	  <ol style="margin: 0;">
		<li>
		ストレージ容量：移行先CVMのクラウドディスク（システムディスクとデータディスクを含む）には、移行元サーバーから移行されたデータを保存するための十分な容量がある必要があります。</li>
		<li>セキュリティグループ：セキュリティグループでは443ポート、80ポートは制限できません。</li>
		<li>
		帯域幅設定：マイグレーションをより迅速に行えるようにするため、できる限り両側の帯域幅を広くすることをお勧めします。マイグレーション中にはデータ量とほぼ同等のトラフィック消費が発生する場合があります。必要に応じ、事前にネットワーク課金モデルの調整を行ってください。</li>
		<li>
		移行先CVMと移行元サーバーのOSタイプが一致しているか：OSが一致していないと、その後に作成するイメージの情報と実際のOSが一致しない場合がありますので、移行先CVMのOSはできる限り移行元サーバーのOSタイプと一致させることをお勧めします。例えば、CentOS
		7システムの移行元サーバーのマイグレーションの場合は、CentOS 7システムのCVMを移行先として選択してください。</li>
	  </ol>
	</td>
  </tr>
</table>



<dx-alert infotype="explain" title="">
- `sudo ./go2tencentcloud_x64 --check`などのツールコマンドを使用して、移行元サーバーを自動的にチェックできます。
- go2tencentcloudマイグレーションツールは、実行を開始すると、デフォルトで自動的にチェックします。このチェックをスキップして強制的に移行する場合は、client.json ファイルの`Client.Extra.IgnoreCheck`フィールドの値を`true`に設定してください。
- go2tencentcloud マイグレーションツールの詳細情報については、 [マイグレーションツールの説明](https://intl.cloud.tencent.com/document/product/213/44340)をご参照ください。
</dx-alert>



### マイグレーションの開始
1. マイグレーションツールgo2tencentcloud.zipをダウンロードするか、または移行元サーバーにアップロードし、次のコマンドを実行して対応するディレクトリに進みます。
    1. 次のコマンドを順に実行し、go2tencentcloud.zipを解凍してディレクトリに進みます。
```sh
unzip go2tencentcloud.zip
```
```sh
cd go2tencentcloud
```
    2. 次のコマンドを順に実行し、go2tencentcloud_console.zipを解凍してディレクトリに進みます。
```sh
unzip go2tencentcloud_console.zip
```
```sh
cd go2tencentcloud_console
```
2. （オプション）移行元サーバー上でマイグレーション不要のファイルおよびディレクトリを削除します。  
Linux移行元サーバーにマイグレーション不要のファイルまたはディレクトリが存在する場合は、ファイルまたはディレクトリを[rsync_excludes_linux.txtファイル](https://intl.cloud.tencent.com/document/product/213/44340)に追加することができます。
3. 移行元をインポートします。
   1. 64ビットのLinux移行元サーバーを例とします。go2tencentcloudファイルディレクトリに入り、root権限で次のコマンドを順に実行し、ツールを実行します。
```shell
chmod +x go2tencentcloud_x64
```
```shell
sudo ./go2tencentcloud_x64
```
下図のように、[準備事項](#prerequisites)で取得したアカウントのAPIアクセスキーの`SecretId`および`SecretKey`を表示に従って入力し、**Enter**を押します。
<img src="https://qcloudimg.tencent-cloud.cn/raw/38ff9f9d8c143a4cb0df39cbeaf18713.png"/>
<br>マイグレーションツールのインターフェースに次のようなメッセージが表示された場合、移行元のコンソールへのインポートは成功しており、コンソールで移行元を確認できます。
<img src="https://qcloudimg.tencent-cloud.cn/raw/f9cf0fd99504aba51ebf82b0cab250b8.png"/>
<br><a href="https://console.cloud.tencent.com/cvm/csm/online?rid=1">オンラインマイグレーションコンソール</a>にログインすると、インポート済みの移行元を確認できます。ステータスは「オンライン」となっています。下図に示します。
<img src="https://qcloudimg.tencent-cloud.cn/raw/11b1e6cada0384dae292e89378629ddc.png"/>
Import source server successfullyと表示されない場合は、移行元のインポートに失敗しています。ログ（デフォルトではマイグレーションツールディレクトリ下のlogs/logファイル）を確認して問題を解決した後、再度マイグレーションツールを実行して移行元をインポートすることができます。
<dx-alert infotype="notice" title="">
移行元のインポート成功後は、移行タスクの完了までの間、インスタンス内のマイグレーションツールを閉じないでください。閉じてしまうと、移行元がオフラインとなった後、移行タスクを完了できなくなります。
</dx-alert>

4. オンラインマイグレーションコンソールに移動し、移行タスクを作成します。
    1. [オンラインマイグレーションコンソール](https://console.cloud.tencent.com/cvm/csm/online?rid=1)にログインし、対象の移行元がある行の右側の**移行タスク作成**をクリックします。
    2. ポップアップされた「移行タスク作成」ウィンドウで、[移行タスク設定説明](https://intl.cloud.tencent.com/document/product/213/44338)の情報を参照して設定します。
    例えば、Linux移行元サーバー1基をTencent Cloud広州リージョンのCVM1基にマイグレーションする場合、移行タスク設定は次のように行います。
    ![](https://qcloudimg.tencent-cloud.cn/raw/63c9481797c861890a2ea9ca37c4f272.png)
5. 移行タスクを起動します。
<dx-alert infotype="explain" title="">
実行を予約するタスクはこの手順をスキップすることができます。予約した実行時間になると、移行タスクは自動的に実行を開始します。
</dx-alert>
下図に示すように、移行タスクを作成すると、**移行タスク**タブをクリックして移行タスクを確認できるようになります。
![](https://qcloudimg.tencent-cloud.cn/raw/7d2447ea7e6f348d779e41ad2c08fd93.png)
下図に示すように、タスクのある行の右側の**開始/リトライ**をクリックすると、移行タスクを開始できます。このとき、タスクのステータスは「移行中」に変わります。
![](https://qcloudimg.tencent-cloud.cn/raw/bcbad8eb9a093814f18ff82aab7bc308.png)
6. 移行タスクが終了するまで待ちます。
下図のように、移行タスクのステータスが「成功」となれば、移行が完了したことを表します。
![](https://qcloudimg.tencent-cloud.cn/raw/7beb11db18bd9913b44941dd05f8a4a4.png)


### マイグレーション後の確認
 - マイグレーションが失敗した場合は、ログファイル（デフォルトではマイグレーションツールディレクトリ下のログファイル）からのエラーメッセージ出力、ガイドラインドキュメントまたは[サービスマイグレーションに関するよくあるご質問](https://intl.cloud.tencent.com/document/product/213/32395)を確認し、トラブルシューティングと問題の修正を行ってください。修正後、移行タスク操作列で**リトライ**をクリックすると、移行タスクを再開できます。
 - マイグレーションが成功した場合は、移行先CVMが正常に起動できるか、移行先CVMのデータが移行元サーバーと一致しているか、ネットワークが正常か、他のシステムサービスが正常かなどを確認してください。


ご不明な点やマイグレーションの異常など、ご質問がありましたら、[サービスマイグレーションに関するよくあるご質問](https://intl.cloud.tencent.com/document/product/213/32395)をご参照いただくか、または[お問い合わせ](https://intl.cloud.tencent.com/document/product/213/34837)から解消してください。

:::
::: ツールによる移行[](id:consoleMigrate)

### 準備事項

- Tencent Cloudアカウントをすでにお持ちであることが必要です。
- 移行中に既存のアプリケーションへの影響を回避するために、ソースサーバーのアプリケーションを一時停止することをお勧めします。
- [APIキー管理](https://console.cloud.tencent.com/cam/capi)ページで`SecretId`および`SecretKey`を作成し、取得します。
- 移行ツール圧縮パッケージをダウンロードするには、[ここ](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip) をクリックしてください。
- ソースサーバーと移行先CVMの両方が移行要件を満たしていることを確認します。例えば、移行先CVMのクラウドディスクには、移行元サーバーから移行されたデータを保存するための十分な容量を持っている必要があります。


### マイグレーションツールを取得する  

[ここをクリック](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip)して、マイグレーションツールの圧縮ファイルをダウンロードします。



### データのバックアップ
- 移行元サーバー：ソースサーバーのスナップショット機能などの方式を選択してデータをバックアップできます。
- 移行先CVM： [スナップショットの作成](https://intl.cloud.tencent.com/document/product/362/5755) などの方式を選択してデータをバックアップできます。


### ネットワーク環境に応じたマイグレーションモードの確定

移行元サーバーと移行先CVMのネットワーク環境に基づいて、適切なマイグレーションモードを確定します。
現在マイグレーションツールはデフォルトモードとプライベートネットワークマイグレーションモードをサポートしています。その中で、プライベートネットワークマイグレーションモードは3つのシナリオに適用されます。異なるマイグレーションモード/シナリオは、移行元サーバーと移行先CVMのネットワーク要件も違います。移行元サーバーと移行先CVMの両方がパブリックネットワークにアクセスできる場合、デフォルトモードで直接マイグレーションできます。移行元サーバーまたは移行先CVMのいずれかがパブリックネットワークに直接アクセスできない場合、まず[VPCピアリング接続](https://intl.cloud.tencent.com/zh/document/product/553)、[VPN接続](https://intl.cloud.tencent.com/zh/document/product/1037)、[CCN](https://intl.cloud.tencent.com/zh/document/product/1003)または[ダイレクト接続](https://intl.cloud.tencent.com/zh/document/product/216)などの方法で接続チャネルを確立してから、プライベートネットワークモードでのマイグレーションを実施する方法を選択することができます。



### マイグレーション前の確認

マイグレーションする前に、移行元サーバーと移行先CVMをそれぞれ確認する必要があります。確認する内容は下表のとおりです。


<table>
  <tr>
	<th style="width: 15%;">移行先CVM</th>
	<td>
	  <ol style="margin: 0;">
		<li>
		ストレージ容量：移行先CVMのクラウドディスク（システムディスクとデータディスクを含む）には、移行元サーバーから移行されたデータを保存するための十分な容量がある必要があります。</li>
		<li>セキュリティグループ：セキュリティグループでは443ポート、80ポートは制限できません。</li>
		<li>
		帯域幅設定：マイグレーションをより迅速に行えるようにするため、できる限り両側の帯域幅を広くすることをお勧めします。マイグレーション中にはデータ量とほぼ同等のトラフィック消費が発生する場合があります。必要に応じ、事前にネットワーク課金モデルの調整を行ってください。</li>
		<li>
		移行先CVMと移行元サーバーのOSタイプが一致しているか：OSが一致していないと、その後に作成するイメージの情報と実際のOSが一致しない場合がありますので、移行先CVMのOSはできる限り移行元サーバーのOSタイプと一致させることをお勧めします。例えば、CentOS
		7システムの移行元サーバーのマイグレーションの場合は、CentOS 7システムのCVMを移行先として選択してください。</li>
	  </ol>
	</td>
  </tr>
  <tr>
	<th>Linux移行元サーバー</th>
	<td>
	  <ol style="margin: 0;">
		<li>Virtioをチェックまたはインストールします。操作の詳細については 
		<a href="https://intl.cloud.tencent.com/document/product/213/9929">LinuxでのVirtioドライバーの確認</a>をご参照ください。</li>
		<li>実行 
		<code>which rsync</code>コマンドで、rsyncがインストールされているかどうかをチェックします。インストールされていない場合は、<a href="https://intl.cloud.tencent.com/document/product/213/32395#installRsync">Rsyncのインストール方法</a>を参照してインストールしてください。</li>
		<li>SELinuxが有効になっているかどうかをチェックします。SELinuxが有効になっている場合は、<a href="https://intl.cloud.tencent.com/document/product/213/32395#closeSELinux">SELinuxを無効化する方法</a>を参照して無効化してください。</li>
		<li>Tencent Cloud APIに対しマイグレーションリクエストを送信すると、Tencent Cloud APIは現在のUNIX時間をチェックして発行された
		Tokenを使用する場合があります。現在のシステム時間が正確であることを確認してください。</li>
		<li>移行元サーバーのログイン方式をチェックします。移行元のAWSサーバーがSSH
		キーペア方式でログインする場合、パスワード方式でのログインに変更することをお勧めします。</li>
	  </ol>
	</td>
  </tr>
</table>



<dx-alert infotype="explain" title="">
- `sudo ./go2tencentcloud_x64 --check`などのツールコマンドを使用して、移行元サーバーを自動的にチェックできます。
- go2tencentcloudマイグレーションツールは、実行を開始すると、デフォルトで自動的にチェックします。このチェックをスキップして強制的に移行する場合は、client.json ファイルの`Client.Extra.IgnoreCheck`フィールドの値を`true`に設定してください。
- go2tencentcloud マイグレーションツールの詳細情報については、 [マイグレーションツールの説明](https://intl.cloud.tencent.com/document/product/213/44340)をご参照ください。
</dx-alert>



### マイグレーションの開始

1. （オプション）移行元サーバーと移行先CVM間に接続チャネルを確立します。
  - [プライベートネットワークマイグレーションモード](https://intl.cloud.tencent.com/document/product/213/44341)を選択する場合は、[VPCピアリング接続](https://intl.cloud.tencent.com/zh/document/product/553)、[VPN接続](https://intl.cloud.tencent.com/zh/document/product/1037)、[CCN](https://intl.cloud.tencent.com/zh/document/product/1003)または[ダイレクト接続](https://intl.cloud.tencent.com/zh/document/product/216)などの方式で、移行元サーバーと移行先CVM間の接続チャネルを確立する必要があります。
  - [パブリックネットワークマイグレーションモード](https://intl.cloud.tencent.com/document/product/213/44340)を選択する場合は、この手順をスキップしてください。
2. マイグレーションツールgo2tencentcloud.zipをダウンロードするか、または移行元サーバーにアップロードし、次のコマンドを実行して対応するディレクトリに進みます。
    1. 次のコマンドを順に実行し、go2tencentcloud.zipを解凍してディレクトリに進みます。
```sh
unzip go2tencentcloud.zip
```
```sh
cd go2tencentcloud
```
    2. 次のコマンドを順に実行し、go2tencentcloud_tool.zipを解凍してディレクトリに進みます。
```sh
unzip go2tencentcloud_tool.zip
```
```sh
cd go2tencentcloud_tool
```
3. `user.json`ファイルを設定します。
`user.json` は移行元サーバーと移行先CVMを設定するためのファイルです。このファイルの設定項目は次のとおりです。
  - アカウントのAPIアクセスキーペアは、SecretIdとSecretKeyです。詳細情報については[アクセスキー](https://intl.cloud.tencent.com/document/product/598/32675)をご参照ください。
  - 移行先CVMが所在するリージョン、CVMがサポートするリージョンについては[リージョンとアベイラビリティーゾーン](https://intl.cloud.tencent.com/document/product/213/6091) をご参照ください。
  - 移行先CVMのインスタンスIDは、[インスタンスリスト](https://console.cloud.tencent.com/cvm/instance/index?rid=1)画面で確認できます。
  - 移行元サーバーのデータディスク設定。（オプション）  
4. `client.json`ファイルを設定します。
`client.json` はマイグレーションモードとその他のマイグレーション設定項目を設定するためのファイルです。どのマイグレーションモード/シナリオを選択しても、client.jsonファイルの‵Client.Net.Mode‵項目で対応するパラメータ値を設定する必要があります。
5. （オプション）移行元サーバー上でマイグレーション不要のファイルおよびディレクトリを削除します。  
Linux移行元サーバーにマイグレーション不要のファイルまたはディレクトリが存在する場合は、ファイルまたはディレクトリを[rsync_excludes_linux.txtファイル](https://intl.cloud.tencent.com/document/product/213/44340)に追加することができます。
6. ツールを実行する。
例えば、64ビットのLinux移行元サーバーでgo2tencentcloudファイルディレクトリに入り、root権限で次のコマンドを実行し、ツールを実行します。
```
sudo ./go2tencentcloud_x64
```
ツールが実行した後、マイグレーションプロセスが完了するまでお待ちください。
通常、マイグレーションが成功すると、コンソールから次のような内容が出力されます。
 ![](https://main.qcloudimg.com/raw/238ce694355a59836762df4f9a716f6f.png)



### マイグレーション後の確認
 - マイグレーションが失敗した場合は、ログファイル（デフォルトではマイグレーションツールディレクトリ下のログファイル）からのエラーメッセージ出力、ガイドラインドキュメントまたは[サービスマイグレーションに関するよくあるご質問](https://intl.cloud.tencent.com/document/product/213/32395)を確認し、トラブルシューティングと問題の修正を行ってください。修正後、移行タスク操作列で**開始/リトライ**をクリックすると、移行タスクを再開できます。
 - マイグレーションが成功した場合は、移行先CVMが正常に起動できるか、移行先CVMのデータが移行元サーバーと一致しているか、ネットワークが正常か、他のシステムサービスが正常かなどを確認してください。


ご不明な点やマイグレーションの異常など、ご質問がありましたら、[サービスマイグレーションに関するよくあるご質問](https://intl.cloud.tencent.com/document/product/213/32395)をご参照いただくか、または[お問い合わせ](https://intl.cloud.tencent.com/document/product/213/34837)から解消してください。

:::
</dx-tabs>









