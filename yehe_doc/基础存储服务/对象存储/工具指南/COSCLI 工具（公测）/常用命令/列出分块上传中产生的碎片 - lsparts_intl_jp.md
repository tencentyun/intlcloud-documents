lspartsコマンドは、マルチパートアップロード中に発生したフラグメントを一覧表示します。

## コマンド形式

```plaintext
./coscli lsparts cos://<bucketAlias>[/prefix/] [flag]
```

>? bucketAliasについては、[設定](https://intl.cloud.tencent.com/document/product/436/43265)をご参照ください。
>

lspartsコマンドには、以下のオプションflagが含まれます。

| flagの略称 | flagの正式名称     | flagの用途                    |
| --------- | ------------- | ---------------------------- |
| -h        | --help        | ヘルプ情報を出力                 |
| -c        | --config-path | 使用する設定ファイルパスを指定     |
|     なし      | --include     | 特定のモードを含むファイル           |
|     なし      | --exclude     | 特定のモードを除外したファイル           |
|     なし      | --limit       | 一覧表示する最大数（0～1000）を指定 |

## 操作事例

### bucket1にあるすべてのファイルフラグメントを一覧表示

```plaintext
./coscli lsparts cos://bucket1
```

### bucket1のpictrueフォルダにあるすべてのフラグメントを一覧表示

```plaintext
./coscli lsparts cos://bucket1/pictrue/
```
