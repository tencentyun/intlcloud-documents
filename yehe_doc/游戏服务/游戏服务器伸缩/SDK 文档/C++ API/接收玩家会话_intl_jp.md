

### インターフェースの説明
このインターフェース（AcceptPlayerSession）は、PlayerSessionの合法性の検証に使用します。GameServerSessionのステータスがActiveで、かつプレイヤーがJoinGameServerSessionまたはJoinGameServerSessionBatchを呼び出したことがあれば、受け入れに成功します。PlayerSessionのステータスを「ACTIVE」に設定します。

JoinGameServerSessionまたはJoinGameServerSessionBatchを呼び出し、60秒以内にレスポンスを受信しない場合は、PlayerSessionのステータスを「TIMEOUT」に変更し、その後にゲームセッション中のプレイヤー位置を改めてリザーブしてください。

### パラメータの説明

|パラメータ名|タイプ/値|説明|
|:---|---|---|
|playerSessionId|String|プレイヤーセッションID|


### 戻り値の説明

- True：成功。
- False：失敗。

エラーメッセージを含む一般的な結果。具体的なタイプはGenericOutcomeです。


### ユースケース
```
TencentCloud::Gse::GenericOutcome outcome = 
   	TencentCloud::Gse::Server::AcceptPlayerSession(playerSessionId);
if(outcome .IsSuccess())
{
        //接続の受け入れ
}
else 
{
        //接続の拒否
} 
```

