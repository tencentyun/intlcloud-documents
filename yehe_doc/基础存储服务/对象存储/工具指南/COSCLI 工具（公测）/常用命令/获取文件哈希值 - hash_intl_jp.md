hashコマンドは、ローカルファイルのハッシュ値を計算したり、Cloud Object Storage(COS)ファイルのハッシュ値を取得したりするために使います。

## コマンド形式


```plaintext
./coscli hash <object-name> [flag]
```

>? bucketAliasについては、[設定](https://intl.cloud.tencent.com/document/product/436/43265)をご参照ください。
>

hashコマンドには、以下のオプションflagが含まれます。

| flagの略称 | flagの正式名称     | flagの用途                              |
| --------- | ------------- | -------------------------------------- |
| -h        | --help        | ヘルプ情報を出力                           |
| -c        | --config-path | 使用する設定ファイルパスを指定               |
|     なし      | --type        | ハッシュタイプ（md5またはcrc64で、デフォルトはcrc64） |

## 操作事例

### ローカルファイルのcrc64を計算します

```plaintext
./coscli hash ~/test.txt
```

### COSファイルのmd5を取得します

```plaintext
./coscli hash cos://bucket1/example.txt --type=md5
```
