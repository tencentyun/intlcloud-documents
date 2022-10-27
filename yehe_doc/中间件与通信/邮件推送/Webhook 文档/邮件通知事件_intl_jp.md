コールバックアドレスを設定すると、Tencent Cloudは「配信成功、Tencent Cloudによる配信拒否、ESPバウンス、ユーザーのメール開封、リンクのクリック、購読解除」などのイベント発生後にコールバックアドレスに通知します。コールバックアドレス設定の操作はSESコンソールから行うことができます。[コールバックアドレス](https://intl.cloud.tencent.com/document/product/1084/40183)をご参照ください。

## リクエスト例
```json
{
    "event":"bounce",
    "email":"example@example.com",
    "bulkId":"qcloudses-30-251200670-date-20220601142439-8jolHvR2XcXC1",
    "timestamp":1654064683,
    "reason":"551 5.1.1 recipient is not exist",
    "bounceType":"hard_bounce",
    "username":"251200670",
    "from":"test@fromexample.com",
    "fromDomain":"fromexample.com",
    "templateId":123456
}
```

| フィールド         | タイプ     | 説明                                                                                 |
| ---------- | ------ | ---------------------------------------------------------------------------------- |
| event      | string | イベントタイプ。詳細については、[イベントタイプ](https://intl.cloud.tencent.com/document/product/1084/39492)をご参照ください |
| email      | string | 受信者アドレス                                                                              |
| link       | string | ユーザーがクリックしたメール内のリンクのURL。`event="click"`のときのみ有効です                                               |
| bulkId     | string | SendEmailインターフェースが返すMessageId                                                          |
| timestamp  | int    | イベント発生時のタイムスタンプ                                                                           |
| reason     | string | メール配信が失敗した理由                                                                          |
| bounceType | string | 受信者のメールサービスプロバイダがメールを受信拒否した場合、受信拒否のタイプと値は、soft\_bounce \| hard\_bounceで、`event="bounce"`のときのみ有効です           |
| username   | string | Tencent Cloudアカウントに対応するappId                                                                     |
| from       | string | 送信アドレス（送信者のエイリアスなし）                                                                      |
| fromDomain | string | 送信ドメイン名                                                                               |
| templateId | int    | テンプレートID                                                                              |

## イベントタイプ[](id:Event_Type)
Value|Description
--|--
deferred|メールは受信者のメールサービスプロバイダによりメール配信が遅延し、再試行中です
delivered|配信に成功しました。受信者のメールサービスプロバイダがメッセージを受信しました
dropped|何らかの理由でこのメールは到達せず、破棄されました
open|受信者がこのメールを開封しました
click|受信者がこのメールにあるリンクをクリックしました
bounce|受信者のメールサービスプロバイダがこのメールの受信を拒否しました（通常はEメールアドレスが間違っているため）
spamreport|受信者がこのメールを通報しました
unsubscribe|受信者が業務サイドの「購読解除」ボタンをクリックした場合、業務サイドは購読解除リンクに「unsubscribe」というキーワードを含める必要があります
