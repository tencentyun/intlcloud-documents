restoreコマンドは、アーカイブファイルを取得するときに使います。

## コマンド形式


```plaintext
./coscli restore cos://<bucketAlias>[/prefix/] [flag]
```

>? bucketAliasについては、[設定](https://intl.cloud.tencent.com/document/product/436/43265)をご参照ください。
>

restoreコマンドには、以下のオプションflagが含まれます。

| flagの略称 | flagの正式名称    | flagの用途                         |
| --------- | ------------- | --------------------------------- |
| -h        | --help        | ヘルプ情報を出力                      |
| -c        | --config-path | 使用する設定ファイルパスを指定          |
|    なし      | --include     | 特定のモードを含むファイル                   |
|    なし       | --exclude     | 特定のモードを除外したファイル                   |
| -d        | --days        | 一時ファイルの有効期限を指定（デフォルトは3日間） |
| -m        | --mode        | リカバリモードを指定（デフォルトはStandard）      |
| -r        | --recursive   | フォルダの再帰的なトラバーサル処理       |

>?
> - `--include`と`--exclude`は標準的な正規表現の構文をサポートしており、これを使えば特定の条件を満たすファイルをフィルタリングすることができます。
> - zshを使用する場合、pattern文字列の両端に二重引用符を付ける必要がある場合があります。
```
./coscli restore cos://bucket1/example/ -r --include ".*.mp4"
```

## 操作事例

### 標準モードでbucket1のアーカイブファイルを取得します

```plaintext
./coscli restore cos://bucket1/picture.jpg
```

### bucket1内のpictureフォルダにあるすべてのアーカイブファイルを超高速モードで取得します

```plaintext
./coscli restore cos://bucket1/picture/ -r --mode Expedited
```

>? このコマンドを実行する前に、フォルダ内のすべてのファイルが同じタイプ（例：ARCHIVEタイプ）であることを確認する必要があります。異なるタイプのファイルがある場合は、`--include`または`--exclude`を使用して、同じタイプのファイルをフィルタリングで除外してください。
>

