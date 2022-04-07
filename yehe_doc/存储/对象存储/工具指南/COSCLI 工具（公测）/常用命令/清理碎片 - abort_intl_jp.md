abortコマンドは、マルチパートアップロード中に発生したファイルフラグメントをクリーンアップするときに使います。

## コマンド形式

```plaintext
./coscli abort cos://<bucketAlias>[/prefix/] [flag]
```

>? bucketAliasについては、[設定](https://intl.cloud.tencent.com/document/product/436/43265)をご参照ください。
>

abortコマンドには、以下のオプションflagが含まれます。

| flagの略称 | flagの正式名称     | flagの用途                |
| --------- | ------------- | ------------------------ |
| -h        | --help        | ヘルプ情報を出力             |
| -c        | --config-path | 使用する設定ファイルパスを指定 |
|    なし       | --include     | 特定のモードを含むファイル       |
|   なし         | --exclude     | 特定のモードを除外したファイル       |

## 操作事例

### bucket1にあるすべてのファイルフラグメントをクリア

```plaintext
./coscli abort cos://bucket1
```

### bucket1のpictrueフォルダにあるすべてのフラグメントをクリア

```plaintext
./coscli abort cos://bucket1/picture/
```
