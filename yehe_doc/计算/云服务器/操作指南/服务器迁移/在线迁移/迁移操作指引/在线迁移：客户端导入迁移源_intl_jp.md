このドキュメントでは、クライアントから移行元をインポートして、移行元サーバーを Tencent Cloud CVM に移行する方法について説明します。

## 移行ワークフロー
クライアントから移行元をインポートする手順は以下のとおりです。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/w6gR606_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230428170713.png)

[](id:prerequisites)
## 移行手順
### 手順1：移行の準備
- [APIキー管理](https://console.cloud.tencent.com/cam/capi)ページに移動してキーを作成し、 `SecretId` と `SecretKey`を取得します。
-移行時に既存のアプリケーションに影響しないように、移行元サーバー上のアプリケーションを一時停止してデータをバックアップすることをお勧めします。
 - 移行元サーバー：スナップショット機能またはその他の方法を使用して、移行元サーバー上のデータをバックアップできます。移行元サーバーは、移行されるサーバーです。
 - 移行先CVM： [スナップショットの作成](https://intl.cloud.tencent.com/document/product/362/5755)などの方式を選択して、移行先CVMのデータをバックアップできます。
-  サブアカウントを使用してコンソールで移行を実行する場合、ルートアカウントで[CAMコンソール](https://console.cloud.tencent.com/cam/policy)にログインし、サブアカウントにQcloudCSMFullAccessとQcloudCVMFullAccess権限を付与する必要があります。
- 移行前、実際の状況に基づいて次の構成を確認する必要があります。ご確認いただきたい内容は以下のとおりです：
 - CVM インスタンスへの移行：移行元サーバーと移行先CVMを確認する必要があります。
 - CVM イメージへの移行：移行元サーバーのみを確認します。
  <table>
  <tr>
	<th>Linux 移行元サーバー</th>
	<td>
	  <ol style="margin: 0;">
		<li>Virtio を確認してインストールします。詳細については、 
		<a href="https://intl.cloud.tencent.com/document/product/213/9929">LinuxでのVirtioドライバーの確認</a>をご参照ください。</li>
		<li>‌‍　 
		<code>which rsync</code>コマンドを実行して、 rsync がインストールされているかどうかを確認します。インストールされていない場合は、<a href="https://intl.cloud.tencent.com/document/product/213/32395#installRsync">rsync をインストールする方法</a>の指示に従ってインストールしてください。</li>
		<li>SELinux が有効化されているかどうかを確認します。SELinuxが有効になっている場合は、<a href="https://intl.cloud.tencent.com/document/product/213/32395#closeSELinux">SELinuxを無効化する方法</a>を参照して無効化してください。</li>
		<li>Tencent Cloud API に移行リクエストを送信した後、API は現在の UNIX 時間を使用して、生成されたトークンを確認します。
		サーバーのシステム時刻が正しいことを確認してください。</li>
	  </ol>
	</td>
 </tr>
  <tr>
	<th>Windows 移行元サーバー</th>
	<td>
	  <ol style="margin: 0;">
		<li>Virtio を確認してインストールします。詳細については、 
		<a href="https://intl.cloud.tencent.com/document/product/213/17815">WindowsでのVirtioドライバーの確認</a>をご参照ください。</li>
		<li>(オプション)Cloudbase-Init を確認してインストールします。詳細については、<a href="https://intl.cloud.tencent.com/document/product/213/32364">Windows への Cloudbase-Init のインストール</a>‍をご参照ください。移行前に移行元サーバーにインストールするか、移行後にターゲットインスタンスにインストールするかを選択できます。<br>移行前にインストールされている場合は、移行後にネットワークの自動構成やアクティベーションなどの初期化作業が行われます。<br>移行前にインストールされていない場合は、<a href="https://intl.cloud.tencent.com/document/product/213/32496">VNC 経由でインスタンスにログイン</a>‍し、ネットワーク構成を手動で変更する必要があります。</li>
	  </ol>
	</td>
  </tr>
  <tr>
	<th style="width: 15%;">移行先CVM </th>
	<td>
	  <ol style="margin: 0;">
		<li>
		ストレージ容量：移行先CVMのクラウドディスク（システムディスクとデータディスクを含む）には、移行元サーバーから移行されたデータを保存するための十分な容量が必要です。</li>
		<li>セキュリティグループ：セキュリティグループでポート80、443、および3389を開放します。</li>
		<li>
		帯域幅：移行をより円滑に進めるためには、移行元と移行先の両方の環境の帯域幅を最大化することをお勧めします。移行プロセス中に消費されるトラフィックは、移行されたデータの量とほぼ同じになります。必要に応じて、移行前にネットワーク課金モデルを調整します。</li>
<li>
		ネットワーク設定：移行元または移行先サーバーが IPv6 のみをサポートし、IPv4 をサポートしていない場合は、<a href="https://intl.cloud.tencent.com/document/product/213/44340">client.jsonファイルのパラメータ説明</a>をご参照ください。</li>
	  </ol>
	</td>
  </tr>
</table>
<dx-alert infotype="explain" title="">
- `sudo ./go2tencentcloud_x64 --check`などのツールコマンドを使用して、移行元サーバーを自動的にチェックできます。
- デフォルトでは、go2tencentcloudツールは起動時に自動的にチェックを実行します。このチェックをスキップして強制移行する場合は、client.json ファイルの`Client.Extra.IgnoreCheck`フィールドの値を`true`に設定してください。
</dx-alert>

[](id:registrationSource)
### ‍手順2：移行元のインポート
#### 移行ツールによる移行元のインポート
<dx-tabs>
::: Linuxサーバー                                       
1. 移行元サーバーで次のコマンドを実行して、移行ツール`go2tencentcloud.zip`を[ダウンロード]( https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip) してディレクトリに進みます。
```shellsession
wget https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip
```
```shellsession
unzip go2tencentcloud.zip
```
```shellsession
cd go2tencentcloud/go2tencentcloud-linux
```
<dx-alert infotype="explain" title="">
`go2tencentcloud`ディレクトリ下のファイルは移行されません。移行するファイルをこのディレクトリに置かないでください。
</dx-alert>
2. （オプション）移行元サーバー上で移行不要のファイルまたはディレクトリを除外します
Linux移行元サーバー上で移行不要のファイルおよびディレクトリがある場合、ファイルおよびディレクトリを[rsync_excludes_linux.txtファイル](https://intl.cloud.tencent.com/document/product/213/44340)に追加できます。
3. 移行元をインポートします。
   1. 例えば、64ビットのLinux移行元サーバーで、root ユーザーとして次のコマンドを順番に実行してツールを実行します。
```shellsession
chmod +x go2tencentcloud_x64
```
```shellsession
sudo ./go2tencentcloud_x64
```
   2. [準備事項](#prerequisites)で取得したアカウントのAPIアクセスキーの`SecretId`および`SecretKey`を入力し、**Enter**を押します。下図に示すとおり：
![](https://qcloudimg.tencent-cloud.cn/raw/38ff9f9d8c143a4cb0df39cbeaf18713.png)
次のメッセージが表示されたら、移行元サーバーは正常にインポートされています。CVM コンソールに移動してサーバーを表示できます。
<img src="https://qcloudimg.tencent-cloud.cn/raw/f9cf0fd99504aba51ebf82b0cab250b8.png"/>
:::

::: Windowsサーバー
1. 移行ツールgo2tencentcloud.zipを移行元サーバーに [ダウンロード](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip)またはアップロードします。この圧縮ファイルを解凍してgo2tencentcloudフォルダーを入手し、その中の「go2tencentcloud-windows」を開くと以下のディレクトリが表示されます。
![](https://qcloudimg.tencent-cloud.cn/raw/3f2c9881d9c5323a14d096d0811814cd.png)    
2. 以下の方法で「go2tencentcloud_x64.exe」アプリケーションを実行します。
	- 方法1：「go2tencentcloud_x64.exe」を右クリックし、管理者権限で「go2tencentcloud_x64.exe」を実行し、ポップアップした画面でSecretId、SecretKeyを入力します。
	- 方法2：管理者権限でcmdまたはpowershelコマンドライン ：cd /d "go2tencentcloud_x64.exeが所在するディレクトリの絶対パス"を起動し、 go2tencentcloud_x64.exeを実行します。
3. ポップアップした画面で Tencent Cloud API キー (SecretIdと SecretKey) を入力します。
![](https://qcloudimg.tencent-cloud.cn/raw/b7af60919e710d7d148e791124fce1a0.png) ![](https://qcloudimg.tencent-cloud.cn/raw/8494a126134389796be195ccd268e03a.png)       

4. 以下のメッセージが表示された場合は、移行元がすでにコンソールにインポートされています。コンソールで移行元を確認できます。
![](https://qcloudimg.tencent-cloud.cn/raw/5ecd29f96415d0cb090fe165909272be.png)
:::
</dx-tabs>
<dx-alert infotype="explain" title="">
「Import source server successfully」が表示されない場合は、移行元のインポートが失敗したことを意味します。ログ（デフォルトでは移行ツールディレクトリ下にあるlogs/logファイル）を確認して問題を解決した後、移行ツールを再実行して移行元をインポートすることができます。
</dx-alert>

#### コンソールでの移行元サーバーの確認
<a href="https://console.cloud.tencent.com/cvm/csm/online?rid=1">オンライン移行コンソール</a>にログインし、インポートされた移行元を確認します。サーバーのステータスは**オンライン**となっています。下図に示すとおり：
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/rS3s122_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230517153526.png"/>

>! 移行元を正常にインポートした後、移行タスクの実行が完了するまで、インスタンス内の移行ツールを停止しないでください。停止すると、移行元がオフラインになり、移行タスクを完了できません。


### 手順3：移行タスクの作成

#### 1. 移行タスクの作成
[オンライン移行コンソール](https://console.cloud.tencent.com/cvm/csm/online?rid=1)にログインし、対象の移行元がある行の右側の**移行タスクの作成**をクリックします。**移行タスクの作成**画面が表示されます。この画面で以下の情報を参照して設定します。下図に示すとおり：
![](https://qcloudimg.tencent-cloud.cn/raw/c0598a38a6d2c6af165a1738930462da.png)
[](id:jobSettings)移行タスクの詳細設定内容は、以下のとおりです。

- 基本オプション：
	<table>
	<thead>
	<tr>
	<th width="18%">アイテム</th>
	<th width="10%">入力必須</th>
	<th>説明</th>
	</tr>
	</thead>
	<tbody>
	<tr>
	<td>移行先リージョン</td>
	<td>はい</td>
		<td>移行元サーバーの移行先となる Tencent Cloudリージョン。リージョンの詳細については、<a href="https://intl.cloud.tencent.com/document/product/213/6091">リージョンとアベイラビリティーゾーン</a>ドキュメントをご参照ください。</td>
	</tr>
	<tr>
	<td>タスク名</td>
	<td>はい</td>
	<td>移行タスクの名前。</td>
	</tr>
	<tr>
	<td>タスクの説明</td>
	<td>いいえ</td>
	<td>移行タスクの説明。</td>
	</tr>
	<tr>
	<td>ターゲットタイプ</td>
	<td>はい</td>
	<td>
		Tencent Cloud に移行する移行元サーバーのターゲットタイプを設定します。
			<ul>
			<li><b>CVMイメージ</b>：移行完了後、移行元サーバーのCVMイメージが生成されます。
				<br>イメージ名：移行元に対して生成されるターゲットCVM イメージの名前。名前がすでに存在する場合は、移行タスク ID が名前に追加されます。
			</li>
			<li><b>CVMインスタンス</b>：移行先リージョン内のCVMインスタンスを移行先として選択します。
				<br>移行先インスタンス：移行先インスタンスと移行元サーバーには同じOSを使用することをお勧めします。‍例えば、CentOS 7 移行元サーバーを移行するには、移行先として CentOS 7 CVM を選択します。
			</li>
		</ul>
	</td>
	</tr>
	<tr>
	<tr>
	<td>ネットワークモード</td>
	<td>はい</td>
	<td>
		データを転送するために使用されるネットワークタイプを設定します。
			<ul>
			<li><b>パブリックネットワーク経由のデータ転送</b>：移行先CVMまたはリレーインスタンスにデータを移行および転送する場合は、パブリックネットワークを使用します。
			</li>
			<li><b>プライベートネットワーク経由のデータ転送：移行先CVMまたはリレーインスタンスにデータを移行および転送する場合は、プライベートネットワークを使用します。詳細については、<a href="https://intl.cloud.tencent.com/document/product/213/44341">プライベートネットワーク経由の移行</a>をご参照ください。
				<br>Virtual Private Cloud（VPC）：CVMイメージに移行する場合、リレーインスタンスはVPC内に作成されます。
				<br>サブネット：CVMイメージに移行する場合、リレーインスタンスはサブネット内に作成されます。
			</li>
		</ul>
	</td>
	</tr>	
	<tr>
	<td rowspan='2'>移行方法</td>
	<td rowspan='2'>はい</td>
	<td>
		Linux インスタンスの場合:
			<ul>
			<li><b>Linuxファイルレベルの移行</b>：移行の粒度はファイルレベルであり、互換性は高く、転送効率は比較的低くなります。
			</li>
			<li><b>Linuxブロックレベルの移行</b>：移行の粒度はディスクのロジックストレージユニットの「ブロック」レベルであり、転送効率は高く、互換性は比較的低くなります。
			</li>
		</ul>
	</td>
	</tr>	
	<tr>
	<td>
	<b>Windowsブロックレベルの移行</b>：移行の粒度はディスクのロジックストレージユニットの「ブロック」レベルであり、Windows移行では、互換性が高く、転送効率が高いブロックレベルの移行がデフォルトで採用されています。
		</ul>
	</td>
	</tr>	
	<tr>
	<td>増分同期の構成</td>
	<td>いいえ</td>
	<td>増分同期時間をカスタマイズし、データを継続的に同期し、移行の配信時間を柔軟に制御します。
		<ul>
			<li><b>無効化</b>：移行ツールによって増分移行を自動的に認識して実行し、通常は1回実行されます。</li>
			<li><b>有効化</b>：増分同期の実行時間を自由に選択でき、ツールは増分データをTencent Cloudに継続的に同期します。タスクリストで増分同期を手動で停止することもできます。</li>
		</ul>
	</td>
	</tr>
	<td>予約実行時間</td>
	<td>いいえ</td> 
	<td>移行タスクを作成後、設定した時間に自動的に移行タスクを開始します。予約実行時間は最短で現在時刻の<b>10</b>分後に設定できます。</td>
	</tr>
	</tbody></table>


- 高度な設定（オプション）：
<table>
<thead>
<tr>
<th width="18%">アイテム</th>
<th width="10%">入力必須</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr>
<td>転送速度制限（KB/s）</td>
<td>いいえ</td>  
<td>移行中、データ転送の帯域幅の上限(0 ～ 25600 KB/s)。デフォルトでは 0 に設定されています。現在、Windows移行はこのオプションをサポートしていません。</td>
</tr>
<tr>
<td>Checksum検証</td>
<td>いいえ</td>  
<td>有効にすると、データの整合性チェックが強化されますが、転送速度は遅くなる場合があります。現在、Windows移行はこのオプションをサポートしていません。</td>
</tr>
</tbody></table>

#### 2. 移行タスクの起動
<dx-alert infotype="explain" title="">
スケジュールされたタスクは、この手順をスキップすることができます。移行タスクは、スケジュールされた時刻に移行を自動的に実行します。
</dx-alert>
移行タスクを作成した後、<b>移行タスク</b>タブをクリックして移行タスクを確認することができます。下図に示すとおり：
<img src="https://qcloudimg.tencent-cloud.cn/raw/7d2447ea7e6f348d779e41ad2c08fd93.png"/>
タスクの右側にある<b>開始/リトライ</b>をクリックしてタスクを開始し、表示された画面から<b>OK</b>をクリックすると、移行タスクを開始できます。このとき、タスクのステータスは「移行中」に変わります。下図に示すとおり：
<img src="https://qcloudimg.tencent-cloud.cn/raw/bcbad8eb9a093814f18ff82aab7bc308.png"/>
<dx-alert infotype="notice" title="">

- 移行先がCVM インスタンスの場合、移行開始後に移行先CVMは移行モードに入ります。移行を完了して移行モードが終了するまで、移行先CVMに対してシステムの再インストール、シャットダウン、破棄、パスワードのリセットなどの操作を行わないでください。
- 移行先がCVMイメージの場合、移行開始後にアカウント下に`do_not_delete_csm_instance`という名前のリレーインスタンスが作成されます。移行が完了して、今回作成されたリレーインスタンスが自動的に破棄されるまで、リレーインスタンスに対してシステムの再インストール、シャットダウン、破棄、パスワードのリセットなどの操作を行わないでください。
</dx-alert>


### ‍手順4：移行後のチェック[](id:checkAfter)
#### 1. コンソールで移行の進行状況の確認
   移行タスクのステータスが**成功**になると、移行処理が正常に完了したことを示します。下図に示すとおり：
![](https://qcloudimg.tencent-cloud.cn/raw/7beb11db18bd9913b44941dd05f8a4a4.png)
<dx-alert infotype="explain" title="">
- データ転送に必要な時間は、移行元データのサイズ、ネットワーク帯域幅などの要因に左右されます。移行が完了するまでお待ちください。
- 移行タスクの開始後、移行タスクのある行で**一時停止**をクリックすると、移行タスクを停止できます。
- 移行ツールはデータ転送の中断からの再開をサポートしています。タスクの一時停止後、**開始/リトライ**をクリックすると、前回一時停止したポイントから移行を継続できます。
- 移行タスクはデータ転送段階での一時停止のみサポートしています。コンソールでの移行タスク中に**一時停止**をクリックすると、移行ツールはデータ転送段階でデータの転送を一時停止します。
- 移行中に消費時間が長くなりすぎ、今回の移行を中止したい場合は、まず移行タスクを一時停止してから**削除**をクリックすると、今回の移行タスクをキャンセルすることができます。
</dx-alert>

#### 2. 移行後のチェック
 - **移行に失敗した場合**：
-ログファイル（デフォルトでは移行ディレクトリ下のログファイル）に出力されている内容を確認し、操作ガイドまたは[サーバー移行に関するよくあるご質問](https://intl.cloud.tencent.com/document/product/213/32395)ドキュメントを参照し、問題のトラブルシューティングを行ってください。問題を解決した後、移行タスクの操作列で**開始/リトライ**をクリックすると、移行タスクを再開できます。
 - **移行に成功した場合**：
移行先がCVMの場合は、移行先CVMが正常に起動できるか、移行先CVMのデータが移行元サーバーと一致しているか、ネットワークが正常か、他のシステムサービスが正常かなどを確認してください。
移行先がCVMイメージの場合は、移行タスクのある行の**CVMイメージID**をクリックし、[CVMイメージページ](https://console.cloud.tencent.com/cvm/image/index)に進むとこのイメージの情報を確認でき、このイメージを使用してCVMインスタンスを作成することができます。
</dx-alert>
ご質問がある場合や移行エラーが発生した場合は、<a href="https://intl.cloud.tencent.com/document/product/213/32395">サービス移行に関するFAQ</a> を参照するか、<a href="https://intl.cloud.tencent.com/document/product/213/34837">お問い合わせ</a>ください。
