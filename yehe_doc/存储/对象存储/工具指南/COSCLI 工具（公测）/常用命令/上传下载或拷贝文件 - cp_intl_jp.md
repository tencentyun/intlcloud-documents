
cpコマンドは、ファイルをアップロード、ダウンロードまたはコピーするときに使います。

## コマンド形式

```plaintext
./coscli cp <source_path> <destination_path> [flags]
```

>? bucketAliasについては、[設定](https://intl.cloud.tencent.com/document/product/436/43265)をご参照ください。
>

cpコマンドには、以下のオプションflagが含まれます。

| flagの略称 | flagの正式名称    | flagの用途                            |
| --------- | --------------- | ------------------------------------ |
| -h        | --help        | ヘルプ情報を出力                         |
| -c        | --config-path   | 使用する設定ファイルパスを指定             |
|    なし       | --include       | 特定のモードを含むファイル                   |
|   なし       | --exclude       | 特定のモードを除外したファイル                   |
| -r        | --recursive     | フォルダ内のすべてのファイルを再帰的にトラバーサル処理するかどうか       |
|   なし       | --storage-class | アップロードするファイルのタイプを指定（デフォルトはSTANDARD） |
|   なし       | --part-size     | ファイルチャンクサイズ（デフォルトは32MB）     |
|   なし       | --thread-num    | 同時実行スレッド数（デフォルトの同時実行は5）      |
|   なし       | --rate-limiting | シングルリンクレート制限(0.1～100MB/s)       |


>?
> -cpコマンドは、大容量ファイルのアップロードやダウンロードを行う場合、アップロード/ダウンロードの同時実行を自動的に有効にします。
> - ファイルが`--part-size`よりも大きい場合、COSCLIはまず`--part-size`に従ってファイルをチャンクにし、次に`--thread-num`個のスレッドを使用してアップロード/ダウンロードのタスクを同時に実行します。
> - 各スレッドは1つのリンクを維持します。各リンクに対して`--rate-limiting`パラメータを使用すると、シングルリンクのレート制限ができます。同時アップロード/ダウンロードが有効な場合、合計レートは、`--thread-num * --rate-limiting`となります。
> - ファイルをチャンクでアップロード/ダウンロードする場合、デフォルトで中断からの再開が有効になります。
> - `--include`と`--exclude`は標準的な正規表現の構文をサポートしており、これを使えば特定の条件を満たすファイルをフィルタリングすることができます。
> - zshを使用する場合、pattern文字列の両端に二重引用符を付ける必要がある場合があります。
```
./coscli cp ~/test/ cos://bucket1/example/ -r --include ".*.mp4"
```

## 操作事例

### アップロード操作

#### 単一ファイルのアップロード

```plaintext
./coscli cp ~/example.txt cos://bucket1/example.txt
```

#### ローカルのtestフォルダにあるすべてのファイルをbucket1内のexampleフォルダにアップロードします

```plaintext
./coscli cp ~/test/ cos://bucket1/example/ -r
```

#### ローカルのtestフォルダにあるすべての.mp4タイプのファイルをbucket1内のexampleフォルダにアップロードします

```plaintext
./coscli cp ~/test/ cos://bucket1/example/ -r --include .*.mp4
```

#### ローカルのtestフォルダにあるすべての.mdタイプではないファイルをbucket1内のexampleフォルダにアップロードします

```plaintext
./coscli cp ~/test/ cos://bucket1/example/ -r --exclude .*.md
```

#### ローカルのdirフォルダにはdirA、dirB、dirC、dirDという4つのフォルダがあり、dirフォルダにあるdirDフォルダを除くすべての内容をアップロードします

```plaintext
./coscli cp dir/ cos://bucket1/example/ -r --exclude dirD/.*
```

#### ローカルのtestフォルダにあるすべてのファイルをbucket1内のexampleフォルダにアップロードし、アーカイブタイプのファイルとして保存します

```plaintext
./coscli cp ~/test/ cos://bucket1/example/ -r --storage-class ARCHIVE
```

### ダウンロード操作

#### 単一ファイルのダウンロード

```plaintext
./coscli cp cos://bucket1/example.txt ~/example.txt
```

#### bucket1のexampleフォルダにあるすべてのファイルをローカルのtestフォルダにダウンロードします

```plaintext
./coscli cp cos://bucket1/example/ ~/test/ -r
```

#### bucket1のexampleフォルダにあるすべての.mp4タイプのファイルをローカルのtestフォルダにダウンロードします

```plaintext
./coscli cp cos://bucket1/example/ ~/test/ -r --include .*.mp4
```

#### bucket1のexampleフォルダにあるすべての.mdタイプではないファイルをローカルのtestフォルダにダウンロードします

```plaintext
./coscli cp cos://bucket1/example/ ~/test/ -r --exclude .*.md
```

### コピー操作

#### バケット内の単一ファイルのコピー

```plaintext
./coscli cp cos://bucket1/example.txt cos://bucket1/example_copy.txt
```

#### バケット間の単一ファイルのコピー

```plaintext
./coscli cp cos://bucket1/example.txt cos://bucket2/example_copy.txt
```

#### bucket1のexample1フォルダにあるすべてのファイルをbucket2のexample2フォルダにコピーします

```plaintext
./coscli cp cos://bucket1/example1/ cos://bucket2/example2/ -r
```

#### bucket1のexample1フォルダにあるすべての.mp4タイプのファイルをbucket2のexample2フォルダにコピーします

```plaintext
./coscli cp cos://bucket1/example1/ cos://bucket2/example2/ -r --include .*.mp4
```

#### bucket1のexample1フォルダにあるすべての.mdタイプではないファイルをbucket2のexample2フォルダにコピーします

```plaintext
./coscli cp cos://bucket1/example1/ cos://bucket2/example2/ -r --exclude .*.md
```
