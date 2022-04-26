## 障害の現象

COS APIを使用してPOSTリクエストを行うと、次のような異常を示すエラーコードが返されます。
- [Condition key q-ak doesn&apos;t match the value XXXXXX](#AccessDenied_q-ak)
- [You post object request has been expired, expiration time: 1621188104 but the time now : 1621245817](#AccessDenied_Expiration)
- [The Signature you specified is invalid.](#SignatureDoesNotMatch_POSTSignature)
- [You must provide condition if you specify a policy in post object request.](#InvalidPolicyDocument_JSONFormat)
- [Condition key bucket doesn&apos;t match the value [bucket-appid]](#AccessDenied_BucketNotConsistent)
- [Condition key key doesn&apos;t match the value XXXXX](#AccessDenied_Condition)
- [The body of your POST request is not well-formed multipart/form-data.](#MalformedPOSTRequest_POSTBody)



## トラブルシューティング

<span id="AccessDenied_q-ak"></span>
### Messageが「Condition key q-ak doesn&apos;t match the value XXXXXX」の場合

COS APIを使用してPOSTリクエストを行うと次のメッセージが表示された場合：

```
<Code>AccessDenied</Code>
<Message>Condition key q-ak doesn&apos;t match the value XXXXXX</Message>
```

#### 考えられる原因

q-akパラメータの入力エラー。

#### ソリューション

1. CAMコンソールにログインし、【[APIキー管理](https://console.cloud.tencent.com/cam/capi)】ページに進み、キー情報を確認します。
2. 確認したキー情報を基に、q-akパラメータに入力エラーがあるかどうかを確認します。
 - 「はい」の場合は、q-akパラメータを正しいSecretIdに変更してください。
 - 「いいえ」の場合は、[お問い合わせ](https://intl.cloud.tencent.com/contact-sales)ください。

<span id="AccessDenied_Expiration"></span>
### Messageが「You post object request has been expired, expiration time: 1621188104 but the time now : 1621245817」の場合

COS APIを使用してPOSTリクエストを行うと次のメッセージが表示された場合：

```
<Code>AccessDenied</Code>
<Message>You post object request has been expired, expiration time: 1621188104 but the time now : 1621245817</Message>
```


#### 考えられる原因

Policyの中のexpirationの値が期限切れになっている。

#### ソリューション

Policyの中のexpirationの値を変更してください。
>! expirationの値は現在時刻より後である必要があります。現在時刻+30分（UTC時刻）に設定することをお勧めします。
>


<span id="SignatureDoesNotMatch_POSTSignature"></span>
### Messageが「The Signature you specified is invalid.」の場合

COS APIを使用してPOSTリクエストを行うと次のメッセージが表示された場合：

```
<Code>SignatureDoesNotMatch</Code>
<Message>The Signature you specified is invalid.</Message>
```

#### 考えられる原因

署名の計算が間違っている。

#### ソリューション

[リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)のドキュメントを参照し、POST署名文字列の生成ルールが正しいかどうかをチェックしてください。


<span id="InvalidPolicyDocument_JSONFormat"></span>
### Messageが「You must provide condition if you specify a policy in post object request.」の場合

COS APIを使用してPOSTリクエストを行うと次のメッセージが表示された場合：

```
<Code>InvalidPolicyDocument</Code>
<Message>You must provide condition if you specify a policy in post object request.</Message>
```


#### 考えられる原因

Policyの形式が間違っている。

#### ソリューション

[POST Object](https://intl.cloud.tencent.com/document/product/436/14690)のドキュメントを参照し、Policyの形式を標準のJSON形式に変更してください。


<span id="AccessDenied_BucketNotConsistent"></span>
### Messageが「Condition key bucket doesn&apos;t match the value [bucket-appid]」の場合

COS APIを使用してPOSTリクエストを行うと次のメッセージが表示された場合：

```
<Code>AccessDenied</Code>
<Message>Condition key bucket doesn&apos;t match the value [bucket-appid]</Message>
```


#### 考えられる原因

Policyのbucketとリクエストされたbucketが異なる。

#### ソリューション

Policyのbucketを使用してリクエストを行ってください。


<span id="AccessDenied_Condition"></span>
### Messageが「Condition key key doesn&apos;t match the value XXXXX」の場合

COS APIを使用してPOSTリクエストを行うと次のメッセージが表示された場合：

```
<Code>AccessDenied</Code>
<Message>Condition key key doesn&apos;t match the value XXXXX</Message>
```


#### 考えられる原因

アップロードしたコンテンツがpolicyルールに適合していない。

#### ソリューション

PolicyのConditionに基づき、その条件に適合したコンテンツをアップロードします。


<span id="MalformedPOSTRequest_POSTBody"></span>
### Messageが「The body of your POST request is not well-formed multipart/form-data.」の場合

COS APIを使用してPOSTリクエストを行うと次のメッセージが表示された場合：

```
<Code>MalformedPOSTRequest</Code>
<Message>The body of your POST request is not well-formed multipart/form-data.</Message>
```

#### 考えられる原因

POST bodyの形式が規定に適合していない。

#### ソリューション

[POST Object](https://intl.cloud.tencent.com/document/product/436/14690)のドキュメントを参照し、bodyの形式を最適化します。




