rbコマンドは、バケットを削除するときに使います。

## コマンド形式

```plaintext
./coscli rb cos://<BucketName-APPID> -r <Region> [flag]
```

rbコマンドには、以下のオプションflagが含まれます。

| flagの略称 | flagの正式名称     | flagの用途                |
| --------- | ------------- | ------------------------ |
| -h        | --help        | ヘルプ情報を出力             |
| -c        | --config-path | 使用する設定ファイルパスを指定 |
| -r        | --region      | バケットリージョン               |

## 操作事例

```plaintext
// bucket3の削除
./coscli rb cos://bucket3-1250000000 -r ap-chengdu
// 設定ファイルの更新
./coscli config delete -a bucket3
```
