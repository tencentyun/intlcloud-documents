## コマンド形式

syncコマンドは、ファイルのアップロード・ダウンロード・コピーを同期させるときに使います。cpコマンドと異なる点は、syncコマンドはまず同名ファイルのcrc64を比較し、crc64の値が同じ場合は転送を行わない点です。

```plaintext
./coscli sync <source_path> <destination_path> [flag]
```

>? bucketAliasについては、[設定](https://intl.cloud.tencent.com/document/product/436/43265)をご参照ください。

syncコマンドには、以下のオプションflagが含まれます。

| flagの略称 | flagの正式名称     | flagの用途                      |
| --------- | ------------- | ------------------------------ |
| -h        | --help        | ヘルプ情報を出力                   |
| -c        | --config-path | 使用する設定ファイルパスを指定       |
|    なし       | --include     | 特定のモードを含むファイル             |
|   なし         | --exclude     | 特定のモードを除外したファイル             |
| -r        | --recursive   | フォルダ内のすべてのファイルを再帰的にトラバーサル処理するかどうか |
|   なし       | --storage-class | アップロードするファイルのタイプを指定（デフォルトはSTANDARD） |
|   なし       | --part-size     | ファイルチャンクサイズ（デフォルトは32MB）     |
|   なし       | --thread-num    | 同時実行スレッド数（デフォルトの同時実行は5）      |
|   なし       | --rate-limiting | シングルリンクレート制限(0.1～100MB/s)       |


>?
> -syncコマンドは、大容量ファイルのアップロードやダウンロードを行う場合、アップロード/ダウンロードの同時実行を自動的に有効にします。
> - ファイルが`--part-size`よりも大きい場合、COSCLIはまず`--part-size`に従ってファイルをチャンクにし、次に`--thread-num`個のスレッドを使用してアップロード/ダウンロードのタスクを同時に実行します。
> - 各スレッドは1つのリンクを維持します。各リンクに対して`--rate-limiting`パラメータを使用すると、シングルリンクのレート制限ができます。同時アップロード/ダウンロードが有効な場合、合計レートは、`--thread-num * --rate-limiting`となります。
> - ファイルをチャンクでアップロード/ダウンロードする場合、デフォルトで中断からの再開が有効になります。
> - `--include`と`--exclude`は標準的な正規表現の構文をサポートしており、これを使えば特定の条件を満たすファイルをフィルタリングすることができます。
> - zshを使用する場合、pattern文字列の両端に二重引用符を付ける必要がある場合があります。
```
./coscli sync ~/test/ cos://bucket1/example/ -r --include ".*.mp4"
```

## 操作事例

### ファイルの同時アップロード

```plaintext
./coscli sync ~/example.txt cos://bucket1/example.txt
```

### ファイルの同時ダウンロード

```plaintext
./coscli sync cos://bucket1/example.txt ~/example.txt
```

### バケット内でのファイル同期コピー

```plaintext
./coscli sync cos://bucket1/example.txt cos://bucket1/example_copy.txt
```

### バケット間でのファイル同期コピー

```plaintext
./coscli sync cos://bucket1/example.txt cos://bucket2/example_copy.txt
```
