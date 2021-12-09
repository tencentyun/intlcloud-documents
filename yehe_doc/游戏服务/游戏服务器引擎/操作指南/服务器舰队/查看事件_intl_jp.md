## シナリオ

ここでは、主にイベントの確認によってアクティビティの追跡、トラブルシューティングとデバッグを行う方法をご説明します。サーバーフリート作成の各段階の完成にともない、フリートおよびフリートの現在の状態に関する一連のイベントが出現しますが、コンソールですべてのイベントを追跡できます。

## 前提条件

[GSE申請書](https://intl.cloud.tencent.com/apply/p/k0b6pvbhs6)を記入して利用資格を取得し、サーバーフリートを作成済みであること。

## 操作手順

1. [GSEコンソール](https://console.cloud.tencent.com/gse/asset)にログインし、サーバーフリートを作成します。詳細については、[サーバーフリートの作成](https://intl.cloud.tencent.com/document/product/1055/36675)をご参照ください。
2. 作成できたサーバーフリートの**ID**をクリックして、サーバーフリートの詳細情報に入り、**イベント**タブをクリックして、イベント画面に入ります。
   イベント詳細リストは、時間、コード、情報、操作に分かれています。
   - **時間**：イベントが発生した時間。表示形式は yyyy-mm-dd hh:mm:ssです。
   - **コード**：記録中のイベントのタイプ。具体的なイベントのタイプは後述をご参照ください。
   - **情報**：イベントメッセージの説明。
   - **操作**：ログをダウンロードできます。
   - **イベントタイプ**：現在あるのは、 [デプロイ・作成イベント](#.E9.83.A8.E7.BD.B2.E5.88.9B.E5.BB.BA.E4.BA.8B.E4.BB.B6)、[VPCピアリングイベント](#vpc-.E5.AF.B9.E7.AD.89.E4.BA.8B.E4.BB.B6)、[その他のフリートのイベント](#.E5.85.B6.E4.BB.96.E8.88.B0.E9.98.9F.E4.BA.8B.E4.BB.B6)です。
![](https://main.qcloudimg.com/raw/2e0240c11acca72a51a07f0c8a511b60.png)




#### デプロイ・作成イベント

| コード                                        | 説明                                                         |
| ------------------------------------------- | ------------------------------------------------------------ |
| FLEET_CREATED                               | 作成完了、ステータスがNEWになります。イベントメッセージにはフリートIDが含まれます                    |
| FLEET_STATE_DOWNLOADING-FLEET               | ステータスがNEWからDOWNLOADINGに変わります。アセットのダウンロードが開始され、フリートインスタンスにインストールされます |
| FLEET_BINARY_DOWNLOAD_FAILED                | アセットをフリートインスタンスにダウンロードできません                                     |
| FLEET_CREATION_EXTRACTING_ASSET             | アセットのインスタンスへのダウンロードが成功し、現在アップロードZIPパッケージの中からアセットのファイルを取り出して、それをインスタンスに保存しようとしています。この段階で失敗するとフリートステータスのACTIVEへの移行が阻止されます。この段階のログには取り出したインスタンスリストが表示され、インスタンス上に保存されます。 **PreSignedLogUrl**の中のURLを使用してログにアクセスします |
| FLEET_CREATION_RUNNING_INSTALLER            | アセットの取り出しに成功し、GSEが現在ビルドのインストールスクリプトを実行中です（スクリプトが含まれている場合）。この段階で失敗するとフリートのACTIVE化が阻止されます。この段階のログにはインストール手順およびインストール成功の可否が表示されます。**PreSignedLogUrl**の中のURLを使用してログにアクセスします |
| FLEET_CREATION_VALIDATING_RUNTIME_CONFIG    | ビルドプロセスが完了し、GSEは現在フリートの動作時の設定の中で指定したゲームサーバーの起動パスを検証しています。リストアップされた起動パスが存在する場合、GSEはゲームサーバープロセスを起動しようとし、このプロセスの準備完了の報告を待ちます。この段階に故障があると、フリートステータスのACTIVEへの移行が阻止されます。この段階のログには動作時の設定の中の起動パスが表示され、各起動パスが見つかったかどうか明示されます。 **PreSignedLogUrl**の中のURLを使用してログにアクセスします |
| FLEET_STATE_VALIDATING- FLEET               | ステータスがDOWNLOADINGからVALIDATINGに変わります                           |
| FLEET_VALIDATION_LAUNCH_PATH_NOT_FOUND      | 動作時の設定の検証に失敗しました。インスタンスの中に起動パスの中で指定した実行可能ファイルが見つかりません |
| FLEET_STATE_ASSETING- FLEET                 | ステータスがVALIDATINGからASSETINGに変わります                               |
| FLEET_VALIDATION_EXECUTABLE_RUNTIME_FAILURE | 動作時の設定検証に失敗しました。起動パスの中で指定した実行可能ファイルがフリートインスタンス上で動作しません |
| FLEET_STATE_ACTIVATING- FLEET               | フリートのステータスがASSETING からACTIVATINGに変わります                          |
| FLEET_ACTIVATION_FAILED- FLEET              | フリートのアクティベートプロセスの中の1ステップがまだ完了していません。このイベントコードは、アセットがすでにフリートインスタンスにダウンロードされ、ビルドと検証が行われていますが、サーバーを起動できないことを表します |
| FLEET_STATE_ACTIVE-FLEET                    | ステータスがACTIVATINGからACTIVEに変わります                                 |


#### VPCピアリングイベント


| コード                          | 説明                                                         |
| ----------------------------- | ------------------------------------------------------------ |
| FLEET_VPC_PEERING_SUCCEEDED   | GSEフリートのVPCとあなたのTencent CloudアカウントのVPCとの間で VPCピアリング接続が確立されました |
| FLEET_VPC_PEERING_FAILED      | リクエストしたVPCピアリング接続に失敗しました。イベントの詳細情報とステータス情報によってより詳しい情報が提供されています。ピアリング失敗のよくある原因は2つのVPCに重複するIPv4アドレスのCIDRのブロックがある場合です。このトラブルを解決したい場合は、Tencent CloudアカウントでVPCのCIDRブロックを変更してください |
| FLEET_VPC_PEERING_DELETED-VPC | VPCピアリング接続を削除しました                                           |


#### その他のフリート関連イベント


| コード                                             | 説明                                                         |
| ------------------------------------------------ | ------------------------------------------------------------ |
| FLEET_SCALING_EVENT                              | フリートの容量設定（必要なインスタンス、最小/最大のスケーリングの制限）を変更しました。イベントメッセージには新しい容量設定が含まれます |
| FLEET_NEW_GAME_SESSION_PROTECTION_POLICY_UPDATED | フリートのゲームサーバーセッションの保護ポリシーの設定を変更しました。イベントメッセージには新旧ポリシーの設定が含まれます |
| FLEET_DELETED                                    | フリート削除のリクエストを発信                                           |
| GENERIC_EVENT                                    | 指定のないイベントが発生しました                                           |
| FLEET_STATE_ERROR                                | ステータスエラー                                                     |
| FLEET_INITIALIZATION_FAILED                      | 初期化の失敗                                                   |
| FLEET_VALIDATION_TIMED_OUT                       | 検証タイムアウト                                                     |
| FLEET_ACTIVATION_FAILED_NO_INSTANCES             | インスタンスがありません                                                     |
| SERVER_PROCESS_INVALID_PATH                      | プロセスのパスが無効です                                                 |
| SERVER_PROCESS_SDK_INITIALIZATION_TIMEOUT        | プロセスSDK初期化のタイムアウト                                            |
| SERVER_PROCESS_PROCESS_READY_TIMEOUT             | プロセス準備のタイムアウト                                                 |
| SERVER_PROCESS_CRASHED                           | プロセスの破棄                                                     |
| SERVER_PROCESS_TERMINATED_UNHEALTHY              | プロセスの不備                                                   |
| SERVER_PROCESS_FORCE_TERMINATED                  | プロセスの強制終了                                                 |
| SERVER_PROCESS_PROCESS_EXIT_TIMEOUT              | プロセス退出のタイムアウト                                                 |
| GAME_SESSION_ACTIVATION_TIMEOUT                  | ゲームサーバーセッションアクティベートのタイムアウト                                       |
| SERVER_PROCESS_PULL_FAILED                      | プロセスプルに失敗しました                                                 |
| SERVER_DOWN                                      | サーバーダウン                                                   |





