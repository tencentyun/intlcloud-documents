ここでは、CVMコンソールのオンライン移行機能を使用し、サーバーのオンライン移行を実行する方法についてご紹介します。

## 移行フロー
オンライン移行の処理フローは下図のとおりです：
![](https://qcloudimg.tencent-cloud.cn/raw/0e290646e08b6af1b509ce324ea6e096.png)
[](id:prerequisites)

## 準備事項
- [APIキー管理](https://console.cloud.tencent.com/cam/capi)ページで`SecretId`と`SecretKey`を作成して取得します。
- 移行時に既存のアプリケーションに影響しないように、サーバー情のアプリケーションを一時停止し、データをバックアップすることをお勧めします。
 - 移行元サーバー：ソースサーバーのスナップショット機能などを使用し、データをバックアップできます。
 - 移行先CVM： [スナップショットの作成](https://intl.cloud.tencent.com/document/product/362/5755) などを使用し、移行先CVMのデータをバックアップできます。
-  サブアカウントを使用しコンソールで移行を実行する場合、ルートアカウントで[CAMコンソール](https://console.cloud.tencent.com/cam/policy)にログインし、サブアカウントにQcloudCSMFullAccessとQcloudCVMFullAccess権限を付与する必要があります。

## 移行手順
### ステップ1：移行前のチェック

移行前に、実際の状況に応じてチェックしてください。チェック内容は下表のとおりです：
 - 移行先がCVMの場合、移行元サーバーと移行先CVMをチェックします。
 - 移行先がCVMイメージの場合、移行元サーバーのみをチェックします。

<table>
  <tr>
	<th>移行元サーバーがLinuxの場合</th>
	<td>
	  <ol style="margin: 0;">
		<li>Virtioをチェックまたはインストールします。操作の詳細については 
		<a href="https://intl.cloud.tencent.com/document/product/213/9929">LinuxでのVirtioドライバーの確認</a>をご参照ください。</li>
		<li>実行 
		<code>which rsync</code>コマンドで、rsyncがインストールされているかをチェックします。インストールされていない場合、<a href="https://intl.cloud.tencent.com/document/product/213/32395#installRsync">Rsyncのインストール方法</a>を参照してインストールしてください。</li>
		<li>SELinuxが有効になっているかをチェックします。SELinuxが有効になっている場合、<a href="https://intl.cloud.tencent.com/document/product/213/32395#closeSELinux">SELinuxを無効にする方法</a>を参照して無効にしてください。</li>
		<li>Tencent Cloud APIに移行リクエストを送信すると、Tencent Cloud APIは現在のUNIX時間を使用し生成された
		Tokenをチェックするため、現在のシステム時間が正確であることを確認してください。</li>
	  </ol>
	</td>
 </tr>
  <tr>
	<th>移行元サーバーがWindowsの場合</th>
	<td>
	  <ol style="margin: 0;">
		<li>Virtioをチェックまたはインストールします。操作の詳細については 
		<a href="https://intl.cloud.tencent.com/document/product/213/17815">WindowsでのVirtioドライバーの確認</a>をご参照ください。</li>
		<li>（オプション）Cloudbase-Initのチェックとインストール。詳細については、<a href="https://intl.cloud.tencent.com/document/product/213/32364">Windows OSのCloudbase-Initのインストール</a>をご参照ください。移行前に移行元サーバーにインストールすることも、移行後にターゲットインスタンスにインストールすることもできます。<br>移行前にインストールする場合、移行後にネットワークの設定、アクティベーションなどの初期化処理が自動的に実行されます。<br>移行前にインストールしていない場合、<a href="https://intl.cloud.tencent.com/document/product/213/32496">VNCを使用してインスタンスにログイン</a>し、ネットワークの設定を手動で設定することがあります。</li>
	  </ol>
	</td>
  </tr>
  <tr>
	<th style="width: 15%;">移行先CVM（オプション）</th>
	<td>
	  <ol style="margin: 0;">
		<li>
		ストレージ容量：移行先CVMのクラウドディスク（システムディスクとデータディスクを含む）に、移行元サーバーから移行されたデータを保存するための十分な容量を確保する必要があります。</li>
		<li>セキュリティグループ：セキュリティグループでポート80、443、および3389を開放します。</li>
		<li>
		帯域幅設定：移行をより迅速に実行するために、できる限り両側の帯域幅を大きくすることをお勧めします。移行中にデータ量とほぼ同等のトラフィック消費が発生します。必要に応じて、事前にネットワーク課金モデルを調整してください。</li>
<li>
		ネットワーク設定：移行元サーバーまたは移行先サーバーにIPv4がなく、IPv6のみがある場合、<a href="https://intl.cloud.tencent.com/document/product/213/44340">client.jsonファイルのパラメータ説明</a>をご参照ください。</li>
	  </ol>
	</td>
  </tr>
</table>


<dx-alert infotype="explain" title="">
-`sudo ./go2tencentcloud_x64 --check`などのコマンドを使用して、移行元サーバーを自動的にチェックできます。
- go2tencentcloud移行ツールは、実行を開始すると、デフォルトで自動的にチェックします。このチェックをスキップして強制的に移行する場合、client.json ファイルの`Client.Extra.IgnoreCheck`フィールドに`true`を設定してください。
</dx-alert>

[](id:registrationSource)
### ステップ2：移行元のインポート
#### 移行ツールによる移行元のインポート
<dx-tabs>
::: Linuxサーバー
1. 移行する移行元サーバーで以下のコマンドを実行し、移行ツールgo2tencentcloud.zipを[ダウンロード](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip)してディレクトリに進みます。
  - 以下のコマンドを順に実行し、go2tencentcloud.zipを[ダウンロード](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip)し、解凍してディレクトリに進みます。
```shellsession
wget https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip
```
```shellsession
unzip go2tencentcloud.zip
```
```shellsession
cd go2tencentcloud
```
- 以下のコマンドを順に実行し、go2tencentcloud-linux.zipを解凍してディレクトリに進みます。

```shellsession
unzip go2tencentcloud-linux.zip
```
```shellsession
cd go2tencentcloud-linux
```
<dx-alert infotype="explain" title="">
`go2tencentcloud`ディレクトリ配下のファイルが移行されないため、移行するファイルをこのディレクトリに置かないでください。
</dx-alert>
2. （オプション）移行元サーバー上の移行しないファイルまたはディレクトリを排除します。
Linux移行元サーバーに移行しないファイルまたはディレクトリが存在する場合、ファイルまたはディレクトリを[rsync_excludes_linux.txtファイル](https://intl.cloud.tencent.com/document/product/213/44340)に追加してください。
3. 移行元をインポートします。
  -  64ビットのLinux移行元サーバーを例として説明します。root権限で以下のコマンドを順に実行し、ツールを実行します。
```shellsession
chmod +x go2tencentcloud_x64
```
```shellsession
sudo ./go2tencentcloud_x64
```
  - 下図のように、[準備事項](#prerequisites)で取得したアカウントのAPIアクセスキーの`SecretId`および`SecretKey`を入力し、**Enter**を押します。
![](https://qcloudimg.tencent-cloud.cn/raw/38ff9f9d8c143a4cb0df39cbeaf18713.png)
移行ツールのUI画面に次のようなメッセージが表示されると、移行元がコンソールに正常にインポートされ、コンソールで移行元を確認できるようになります。
<img src="https://qcloudimg.tencent-cloud.cn/raw/f9cf0fd99504aba51ebf82b0cab250b8.png"/>
:::

::: Windowsサーバー
1. 移行ツールgo2tencentcloud.zipを移行元サーバーに[ダウンロード](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip)またはアップロードし、解凍してgo2tencentcloudフォルダーを取得します。このフォルダーからgo2tencentcloud-windows.zipを取得して解凍すると、下図に示すディレクトリを入手できます：
![](https://qcloudimg.tencent-cloud.cn/raw/3f2c9881d9c5323a14d096d0811814cd.png)    
2. 以下の方法でgo2tencentcloud_x64.exeを実行します。
	- 方法1：右クリックして管理者権限でgo2tencentcloud_x64.exeを実行し、ポップアップしたダイアログにSecretId、SecretKeyを入力します。
	- 方法2：管理者権限でcmdまたはpowershelコマンドラインを起動し、cd /d "go2tencentcloud_x64.exeが所在するディレクトリの絶対パス"を入力して、go2tencentcloud_x64.exeを実行します。
3. ポップアップしたダイアログにTencent CloudのAPIキー（SecretIdとSecretKey）を入力します。
![](https://qcloudimg.tencent-cloud.cn/raw/b7af60919e710d7d148e791124fce1a0.png) ![](https://qcloudimg.tencent-cloud.cn/raw/8494a126134389796be195ccd268e03a.png)       

3. 移行ツールのUI画面に下図のようなメッセージが表示されると、移行元がコンソールに正常にインポートされ、コンソールで移行元を確認できるようになります。
![](https://qcloudimg.tencent-cloud.cn/raw/5ecd29f96415d0cb090fe165909272be.png)
:::
</dx-tabs>
<dx-alert infotype="explain" title="">
Import source server successfullyが表示されなかった場合、移行元のインポートに失敗しています。ログ（デフォルトでは移行ツールディレクトリ配下のlogs/logファイル）を確認して問題を解決した後、もう一度移行ツールを実行して移行元をインポートしてください。
</dx-alert>

## コンソールでの移行元の確認
<a href="https://console.cloud.tencent.com/cvm/csm/online?rid=1">オンライン移行コンソール</a>にログインすると、インポートされた移行元を確認できます。下図に示すように、ステータスは「オンライン」となっています：
<img src="https://qcloudimg.tencent-cloud.cn/raw/11b1e6cada0384dae292e89378629ddc.png"/>

>! 移行元を正常にインポートした後、移行タスクの実行が完了するまで、インスタンス内の移行ツールを停止しないでください。停止すると、移行元がオフラインになり、移行タスクを完了できません。


### ステップ3：移行タスクの作成と起動

1. 移行タスクの作成
[オンライン移行コンソール](https://console.cloud.tencent.com/cvm/csm/online?rid=1)にログインし、移行元がある行の右側の**移行タスク作成**をクリックします。ポップアップした「移行タスク作成」ウィンドウで、下図に示すように、以下を参照して設定してください：
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
  <td>移行元サーバーを移行するTencent Cloudリージョンです。リージョンについては、<a href="https://intl.cloud.tencent.com/document/product/213/6091">リージョンとアベイラビリティーゾーン</a>をご参照ください。</td>
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
    <li><b>CVMイメージ</b>：移行タスクの実行が完了した後、移行元のTencent Cloudイメージが移行先に生成されます。
      <br>イメージ名：移行先に生成した移行元のTencent Cloudイメージの名称です。イメージ名が移行先のリージョンにすでに存在している場合、移行タスクは自動的にタスクIDをイメージ名に追加します。
    </li>
    <li><b>CVMインスタンス</b>：移行先として移行先リージョンにおけるCVMインスタンスを1台を選択します。
      <br>移行先インスタンス：移行先のCVMのOSはできる限り移行元サーバーのOSタイプと同じにすることをお勧めします。例えば、移行元サーバーのOSがCentOS 7の場合、移行先としてOSがCentOS 7のCVMを選択してください。
    </li>
  </ul>
</td>
</tr>
<tr>
<tr>
<td>ネットワークモード</td>
<td>はい</td>
<td>
  移行時にデータの転送に使用するネットワークタイプを設定します。
    <ul>
    <li><b>パブリックネットワーク転送</b>：移行時に、パブリックネットワークを使用してデータを移行先のCVMまたは中間インスタンスに転送します。
    </li>
    <li><b>プライベートネットワーク転送</b>：移行時に、プライベートネットワークを使用してデータを移行先のCVMまたは中間インスタンスに転送します。<a href="https://intl.cloud.tencent.com/document/product/213/44341">プライベートネットワークによる移行手引書</a>をご参照ください。
      <br>Virtual Private Cloud（VPC）：CVMイメージに移行する場合、中間インスタンスはVPCに作成されます。
      <br>サブネット：CVMイメージに移行する場合、中間インスタンスはサブネットに作成されます。
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
    <li><b>Linuxファイルレベルの移行</b>：移行はファイル単位で行われ、互換性が良く、転送効率が比較的低いです。
    </li>
    <li><b>Linuxブロックレベルの移行</b>：移行はディスクのロジックストレージユニットである「ブロック」単位で行われ、転送効率が高く、互換性が比較的低いです。
    </li>
  </ul>
</td>
</tr>	
<tr>
<td>
<b>Windowsブロックレベルの移行</b>：移行はディスクのロジックストレージユニットである「ブロック」単位で行われます。転送効率が高く、互換性が比較的低いです。Windows では、デフォルトでブロックレベルの移行を実行します。
  </ul>
</td>
</tr>	
<tr>
<td>増分同期の設定</td>
<td>いいえ</td>
<td>増分同期時間を自由に設定し、データを継続的に同期を取り、移行の交代時間を柔軟に制御します。
	<ul>
		<li><b>無効にした場合</b>：移行ツールは増分移行を自動的に識別して実行します。通常1回実行されます。</li>
		<li><b>有効にした場合</b>：増分同期の実行時間を自由に設定できます。ツールは増分データをTencent Cloudに継続的に同期を取ります。タスクリストで増分同期を手動で停止することができます。</li>
	</ul>
</td>
</tr>
<td>予約実行時間</td>
<td>いいえ</td> 
<td>移行タスクを作成後に、設定した時間になると、移行タスクが自動的に実行を開始します。予約実行時間は現在時刻の<b>10</b>分後から設定できます。</td>
</tr>
</tbody></table>
 - **高度な設定（オプション）**：
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
<td>移行中のデータ転送の帯域幅上限であり、単位はKB/s、範囲は[0, 25600]です。デフォルトでは上限なしとします。現在、Windowsでの移行では、このオプションはサポートされていません。</td>
</tr>
<tr>
<td>Checksum検証</td>
<td>いいえ</td>  
<td>有効にすると、データ整合性の検証を強化できるが、転送速度が遅くなることがあります。現在、Windowsでの移行では、このオプションはサポートされていません。</td>
</tr>
</tbody></table>
2. 移行タスクを起動します。
<dx-alert infotype="explain" title="">
実行を予約したタスクはこの手順をスキップすることができます。予約した実行時間になると、移行タスクは自動的に実行を開始します。
</dx-alert>
下図に示すように、移行タスクを作成すると、<b>移行タスク</b>タブをクリックして移行タスクを確認できるようになります。
<img src="https://qcloudimg.tencent-cloud.cn/raw/7d2447ea7e6f348d779e41ad2c08fd93.png"/>
下図に示すように、タスクのある行の右側の<b>開始/リトライ</b>をクリックし、ポップアップした確認ウィンドウで<b>OK</b>をクリックすると、移行タスクが実行を開始し。このとき、タスクのステータスは「移行中」に変わります。
<img src="https://qcloudimg.tencent-cloud.cn/raw/bcbad8eb9a093814f18ff82aab7bc308.png"/>
<dx-alert infotype="notice" title="">
- 移行先がCVMの場合、移行開始後に、移行先のCVMは移行モードに入ります。移行が完了して移行モードを終了するまで、移行先のCVMに対して、OSの再インストール、シャットダウン、廃棄、パスワードのリセットなどの操作を行わないでください。
- 移行先がCVMイメージの場合、移行開始後に、ご利用のアカウント配下に`do_not_delete_csm_instance`という中間インスタンスが作成されます。移行が完了して、システムが今回作成された中間インスタンスを自動的に廃棄するまで、中間インスタンスに対して、OSの再インストール、シャットダウン、廃棄、パスワードのリセットなどの操作を行わないでください。
</dx-alert>

### ステップ4：移行タスクの実行が終了するまで待ちます

下図に示すように、移行タスクのステータスが「成功」になると、移行が完了します。
![](https://qcloudimg.tencent-cloud.cn/raw/7beb11db18bd9913b44941dd05f8a4a4.png)

<dx-alert infotype="explain" title="">
- データ転送にかかる時間は、移行元のデータサイズ、ネットワーク帯域幅などの要因によります。移行処理が完了するまでお待ちください。
- 移行タスク開始後に、移行タスクのある行で**一時停止**をクリックすると、移行タスクを停止できます。
- 移行ツールはデータ転送中の一時停止したところから再開することができます。タスクを一時停止した場合、**開始/リトライ**をクリックすると、一時停止したところから移行を再開できます。
- 移行タスクはデータ転送段階での一時停止のみをサポートします。コンソールの移行タスクで**一時停止**をクリックすると、移行ツールはデータ転送段階でデータの転送を一時停止します。
- 移行に時間がかかり、移行を中止する場合、移行タスクを一時停止して**削除**をクリックすると、実行中の移行タスクをキャンセルできます。
</dx-alert>

### ステップ5：移行後の確認[](id:checkAfter)

- **移行に失敗した場合**：
ログファイル（デフォルトでは移行ツールディレクトリ配下のログファイル）に出力されたエラーメッセージ、ガイドラインドキュメントまたは[サービス移行に関するよくあるご質問](https://intl.cloud.tencent.com/document/product/213/32395)を確認し、トラブルシューティングと問題修正を行ってください。修正後に、移行タスクの操作列で**開始/リトライ**をクリックすると、移行タスクを再開できます。
- **移行に成功した場合**：
 - 移行先がCVMの場合、移行先のCVMを正常に起動できるか、移行先のCVMにおけるデータが移行元サーバーのデータと一致しているか、ネットワークや他のシステムサービスが正常に動作しているかなどを確認してください。
 - 移行先がCVMイメージの場合、移行タスクのある行の「CVMイメージID」をクリックし、[CVMイメージページ](https://console.cloud.tencent.com/cvm/image/index)に進んで、イメージの情報を確認してください。このイメージを使用してCVMを作成することができます。

ご不明な点や移行異常関連のご質問がありましたら、[サービス移行に関するよくあるご質問](https://intl.cloud.tencent.com/document/product/213/32395)をご参照いただくか、[お問い合わせ](https://intl.cloud.tencent.com/document/product/213/34837)に連絡してください。
