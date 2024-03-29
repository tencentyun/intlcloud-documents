## 1\. **背景**

本モジュールは、お客様がBastion Host機能（「**本機能**」）を利用する場合に適用されます。本モジュールは、DPSAに掲載されているData Processing and Security Agreement（データ処理およびセキュリティに関する契約）（以下「[DPSA](https://intl.cloud.tencent.com/document/product/301/17347 )」）に組み込まれます。本モジュールにおける用語のうち本書内に定義のないものは、DPSA内で定義された意味を有するものとします。DPSAと本モジュールとの間に矛盾がある場合には、その不一致の範囲で本モジュールを優先するものとします。

## 2\. **処理**

当社は、本機能に関連して以下のデータを処理します。

| **個人情報**                                     | **用途**                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| **アセット管理情報：** ホストIP、ホストOS、ホストポート、ホストアカウント、データベースIP、データベースタイプ、データベースポート、データベースアカウント、アセットグループ、アセットパスワード | 当社は、お客様固有の設定に基づいて本機能をご提供する目的でのみ左記データを処理します。なお、左記情報は当社のMySQL機能に保存されます。 |
| **支払記録データ：** インスタンスID、クライアントIP、インスタンス番号、有効期限、リージョン、操作 | 当社は、お客様固有の設定に基づいて本機能をご提供する目的でのみ左記データを処理します。なお、左記情報は当社のMySQL機能に保存されます。 |
| **アクセス制御情報：** 権限名、ステータス、ユーザー名、アセットアカウント、承認されたアクション、危険度の高いコマンド | 当社は、お客様固有の設定に基づいて本機能をご提供する目的でのみ左記データを処理します。なお、左記情報は当社のMySQL機能に保存されます。 |
| **ユーザー管理情報：** 名前、電話番号、検証方法、電子メール、ユーザーグループ、アクセス時間 | 当社は、お客様固有の設定に基づいて本機能をご提供する目的でのみ左記データを処理します。なお、左記情報は当社のMySQL機能に保存されます。 |
| **メンテナンス情報：** タスクID/名前、実行方法、実行期間、実行時刻、実行コマンド、アセット情報 | 当社は、お客様固有の設定に基づいて本機能をご提供する目的でのみ左記データを処理します。なお、左記情報は当社のMySQL機能に保存されます。 |
| **操作ログ：** アセットIP、ソースIP、アセットアカウント、時刻、アセット名、ユーザー名、セッション期間\セッションサイズ、コマンド量\ブロックコマンド量、ステータス、操作の再生 | 当社は、お客様固有の設定に基づいて本機能をご提供する目的でのみ左記データを処理します。なお、左記情報は当社のMySQL機能に保存されます。 |
| **システムアクセスログ：** 時刻、ユーザー名、ソースIP、ログイン方法、ログイン結果、解像度、アクセスモード。 | 当社は、お客様固有の設定に基づいて本機能をご提供する目的でのみ左記データを処理します。なお、左記情報は当社のMySQL機能に保存されます。 |
| **監査ログ：** 時刻、監査担当者アカウント、ソースIP、監査対象アセットID、監査対象アセットIP、操作、セッションタイプ、監査の詳細 | 当社は、お客様固有の設定に基づいて本機能をご提供する目的でのみ左記データを処理します。なお、左記情報は当社のMySQL機能に保存されます。 |
| **リスクイベントログ：** イベントの種類、イベントの説明、時刻    | 当社は、お客様固有の設定に基づいて本機能をご提供する目的でのみ左記データを処理します。なお、左記情報は当社のMySQL機能に保存されます。 |
| **システム構成：** ホワイトリスト、セキュリティ設定（Web非アクティブ期間、パスワードエラー回数、 ブロック期間）、設定の確認（パスワードの複雑さ、パスワードの最小文字数、パスワードの有効期限、過去の同じパスワード、2要素認証、LDAP情報） | 当社は、お客様固有の設定に基づいて本機能をご提供する目的でのみ左記データを処理します。なお、左記情報は当社のMySQL機能に保存されます。 |
| **バックアップログ：** システムログインログ（時刻、ユーザー名、ソースIP、ログイン方法、ログイン結果）、アセットログインログ（アセットIP、ソースIP、アセットアカウント、時刻、アセット名、ユーザー名、セッション期間） | 当社は、お客様固有の設定に基づいて本機能をご提供する目的でのみ左記データを処理します。なお、このデータは当社のSecurity Operations Center機能にバックアップされます。 |

## 3\. **サービス地域**

DPSAに規定されるとおりです。

## 4\. **副処理者**

DPSAに規定されるとおりです。

## 5\. **データ保持**

当社は、本機能に関連して処理された個人データを、以下のとおり保管します（適用されるデータ保護法によって別途要求される場合を除きます）。

| **個人情報**         | **保持ポリシー**                                         |
| -------------------------------- | ------------------------------------------------------------ |
| **アセット管理情報** | 当社は、お客様が本機能のサブスクリプションを終了するまで当該データを保持しますが、サブスクリプション終了日から7日以内に削除します。 |
| **支払記録データ**         | 当社は、お客様が本機能のサブスクリプションを終了するまで当該データを保持しますが、サブスクリプション終了日から7日以内に削除します。 |
| **アクセス制御情報**   | 当社は、お客様が本機能のサブスクリプションを終了するまで当該データを保持しますが、サブスクリプション終了日から7日以内に削除します。 |
| **ユーザー管理情報**  | 当社は、お客様が本機能のサブスクリプションを終了するまで当該データを保持しますが、サブスクリプション終了日から7日以内に削除します。 |
| **メンテナンス情報**      | 当社は、お客様が本機能のサブスクリプションを終了するまで当該データを保持しますが、サブスクリプション終了日から7日以内に削除します。 |
| **操作ログ**                | 当社は、お客様が本機能のサブスクリプションを終了するまで当該データを保持しますが、サブスクリプション終了日から7日以内に削除します。 |
| **システムアクセスログ**            | 当社は、お客様が本機能のサブスクリプションを終了するまで当該データを保持しますが、サブスクリプション終了日から7日以内に削除します。 |
| **監査ログ**                    | 当社は、お客様が本機能のサブスクリプションを終了するまで当該データを保持しますが、サブスクリプション終了日から7日以内に削除します。 |
| **リスクイベントログ**               | 当社は、お客様が本機能のサブスクリプションを終了するまで当該データを保持しますが、サブスクリプション終了日から7日以内に削除します。 |
| **システム構成**         | 当社は、お客様が本機能のサブスクリプションを終了するまで当該データを保持しますが、サブスクリプション終了日から7日以内に削除します。 |
| **バックアップログ**                   | 当社は、お客様が本機能のサブスクリプションを終了するまで当該データを保持しますが、サブスクリプション終了日から7日以内に削除します。 |

お客様は、DPSAに従って、当該個人データの削除を要請することができます。

## 6\. **特別な条件**

お客様は、(i) 当社が本機能が適用される法令に準拠することを表明または保証せず、約束しないこと、(ii) 本機能の使用において、または関連して求められる可能性のある必要なライセンス、登録、または承認を取得していること（支払処理活動に関連することなど、その記録は、本機能の一部として反映される場合があります）、および (iii) 本機能への依存または使用は、お客様の単独の責任において行われることを了承し、理解し、これに同意するものとします。