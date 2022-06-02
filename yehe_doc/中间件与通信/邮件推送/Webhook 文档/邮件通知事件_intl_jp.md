メールに配信、失敗、バウンス、開封、クリック、購読解除といったイベントが発生すると、Tencent Cloudはそれをメッセージ通知としてコールバックアドレスに配信します。以下にイベントプッシュのプロトコル形式を示します。
## リクエスト例
```json
{
  "event": "delivered",
  "email": "example@example.com",
  "bulkId": "qcloud-ses-4F001945B2D9BXXXXXX",
  "timestamp": 1587953211,
  "reason": "the reason when email failed to delivered",
  "bounceType": ""
}
```

フィールド|タイプ|説明
--|--|--
event|string|イベントタイプ。詳細については、[イベントタイプ](#Event_Type)をご参照ください
email|string|受信者アドレス
link|string|ユーザーがクリックしたメール内のリンクのURL。`event="click"`のときのみ有効です。
bulkId|string|SendEmailインターフェースが返すMessageId
timestamp|int|イベント発生時のタイムスタンプ
reason|string|メール配信が失敗する理由
bounceType|string|受信者のメールサービスプロバイダがメールを受信拒否した場合、受信拒否のタイプと値は、soft &brvbar; hardで、`event="bounce"`のときのみ有効です

[](id:Event_Type)
## イベントタイプ
Value|Description
--|--
processed|配信では、この状態は中間的なものであり、必ずしもコールバックされるわけではありません
deferred|メールは受信者のメールサービスプロバイダによりメール配信が遅延し、再試行中です
delivered|配信に成功しました。受信者のメールサービスプロバイダがメッセージを受信しました
dropped|何らかの理由でこのメールは到達せず、破棄されました
open|受信者がこのメールを開封しました
click|受信者がこのメールにあるリンクをクリックしました
bounce|受信者のメールサービスプロバイダがこのメールの受信を拒否しました（通常はEメールアドレスが間違っているため）
spamreport|受信者がこのメールを通報しました
unsubscribe|受信者が業務サイドの「購読解除」ボタンをクリックした場合、業務サイドは購読解除リンクに「unsubscribe」というキーワードを含める必要があります
