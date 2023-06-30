## 概要

このドキュメントでは、Cloud Virtual Machine (CVM)コンソールのオンラインマイグレーション機能の**プライベートネットワークマイグレーション**モードを使用して、ソースサーバー上のシステム、アプリケーションプログラムなどを自分で作成したコンピュータルーム(IDC)やクラウドプラットフォームなどのソース環境からCVMに移行する操作手順についてご紹介します。

プライベートネットワークを使用したマイグレーションはパブリックネットワークマイグレーションに比べて移行の転送速度が速く、移行効率が顕著に向上します。また、移行元マシンのパブリックネットワークアクセス機能を制限せず、柔軟なマイグレーション設定を行うことができます。


## 準備事項[](id:prerequisites)
- Tencent Cloudアカウントをすでに持っていることが必要です。
- サブアカウントを使用してコンソールによる移行を行う場合は、ルートアカウントを使用して[CAMコンソール](https://console.cloud.tencent.com/cam/policy)にログインし、サブアカウントに`QcloudCSMFullAccess`権限を付与する必要があります。
- [APIキー管理](https://console.cloud.tencent.com/cam/capi)ページで`SecretId`および`SecretKey`を作成し、取得します。
- 移行ツール圧縮パッケージをダウンロードするには、[ここ](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip) をクリックしてください。
- 移行中に既存のアプリケーションへの影響を回避するために、ソースサーバーのアプリケーションを一時停止することをお勧めします。


## 操作手順

### データのバックアップ
- 移行元サーバー：ソースサーバーのスナップショット機能などの方式を選択してデータをバックアップできます。
- 移行先CVM： [スナップショットの作成](https://intl.cloud.tencent.com/document/product/362/5755) などの方式を選択してデータをバックアップできます。

### コンソールマイグレーションツールを取得する  
[ここをクリック](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip)して、マイグレーションツールの圧縮パッケージをダウンロードします。

### ネットワーク環境に応じたマイグレーションモードの確定

移行元サーバーと移行先CVMのネットワーク環境に基づいて、適切なマイグレーションモードを確定します。
現在コンソールのオンラインマイグレーションはパブリックネットワークモードとプライベートネットワークマイグレーションモードをサポートしています。その中で、プライベートネットワークマイグレーションモードは3つのシナリオに詳しく分けられます。異なるマイグレーションモード/シナリオは、移行元サーバーと移行先CVMのネットワーク要件も違います。移行元サーバーと移行先CVMの両方がパブリックネットワークにアクセスできる場合、デフォルトモードで直接マイグレーションできます。移行元サーバーまたは移行先CVMのいずれかがパブリックネットワークに直接アクセスできない場合、まず[VPC Peering Connection](https://intl.cloud.tencent.com/document/product/553)、[VPN Connection](https://intl.cloud.tencent.com/document/product/1037)、[CCN](https://intl.cloud.tencent.com/document/product/1003)または[Direct Connection](https://intl.cloud.tencent.com/document/product/216)などの方法で接続チャネルを確立してから、プライベートネットワークモードでのマイグレーションを実施する方法を選択することができます。

### マイグレーション前の確認
マイグレーション前に、実際の状況に応じて確認を行う必要があります。確認する内容は下表のとおりです：
- 移行先がCVMの場合は、移行元サーバーと移行先CVMを確認してください。
- 移行先がCVMイメージの場合は、移行元サーバーのみを確認します。

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
		Tokenを使用してください。現在のシステム時間が正確であることを確認してください。</li>
	  </ol>
	</td>
  </tr>
  <tr>
	<th style="width: 15%;">移行先CVM（オプション）</th>
	<td>
	  <ol style="margin: 0;">
		<li>
		ストレージ容量：移行先CVMのクラウドディスク（システムディスクとデータディスクを含む）には、移行元サーバーから移行されたデータを保存するための十分な容量が必要です。</li>
		<li>セキュリティグループ：セキュリティグループでは443ポート、80ポートは制限できません。</li>
		<li>
		帯域幅設定：マイグレーションをより迅速に行えるようにするため、できる限り両側の帯域幅を広くすることをお勧めします。マイグレーション中にはデータ量とほぼ同等のトラフィック消費が発生する場合があります。必要に応じて、事前にネットワーク課金モデルの調整を行ってください。</li>
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


## 移行の開始
1. 移行元サーバーとTencent Cloud間のプライベートネットワーク接続チャネルを確立します。
 - 移行先が移行先CVMである場合：[VPC Peering Connection](https://intl.cloud.tencent.com/document/product/553) / [VPN Connection](https://intl.cloud.tencent.com/document/product/1037) / [CCN](https://intl.cloud.tencent.com/document/product/1003)などの方法によって、移行元サーバーと移行先CVM間の接続チャネルを確立します。
 - 移行先がCVMイメージである場合：[VPC Peering Connection](https://intl.cloud.tencent.com/document/product/553) / [VPN Connection](https://intl.cloud.tencent.com/document/product/1037) / [CCN](https://intl.cloud.tencent.com/document/product/1003)などの方法によって、移行元サーバーとTencent Cloud VPC間の接続チャネルを確立します。
2. マイグレーションツールgo2tencentcloud.zipをダウンロードするか、または移行元サーバーにアップロードし、次のコマンドを実行して対応するディレクトリに進みます。
 i. 次のコマンドを順に実行し、go2tencentcloud.zipを解凍してディレクトリに進みます。
```shellsession
unzip go2tencentcloud.zip
```
```shellsession
cd go2tencentcloud
```
 ii. 次のコマンドを順に実行し、go2tencentcloud-linux.zipを解凍してディレクトリに進みます。
```shellsession
unzip go2tencentcloud-linux.zip
```
```shellsession
cd go2tencentcloud-linux
```
<dx-alert infotype="explain" title="">
 `go2tencentcloud`ディレクトリ下のファイルは移行されません。移行が必要なファイルをこのディレクトリ下に置かないでください。
</dx-alert>

3. （オプション）移行元サーバー上でマイグレーション不要のファイルおよびディレクトリを削除します。 
Linux移行元サーバーにマイグレーション不要のファイルまたはディレクトリが存在する場合は、ファイルまたはディレクトリを [rsync_excludes_linux.txtファイル](https://intl.cloud.tencent.com/document/product/213/44340)に追加することができます。

4. （オプション）ネットワークプロキシを設定します。
 - マイグレーションシナリオが [プライベートネットワークマイグレーションモード：シナリオ2](https://intl.cloud.tencent.com/document/product/213/44340)である場合は、この手順をスキップしてください。
 - マイグレーションシナリオが [プライベートネットワークマイグレーションモード：シナリオ3](https://intl.cloud.tencent.com/document/product/213/44340)である場合は、プロキシネットワークのIPアドレスとポートを構成してください：
    - `client.json`ファイルの`Client.Net.Proxy.Ip`と`Client.Net.Proxy.Port`の項目をネットワークプロキシのIPアドレスとポートに設定してください。
    - ネットワークプロキシに認証が必要である場合、`Client.Net.Proxy.User`と`Client.Net.Proxy.Password`の項目にネットワークプロキシのユーザー名とパスワードを記入してください。認証が不要な場合は、空白のままにします。

5. 移行元をインポートします。
 i.例えば、64ビットのLinux移行元サーバーで、root権限を指定して次のコマンドを実行し、ツールを実行します。
```shellsession
chmod +x go2tencentcloud_x64
```
```shellsession
sudo ./go2tencentcloud_x64
```
 ii. 下図のように、[準備事項](#prerequisites)で取得したアカウントのAPIアクセスキーの`SecretId`および`SecretKey`を表示に従って入力し、**Enter**を押します：
![](https://qcloudimg.tencent-cloud.cn/raw/6e38d7e0487da4a2f6fd001e9953466a.png)
マイグレーションツールのインターフェースに次のようなメッセージが表示された場合、移行元のコンソールへのインポートは成功しており、コンソールで移行元を確認できます。
<img src="https://qcloudimg.tencent-cloud.cn/raw/9261d9c0ce1789c1b7afa1accd6bf884.png"/>
<a href="https://console.cloud.tencent.com/cvm/csm/online?rid=1">オンラインマイグレーションコンソール</a>にログインすると、インポート済みの移行元を確認できます。ステータスは「オンライン」となっています。下図に示したとおりです：
<img src="https://qcloudimg.tencent-cloud.cn/raw/11b1e6cada0384dae292e89378629ddc.png"/>
Import source server successfullyと表示されない場合は、移行元のインポートに失敗することを示します。ログ（デフォルトではマイグレーションツールディレクトリ下のlogs/logファイル）を確認して問題を解決した後、再度マイグレーションツールを実行して移行元をインポートすることができます。
<dx-alert infotype="notice" title="">
移行元のインポート成功後は、移行タスクの完了までの間、インスタンス内のマイグレーションツールを閉じないでください。閉じてしまうと、移行元がオフラインとなった後、移行タスクを完了できなくなります。
</dx-alert>

6. オンラインマイグレーションコンソールに移動し、移行タスクを作成します。
 i. [オンラインマイグレーションコンソール](https://console.cloud.tencent.com/cvm/csm/online?rid=1)にログインし、対象の移行元がある行の右側の**移行タスク作成**をクリックします。
 ii. ポップアップされた「移行タスク作成」ウィンドウで、[移行タスク設定説明](https://intl.cloud.tencent.com/document/product/213/44338)の情報を参照して設定します。
例えば、プライベートネットワークを使用してLinux移行元サーバーをTencent Cloud上海リージョンにマイグレーションして、移行先CVMのイメージを生成します。移行タスク設定は下図のように行います：
![](https://qcloudimg.tencent-cloud.cn/raw/63c9481797c861890a2ea9ca37c4f272.png)

7. 移行タスクを起動します。
<dx-alert infotype="explain" title="">
実行を予約するタスクはこの手順をスキップすることができます。予約した実行時間になると、移行タスクは自動的に実行を開始します。
</dx-alert>
下図に示すように、移行タスクを作成すると、<b>移行タスク</b>タブをクリックして移行タスクを確認できるようになります：
<img src="https://qcloudimg.tencent-cloud.cn/raw/7d2447ea7e6f348d779e41ad2c08fd93.png"/>
下図に示すように、タスクのある行の右側の<b>開始/リトライ</b>をクリックすると、ポップアップ表示された確認ウィンドウで<b>確定</b>をクリックして、移行タスクを開始できます。このとき、タスクのステータスは「移行中」に変わります：
<img src="https://qcloudimg.tencent-cloud.cn/raw/bcbad8eb9a093814f18ff82aab7bc308.png"/>

8. 移行タスクが終了するまで待ちます。
下図のように、移行タスクのステータスが「成功」となれば、移行が完了したことを表します：
![](https://qcloudimg.tencent-cloud.cn/raw/7beb11db18bd9913b44941dd05f8a4a4.png)
<dx-alert infotype="explain" title="">
データ転送の消費時間は、移行元データのサイズ、ネットワーク帯域幅などの要因に左右されます。マイグレーションフローが完了するまでお待ちください。マイグレーションツールはデータ転送の中断からの再開をサポートしています。
</dx-alert>

### マイグレーション後の確認

- **マイグレーション結果の失敗**：
ログファイル（デフォルトではマイグレーションツールディレクトリ下のログファイル）からのエラーメッセージ出力、ガイドラインドキュメントまたは[サービスマイグレーションに関するよくあるご質問](https://intl.cloud.tencent.com/document/product/213/32395)を確認し、トラブルシューティングと問題の修正を行ってください。修正後、移行タスク操作列で**開始/リトライ**をクリックすると、移行タスクを再開できます。
- **マイグレーション結果の成功**：
 - 移行先がCVMの場合は、移行先CVMが正常に起動できるか、移行先CVMのデータが移行元サーバーと一致しているか、ネットワークが正常か、他のシステムサービスが正常かなどを確認してください。
 - 移行先がCVMイメージの場合は、移行タスクのある行の「CVMイメージID」をクリックし、[CVMイメージページ](https://console.cloud.tencent.com/cvm/image/index)に進むとこのイメージの情報を確認でき、このイメージを使用してCVMを作成することができます。

ご不明な点やマイグレーションの異常など、ご質問がありましたら、[サービスマイグレーションに関するよくあるご質問](https://intl.cloud.tencent.com/document/product/213/32395)をご参照いただくか、または[お問い合わせ](https://intl.cloud.tencent.com/document/product/213/34837)で解決してください。
