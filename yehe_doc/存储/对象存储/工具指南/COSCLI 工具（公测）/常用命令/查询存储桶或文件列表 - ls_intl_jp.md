lsコマンドは、すべてのバケットリスト、バケット内のファイルリストおよびフォルダ内のファイルリストを照会するために使います。

## コマンド形式

```plaintext
./coscli ls [cos://bucketAlias[/prefix/]]
```

>? 
>? bucketAliasについては、[ダウンロードとインストール設定](https://intl.cloud.tencent.com/document/product/436/43265)をご参照ください。
>- このコマンドのその他の共通オプション（例えばバケットの切り替え、ユーザーアカウントの切り替えなど）に関しては、[共通オプション](https://intl.cloud.tencent.com/document/product/436/46273)のドキュメントをご参照ください。
>

lsコマンドには、次のオプションのパラメータが含まれます。

| パラメータ形式          | パラメータ用途       | 事例                 |
| ----------------- | -------------- | -------------------- |
| cos://bucketAlias | バケットの指定     | cos://bucket1          |
| /prefix/          | いずれかのフォルダを指定します | /picture/ |




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


