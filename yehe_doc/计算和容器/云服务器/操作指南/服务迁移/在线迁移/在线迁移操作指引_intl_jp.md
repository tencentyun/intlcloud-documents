本書では、CVMコンソールのオンライン移行機能を使用し、サーバーのオンライン移行を行う方法を説明します。


## 移行フロー
オンライン移行のプロセスは下図に示すとおりです：
![](https://qcloudimg.tencent-cloud.cn/raw/0e290646e08b6af1b509ce324ea6e096.png)

[](id:prerequisites)
## 準備事項

- Tencent Cloudアカウントをすでに持っていること。
- サブアカウントを使用しコンソールで移行を行う場合、ルートアカウントを使用して[CAMコンソール](https://console.cloud.tencent.com/cam/policy)にログインし、サブアカウントに`QcloudCSMFullAccess` および `QcloudCVMFullAccess` 権限を付与する必要があります。
- [APIキー管理](https://console.cloud.tencent.com/cam/capi)ページで`SecretId`および`SecretKey`を作成して取得します。
- [ダウンロード先](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip) をクリックして、移行ツール圧縮パッケージをダウンロードします。
- 移行中に既存のアプリケーションへの影響を回避するために、移行元サーバーのアプリケーションを一時停止することをお勧めします。
- 移行前に、以下の方法でデータをバックアップすることをお勧めします：
  - 移行元サーバー：移行元サーバーのスナップショット機能などを使用しデータをバックアップできます。
  - 移行先CVM： [スナップショットの作成](https://intl.cloud.tencent.com/document/product/362/5755) などを使用し、移行先CVMのデータをバックアップできます。

## 移行手順


### 移行前の確認

移行前に、必要に応じてチェックしてください。チェック内容は下表のとおりです：
 - 移行先がCVMの場合、移行元サーバーと移行先CVMをチェックします。
 - 移行先がCVMイメージの場合、移行元サーバーのみをチェックします。

<table>
  <tr>
	<th>OSがLinuxの移行元サーバー</th>
	<td>
	  <ol style="margin: 0;">
		<li>Virtioをチェックまたはインストールします。詳細については、 
		<a href="https://intl.cloud.tencent.com/document/product/213/9929">LinuxでのVirtioドライバーの確認</a>をご参照ください。</li>
		<li>    
		<code>which rsync</code>コマンドを実行し、rsyncがインストールされているかをチェックします。インストールされていない場合、<a href="https://intl.cloud.tencent.com/document/product/213/32395#installRsync">Rsyncのインストール方法</a>を参照してインストールしてください。</li>
		<li>SELinuxが有効になっているかをチェックします。SELinuxが有効になっている場合、<a href="https://intl.cloud.tencent.com/document/product/213/32395#closeSELinux">SELinuxを無効化する方法</a>を参照して無効にしてください。</li>
		<li>Tencent Cloud APIに移行リクエストを送信すると、Tencent Cloud APIは現在のUNIX時間をチェックして生成された
		Tokenをチェックするため、現在のシステム時間が正しいであることを確認してください。</li>
	  </ol>
	</td>
 </tr>
  <tr>
	<th>OSがWindowsの移行元サーバー</th>
	<td>
	  <ol style="margin: 0;">
		<li>Virtioをチェックまたはインストールします。詳細については、 
		<a href="https://intl.cloud.tencent.com/document/product/213/17815">WindowsでのVirtioドライバーの確認</a>をご参照ください。</li>
		<li>（オプション）Cloudbase-Initをチェックまたはインストールします。詳細については、<a href="https://intl.cloud.tencent.com/document/product/213/32364"> Windows OSのCloudbase-Initのインストール方法</a>をご参照ください。移行前に移行元サーバーにインストールすることも、移行後に移行先インスタンスにインストールすることもできます。<br>移行前にインストールする場合、移行後にネットワークの設定、アクティブ化などの初期化処理が自動的に行われます。<br>移行前にインストールしていない場合、<a href="https://intl.cloud.tencent.com/document/product/213/32496">VNCを使用してインスタンスにログイン</a>し、ネットワークの設定を手動で変更してください。</li>
	  </ol>
	</td>
  </tr>
  <tr>
	<th style="width: 15%;">移行先CVM（オプション）</th>
	<td>
	  <ol style="margin: 0;">
		<li>
		ストレージ容量：移行先CVMのCBS（システムディスクとデータディスクを含む）には、移行元サーバーから移行されたデータを保存するための十分な容量を確保する必要があります。</li>
		<li>セキュリティグループ：セキュリティグループでは443ポートと80ポートを制限してはなりません。</li>
		<li>
		帯域幅の設定：移行をより迅速に実行するように、できる限り移行元と移行先の帯域幅を大きく設定することをお勧めします。移行中にはデータ量とほぼ同等のトラフィック使用量が発生します。必要に応じ、事前にネットワーク課金モデルの調整を行ってください。</li>
	  </ol>
	</td>
  </tr>
</table>


<dx-alert infotype="explain" title="">
- `sudo ./go2tencentcloud_x64 --check`などのツールコマンドを実行し、移行元サーバーを自動的にチェックできます。
- go2tencentcloud移行ツールは、動作が始まると、デフォルトで自動的にチェックを実行します。このチェックをスキップして強制的に移行する場合、client.json ファイルの`Client.Extra.IgnoreCheck`フィールドに`true`を設定してください。
</dx-alert>


[](id:registrationSource)
### 移行元の登録
#### 移行ツールによる移行元のインポート
<dx-tabs>
::: Linuxサーバー
1. 移行ツールgo2tencentcloud.zipを移行元サーバーにダウンロードまたはアップロードし、以下のコマンドを実行して対応するディレクトリに進みます。
   1. 以下のコマンドを順に実行し、go2tencentcloud.zipを解凍してディレクトリに進みます。
```shellsession
unzip go2tencentcloud.zip
```
```shellsession
cd go2tencentcloud
```
   1. 以下のコマンドを順に実行し、go2tencentcloud-linux.zipを解凍してディレクトリに進みます。
```shellsession
unzip go2tencentcloud-linux.zip
```
```shellsession
cd go2tencentcloud-linux
```
<dx-alert infotype="explain" title="">
`go2tencentcloud`ディレクトリ配下のファイルが移行されないため、移行するファイルをこのディレクトリに置かないでください。
</dx-alert>
2. （オプション）移行元サーバーから移行しないファイルやディレクトリを排除します。
Linux移行元サーバーに移行しないファイルまたはディレクトリが存在する場合、そのファイルやディレクトリを[rsync_excludes_linux.txtファイル](https://intl.cloud.tencent.com/document/product/213/44340)に追加します。
3. 移行元をインポートします。
   1. 以下では、64ビットのLinux移行元サーバーを例として説明します。root権限で以下のコマンドを実行してツールを実行します。
```shellsession
chmod +x go2tencentcloud_x64
```
```shellsession
sudo ./go2tencentcloud_x64
```
   2. 下図に示すように、[準備事項](#prerequisites)で取得したアカウントのAPIアクセスキーの`SecretId`および`SecretKey`を入力し、**Enter**を押します。
![](https://qcloudimg.tencent-cloud.cn/raw/38ff9f9d8c143a4cb0df39cbeaf18713.png)
移行ツールのUI画面に下図のようなメッセージが表示された場合、移行元がすでにコンソールにインポートされています。コンソールで移行元を確認できます。
<img src="https://qcloudimg.tencent-cloud.cn/raw/f9cf0fd99504aba51ebf82b0cab250b8.png"/>
:::

::: Windowsサーバー
1. 移行ツールgo2tencentcloud.zipを移行元サーバーにダウンロードまたはアップロードします。この圧縮ファイルを解凍してgo2tencentcloudフォルダーを入手します。その中のgo2tencentcloud-windows.zipをさらに解凍して、下図に示すディレクトリを入手します。
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
<a href="https://console.cloud.tencent.com/cvm/csm/online?rid=1">オンライン移行コンソール</a>にログインして、インポート済みの移行元を確認できます。下図に示すように、状態は「オンライン」になっています：
<img src="https://qcloudimg.tencent-cloud.cn/raw/11b1e6cada0384dae292e89378629ddc.png"/>
Import source server successfullyが表示されなかった場合、移行元のインポートに失敗しています。ログ（デフォルトでは移行ツールディレクトリ配下のlogs/logファイル）を確認して問題を解決した後、改めて移行ツールを実行して移行元をインポートします。

>! 移行元を正常にインポートした後、移行タスクの実行が完了するまで、インスタンス内の移行ツールを停止しないでください。停止すると、移行元がオフラインになり、移行タスクを完了できません。


### 移行タスクの作成と起動

1. 移行タスクを作成します
下図に示すように、[オンライン移行コンソール](https://console.cloud.tencent.com/cvm/csm/online?rid=1)にログインし、対象となる移行元が所在する行の右側の**移行タスクの作成**をクリックします。ポップアップした「移行タスクの作成」ウィンドウで、以下の情報を参考にして設定を行います：
![](https://qcloudimg.tencent-cloud.cn/raw/63c9481797c861890a2ea9ca37c4f272.png)
[](id:jobSettings)移行タスクの詳細な設定の説明は下表のとおりです：
 - **基本オプション**：
<table>
<thead>
<tr>
<th width="18%">設定オプション</th>
<th width="10%">入力必須か</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr>
<td>移行先リージョン</td>
<td>はい</td>
  <td>移行元サーバーの移行先となるTencent Cloudのリージョンです。リージョンについては、<a href="https://intl.cloud.tencent.com/document/product/213/6091">リージョンとアベイラビリティーゾーン</a>をご参照ください。</td>
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
  移行元をTencent Cloudに移行する移行先のタイプを設定します。
    <ul>
    <li><b>CVMイメージ</b>：移行タスクが実行完了後、移行元のTencent Cloudイメージが移行先に生成されます。
      <br>イメージ名：移行元に対して生成した移行先のTencent Cloudイメージの名称です。イメージ名が移行先のリージョンにおけるイメージ名と重複する場合、移行タスクは自動的にタスクIDをイメージ名に追加します。
    </li>
    <li><b>CVMインスタンス</b>：移行先として移行先リージョンにおけるCVMインスタンスを1つ選択します。
      <br>移行先インスタンス：移行先のCVMのOSはできる限り移行元サーバーのOSタイプと同じにすることをお勧めします。例えば、OSがCentOS 7の移行元サーバーを移行する場合、OSがCentOS 7のCVMを移行先として選択してください。
    </li>
  </ul>
</td>
</tr>
<tr>
<td>予約実行時間</td>
<td>いいえ</td> 
  <td>移行タスクを作成後、設定した時間になると、移行タスクは自動的に実行を開始します。予約実行時間は現在時刻の<b>10</b>分後以降に設定できます。</td>
</tr>
</tbody></table>
 - **高度な設定（オプション）**：
<table>
<thead>
<tr>
<th width="18%">設定オプション</th>
<th width="10%">入力必須か</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr>
<td>ネットワークモード</td>
<td>いいえ</td>
<td>
  移行中にデータを転送する時に使用するネットワークのタイプを設定します。
    <ul>
    <li><b>パブリックネットワーク転送</b>：移行中にデータを移行先CVMまたは中継インスタンスに転送する時に、パブリックネットワークを使用します。
    </li>
    <li><b>プライベートネットワーク転送</b>：移行中にデータを移行先のCVMまたは中継インスタンスに転送する時に、プライベートネットワークを使用します。詳細については、 <a href="https://intl.cloud.tencent.com/document/product/213/44341">プライベートネットワーク移行手引書</a>をご参照ください。
      <br>Virtual Private Cloud (VPC)：CVMイメージに移行する場合、中継インスタンスはVPCに作成されます。
      <br>サブネット：CVMイメージに移行する場合、中継インスタンスはサブネットに作成されます。
    </li>
  </ul>
</td>
</tr>	
<tr>
<td>転送制限(KB/s)</td>
<td>いいえ</td>  
<td>移行中のデータ転送時の帯域幅の上限です。単位はKB/s、範囲は[0, 25600]で、デフォルトでは速度は無制限です。Windowsに関係する移行では、このオプションはサポートされていません。</td>
</tr>
<tr>
<td>Checksum検証</td>
<td>いいえ</td>  
<td>有効にすると、データ整合性の検証を強化できるが、転送速度が落ちる場合があります。Windowsに関係する移行では、このオプションはサポートされていません。</td>
</tr>
</tbody></table>
2. 移行タスクを起動します。
<dx-alert infotype="explain" title="">
実行を予約したタスクはこのステップをスキップできます。予約した実行時間になると、移行タスクは自動的に実行を開始します。
</dx-alert>
下図に示すように、移行タスクを作成した後、<b>移行タスク</b>タブをクリックして移行タスクを確認できます。
<img src="https://qcloudimg.tencent-cloud.cn/raw/7d2447ea7e6f348d779e41ad2c08fd93.png"/>
下図に示すように、タスクが所在する行の右側の<b>開始/リトライ</b>をクリックし、ポップアップした確認ウィンドウで<b>OK</b>をクリックすると、移行タスクが開始します。この時、タスクの状態は「移行中」に変わります。
<img src="https://qcloudimg.tencent-cloud.cn/raw/bcbad8eb9a093814f18ff82aab7bc308.png"/>
<dx-alert infotype="notice" title="">
- 移行先がCVMの場合、移行開始後に、移行先CVMが移行モードに入ります。移行が完了して移行モードが終了するまで、移行先CVMに対してOSの再インストール、シャットダウン、破棄、パスワードのリセットなどの操作を行わないでください。
- 移行先がCVMイメージの場合、移行開始後に、アカウント配下に`do_not_delete_csm_instance`という中継インスタンスが作成されます。移行が完了してシステムが今回作成した中継インスタンスを自動的に破棄するまで、中継インスタンスに対してOSの再インストール、シャットダウン、破棄、パスワードのリセットなどの操作を行わないでください。
</dx-alert>


### 移行タスクが終了するまで待機

下図に示すように、移行タスクの状態が「成功」になると、移行が完了します。
![](https://qcloudimg.tencent-cloud.cn/raw/7beb11db18bd9913b44941dd05f8a4a4.png)

<dx-alert infotype="explain" title="">
- データの転送にかかる時間は、移行元データのサイズ、ネットワーク帯域幅などの要因に影響されます。移行が完了するまでお待ちください。
- 移行タスク開始後に、移行タスクが所在する行で**一時停止**をクリックして、移行タスクを停止できます。
- 移行ツールはデータ転送を中断したところから再開する機能をサポートします。タスクを一時停止した後、**開始/リトライ**をクリックすると、前回一時停止したポイントから移行を再開できます。
- 移行タスクはデータ転送段階での一時停止のみサポートします。コンソールの移行タスクで**一時停止**をクリックすると、移行ツールはデータ転送段階でデータの転送を一時停止します。
- 移行に時間がかかり、移行を中止する場合、移行タスクを一時停止して**削除**をクリックすると、今回の移行タスクをキャンセルできます。
</dx-alert>

### 移行後の確認[](id:checkAfter)

- **移行失敗**：
ログファイル（デフォルトでは移行ツールディレクトリ配下のログファイル）で出力されたエラーメッセージ、ガイドドキュメントまたは[サービス移行に関するよくあるご質問](https://intl.cloud.tencent.com/document/product/213/32395)を確認し、トラブルシューティングと問題修正を行ってください。修正後に、移行タスクの操作列で**開始/リトライ**をクリックすると、移行タスクを再開できます。
- **移行成功**：
 - 移行先がCVMの場合、移行先CVMが正常に起動できるか、移行先CVMのデータが移行元サーバーと一致しているか、ネットワークが正常か、他のシステムサービスが正常かなどを確認してください。
 - 移行先がCVMイメージの場合、移行タスクが所在する行の「CVMイメージID」をクリックし、[CVMイメージページ](https://console.cloud.tencent.com/cvm/image/index)に進んで、そのイメージの情報を確認します。そのイメージを使用してCVMを作成することができます。

ご不明な点や移行異常などがありましたら、[サービス移行に関するよくあるご質問](https://intl.cloud.tencent.com/document/product/213/32395)を参照するか、[お問い合わせ](https://intl.cloud.tencent.com/document/product/213/34837)までご連絡ください。



