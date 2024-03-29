- [オフライン移行に関するよくある質問](#OfflineMigration)
- [オンライン移行に関するよくある質問](#OnlineMigration)
- [コンソール経由での移行に関するよくある質問](#ConsoleOnlineMigration)
- [オンライン移行ツールに関するよくある質問](#OnlineMigrationTool)



[](id:OfflineMigration)
## オフライン移行

### COS へのアップロードと移行にかなり時間がかかるのはなぜですか？
COSへのイメージのアップロードにかかる時間は、イメージファイルのサイズと帯域幅に関係します。転送と移行の時間を短縮するために、圧縮イメージ形式 (QCOW2 または VHD) を使用することをお勧めします。

### 移行タスクが失敗したのはなぜですか?
 - Tencent Cloud のサービス移行では、QCOW2、VHD、VMDK、RAW 形式のイメージがサポートされています。 イメージが上記のいずれかの形式であることを確認してください。
 - イメージファイルがCOSに完全にアップロードされていることを確認し、COS権限をチェックし、一時 URLが有効であり、ファイルが破損していないことを確認してください。
 - ターゲットCVMまたはクラウドディスクの有効期限が切れていないことを確認してください。

### 移行タスクで発生したエラーをトラブルシューティングするにはどうすればよいですか?
- **「イメージファイルのメタデータの取得に失敗しました」**というメッセージが表示された場合は、通常、イメージファイルが破損しているか、イメージファイルの形式がサポートされていないことなどが原因です。イメージの作成/エクスポート、アップロードなどの段階でエラーが発生していないか確認してください。またはqcow2、vhd、vmdk、raw形式のイメージファイルを提供して、再試行してください。
- **「イメージの解凍に失敗しました」**というメッセージが表示された場合は、通常、イメージ作成のエラーが原因です。イメージ圧縮パッケージの正当性を確認するか、イメージを再度エクスポートして、ターゲットディスクの容量がソースディスクよりも大きいことを確認して、再試行してください。
- **「ターゲットデバイスのストレージ容量が小さすぎます」**というメッセージが表示された場合は、通常、現在の移行タスクのターゲットシステムディスクまたはデータディスクのストレージ容量がソースディスクよりも小さいか、ターゲットシステムディスクまたはデータディスクのストレージ容量がイメージファイルのサイズよりも小さいなどが原因です。この場合、ターゲットシステムディスクまたはデータディスクのサイズを変更して、ターゲットディスクの容量がソースディスクの容量より大きいことを確認して、再試行してください。
- **「COSイメージファイルへのアクセスに失敗しました」**というメッセージが表示された場合は、通常、COS権限の問題です。COSファイルが現在のリージョンにあり、COS権限をチェックし、一時 URLの有効性を確認して、再試行してください。
- 「ターゲットディスクへの移行に失敗しました」というメッセージが表示された場合は、考えられる理由は通常、次のとおりです：
 - 十分なディスク容量がありません。
 - イメージの作成中にエラーが発生しました。
これらの問題をトラブルシューティングした後、再試行してください。
- **「タスクタイムアウト」**、**「システムエラー」**、**「その他の原因」**などのメッセージが表示された場合、または移行タスクを再試行しても失敗する場合は、 [お問い合わせ](https://intl.cloud.tencent.com/document/product/213/34837) ください。

###  Windowsサーバーをオフラインに移行した後にネットワークが切断された場合はどうすればよいですか?

以下の手順に従って、Windowsネットワーク構成をリセットするか、または [インスタンスにPingが通らない](https://intl.cloud.tencent.com/document/product/213/14639)ドキュメントをご覧ください。

1）2018 年 6 月より前に作成された VPC の場合は、サーバーがdhcpをサポートしているかどうかを確認してください。サポートしない場合は、静的IPが正しいかどうかを確認してください。

2）サーバーがdhcpをサポートしている場合は、割り当てられたプライベート IP が正しいかどうかを確認してください。正しくない場合は、サーバーを再起動せずに、管理者としてコマンド`ipconfig /release; ipconfig /renew` を実行してください。

3）割り当てられた IP は正しいが、ネットワークが切断されている場合は、ncpa.cpl を実行してローカル接続を開き、ENIを無効にしてから有効にします。

4）管理者として次のコマンド実行し、サーバーを再起動します：`reg delete "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Profiles"  /f`。

[](id:OnlineMigration)
## オンライン移行に関するよくある質問

### オンライン移行ではどのタイプのOSやディスクをサポートしていますか？
- 主流のLinux系OSおよび Windows系OSをサポートします。
- 移行はディスクの種類や使用状況には関係ありません。


### オンライン移行とイメージのインポートの違いは何ですか?
オンライン移行は、イメージのインポートと似ています。どちらもソースシステムをTencent Cloudに移行できます。オンライン移行とイメージのインポートの違いとして最も大きな点は、オンライン移行を使用すると、イメージを手動で作成、エクスポート、インポートすることなく、システムとデータをソースサーバーから Tencent Cloud に転送できます。


### 移行元サーバーのパブリックIPは移行されますか?
いいえ。オンライン移行ではソースシステムとデータのみが同期され、パブリック IPは移行できません。


### オンライン移行ツールはチェックポイントからの再起動をサポートしていますか？

 中断後にツールを再度実行すると、転送を再開できます。


### 移行完了後もツールを保持する必要がありますか?
いいえ。移行が完了したら、移行元サーバー上のツールを直接削除できます。


### 移行速度とコストについてはどうですか?
- 速度：ターゲットCVM インスタンスの帯域幅によって決まります。帯域幅12Mbpsの1CIG 従量課金制インスタンスを使用したテストでは、実際の移行速度は約9 Mbpsです。具体的な計算方法については、[移行時間予測チュートリアル](https://intl.cloud.tencent.com/document/product/213/44342)をご参照ください。
- 費用：移行ツールは無料です。移行中に使用される帯域幅およびその他のリソースに対して料金が発生します。トラフィックやと期間に応じて課金されます。詳細については、 [課金説明](https://www.tencentcloud.com/document/product/213/54429)をご参照ください。


### 複数のCVMの同時移行はサポートされていますか？
はい。 複数のCVMを異なる移行先CVM に同時に移行できます。


### Virtio を確認してインストールするにはどうすればよいですか?
 [LinuxでのVirtioドライバーの確認](https://intl.cloud.tencent.com/document/product/213/9929)を参照して、Virtio を確認してインストールします。


### Rsync をインストールするにはどうすればよいですか?[](id:installRsync)
Rsyncをインストールする移行元サーバーのOSに応じて、対応するコマンドを選択して、Rsyncをインストールできます。
- CentOS：`yum -y install rsync`
- Ubuntu：`apt-get -y install rsync`
- SUSE：`zypper install rsync`
他の Linux ディストリビューションの特定のコマンドについては、対応する公式 Web サイトのインストールドキュメントをご参照ください。


### SELinux を無効にするにはどうすればよいですか？[](id:closeSELinux)
 `/etc/selinux/config` ファイルを編集し、 `SELINUX=disabled`を設定します。


[](id:ConsoleOnlineMigration)
## コンソール経由でのオンライン移行に関するよくある質問

### オンライン移行ツールはどこでダウンロードできますか？
[ここをクリックして](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip) オンライン移行ツールパッケージをダウンロードし、 [オンライン移行の操作ガイド](https://intl.cloud.tencent.com/document/product/213/44338) の指示に従ってツールを使用してください。


### 移行元をインポートするにはどうすればよいですか?
1.  [オンライン移行ツールパッケージ](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip) をダウンロードして解凍します。
2. ソースサーバーアーキテクチャの実行可能ファイルを実行して、移行ソースを CVM コンソールのオンライン移行ページにインポートします。
 - ソースサーバーが 32 ビットの場合は、`go2tencentcloud_x32`を実行します。
 - ソースサーバーが 64 ビットの場合は、`go2tencentcloud_x64`を実行します。


### 移行元を更新したり、移行元を再インポートするにはどうすればよいですか?
移行元ディスクなどの情報が変更された場合は、移行元情報を更新するか、再インポートする必要があります。 まず既存の移行元を削除してから、クライアントを実行して移行元を再インポートします。


### 移行元を削除するにはどうすればよいですか?
[オンライン移行コンソール](https://console.cloud.tencent.com/cvm/csm/online?rid=1)にログインし、ターゲット移行元の右側にある**削除**をクリックします。移行元が完了していない移行タスクに関連付けられている場合は、移行タスクを中止し削除してから、移行元を削除してください。


### 移行前に移行先CVMインスタンスを選択するにはどうすればよいですか?
移行元サーバーと移行先 CVMインスタンスには同じOSを使用することをお勧めします。たとえば、CentOS 7 移行元サーバーを移行するには、移行先として CentOS 7 CVM を選択してください。


### タスクが完了したことを示す移行タスクのステータスはどれですか?
移行タスクのステータスが「成功」の場合のみ完了を意味し、その他のステータスはすべて未完了を意味します。


### 移行タスクを削除するにはどうすればよいですか?
実際の移行タスクのステータスに基づいて、次の操作を実行します。
- 移行タスクのステータスが「未開始」または「成功」の場合、移行タスクの右側にある**削除**をクリックしてタスクを直接削除できます。
- 移行タスクのステータスが「失敗」の場合、移行タスクを削除したい場合は、移行元をオンライン状態のままにし、移行タスクの右側にある**削除**をクリックして移行タスクを削除する必要があります。その後、タスクのステータスが「削除中」になり、移行ツールは、移行タスクによって生成されたリソースを自動的にクリアし、移行タスクを削除します。


### 時間がかかりすぎる場合、移行タスクをキャンセルするにはどうすればよいですか?
[オンライン移行コンソール](https://console.cloud.tencent.com/cvm/csm/online?rid=1)にログインして移行タスクを一時停止し、移行タスクの右側にある**削除**をクリックしてタスクを削除します。


### リレーインスタンスが終了した場合はどうすればよいですか?
移行先Tencent Cloud イメージへの移行中に、作成されたリレーインスタンスが誤って終了した場合、現在の移行タスクを削除し、移行元の移行タスクを再度作成して開始できます。


### コンソールでの移行中にエラーまたは障害が発生した場合はどうすればよいですか?
一部の移行失敗理由とエラーについては、以下を参照してください:


- 移行先CVMに移行する場合、移行先CVMのセキュリティグループでポート 80 と 443 が開きません。
**解決策**：移行先CVMインスタンスのセキュリティグループルールを変更して、ポート80と443を開きます。
- 移行先CVMに移行する場合、移行先CVMインスタンスのディスク容量が不足します。
**解決策**：十分な容量のあるCVMインスタンスを選択し、それに十分な容量のあるディスクをマウントし、移行タスクを再作成して移行を開始します。
- 移行先Tencent Cloudイメージに移行する場合、リレーインスタンスを作成するときにエラーが発生しました。たとえば、ログエラー メッセージ「Failed create transit instance, maybe no available source in target region」が表示されます。
**解決策**：移行タスクの移行先リージョンに利用可能なリソースがありません。この場合は、別のリージョンを選択するか、指定されたCVMインスタンスにサーバーを移行できます。

依然として問題が解決しない場合、または上記の原因に該当しない場合は、その時点の移行ログファイル（デフォルトでは移行ツールディレクトリのlogファイル）を保持し、弊社まで[お問い合わせ](https://intl.cloud.tencent.com/document/product/213/34837) ください。



### 移行完了後に何を得ることができますか？
移行タスクが完了すると、プラットフォームは移行タスクに設定した移行先タイプに従ってTencent Cloud リソースが生成されます。
- **CVMイメージへの移行**：移行後、移行元のTencent Cloud イメージが生成されます。移行タスクの行にある**CVMイメージ ID **をクリックして、 [CVMイメージ](https://console.cloud.tencent.com/cvm/image/index) ページでイメージの詳細をを確認でき、このイメージを使用してCVMをすばやく作成できます。CVMイメージが正常に作成されると、このイメージに関連付けられた**CVM スナップショット**も同時に作成されます。
- **CVMインスタンスへの移行**：移行後、移行元は移行先CVMインスタンスに移行されます。


### Linux サーバーの移行後にシステムを確認するにはどうすればよいですか?
移行先 CVMインスタンスが正常に起動するかどうか、移行先 CVM インスタンス上のデータが移行元サーバー上のデータと一致しているかどうか、ネットワークやその他のシステムサービスが正常であるかどうかを確認してください。


### 移行完了後に移行元を再移行するにはどうすればよいですか?
 [オンライン移行コンソール](https://console.cloud.tencent.com/cvm/csm/online?rid=1)にログインし、移行元の移行タスクを作成して再度開始します。

### オンラインからWindowsサーバーを移行した後、ネットワークが切断された場合はどうすればよいですか?

以下の手順に従って、Windowsネットワーク構成をリセットするか、または [インスタンスにPingが通らない](https://intl.cloud.tencent.com/document/product/213/14639)ドキュメントをご覧ください。

1）2018 年 6 月より前に作成された VPC の場合は、サーバーがdhcpをサポートしているかどうかを確認してください。サポートしない場合は、静的IPが正しいかどうかを確認してください。

2）サーバーがdhcpをサポートしている場合は、割り当てられたプライベート IP が正しいかどうかを確認してください。正しくない場合は、サーバーを再起動せずに、管理者としてコマンド`ipconfig /release; ipconfig /renew`を実行してください。

3）割り当てられた IP は正しいが、ネットワークが切断されている場合は、ncpa.cpl を実行してローカル接続を開き、ENIを無効にしてから有効にします。

4）管理者として次のコマンド実行し、サーバーを再起動します：`reg delete "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Profiles"  /f`。

[](id:OnlineMigrationTool)
## オンライン移行ツールに関するよくある質問


### オンライン移行ツールはどこでダウンロードできますか?
[ここをクリックして](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip) 圧縮移行ツール パッケージをダウンロードし、 [オンライン移行ツール ](https://intl.cloud.tencent.com/document/product/213/35640) の指示に従って操作を行います。


### 移行ツールを使用するにはどう設定すればよいですか。
移行ツールをダウンロードして移行元サーバーにアップロードし、実行する前に実際のサーバーの状況に基づいて構成ファイルを変更する必要があります。バッチ移行を実行するには、バッチ処理を実装するスクリプトを作成します。


### ツールを使用した移行中にエラーまたは障害が発生した場合はどうすればよいですか?

一部の移行失敗理由とエラーについては、以下を参照してください:
- 移行先CVMのセキュリティグループでポート80と443が開きません。
- user.jsonファイルのDataDisksフィールドは、移行元サーバーのデータディスクを移行するように構成されていません。すべてのデータがターゲットCVMシステムディスクに送信されるため、ディスク容量が不足していた。
-  [プライベートネットワーク移行モード](https://intl.cloud.tencent.com/document/product/213/44340) では移行ステージ 3 が実行されないため、移行先CVM は移行モードを終了します。

依然として問題が解決しない場合、または上記の原因に該当しない場合は、その時点の移行ログファイル（デフォルトでは移行ツールディレクトリのlogファイル）を保持し、弊社まで[お問い合わせ](https://intl.cloud.tencent.com/document/product/213/34837) ください。