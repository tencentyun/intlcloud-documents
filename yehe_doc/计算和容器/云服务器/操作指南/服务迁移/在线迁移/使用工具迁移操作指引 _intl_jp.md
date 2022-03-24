ここでは、go2tencentcloudマイグレーションツールを使用して、サーバーのオンラインマイグレーションを行う方法についてご紹介いたします。


## マイグレーションフロー
ツールを使用したマイグレーションのフローは下図のとおりです。
![](https://qcloudimg.tencent-cloud.cn/raw/d967dcfa7799a37f6184fbad7849de69.png)

## 準備事項

- Tencent Cloudアカウント、および移行先のCVMがすでにあることが必要です。
- 移行中に既存のアプリケーションへの影響を回避するために、ソースサーバーのアプリケーションを一時停止することをお勧めします。
- 移行ツール圧縮パッケージをダウンロードするには、[ここ](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip) をクリックしてください。
- [APIキー管理](https://console.cloud.tencent.com/cam/capi)ページで`SecretId`および`SecretKey`を作成し、取得します。
- ソースサーバーと移行先CVMの両方が移行要件を満たしていることを確認します。例えば、移行先CVMのクラウドディスクには、移行元サーバーから移行されたデータを保存するための十分な容量を持っている必要があります。
- マイグレーション前に、次の方式でデータをバックアップすることをお勧めします。
 - 移行元サーバー：ソースサーバーのスナップショット機能などの方式を選択してデータをバックアップできます。
 - 移行先CVM： [スナップショットの作成](https://intl.cloud.tencent.com/document/product/362/5755) などの方式を選択して、移行先CVMのデータをバックアップできます。

## 移行手順


### 設定ファイルの修正[](id:modifyConfiguration)

1. マイグレーションツールgo2tencentcloud.zipをダウンロードするか、または移行元サーバーにアップロードし、次のコマンドを実行して対応するディレクトリに進みます。
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
<dx-alert infotype="explain" title="">
`go2tencentcloud`ディレクトリ下のファイルは移行されません。移行が必要なファイルをこのディレクトリ下に置かないでください。
</dx-alert>
2. `user.json`ファイル内で移行先CVMを設定します。
[user.jsonファイルパラメータの説明](https://intl.cloud.tencent.com/document/product/213/44340)に従って、入力必須項目および必要な項目の値を設定してください。次の事例を参照して、対応するパラメータ値を実際の設定パラメータに置き換えてください。
 - 事例1：Linux移行元サーバー1基をTencent Cloud広州リージョンのCVM1基にマイグレーションする場合、`user.json` ファイルは次のように構成されます。
```json
{  
	"SecretId": "your secretId",
	"SecretKey": "your secretKey",  
	"Region": "ap-guangzhou",  
	"InstanceId": "your instance id"
} 
```
 - 事例2：Linux移行元サーバー1基（データディスク1枚を含む。マウントポイントは`/mnt/disk1`、サイズは`10GB`）をTencent Cloud広州リージョンの移行先CVM1基（少なくとも1枚のデータディスクがマウントされている）にマイグレーションする場合、`user.json`ファイルは次のように構成されます。
```json
{  
	"SecretId": "your secretId",
	"SecretKey": "your secretKey",  
	"Region": "ap-guangzhou",  
	"InstanceId": "your instance id",
	"DataDisks": [
		{
			"Index": 1,
			"Size": 10,
			"MountPoint": "/mnt/disk1"
		}
	]
}
```
 - 事例3：Linux移行元サーバー1基（データディスク2枚を含む。ディスク1のマウントポイントは`/mnt/disk1`、サイズは`10GB`で、移行先CVMの最初のデータディスクにマイグレーションしたい場合。ディスク2のマウントポイントは`/mnt/disk2`、サイズは`20GB`で、移行先CVMの2番目のデータディスクにマイグレーションしたい場合）をTencent Cloud広州リージョンの移行先CVM1基（少なくとも2枚のデータディスクがマウントされている）にマイグレーションする場合、`user.json`ファイルは次のように構成されます。
```json
{  
	"SecretId": "your secretId",
	"SecretKey": "your secretKey",  
	"Region": "ap-guangzhou",  
	"InstanceId": "your instance id",
	"DataDisks": [
		{
			"Index": 1,
			"Size": 10,
			"MountPoint": "/mnt/disk1"
		},
		{
			"Index": 2,
			"Size": 20,
			"MountPoint": "/mnt/disk2"
		}
	]
}  
```
2. （オプション）`client.json`ファイルでマイグレーションモードとその他の項目を設定します。
[client.jsonファイルパラメータの説明](https://intl.cloud.tencent.com/document/product/213/44340)に従って設定してください。移行元サーバーと移行先CVMのいずれかがパブリックネットワークに直接アクセスできない場合は、先に[VPCピアリング接続](https://intl.cloud.tencent.com/zh/document/product/553)、[VPN接続](https://intl.cloud.tencent.com/zh/document/product/1037)、[CCN](https://intl.cloud.tencent.com/zh/document/product/1003)または[ダイレクト接続](https://intl.cloud.tencent.com/zh/document/product/216)などの方式で接続チャネルを確立してから、プライベートネットワークモードでのマイグレーションを実施する方法を選択することができます。詳細については[プライベートネットワークマイグレーションのチュートリアル](https://intl.cloud.tencent.com/document/product/213/44341)をご参照ください。
3. （オプション）移行元サーバー上でマイグレーション不要のファイルまたはディレクトリを削除します。
Linux移行元サーバーにマイグレーション不要のファイルまたはディレクトリが存在する場合は、ファイルまたはディレクトリを[rsync\_excludes\_linux.txtファイル](https://intl.cloud.tencent.com/document/product/213/44340)に追加することができます。

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
	  </ol>
	</td>
  </tr>
</table>
<dx-alert infotype="explain" title="">
- `sudo ./go2tencentcloud_x64 --check`などのツールコマンドを使用して、移行元サーバーを自動的にチェックできます。
- go2tencentcloudマイグレーションツールは、実行を開始すると、デフォルトで自動的にチェックします。このチェックをスキップして強制的に移行する場合は、client.json ファイルの`Client.Extra.IgnoreCheck`フィールドの値を`true`に設定してください。
</dx-alert>



### マイグレーションの開始

次のコマンドを実行し、ツールを実行します。
ここでは、64ビットのLinux移行元サーバーを例とします。go2tencentcloud_toolファイルディレクトリに入り、root権限で次のコマンドを実行し、ツールを実行します。
```sh
sudo ./go2tencentcloud_x64
```

### マイグレーション終了待機

Tencent Cloudが提供するgo2tencentcloudマイグレーションツールはブレークポイント転送をサポートし、マイグレーションプロセス全体を次の3つの段階に分割します。ユーザーは、ツールの実行中にマイグレーションの進行状況を直観的に理解することができます。

- **ステージ1**：移行先CVMが移行モードに入り、移行を準備します
- **ステージ2**：移行先CVMが移行モードにあり、データを移行しています
- **ステージ3**：移行先CVMが移行モードを終了し、移行が完了します

各ステージではいずれもいくつかのサブタスクが発生し、関連の操作を実行します。時間がかかる一部のサブタスクには、デフォルトの最大タイムアウト時間が存在します。データ転送の消費時間は、移行元データのサイズ、ネットワーク帯域幅などの要因に左右されます。マイグレーションフローが完了するまでお待ちください。

<dx-alert infotype="notice" title="">
マイグレーションの開始後、移行先CVMはマイグレーションモードに入ります。マイグレーションが完了してマイグレーションモードを終了するまで、移行先CVMに対してシステムの再インストール、シャットダウン、破棄、パスワードのリセットなどの操作を行わないでください。 
</dx-alert>

通常、パブリックネットワークマイグレーションモードでは、マイグレーションが成功すると、コンソールから次の内容が出力されます。
![](https://main.qcloudimg.com/raw/b056d6b1d5ac457ff43e48883848af01.png)

### マイグレーション後の確認

- マイグレーションが失敗した場合は、ログファイル（デフォルトではマイグレーションツールディレクトリ下のログファイル）からのエラーメッセージ出力、ガイドラインドキュメントまたは[サービスマイグレーションに関するよくあるご質問](https://intl.cloud.tencent.com/document/product/213/32395)を確認し、トラブルシューティングと問題の修正を行ってください。
- マイグレーションが成功した場合は、移行先CVMが正常に起動できるか、移行先CVMのデータが移行元サーバーと一致しているか、ネットワークが正常か、他のシステムサービスが正常かなどを確認してください。

ご不明な点やマイグレーションの異常など、ご質問がありましたら、[サービスマイグレーションに関するよくあるご質問](https://intl.cloud.tencent.com/document/product/213/32395)をご参照いただくか、または[お問い合わせ](https://intl.cloud.tencent.com/document/product/213/34837)から解消してください。
