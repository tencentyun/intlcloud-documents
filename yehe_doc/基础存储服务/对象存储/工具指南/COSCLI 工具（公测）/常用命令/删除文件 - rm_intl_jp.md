rmコマンドは、ファイルを削除するときに使います。

## コマンド形式

```plaintext
./coscli rm cos://<bucketAlias>[/prefix/] [cos://<bucket-name>[/prefix/]...] [flag]
```

>? bucketAliasについては、[設定](https://intl.cloud.tencent.com/document/product/436/43265)をご参照ください。
>

rmコマンドには、以下のオプションflagが含まれます。

| flagの略称 | flagの正式名称     | flagの用途                            |
| --------- | ------------- | ------------------------------------ |
| -h        | --help        | ヘルプ情報を出力                         |
| -c        | --config-path | 使用する設定ファイルパスを指定             |
|     なし      | --include     | 特定のモードを含むファイル                   |
|     なし      | --exclude     | 特定のモードを除外したファイル                   |
| -r        | --recursive   | フォルダ内のすべてのファイルを再帰的にトラバーサル処理するかどうか       |
| -f        | --force       | 強制削除（ファイルを削除するまで確認情報はポップアップ表示されません） |

>?
> - `--include`と`--exclude`は標準的な正規表現の構文をサポートしており、これを使えば特定の条件を満たすファイルをフィルタリングすることができます。
> - zshを使用する場合、pattern文字列の両端に二重引用符を付ける必要がある場合があります。
```
./coscli rm cos://bucket1/example/ -r --include ".*.mp4"
```

## 操作事例

### ファイルの削除

```plaintext
./coscli rm cos://bucket1/fig1.png
```

### pictrueフォルダからすべてのファイルを削除

```plaintext
./coscli rm cos://bucket1/pictrue/ -r
```
