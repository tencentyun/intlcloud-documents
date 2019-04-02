## 機能説明

このドキュメントでは、APIリクエストでエラーが発生したときに返されるエラーコードと対応するエラーメッセージについて説明します。HTTPのStatusCodeとBodyに基づいて問題を識別できます。Bodyのフォーマットは次のとおりです。
```
{
    "errorcode" : "<ErrorCode>",
    "errormessage" : "<ErrorMessage>"
}
```
## エラーコードリスト

| HTTPステータスコード（StatusCode） | エラーコード（ErrorCode）       | 説明（ErrorMessage）                |
| -------------------- | -------------------- | ------------------------------- |
| 400                   | InvalidAuthorization | 署名文字列のフォーマットが無効です                        |
| 400                  | InvalidCompressType  | 指定されたx-cls-compress-typeはサポートされていません       |
| 400                  | InvalidContent       | メッセージ本文エラー。解凍または解決に失敗します                |
| 400                  | InvalidContentType   |指定されたContent-Typeはサポートされていません              |
| 400                  | InvalidParam         | 必須パラメーターが欠落しているか、一部のパラメーターが無効です                 |
| 400                  | MissingAgentIp       | x-cls-agent-ipが欠落しています                |
| 400                  | MissingAgentVersion  | x-cls-agent-versionが欠落しています           |
| 400                  | MissingAuthorization | Authorizationが欠落しています                 |
| 400                  | MissingContent       | メッセージ本文が空です                          |
| 400                  | MissingContentType   | Content-Typeが欠落しています                  |
| 400                  | TopicClosed          | 指定されたログトピックの収集機能は無効です          |
| 400	               | IndexRuleEmpty	      | 指定されたログトピックにはインデックス規則がありません          |
| 400	               | LogsetNotEmpty       | 指定されたログセットは空ではなく、ログトピックがあります            |
| 401                  | Unauthorized         | 認証に失敗しました。IDエラー、重複署名、署名計算エラーなどが考えられます |
| 403                  | LogsetExceed         | ログセットの数が20の制限を超えています                 |
| 403                  | LogSizeExceed        | 提出されたログのサイズが5MBの制限を超えています               |
| 403                  | MachineGroupExceed   | サーバーグループの数が200個の制限を超えています        |
| 403                  | NotAllowed           | この操作は許可されていません                          |
| 403                  | TopicExceed          | ログトピックの数が10個の制限を超えています                |
| 403                  | ShipperExceed        | 配信規則の数が10個の制限を超えています        |
| 403                  | TaskReadOnly         | 失敗した配信タスクのみを再開でき、他の状態は変更できません   |
| 404                  | CursorNotExist       | 指定された場所にダウンロード可能なログはありません          |
| 404                  | TaskNotExist         | 指定された配信タスクが存在しません                      |
| 404                  | IndexNotExist        | 指定されたインデックス規則は存在しません                      |
| 404                  | LogsetNotExist       | 指定されたログセットが存在しません                       |
| 404                  | MachineGroupNotExist | 指定されたサーバーグループは存在しません                       |
| 404                  | ShipperNotExist      | 指定された配信規則は存在しません                      |
| 404                  | TopicNotExist        | 指定されたログトピックは存在しません                      |
| 404                  | ConsumerNotExist     | 指定されたログトピックには消費タスクが存在しません              |
| 405                  | NotSupported         | この操作はサポートされていません                          |
| 409                  | IndexConflict        | インデックス規則は既に存在します                      |
| 409                  | LogsetConflict       | 同じログセットは既に存在します                       |
| 409                  | MachineGroupConflict | 同じサーバーグループは既に存在します                       |
| 409                  | ShipperConflict      | 同じ配信規則は既に存在します                      |
| 409                  | TopicConflict        | 同じログトピックは既に存在します                      |
| 409                  | ConsumerConflict     | ログトピックの消費タスクは既に存在します              |
| 500                  | InternalError        | 内部エラー                            |

