lsコマンドは、すべてのバケットリスト、バケット内のファイルリストおよびフォルダ内のファイルリストを照会するために使います。

## コマンド形式

```plaintext
./coscli ls [cos://bucketAlias[/prefix/]] [flag]
```

>? bucketAliasについては、[設定](https://intl.cloud.tencent.com/document/product/436/43265)をご参照ください。
>

lsコマンドには、次のオプションのパラメータが含まれます。

| パラメータ形式          | パラメータ用途       | 事例                 |
| ----------------- | -------------- | -------------------- |
| cos://bucketAlias | バケットの指定     | cos://bucket1          |
| /prefix/          | いずれかのフォルダを指定します | /picture/ |

lsコマンドには、以下のオプションflagが含まれます。

| flagの略称 | flagの正式名称   | flagの用途                            |
| --------- | ----------- | ------------------------------------ |
| -h        | --help      | ヘルプ情報を出力                         |
|     なし      | --include   | 特定のモードを含むファイル                   |
|     なし       | --exclude     | 特定のモードを除外したファイル                   |
| -r        | --recursive   | フォルダを再帰的にトラバーサル処理、してすべてのファイルを一覧表示するかどうか |

>? 
> - `--include`と`--exclude`は標準的な正規表現の構文をサポートしており、これを使えば特定の条件を満たすファイルをフィルタリングすることができます。
> - zshを使用する場合、pattern文字列の両端に二重引用符を付ける必要がある場合があります。
```plaintext
./coscli ls cos://bucket1 -r --include ".*.mp4"
```

## 操作事例


### 現在のアカウント下のすべてのバケットを一覧表示します

```plaintext
./coscli ls
```

### ファイルの一覧表示

### bucket1にあるすべてのファイルを一覧表示します

```plaintext
./coscli ls cos://bucket1
```

#### bucket1内のpictureフォルダにあるすべてのファイルとフォルダを一覧表示します

```plaintext
./coscli ls cos://bucket1/picture/
```

### bucket1内のpictrueフォルダにあるすべてのファイルを再帰的に一覧表示します

```plaintext
./coscli ls cos://bucket1/picture/ -r
```

#### bucket1内の.mp4タイプのすべてのファイルを再帰的に一覧表示します

```plaintext
./coscli ls cos://bucket1 -r --include .*.mp4
```



#### bucket1内の.mp4タイプ以外のすべてのファイルを再帰的に一覧表示します

```plaintext
./coscli ls cos://bucket1 -r --exclude .*.mp4
```

#### bucket1内のpictureフォルダ内のtestで始まり、jpgタイプではないすべてのファイルを再帰的に一覧表示します

```plaintext
./coscli ls cos://bucket1/picture -r --include ^picture/test.* --exclude .*.jpg
```
