ここでは、CVMコンソールのオンラインマイグレーション機能によって、サーバーのオンラインマイグレーションを行う方法についてご紹介します。


## マイグレーションフロー
オンラインマイグレーションのプロセスは、下図のとおりです：
![](https://qcloudimg.tencent-cloud.cn/raw/0e290646e08b6af1b509ce324ea6e096.png)

[](id:prerequisites)
## 準備事項

- Tencent Cloudアカウントをすでに持っていることが必要です。
- サブアカウントを使用してコンソールによる移行を行う場合は、ルートアカウントを使用して[CAMコンソール](https://console.cloud.tencent.com/cam/policy)にログインし、サブアカウントに`QcloudCSMFullAccess` および `QcloudCVMFullAccess` 権限を付与する必要があります。
- [APIキー管理](https://console.cloud.tencent.com/cam/capi)ページで`SecretId`および`SecretKey`を作成し、取得します。
- 移行ツール圧縮パッケージをダウンロードするには、[ここ](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip) をクリックしてください。
- 移行中に既存のアプリケーションへの影響を回避するために、ソースサーバーのアプリケーションを一時停止することをお勧めします。
- マイグレーション前に、次の方式でデータをバックアップすることをお勧めします。
   - 移行元サーバー：ソースサーバーのスナップショット機能などの方式を選択してデータをバックアップできます。
   - 移行先CVM： [スナップショットの作成](https://intl.cloud.tencent.com/document/product/362/5755) などの方式を選択して、移行先CVMのデータをバックアップできます。

## 移行手順


### マイグレーション前の確認

マイグレーション前に、実際の状況に応じて確認を行う必要があります。確認する内容は下表のとおりです。
 - 移行先がCVMの場合は、移行元サーバーと移行先CVMを確認する必要があります。
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
		Tokenを使用する場合があります。現在のシステム時間が正確であることを確認してください。</li>
	  </ol>
	</td>
 </tr>
  <tr>
	<th>Windows移行元サーバー</th>
	<td>
	  <ol style="margin: 0;">
		<li>Virtioをチェックまたはインストールします。操作の詳細については 
		<a href="https://intl.cloud.tencent.com/document/product/213/17815">WindowsでのVirtioドライバーの確認</a>をご参照ください。</li>
		<li>（オプション）Cloudbase-Initのチェックとインストールについての詳細は<a href="https://intl.cloud.tencent.com/document/product/213/32364"> Windows OSのCloudbase-Initのインストール</a>をご参照ください。移行前に移行元サーバーでインストールすることも、移行後にターゲットインスタンスでインストールすることもできます：<br>移行前にインストールする場合，移行後にネットワークの設定、アクティベーションなどの初期化操作が自動的に行われます。<br>移行前にインストールしていない場合、<a href="https://intl.cloud.tencent.com/document/product/213/32496">VNCを使用してインスタンスにログインし</a>、ネットワーク設定を手動設定する必要があります。</li>
	  </ol>
	</td>
  </tr>
  <tr>
	<th style="width: 15%;">移行先CVM（オプション）</th>
	<td>
	  <ol style="margin: 0;">
		<li>
		ストレージ容量：移行先CVMのクラウドディスク（システムディスクとデータディスクを含む）には、移行元サーバーから移行されたデータを保存するための十分な容量がある必要があります。</li>
		<li>セキュリティグループ：セキュリティグループでポート80、443、および3389をオープンします。</li>
		<li>
		帯域幅設定：マイグレーションをより迅速に行えるようにするため、できる限り両側の帯域幅を広くすることをお勧めします。マイグレーション中にはデータ量とほぼ同等のトラフィック消費が発生する場合があります。必要に応じ、事前にネットワーク課金モデルの調整を行ってください。</li>
<li>
		ネットワーク設定：移行元または移行先サーバーにIPv6のみがあり、IPv4がない場合、<a href="https://intl.cloud.tencent.com/document/product/213/44340">client.jsonファイルのパラメータ説明</a>をご参照ください。</li>
	  </ol>
	</td>
  </tr>
</table>


<dx-alert infotype="explain" title="">
- `sudo ./go2tencentcloud_x64 --check`などのツールコマンドを使用して、移行元サーバーを自動的にチェックできます。
- go2tencentcloudマイグレーションツールは、実行を開始すると、デフォルトで自動的にチェックします。このチェックをスキップして強制的に移行する場合は、client.json ファイルの`Client.Extra.IgnoreCheck`フィールドの値を`true`に設定してください。
</dx-alert>


[](id:registrationSource)
### 移行元の登録
#### 移行ツールによる移行元のインポート
<dx-tabs>
::: Linuxサーバー
1. 移行ツールgo2tencentcloud.zipを移行元サーバーに[ダウンロード](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip)またはアップロードし、次のコマンドを実行して、対応するディレクトリに進みます。
   1. 次のコマンドを順に実行し、go2tencentcloud.zipを解凍してディレクトリに進みます。
```shellsession
wget https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip
```
```shellsession
unzip go2tencentcloud.zip
```
```shellsession
cd go2tencentcloud/go2tencentcloud-linux
```
   1. 次のコマンドを順に実行し、go2tencentcloud-linux.zipを解凍してディレクトリに進みます。
```shellsession
unzip go2tencentcloud-linux.zip
```
```shellsession
cd go2tencentcloud-linux
```
<dx-alert infotype="explain" title="">
`go2tencentcloud`ディレクトリ下のファイルは移行されません。移行が必要なファイルをこのディレクトリ下に置かないでください。
</dx-alert>
2. （オプション）移行元サーバー上でマイグレーション不要のファイルまたはディレクトリを削除します。
Linux移行元サーバーにマイグレーション不要のファイルまたはディレクトリが存在する場合は、ファイルまたはディレクトリを[rsync_excludes_linux.txtファイル](https://intl.cloud.tencent.com/document/product/213/44340)に追加することができます。
3. 移行元をインポートします。
   1. 例えば、64ビットのLinux移行元サーバーで、root権限を指定して次のコマンドを実行し、ツールを実行します。
```shellsession
chmod +x go2tencentcloud_x64
```
```shellsession
sudo ./go2tencentcloud_x64
```
   2. 下図のように、[準備事項](#prerequisites)で取得したアカウントのAPIアクセスキーの`SecretId`および`SecretKey`を表示に従って入力し、**Enter**を押します。
![](https://qcloudimg.tencent-cloud.cn/raw/38ff9f9d8c143a4cb0df39cbeaf18713.png)
マイグレーションツールのインターフェースに次のようなメッセージが表示された場合、移行元のコンソールへのインポートは成功しており、コンソールで移行元を確認できます。
<img src="https://qcloudimg.tencent-cloud.cn/raw/f9cf0fd99504aba51ebf82b0cab250b8.png"/>
:::

::: Windowsサーバー
1. 移行ツールgo2tencentcloud.zipを移行元サーバーにダウンロードまたはアップロードします。この圧縮ファイルを解凍してgo2tencentcloudフォルダーを入手します。go2tencentクラウドウィンドウを開き、下図に示すディレクトリを入手します。
![](https://qcloudimg.tencent-cloud.cn/raw/3f2c9881d9c5323a14d096d0811814cd.png)    
2. 以下の方法でgo2tencentcloud_x64.exeを実行します。
	- 方法1：右クリックして管理者権限でgo2tencentcloud_x64.exeを実行し、ポップアップしたダイアログにSecretId、SecretKeyを入力します。
	- 方法2：管理者権限でcmdまたはpowershelコマンドラインを起動し、cd /d "go2tencentcloud_x64.exeが所在するディレクトリの絶対パス"を入力して、 go2tencentcloud_x64.exeを実行します。
3. ポップアップしたダイアログにTencent CloudのAPIキー（SecretIdとSecretKey）を入力します。
![](https://qcloudimg.tencent-cloud.cn/raw/b7af60919e710d7d148e791124fce1a0.png) ![](https://qcloudimg.tencent-cloud.cn/raw/8494a126134389796be195ccd268e03a.png)       

3. 移行ツールのUI画面に下図のようなメッセージが表示された場合、移行元がすでにコンソールにインポートされています。コンソールで移行元を確認できます。
![](https://qcloudimg.tencent-cloud.cn/raw/5ecd29f96415d0cb090fe165909272be.png)
:::
</dx-tabs>

## コンソールでの移行元の確認
<a href="https://console.cloud.tencent.com/cvm/csm/online?rid=1">オンラインマイグレーションコンソール</a>にログインすると、インポート済みの移行元を確認できます。ステータスは「オンライン」となっています。下図に示すとおりです：
<img src="https://qcloudimg.tencent-cloud.cn/raw/11b1e6cada0384dae292e89378629ddc.png"/>
Import source server successfullyと表示されない場合は、移行元のインポートに失敗しています。ログ（デフォルトではマイグレーションツールディレクトリ下のlogs/logファイル）を確認して問題を解決した後、再度マイグレーションツールを実行して移行元をインポートすることができます。

>! 移行元を正常にインポートした後、移行タスクの実行が完了するまで、インスタンス内の移行ツールを停止しないでください。停止すると、移行元がオフラインになり、移行タスクを完了できません。


### 移行タスクの作成と起動

1. 移行タスクの作成
[オンラインマイグレーションコンソール](https://console.cloud.tencent.com/cvm/csm/online?rid=1)にログインし、対象の移行元がある行の右側の**移行タスク作成**をクリックします。ポップアップされた「移行タスク作成」ウィンドウで、次の情報を参照して設定を行います。下図に示します。
![](https://qcloudimg.tencent-cloud.cn/raw/63c9481797c861890a2ea9ca37c4f272.png)
[](id:jobSettings)移行タスクの詳細設定の説明は下表のとおりです：
 - **基本オプション**：
<table>
<thead>
<tr>
<th width="18%">設定オプション</th>
<th width="10%">入力必須かどうか</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr>
<td>移行先リージョン</td>
<td>はい</td>
  <td>移行元サーバーを移行するTencent Cloudリージョンです。リージョンについては<a href="https://intl.cloud.tencent.com/document/product/213/6091">リージョンとアベイラビリティーゾーン</a>をご参照ください。</td>
</tr>
<tr>
<td>タスク名</td>
<td>はい</td>
<td>移行タスクの名称です。</td>
</tr>
<tr>
<td>タスク説明</td>
<td>いいえ</td>
<td>移行タスクの説明です。</td>
</tr>
<tr>
<td>移行先タイプ</td>
<td>はい</td>
<td>
  移行元を移行するTencent Cloudの移行先タイプを設定します。
    <ul>
    <li><b>CVMイメージ</b>：移行タスクの完了後、移行元のTencent Cloudイメージが移行先に生成されます。
      <br>イメージ名：移行元に生成した移行先のTencent Cloudイメージの名称です。イメージ名が移行先のリージョンで重複する場合は、移行タスクが自動的にタスクIDをイメージ名に追加します。
    </li>
    <li><b>CVMインスタンス</b>：移行先リージョンのCVMインスタンス1基を移行先として選択します。
      <br>移行先インスタンス：移行先のCVMのOSはできる限り移行元サーバーのOSタイプと同じにすることをお勧めします。例えば、CentOS 7システムの移行元サーバーのマイグレーションの場合は、CentOS 7システムのCVMを移行先として選択してください。
    </li>
  </ul>
</td>
</tr>
<tr>
<tr>
<td>ネットワークモード</td>
<td>はい</td>
<td>
  転送データを移行するときに使用するネットワークタイプを設定します。
    <ul>
    <li><b>パブリックネットワーク転送</b>：移行先のCVMまたはトランジットインスタンスに転送データを移行するときに、パブリックネットワークを使用して送信します。
    </li>
    <li><b>プライベートネットワーク転送</b>：移行先のCVMまたはトランジットインスタンスに転送データを移行するときに、プライベートネットワークを使用して送信します。詳細については、 <a href="https://intl.cloud.tencent.com/document/product/213/44341">プライベートネットワークマイグレーションのチュートリアル</a>をご参照ください。
      <br>Virtual Private Cloud(VPC)：CVMイメージに移行する場合、トランジットインスタンスはVPCに作成されます。
      <br>サブネット：CVMイメージに移行する場合、トランジットインスタンスはサブネットに作成されます。
    </li>
  </ul>
</td>
</tr>	
<tr>
<td rowspan='2'>移行方法</td>
<td rowspan='2'>はい</td>
<td>
  Linuxブロックレベル移行データの移行方法の種類を設定します。
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
<b>Windowsブロックレベルの移行</b>：移行の粒度はディスクのロジックストレージユニットの「ブロック」レベルであり、Windowsの移行では、互換性が高く、転送効率が高いブロックレベルの移行がデフォルトで採用されています。
  </ul>
</td>
</tr>	
<tr>
<td>増分同期の構成</td>
<td>いいえ</td>
<td>増分同期時間をカスタマイズ設定し、データを継続的に同期し、移行の配信時間を柔軟に制御します。
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
 - **高度な構成（オプション）**：
<table>
<thead>
<tr>
<th width="18%">設定オプション</th>
<th width="10%">入力必須かどうか</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr>
<td>転送制限（KB/s）</td>
<td>いいえ</td>  
<td>移行プロセスでは、データ転送の帯域幅の上限が制限されており、単位はKB/s、範囲は[0, 25600]で、デフォルトでは速度は無制限です。</td>
</tr>
<tr>
<td>Checksum検証</td>
<td>いいえ</td>  
<td>有効にすると、データの整合性の検証を強化できますが、転送速度は遅くなる場合があります。現在、Windowsマイグレーションはこのオプションをサポートしていません。</td>
</tr>
</tbody></table>
2. 移行タスクを起動します。
<dx-alert infotype="explain" title="">
実行を予約するタスクはこの手順をスキップすることができます。予約した実行時間になると、移行タスクは自動的に実行を開始します。
</dx-alert>
下図に示すように、移行タスクを作成すると、<b>移行タスク</b>タブをクリックして移行タスクを確認できるようになります。
<img src="https://qcloudimg.tencent-cloud.cn/raw/7d2447ea7e6f348d779e41ad2c08fd93.png"/>
下図に示すように、タスクのある行の右側の<b>開始/リトライ</b>をクリックすると、ポップアップ表示された確認ウィンドウで<b>確定</b>をクリックして、移行タスクを開始できます。このとき、タスクのステータスは「移行中」に変わります：
<img src="https://qcloudimg.tencent-cloud.cn/raw/bcbad8eb9a093814f18ff82aab7bc308.png"/>
<dx-alert infotype="notice" title="">
- 移行先がCVMの場合、マイグレーションの開始後、移行先CVMはマイグレーションモードに入ります。マイグレーションが完了してマイグレーションモードを終了するまで、移行先CVMに対してシステムの再インストール、シャットダウン、破棄、パスワードのリセットなどの操作を行わないでください。
- 移行先がCVMイメージの場合、マイグレーションの開始後、アカウント下に`do_not_delete_csm_instance`という名前の中継インスタンスが作成されます。マイグレーションが完了して、今回作成された中継インスタンスが自動的に破棄されるまで、中継インスタンスに対してシステムの再インストール、シャットダウン、破棄、パスワードのリセットなどの操作を行わないでください。
</dx-alert>


### 移行タスク終了待機


下図のように、移行タスクのステータスが「成功」となれば、移行が完了したことを表します。
![](https://qcloudimg.tencent-cloud.cn/raw/7beb11db18bd9913b44941dd05f8a4a4.png)

<dx-alert infotype="explain" title="">
- データ転送の消費時間は、移行元データのサイズ、ネットワーク帯域幅などの要因に左右されます。マイグレーションフローが完了するまでお待ちください。
- 移行タスクの開始後、移行タスクのある行で**一時停止**をクリックすると、移行タスクを停止できます。
- マイグレーションツールはデータ転送の中断からの再開をサポートしています。タスクの一時停止後、**開始/リトライ**をクリックすると、前回一時停止したポイントから移行を継続できます。
- 移行タスクはデータ転送段階での一時停止のみサポートしています。コンソールでの移行タスク中に**一時停止**をクリックすると、マイグレーションツールはデータ転送段階でデータの転送を一時停止します。
- 移行中に消費時間が長くなりすぎ、今回のマイグレーションを中止したい場合は、まず移行タスクを一時停止してから**削除**をクリックすると、今回の移行タスクをキャンセルすることができます。
</dx-alert>

### マイグレーション後の確認[](id:checkAfter)

- **マイグレーション結果の失敗**：
ログファイル（デフォルトではマイグレーションツールディレクトリ下のログファイル）からのエラーメッセージ出力、ガイドラインドキュメントまたは[サービスマイグレーションに関するよくあるご質問](https://intl.cloud.tencent.com/document/product/213/32395)を確認し、トラブルシューティングと問題の修正を行ってください。修正後、移行タスク操作列で**開始/リトライ**をクリックすると、移行タスクを再開できます。
- **マイグレーション結果の成功**：
 - 移行先がCVMの場合は、移行先CVMが正常に起動できるか、移行先CVMのデータが移行元サーバーと一致しているか、ネットワークが正常か、他のシステムサービスが正常かなどを確認してください。
 - 移行先がCVMイメージの場合は、移行タスクのある行の「CVMイメージID」をクリックし、[CVMイメージページ](https://console.cloud.tencent.com/cvm/image/index)に進むとこのイメージの情報を確認でき、このイメージを使用してCVMを作成することができます。

ご不明な点やマイグレーションの異常など、ご質問がありましたら、[サービスマイグレーションに関するよくあるご質問](https://intl.cloud.tencent.com/document/product/213/32395)をご参照いただくか、または[お問い合わせ](https://intl.cloud.tencent.com/document/product/213/34837)から解消してください。



