[//]: # (chinagitpath:XXXXX)

APIの呼び出しが失敗した場合、最後に返された結果のエラーコードcodeは0ではなく、messageフィールドに詳細なエラーメッセージが表示されます。ユーザーは、codeとmessageに基づいて[エラーコード](https://cloud.tencent.com/document/product/1014/31229)ページで具体的なエラーメッセージを確認できます。
返されたエラーの例は次の通りです。

```
{
    "code": 5100,
    "message": "(100004)projectIdが正しくない"
}
```

