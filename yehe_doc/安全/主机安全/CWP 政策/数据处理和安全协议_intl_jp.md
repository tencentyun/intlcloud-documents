## 1\. 背景

本モジュールは、お客様がCloud Workload Protection Platform (CWPP)（以下「**本機能**」）を使用する場合に適用されます。本モジュールは、 に掲載されているData Processing and Security Agreement（データ処理およびセキュリティに関する契約）（以下「[DPSA](https://intl.cloud.tencent.com/document/product/301/17347)」）に組み込まれます。本モジュールにおける用語のうち本書内に定義のないものは、DPSA内で定義された意味を有するものとします。DPSAと本モジュールとの間に矛盾がある場合には、その不一致の範囲で本モジュールを優先するものとします。

## 2\. 処理

当社は、本機能に関連して以下のデータを処理します。

| **個人情報**                                     | **用途**                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| クライアント保護リソース  情報：<br><li>**Tencent Cloudサーバーの保護用**：APPID、UIN、 ご使用のサーバー情報（名前、IPアドレス、タイプ、OS、エージェントバージョン、エージェントインストール日、 最終ログイン時刻、オンラインステータス、インストール済みコンポーネント、 セキュリティレベル）<br><li>**Tencent Cloudサーバー以外の保護用**：リソースモニタリング、 アカウント、ポート、ソフトウェアアプリケーション、プロセス、データベース、Webアプリケーション、 Webサービス、Webフレームワーク、Webサイト、Jarパッケージ、起動サービス、 定期タスク、環境変数、カーネルモジュール | 当社は、お客様に本機能を提供する目的でのみ、 このデータを処理します。 <br/> なお、お客様から許可をいただかない限り、 当社は、データベースに保存されている個人情報がある場合でも、 その情報にアクセスしたり管理したりすることはできません。<br/> このデータは、当社のTencentDB for MySQL（MySQL）機能に保存およびバックアップされますので、その旨ご留意ください。 |
| セキュリティインシデント情報：  **本機能の 無料サブスクリプションの場合：**  <br><li>侵入 検出情報：クライアントサーバー異常ログイン、パスワード クラッキングなどのイベント、関連イベントに関する情報（サーバーUUID、イベント 詳細、脅威レベル、処理ステータス）。  **本機能の 有料サブスクリプションの場合、以下が追加で処理されます。**  <br><li> サーバーのセキュリティホールにおける検出 情報：影響を受けたサーバーのUUID、検出されたセキュリティホールの名称および説明、現在のステータス、最新の検出日時。 <br><li>セキュリティベースライン情報：サーバーの UUID、セキュリティベースラインの名称、検出の種類、セキュリティ脅威レベル、現在のステータス、最新の検出日時。  <br><li>サーバーのセキュリティレポート  ：ログに記録されたクライアント異常ログインの総数、脆弱性  スキャン結果、パスワードクラッキング、悪意のあるファイルスキャン。 お客様が購入した本機能のサブスクリプションの種類。 | 当社は、お客様に本機能を提供する目的でのみ、 このデータを処理します。また、本機能を改善するために、特定のセキュリティインシデント情報を匿名化および非特定化する場合もあります。  <br/>このデータは、当社のMySQL機能で保存およびバックアップされます。 |
| クライアント構成データ：<br><li> 脆弱性/ベースライン/ファイルの検出設定：定期的な検出設定、無視された脆弱性/ベースライン、信頼できるファイル、隔離されたファイル。 <br><li> 侵入防止機能のホワイトリスト設定：ホワイトリスト条件、対象となるサーバー。 <br><li>その他の構成：自動保護アップグレード設定、自動更新設定、アラーム設定。 | 当社は、お客様固有の設定に基づいて本機能をご提供する目的でのみ左記データを処理します。<br/>このデータは、当社のMySQL機能で保存およびバックアップされます。 |

## 3\. サービス地域

DPSAに規定されるとおりです。

## 4\. 副処理者

DPSAに規定されるとおりです。

## 5\. データ保持

当社は、本機能に関連して処理された個人データを以下のとおり保管します。

| **個人情報**                                     | **保持ポリシー**                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| クライアント保護リソース情報セキュリティインシデント情報クライアント構成データ | 当社は、お客様が手動で個人情報を削除するまで当該情報を保持します。それ以外の場合でも、お客様が本機能のサブスクリプションを終了するか、自分のアカウントを削除すると、当社はお客様の個人情報を 7日以内に削除します。 |

お客様は、DPSAに従って、当該個人データの削除を要請することができます。

## 6\. 特別な条件

お客様は、本機能を、個人が自己の個人データの処理に同意できる最低年齢に達しているエンドユーザーのみが使用できるようにしなければなりません。これは、エンドユーザーが所在する司法管轄区によって異なる場合があります。