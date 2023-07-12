
duコマンドは、バケットまたはフォルダ内の各バケットタイプのファイルの統計情報を一覧表示するために使います。この統計情報には、異なるストレージタイプのファイルの総数や各タイプのファイルの合計サイズが含まれます。

## コマンド形式

```plaintext
./coscli du cos://<bucketAlias>[/prefix/] [flag]
```

>? bucketAliasについては、[設定](https://intl.cloud.tencent.com/document/product/436/43265)をご参照ください。
>

lsコマンドには、次のオプションのパラメータが含まれます。

| パラメータ形式 | パラメータ用途       | 事例                 |
| -------- | -------------- | -------------------- |
| /prefix/ | いずれかのフォルダを指定します | cos://bucket1/picture/ |

duコマンドには、以下のオプションflagが含まれます。

| flagの略称 | flagの正式名称     | flagの用途                |
| --------- | ------------- | ------------------------ |
| -h        | --help        | ヘルプ情報を出力             |
| -c        | --config-path | 使用する設定ファイルパスを指定 |
|    なし       |--include     | 特定のモードを含むファイル                   |
|      なし       |--exclude     | 特定のモードを除外したファイル       |

>? 
>- `--include` は標準的な正規表現の構文をサポートしており、これを使えば特定の条件を満たすファイルをフィルタリングすることができます。
>- zshを使用する際、pattern文字列の両端に二重引用符を付ける必要がある場合があります。
```plaintext
./coscli du cos://bucket1/picture/ --include ".*.mp4"
```

## 操作事例

### bucket1にあるファイルの統計情報を一覧表示します

```plaintext
./coscli du cos://bucket1
```

### bucket1のpictrueフォルダにあるファイルの統計情報を一覧表示します

```plaintext
./coscli du cos://bucket1/picture/
```

### bucket1のpictrueフォルダにあるすべての.mp4タイプのファイルの統計情報を一覧表示します

```plaintext
./coscli du cos://bucket1/picture/ --include .*.mp4
```

### bucket1のpictrueフォルダにあるすべての.mdタイプのファイルの統計情報を一覧表示します

```plaintext
./coscli du cos://bucket1/picture/ --exclude .*.md
```
