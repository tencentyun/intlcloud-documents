## 機能説明

返された結果のエラーコードは、ユーザーがCloud APIを呼び出した結果を表します。

- codeは、すべてのモジュールのAPIに適用される共通エラーコードです。codeが0の場合、呼び出しは成功します。それ以外の場合、呼び出しは失敗します。呼び出しが失敗した場合、ユーザーは共通エラーコードリストに基づいてエラーの原因を確認し、対処することができます。
- codeDescは、モジュールに関連したエラーを示すモジュールエラーコードです。呼び出しが失敗した場合、ユーザーはモジュールのエラーコードリストに基づいてエラーの原因を確認し、対処することができます。

## エラーコードリスト

### 共通エラーコード

| エラーコード | エラータイプ     | 対処方法                                                     |
| -------- | ------------ | ------------------------------------------------------------ |
| 4000     | 不正なリクエストパラメータ | 必要なパラメータが欠落しているか、パラメータ値のフォーマットが正しくありません。具体的なエラー情報については、エラーの説明messageフィールドを参照してください。 |
| 4100     | 認証失敗     | 署名の認証に失敗しました。                                               |
| 4200     | リクエスト期限切れ     | リクエストは期限切れです。                                               |
| 4300     | アクセスの拒否     | アカウントがブロックされているか、APIの対応ユーザー範囲外です。                 |
| 4400     | 割り当て量超過     | リクエスト数が割り当て量制限を超えています。[チケットの提出](https://console.cloud.tencent.com/workorder/category)を通じてカスタマサービスに連絡してください           |
| 4500     |  Replay Attack     | リクエストのNonceおよびTimestampパラメータは、各リクエストがサーバー側で一度だけ実行されるようにするために使用されます。したがって、今回のNonceを前回のと同じにすることも、TimestampをTencentサーバーの時間から2時間以上離れることもできません。 |
| 4600     | プロトコルはサポートされていない   | プロトコルはサポートされていません。                                                 |
| 5100     | 認証情報作成エラー | APIの認証情報生成エラーで、バックエンドサービスのエラーです。                         |

### モジュールエラーコード

| エラーコード | モジュールエラーコード（codeDesc）                                        | 説明                                                         | 対処方法                                                 |
| ---- | ----------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 4000 | InvalidParameter.policyName.InUse               | ポリシー名はすでに存在します。CAMでは、同じアカウントのポリシー名が重複できません           | 新しいポリシー名を使用してください                                             |
| 4000 | InvalidParameter                                | 無効な入力パラメータ                                                     | 返されたerror messageを参照して、対応するパラメータを確認してください                   |
| 5100 | InternalError                                   | 内部システムエラー                                                 |       -                                                       |
| 4000 | InvalidParameter.AttachmentFull                 | ユーザー/ユーザーグループ/ロールにバインディングされたポリシーが上限に達しました。1人のユーザー/ユーザーグループ/ロールに付加されるポリシーの最大数は200であり、バインディングを続けると失敗します | 古いポリシーをバインディング解除してください                                               |
| 4000 | InvalidParameter.principal.Error                | ポリシー構文のprincipalフィールドエラー                                | ドキュメントの[principal](https://intl.cloud.tencent.com/document/product/598/10603#8..E7.AD.96.E7.95.A5.E6.A0.B7.E4.BE.8B)フィールドの説明を参照してください |
| 4000 | InvalidParameter.action.Error                   | ポリシー構文のactionフィールドエラー                                   | ドキュメントの[action](https://intl.cloud.tencent.com/document/product/598/10603#8..E7.AD.96.E7.95.A5.E6.A0.B7.E4.BE.8B)フィールドの説明を参照してください |
| 4000 | InvalidParameter.effect.Error                   | ポリシー構文のeffectフィールドエラー                                   | ドキュメントのeffectフィールドの説明を参照してください                               |
| 4000 | MissingParameter.action                         | ポリシー構文にactionフィールドがない                                     | ポリシーの構文に[action](https://intl.cloud.tencent.com/document/product/598/10603#8..E7.AD.96.E7.95.A5.E6.A0.B7.E4.BE.8B)フィールドを追加してください |
| 4000 | InvalidParameter.policyName.TypeError           | ポリシー名タイプが正しくありません。ポリシー名は文字列でなければなりません                           | ポリシー名をString型に変更してください                                   |
| 4000 | InvalidParameter.policyName.Error               | ポリシー名に不正な文字が含まれているか、長さが制限を超えています。ポリシー名の最大長さは128バイトです。ポリシー名の文字は、英字、数字、または特殊文字`+=、。@_-`のみで記入可能です | 説明に従ってポリシーの内容を調整してください                                       |
| 4000 | InvalidParameter.policyDocument.TypeError       | ポリシー構文タイプエラー                                             | ポリシー名をString型に変更してください                                   |
| 4000 | MissingParameter.version                        | ポリシー構文にversionフィールドがない                                    | [version](https://intl.cloud.tencent.com/document/product/598/10603#8..E7.AD.96.E7.95.A5.E6.A0.B7.E4.BE.8B)パラメータを入力してください |
| 4000 | InvalidParameter.version.Error                  | ポリシー構文のversionフィールドエラー                                    | ポリシー構文の[version](https://intl.cloud.tencent.com/document/product/598/10603#8..E7.AD.96.E7.95.A5.E6.A0.B7.E4.BE.8B)のフォーマットが正しいかどうかを確認してください |
| 4000 | MissingParameter.statement                      | ポリシー構文にstatementフィールドがない                                  | [statement](https://intl.cloud.tencent.com/document/product/598/10603#8..E7.AD.96.E7.95.A5.E6.A0.B7.E4.BE.8B)パラメータを入力してください |
| 4000 | InvalidParameter.statement.Error                | ポリシー構文のstatementフィールドエラー                                  | ポリシー構文の[statement](https://intl.cloud.tencent.com/document/product/598/10603#8..E7.AD.96.E7.95.A5.E6.A0.B7.E4.BE.8B)のフォーマットが正しいかどうかを確認してください |
| 4000 | InvalidParameter.policyDocument.LengthOverlimit | ポリシー構文の長さが制限を超えており、制限サイズは4096バイトです                   | ポリシー説明の長さを短くしてください。ポリシー内容が多すぎる場合は複数のポリシーに分けることができます           |
| 4000 | InvalidParameter.condition.Error                | ポリシー構文のconditionフィールドエラー                                  | ポリシー構文の[condition](https://intl.cloud.tencent.com/document/product/598/10603#8..E7.AD.96.E7.95.A5.E6.A0.B7.E4.BE.8B)が正しいかどうかを確認してください |
| 4000 | MissingParameter.resource                       | ポリシー構文にresourceフィールドがない                                   | [resource](https://intl.cloud.tencent.com/document/product/598/10603#8..E7.AD.96.E7.95.A5.E6.A0.B7.E4.BE.8B)パラメータを入力してください |
| 4000 | InvalidParameter.resource.Error                 | ポリシー構文のresourceフィールドエラー                                   | ポリシー構文の[resource](https://intl.cloud.tencent.com/document/product/598/10603#8..E7.AD.96.E7.95.A5.E6.A0.B7.E4.BE.8B)のフォーマットが正しいかどうかを確認してください |
| 4000 | InvalidParameter.resource.user.Error            | ポリシー文法のresourceは、自分のアカウントのリソースでない                       | 現在のメインアカウントとして、ポリシー構文の[resource](https://intl.cloud.tencent.com/document/product/598/10603#8..E7.AD.96.E7.95.A5.E6.A0.B7.E4.BE.8B)のリソース所有者を入力してください |
| 4000 | InvalidParameter.description.LengthOverlimit    | ポリシー記述の長さが制限を超えており、制限サイズは300バイトです                    | ポリシー説明の長さを短くしてください                                           |
| 4000 | MissingParameter.policyName                     | policyName入力パラメータがない                                         | policyNameパラメータを入力してください                                       |
| 4000 | MissingParameter.policyDocument                 | policyDocumentパラメータがない                                     | policyDocumentパラメータを入力してください                                   |
| 4000 | InvalidParameter.description.TypeError          | ポリシー説明のタイプが正しくありません。ポリシー説明は文字列でなければなりません                       | ポリシー説明のタイプを確認してください                                           |
| 4000 | InvalidParameter.policyId.NotExist              | ポリシーIDが存在しない                                               | 正しいポリシーIDを使用してください                                         |
| 4000 | MissingParameter.policyId                       | policyId入力パラメータがない                                           | policyIdパラメータを入力してください                                         |
| 4000 | InvalidParameter.policyId.TypeError             | ポリシーIDタイプが正しくありません。ポリシーIDは数字でなければなりません                         | ポリシーIDタイプを確認してください                                           |
| 4000 | InvalidParameter.policyFull                     | このアカウントが所有しているポリシーの数が上限に達し、上限は1000です                     | 無駄なポリシーを削除してください                                             |
| 4000 | InvalidParameter.user.NotExist                  | ユーザーが存在しない、またはポリシー構文principalフィールドのユーザーが存在しません            | 該当するユーザーが存在するか確認してください                                     |
| 4000 | InvalidParameter.group.NotExist                 | ユーザーグループが存在しない、またはポリシー構文principalフィールドのユーザーグループが存在しません        | 該当するユーザーグループが存在するか確認してください                                   |
| 4000 | InvalidParameter.role.NotExist                  | ロールが存在しない                                                   | 対応するロールを作成してください                                             |
| 4000 | InvalidParameter.roleName.TypeError             | ロール名のタイプが正しくありません。ロール名は文字列でなければなりません                           | 説明に従って、ロール名のタイプが有効かどうかを確認してください                             |
| 4000 | InvalidParameter.roleName.Error                 | ロール名に不正な文字が含まれているか、長さが制限を超えています。ロール名の最大長さは128バイトです。ポリシー名の文字は、英字、数字、または`+=、。@_-`のみで記入可能です | 説明に従ってロール名が有効かどうかを確認してください                                       |
| 4000 | InvalidParameter.roleFull                       | アカウントには最大250のロール数上限があります。      | 無駄なロールを削除してください                                             |
| 4000 | InvalidParameter.roleName.InUse                 | ロール名はすでに存在します。同じアカウントのロール名が重複できません                     | 新しいロール名を使用するか、既存の同じ名前のロールを削除してください                       |
| 4000 | CanNotGetOwnerUin                               | ユーザーOwnerUin取得失敗                                       | アカウントが間違っていないか確認してください                                           |
| 4000 | GetAppIdError                                   | ユーザーAppId取得失敗                                          | アカウントが間違っていないか確認してください                                           |
| 4000 | SetTimeOutOfTime                                | ユーザーが設定した一時的認証情報の有効期間が最大制限時間を超えています                           | 具体的なAPIのパラメータの説明を参照してください                                     |
| 4000 | StrategyInvalid                                 | 統合身元一時的証明書設定ポリシー情報の取得エラー                         | message情報を参照してください                                          |
