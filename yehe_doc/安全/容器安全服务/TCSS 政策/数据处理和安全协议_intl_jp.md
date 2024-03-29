## 1\. 背景

本モジュールは、お客様がTencent Container Security Service（「**本機能**」）を使用する場合に適用されます。本モジュールは、DPSAに掲載されているData Processing and Security Agreement（データ処理およびセキュリティに関する契約）（以下「[DPSA](https://intl.cloud.tencent.com/document/product/301/17347)」）に組み込まれます。本モジュールにおける用語のうち本書内に定義のないものは、DPSA内で定義された意味を有するものとします。DPSAと本モジュールとの間に矛盾がある場合には、その不一致の範囲で本モジュールを優先するものとします。

## 2\. 処理

当社は、本機能に関連して以下のデータを処理します。

| **個人情報**                                     | **用途**                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| **アセット基本データ：** サーバー、コンテナ、イメージ、およびクラスタの基本情報（アセットフィンガープリント情報（リソースモニタリング、アカウント、ポート、ソフトウェアアプリケーション、プロセス、データベース、Webアプリケーション、Webサービス、Webフレームワーク、Webサイト、Jarパッケージ起動サービス、定期実行タスク、環境変数、カーネルモジュール）、イメージリポジトリの基本情報（イメージリポジトリアドレス、リポジトリタイプ、イメージ名、イメージID、イメージバージョン、イメージサイズ、 セキュリティリスク（セキュリティ脆弱性、トロイの木馬ウイルス、機密情報を含む）、構築履歴） | 当社は、お客様に本機能を提供する目的でのみ、このデータを処理します。<br/>なお、このデータは、TencentDB for MongoDB（MongoDB）およびTencentDB for MySQL（MySQL）機能に保存およびバックアップされ、当社のクラウドオブジェクトストレージ（COS）機能に一時的に保存およびバックアップされ、 お客様が登録している関連ホスティングサービス（この機能のプライバシーポリシーモジュールで定義される）と統合されます。お客様が当社のTencent Kubernetes Engine（TKE）クラスタを購入した場合、お客様に本機能を提供すること（セキュリティチェックの実行を含む）を目的として、お客様の承認を得た上でイメージリポジトリの基本情報も当社と共有されます。 |
| **コンソール構成データ：**<br/><li>イメージ、クラスタ、脆弱性、ベースライン、ファイル、  ログ検出の構成：定期的な検出、脆弱性/ベースラインの無視、お客様によるファイルの信頼またはファイルの隔離の確認、プロセスの傍受、イメージの傍受、コンテナネットワークアクセスの傍受）<li>コンテナエスケープ、リバースシェル、ファイルチェック、異常プロセス、ファイル改ざん、高リスクシステムドロップコール、およびその他の侵入防御機能のホワイトリスト構成：ホワイトリスト条件、有効なミラー範囲、その他の構成情報：自動サーバーアップグレード保護設定、自動更新設定、アラーム設定 | 当社は、お客様固有の設定に基づいて本機能をご提供する目的でのみ左記データを処理します。<br/>なお、このデータは、TencentDB for MongoDB（MongoDB）およびTencentDB for MySQL（MySQL）機能に保存およびバックアップされ、お客様が登録している関連ホスティングサービス（この機能のプライバシーポリシーモジュールで定義される）と統合されます。 |

## 3\. サービス提供地域

DPSAに規定されるとおりです。

## 4\. 副処理者

DPSAに規定されるとおりです。

## 5\. データ保持

当社は、本機能に関連して処理された個人データを以下のとおり保管します。

| **個人情報**   | **保持ポリシー**                                         |
| -------------------------- | ------------------------------------------------------------ |
| アセット基本データ           | 当該データは、最低でも180日間保持されます。当社は、お客様が関連ホスティングサービスの使用を終了するまで当該データを保持します。その場合、当社はこのデータを当社のCOS機能に一時的に保持し、(i) 30日後または (ii) 180日間の最小データ保持しきい値を満たすために必要な最小日数（該当する場合）の経過後、当該データを削除します。 |
| コンソール構成データ | お客様が削除を要請するまで保存され、その後30営業日以内に削除されます。お客様が削除を要求しない場合、当該データは、適用されるデータ保護法で別段の定めがない限り、この機能の使用が終了してから1か月後に削除されます。 |

お客様は、DPSAに従って、当該個人データの削除を要請することができます。

## 6\. 特別な条件

お客様は、本機能を、個人が自己の個人データの処理に同意できる最低年齢に達しているエンドユーザーのみが使用できるようにしなければなりません。これは、エンドユーザーが所在する司法管轄区によって異なる場合があります。

本機能は、機密データの処理を目的としたものではありません。お客様は、本機能がお客様またはお客様のエンドユーザーによる機密データの転送またはその他の処理に使用されないことを保証しなければなりません。