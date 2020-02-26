## 使用説明
このスクリプトは、指定されたドメイン名と指定された日付（日付範囲は30日以内）のログデータパケットを取得するために使用されます。

[スクリプトのダウンロード](https://mc.qcloudimg.com/static/archive/b958077bcfeb0a4a35995f4790a91f7c/GetDayLog.zip)

**動作環境**：
+ Python2.7
+ Linux システム

### 使用前準備

上記のpythonスクリプトを使用するには、requestsをインストールする必要があります。以下のコマンドを使用してください。

```
pip install requests
```

##### パラメータの説明

```
hostドメイン名
-u SECRET_ID
-p SECRET_KEY
--day 日付
--dstpath ログのダウンロードパス
```

+ SecretIdとSecretKeyは[クラウドAPIキー](https://console.cloud.tencent.com/capi)で取得されます。
+30日以内のログダウンロードのみ対応します。
+ デフォルトでは、指定された日付のログストレージアドレスは現在のパスです。

### 実例

```
python GetDayLog.py www.test.com -u XXXXXXXXXXXXXXX -p XXXXXXXXXXXXXX --day 20161130 --dstpath /home/test/
```

使用に成功すると、指定されたディレクトリの下に必要なログファイルを見ることができます。ファイル名は：

```
20161130-www.test.com.gz
```

