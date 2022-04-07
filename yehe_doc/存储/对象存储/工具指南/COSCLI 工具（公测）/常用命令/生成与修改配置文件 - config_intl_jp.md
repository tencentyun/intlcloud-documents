
## コマンド形式

以下のconfigコマンドは、設定ファイルを発行・変更するときに使います。

```
./coscli config [command] [flag]
```

>? 各設定項目を正しく入力すると、`./coscli config show`を使用して設定情報を確認することができます。
>

<span id="config"></span>

configコマンドには、以下のサブコマンドが含まれます。

| command名 | commandの用途                               |
| ------------ | ------------------------------------------ |
| add          | 新しいバケット設定を追加します。                   |
| delete       | 既存のバケット設定を削除します。             |
| init         | 設定ファイルをインタラクティブに作成します。                     |
| set          | 設定ファイルのbaseグループの1つまたは複数の設定項目を変更します。 |
| show         | 指定された設定ファイルの情報を印刷します。                 |

configとそのサブコマンドには、以下のオプションflagが含まれます。

| flagの略称 | flagの正式名称     | flagの用途                  |
| --------- | ------------- | -------------------------- |
| -h        | --help        | ヘルプ情報を出力します。             |
| -c        | --config-path | 使用する設定ファイルパスを指定します。 |

config addサブコマンドには、以下のオプションflagが含まれます。

| flagの略称 | flagの正式名称 | flagの用途    |
| --------- | --------- | ------------ |
| -a        | --alias   | バケットエイリアス。 |
| -b        | --bucket  | バケット名。 |
| -r        | --region  | バケットリージョン。 |

config deleteサブコマンドには、以下のオプションflagが含まれます。

| flagの略称 | flagの正式名称 | flagの用途    |
| --------- | --------- | ------------ |
| -a        | --alias   | バケットエイリアス。 |

config setサブコマンドには、以下のオプションflagが含まれます。

| flagの略称 | flagの正式名称    | flagの用途         |
| --------- | ------------ | ----------------- |
| -i        | --secret_id  | secret IDを設定します。  |
| -k        | --secret_key | secret keyを設定します。 |
| -t        | --token      | tokenを設定します。      |

## 操作事例

### 新しいバケット設定の追加

```
./coscli config add -b examplebucket3-1250000000 -r ap-chengdu -a bucket3
```

### 既存のバケット設定の削除

```
./coscli config delete -a bucket3
```

### デフォルトの設定ファイルのsession-tokenの変更

```
./coscli config set -t test-token123
```

### 指定された設定ファイルの情報の印刷

```
./coscli config show -c /your/config/path.yaml
```
