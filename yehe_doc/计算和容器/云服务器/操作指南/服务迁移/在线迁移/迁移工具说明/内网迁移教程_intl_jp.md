## 概要
このドキュメントでは、オンラインマイグレーションツールの**プライベートネットワークマイグレーション**モードを使用して、ソースサーバー上のシステム、アプリケーションプログラムなどを自分で作成したコンピュータルーム（IDC）やクラウドプラットフォームなどのソース環境からTencent Cloud CVMに移行する操作手順についてご紹介します。

プライベートネットワークを使用したマイグレーションはパブリックネットワークマイグレーションに比べて移行の転送速度が速く、移行効率が顕著に向上します。また、移行元マシンのパブリックネットワークアクセス機能を制限せず、柔軟なマイグレーション設定を行うことができます。


## 準備事項

- Tencent Cloudアカウントおよび移行先のCVMがすでにあることが必要です。
- 移行中に既存のアプリケーションへの影響を回避するために、ソースサーバーのアプリケーションを一時停止することをお勧めします。
- [APIキー管理](https://console.cloud.tencent.com/cam/capi)ページで`SecretId`および`SecretKey`を作成し、取得します。
- ソースサーバーと移行先CVMの両方が移行要件を満たしていることを確認します。例えば、移行先CVMのクラウドディスクには、移行元サーバーから移行されたデータを保存するための十分な容量を持っている必要があります。


## 操作手順

### データのバックアップ
- 移行元サーバー：ソースサーバーのスナップショット機能などの方式を選択してデータをバックアップできます。
- 移行先CVM： [スナップショットの作成](https://intl.cloud.tencent.com/document/product/362/5755) などの方式を選択してデータをバックアップできます。


### マイグレーションツールを取得する  
[ここをクリック](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip)して、マイグレーションツールの圧縮ファイルをダウンロードします。


### ネットワーク環境に応じたマイグレーションモードの確定
移行元サーバーと移行先CVMのネットワーク環境に基づいて、適切なマイグレーションモードを確定します。
現在マイグレーションツールはパブリックネットワークモードとプライベートネットワークマイグレーションモードをサポートしています。その中で、プライベートネットワークマイグレーションモードは3つのシナリオに適用されます。異なるマイグレーションモード/シナリオは、移行元サーバーと移行先CVMのネットワーク要件も違います。移行元サーバーと移行先CVMの両方がパブリックネットワークにアクセスできる場合、デフォルトモードで直接マイグレーションできます。移行元サーバーまたは移行先CVMのいずれかがパブリックネットワークに直接アクセスできない場合、まず[VPCピアリング接続](https://intl.cloud.tencent.com/zh/document/product/553)、[VPN接続](https://intl.cloud.tencent.com/zh/document/product/1037)、[CCN](https://intl.cloud.tencent.com/zh/document/product/1003)または[ダイレクト接続](https://intl.cloud.tencent.com/zh/document/product/216)などの方法で接続チャネルを確立してから、プライベートネットワークモードでのマイグレーションを実施する方法を選択することができます。

### マイグレーション前の確認

マイグレーションする前に、移行元サーバーと移行先CVMをそれぞれ確認する必要があります。確認内容は下表のとおりです。


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
プライベートネットワークマイグレーションモードの各シナリオに対応する手順は次のとおりです。

<dx-tabs>

::: シナリオ1

1. 移行元サーバーと移行先CVMの間に接続チャネルを確立します。
[VPN Peering Connection](https://intl.cloud.tencent.com/zh/document/product/553) / [VPN Connection](https://intl.cloud.tencent.com/zh/document/product/1037) / [CCN](https://intl.cloud.tencent.com/zh/document/product/1003) などの方法によって移行元サーバーと移行先CVMの間に接続チャネルを確立します。
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
3. `user.json`ファイルで移行先CVMを設定します。
[user.jsonファイルパラメータの説明](https://intl.cloud.tencent.com/document/product/213/44340)に従って、入力必須項目および必要な項目の値を設定してください。
4. `client.json`ファイルでマイグレーションモードとその他の項目を設定します。
`client.json`ファイルの`Client.Net.Mode`項目を`1`に設定します。これは、[プライベートネットワークマイグレーションモード：シナリオ1](https://intl.cloud.tencent.com/document/product/213/44340)のマイグレーションが実行されることを意味します。 また、他の項目を設定する必要がある場合は、[client.jsonファイルパラメータの説明](https://intl.cloud.tencent.com/document/product/213/44340)に従って設定してください。
5. （オプション）移行元サーバー上でマイグレーション不要のファイルまたはディレクトリを削除します。
Linux移行元サーバーにマイグレーション不要のファイルまたはディレクトリが存在する場合は、ファイルまたはディレクトリを[rsync_excludes_linux.txtファイル](https://intl.cloud.tencent.com/document/product/213/44340)に追加することができます。
6. [](id:Scenario1_step05)パブリックネットワークにアクセスできるサーバー（ゲートウェイなど）上でツールを実行します。
例えば、パブリックネットワークにアクセスできるサーバーで、次のコマンドを実行し、ツールを実行して、ステージ1の移行を実行します。
``` sh
chmod +x go2tencentcloud_x64
sudo ./go2tencentcloud_x64
```
下図に示すように、`Stage 1 is finished and please run next stage at source machine.`と表示された場合は、ステージ1が完了しています。
![](https://main.qcloudimg.com/raw/f861b47c464f58ea184e5cc5a6a30e1c.png)
7. [](id:Scenario1_step06)移行対象の移行元サーバー上でツールを実行します。
[ステップ5](#Scenario1_step05)（ステージ1）が完了した後、まずステージ1のツールディレクトリ全体を移行対象の移行元サーバーにコピーし、次にツールを実行してステージ2の移行を実行します。
例えば、次のコマンドを実行してツールを実行し、ステージ2の移行を実行します。
```sh
sudo ./go2tencentcloud_x64
```
下図に示すように、`Stage 2 is finished and please run next stage at gateway machine.`と表示された場合は、ステージ2が完了しています。
![](https://main.qcloudimg.com/raw/5684fc8aee6ebf8ba01e42deff3b4fc2.png)
8. パブリックネットワークにアクセスできるサーバー（ゲートウェイなど）でツールを実行します。
[ステップ6](#Scenario1_step06)（ステージ2）が完了した後、まずステージ2のツールディレクトリ全体をステージ1のサーバーにコピーし、次にツールを実行してステージ3の移行を実行します。
例えば、次のコマンドを実行してツールを実行し、ステージ3の移行を実行します。
```sh
sudo ./go2tencentcloud_x64
```
下図に示すように、`Migrate successfully.`と表示された場合は、すべての移行タスクが完了しています。
![](https://main.qcloudimg.com/raw/851e90fdc07fb601d3d158386d524985.png)

:::
::: シナリオ2

1. 移行元サーバーと移行先CVMの間に接続チャネルを確立します。
[VPN Peering Connection](https://intl.cloud.tencent.com/zh/document/product/553) / [VPN Connection](https://intl.cloud.tencent.com/zh/document/product/1037) / [CCN](https://intl.cloud.tencent.com/zh/document/product/1003) などの方法によって移行元サーバーと移行先CVMの間に接続チャネルを確立します。
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
3. `user.json`ファイルで移行先CVMを設定します。
 [user.jsonファイルパラメータの説明](https://intl.cloud.tencent.com/document/product/213/44340)に従って、入力必須項目および必要な項目の値を設定してください。
4. `client.json`ファイルでマイグレーションモードとその他の項目を設定します。
 `client.json`ファイルの`Client.Net.Mode`項目を`2`に設定します。これは、[プライベートネットワークマイグレーションモード：シナリオ2](https://intl.cloud.tencent.com/document/product/213/44340)のマイグレーションが実行されることを意味します。 また、他の項目を設定する必要がある場合は、[client.jsonファイルパラメータの説明](https://intl.cloud.tencent.com/document/product/213/44340)に従って設定してください。
5. （オプション）移行元サーバー上でマイグレーション不要のファイルまたはディレクトリを削除します。
Linux移行元サーバーにマイグレーション不要のファイルまたはディレクトリが存在する場合は、ファイルまたはディレクトリを[rsync_excludes_linux.txtファイル](https://intl.cloud.tencent.com/document/product/213/44340)に追加することができます。
6. ツールを実行する。
例えば、64ビットのLinux移行元サーバーで、root権限を指定して次のコマンドを実行し、ツールを実行します。
```sh
sudo ./go2tencentcloud_x64
```
ツールが実行した後、マイグレーションプロセスが完了するまでお待ちください。
通常、マイグレーションが成功すると、コンソールから次のようなメッセージが出力されます。
![](https://main.qcloudimg.com/raw/d32b4be8287d4b06697f0cb03cc6cff8.png)



:::

::: シナリオ3

1. 移行元サーバーと移行先CVMの間に接続チャネルを確立します。
[VPN Peering Connection](https://intl.cloud.tencent.com/zh/document/product/553) / [VPN Connection](https://intl.cloud.tencent.com/zh/document/product/1037) / [CCN](https://intl.cloud.tencent.com/zh/document/product/1003) などの方法によって移行元サーバーと移行先CVMの間に接続チャネルを確立します。
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
3. `user.json`ファイルで移行先CVMを設定します。
    [user.jsonファイルパラメータの説明](https://intl.cloud.tencent.com/document/product/213/44340)に従って、入力必須項目および必要な項目の値を設定してください。
4. `client.json`ファイルでマイグレーションモードとその他の項目を設定します。
    1. `client.json`ファイルの`Client.Net.Mode`項目を`3`に設定して、[プライベートネットワークマイグレーションモード：シナリオ3](https://intl.cloud.tencent.com/document/product/213/44340)のマイグレーションを実行します。
    2. `client.json`ファイルの`Client.Net.Proxy.Ip`と`Client.Net.Proxy.Port`の項目をネットワークプロキシのIPアドレスとポートに設定します。
        ネットワークプロキシで認証が​​必要な場合は、ネットワークプロキシのユーザー名とパスワードを`Client.Net.Proxy.User`と`Client.Net.Proxy.Password`に入力してください。認証が不要な場合は、空白のままにしてください。また、他の項目を設定する必要がある場合は、[client.jsonファイルパラメータの説明](https://intl.cloud.tencent.com/document/product/213/44340) に従って設定してください。
5. （オプション）移行元サーバー上でマイグレーション不要のファイルまたはディレクトリを削除します。
Linux移行元サーバーにマイグレーション不要のファイルまたはディレクトリが存在する場合は、ファイルまたはディレクトリを[rsync_excludes_linux.txtファイル](https://intl.cloud.tencent.com/document/product/213/44340)に追加することができます。
6. ツールを実行する。
例えば、64ビットのLinux移行元サーバーで、root権限を指定して次のコマンドを実行し、ツールを実行します。
```sh
sudo ./go2tencentcloud_x64
```
ツールが実行した後、マイグレーションプロセスが完了するまでお待ちください。
通常、マイグレーションが成功すると、コンソールから次の内容が出力されます。
![](https://main.qcloudimg.com/raw/2195589176d3669f08fbb5745901040b.png)

:::

</dx-tabs>



### マイグレーション後の確認

- マイグレーションが失敗した場合は、ログファイル（デフォルトではマイグレーションツールディレクトリ下のログファイル）からのエラーメッセージ出力、ガイドラインドキュメントまたは[サービスマイグレーションに関するよくあるご質問](https://intl.cloud.tencent.com/document/product/213/32395)を確認し、トラブルシューティングと問題の修正を行ってください。
- マイグレーションが成功した場合は、移行先CVMが正常に起動できるか、移行先CVMのデータが移行元サーバーと一致しているか、ネットワークが正常か、他のシステムサービスが正常かなどを確認してください。

ご不明な点やマイグレーションの異常など、ご質問がありましたら、[サービスマイグレーションに関するよくあるご質問](https://intl.cloud.tencent.com/document/product/213/32395)をご参照いただくか、または[お問い合わせ](https://intl.cloud.tencent.com/document/product/213/34837)から解消してください。











