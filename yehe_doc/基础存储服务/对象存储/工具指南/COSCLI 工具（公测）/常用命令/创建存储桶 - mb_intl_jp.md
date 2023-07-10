mbコマンドは、バケットを作成するときに使います。

## コマンド形式

```plaintext
./coscli mb cos://<BucketName-APPID> -r <Region> [flag]
```

mbコマンドには、以下のオプションflagが含まれます。

| flagの略称 | flagの正式名称     | flagの用途                |
| --------- | ------------- | ------------------------ |
| -h        | --help        | ヘルプ情報を出力             |
| -c        | --config-path | 使用する設定ファイルパスを指定 |
| -r        | --region      | バケットリージョン               |

>! COSCLIにおいてmbコマンドで作成したバケットを操作する場合は、mbコマンドが成功した後、config addコマンドで設定ファイル内のバケット設定を更新する必要があります。
>

## 操作事例

```plaintext
// バケットbucket3の作成
./coscli mb cos://bucket3-1250000000 -r ap-chengdu
// 設定ファイルの更新
./coscli config add -b bucket3-1250000000 -r ap-chengdu -a bucket3
// cos://bucket3を更新すると、このバケットにアクセスできるようになります
```
