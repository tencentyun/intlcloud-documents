## 概要

COSのリソースに変動（新規ファイルのアップロード、ファイルの削除など）があった場合、ユーザーは速やかにメッセージ通知を受信できます。イベント通知は[SCF](https://intl.cloud.tencent.com/product/scf)（Serverless Cloud Function）と組み合わせることで、より豊富なユースケースを実現できます。

- **製品間連携**：例えば、新たなファイルがCOSにアップロードされると、CDNキャッシュの自動更新を行います。新たなファイルがCOSにアップロードされると、データベースを自動更新します。
- **システム統合**：COS上のファイルに変更（新規作成、削除、上書き）が発生した場合、自身のサービスインターフェースを自動的に呼び出します。UGC（User Generated Content）のケースでは、イベント通知機能をベースにしてモバイル端末とサーバーの連携を実現することができます。
- **データ処理**：COS上のファイルに対し、自動解凍、AI認識などの自動処理を行います。
![](https://qcloudimg.tencent-cloud.cn/raw/4a32cb2d7739e6d183cbb94523689e1c.png)

COSイベント通知には次のような特徴があります。

- 非同期処理：通知の送信は正常なCOS操作に影響を与えません。
- 通知先：通知は同リージョンのSCF関数への送信のみサポートされます。

現在は次のCOSイベントをサポートしています。

| イベントタイプ                                  | 説明                                                         |
| ----------------------------------------- | ------------------------------------------------------------ |
| cos:ObjectCreated:*                       | 次に挙げるアップロードイベントはすべてSCFをトリガーします                         |
| cos:ObjectCreated:Put                     | PUT Objectインターフェースを使用してファイルを作成した際にSCFをトリガーします                     |
| cos:ObjectCreated:Post                    | POST Objectインターフェースを使用してファイルを作成した際にSCFをトリガーします                    |
| cos:ObjectCreated:Copy                    | PUT Object - Copyインターフェースを使用してファイルを作成した際にSCFをトリガーします              |
| cos:ObjectCreated:CompleteMultipartUpload | Complete Multipart Uploadインターフェースを使用してファイルを作成した際にSCFをトリガーします    |
| cos:ObjectCreated:Origin                  | イメージのback-to-originが発生した際にSCFをトリガーします                                    |
| cos:ObjectCreated:Replication             | 地域間コピーによってオブジェクトを作成した際にSCFをトリガーします                           |
| cos:ObjectRemove:*                        | 次に挙げる削除イベントはすべてSCFをトリガーします                         |
| cos:ObjectRemove:Delete                   | バージョン管理を有効にしていないバケットで、DELETE Objectインターフェースを使用してオブジェクトを削除するか、またはversionidを使用して指定のバージョンのオブジェクトを削除した際にSCFをトリガーします |
| cos:ObjectRemove:DeleteMarkerCreated      | バージョン管理を有効化または一時停止しているバケットで、DELETE Objectインターフェースを使用してオブジェクトを削除した際にSCFをトリガーします |
| cos:ObjectRestore:Post                    | アーカイブ復元タスクを作成した際にSCFをトリガーします                             |
| cos:ObjectRestore:Completed               | アーカイブ復元タスクを完了した際にSCFをトリガーします                                 |

## COSイベント通知の利用方法

COSイベント通知の利用には次の手順が含まれます。

1. SCF関数の作成
   - [SCFコンソール](https://console.cloud.tencent.com/scf?rid=1)またはCLIによって関数を作成することができます。関数作成の過程では、実行環境の選択（その後の関数作成に使用する言語に基づいて選択します）、関数コードの送信（オンラインでの編集またはローカルでのコードパッケージのアップロードをサポートしています）が必要です。
   - SCFのプリセットテンプレートによる簡略化した作成フローを使用することもできます。詳細については、[関数の作成](https://intl.cloud.tencent.com/document/product/583/19806)をご参照ください。関数の書き方はプログラミング言語によって異なります。詳細については、[SCF](https://intl.cloud.tencent.com/document/product/583)のドキュメントをご参照ください。
2. 関数のテスト
   関数の作成完了後に、テストテンプレート機能を使用して一次テストを行うことができます。テストテンプレートはCOSイベントを再現し、関数の実行をトリガーします。詳細については、[関数のテスト](https://intl.cloud.tencent.com/document/product/583/14572)をご参照ください。
3. トリガーの追加
   一次テストの完了後、COSトリガーを作成してSCF関数をバケットにバインドすることができます。トリガーの追加はコンソールまたはコマンドラインによって行うことができます。詳細については、[トリガーの作成](https://intl.cloud.tencent.com/document/product/583/31441)のドキュメントをご参照ください。
4. 実際の検証
   上記の手順が完了すると、COS内のバケットの操作および、フロー全体が正常かどうかの検証が行えるようになります。例えば、コンソール、COS Browserなどのツールによってファイルをアップロード、削除できるほか、**[SCFコンソール](https://console.cloud.tencent.com/scf?rid=1)** > **関数の詳細** >  **対応する関数名** > **実行ログ**に進み、正常に動作しているかを検証することができます。

SCF COSトリガーに関するその他の詳細については、 [COSトリガー](https://intl.cloud.tencent.com/document/product/583/9707)のドキュメントをご参照ください。
