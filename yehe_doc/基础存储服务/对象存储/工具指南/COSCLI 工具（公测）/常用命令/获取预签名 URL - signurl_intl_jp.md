signurlコマンドは、オブジェクトの事前署名付きURLを取得するために使い、このURLからオブジェクトに匿名でアクセスすることができます。

## コマンド形式

```plaintext
./coscli signurl cos://<bucketAlias>/<key> [flag]
```

>? bucketAliasについては、[設定](https://intl.cloud.tencent.com/document/product/436/43265)をご参照ください。
>

signurlコマンドには、以下のオプションflagが含まれます。

| flagの略称 | flagの正式名称     | flagの用途                    |
| --------- | ------------- | ---------------------------- |
| -h        | --help        | ヘルプ情報を出力                 |
| -c        | --config-path | 使用する設定ファイルパスを指定     |
| -t        | --time        | URLの有効期限を設定（デフォルトは1000s） |

## 操作事例

### bucket1内にあるpicture.jpgの事前署名付きURLを取得します

```plaintext
./coscli signurl cos://bucket1/picture.jpg
```

### bucket2内のpicture.jpgの事前署名付きURLを取得し、URLの有効期限を1314秒に設定します

```plaintext
./coscli signurl cos://bucket2/picture.jpg --time 1314
```

