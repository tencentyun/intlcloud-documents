### ReplyToAddressesというパラメータはどういう意味ですか。
ユーザーのメールボックスへのメール送信が成功し、ユーザーが「返信」ボタンをクリックすると、返信内容がリアルなメールボックスに返されます（メールボックスは通常どおりメールを受信できます）。

### メール送信エラー：FailedOperation.ExceedSendLimitは、その日の総送信量上限の超過というエラーですが、上限はどのくらいで、拡張は可能ですか。
各アカウントの1日あたりの総送信量上限はデフォルトで30万通ですが、拡張は可能です。拡張したい場合は、[Tencent Cloudテクニカルサポート](https://console.cloud.tencent.com/workorder/category)にお問い合わせください。

### SendEmailインターフェースのTemplate.TemplateDataフィールドは、どのように入力すればよいですか。
“`{}`”は変数が渡されないことを意味します。詳細については、APIドキュメント[TemplateData](https://intl.cloud.tencent.com/document/product/1084/39418#Template)のフィールド形式をご参照ください。
