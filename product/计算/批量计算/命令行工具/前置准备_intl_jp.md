CLIをインストールする前に、システムにPython環境がインストールされていることを確認してください。具体的には、Python2.7とpython-pipをインストールする必要があります。

## 1. Tencent Cloud CLIのインストール	
### I. **内部テスト申請に合格したこと**を確認します
それ以外の場合は、CLIのBatch関連コマンドを使用するときにアクセス権限がないメッセージが表示されます。

### II. CLIをインストールします：
* CLIがインストールされていない場合：pipを使って、Tencent Cloud CLIを素早くインストールできます。
```
$ sudo pip install qcloudcli
```

* CLIがインストールされている場合：pipを通してクイックアップグレードができます。コマンドは以下のとおりです
```
$ sudo pip install --upgrade qcloudcli
```

### III. CLIが正常にインストールされ、Batchの関連機能が含まれていることを確認します：
```
$ qcloudcli batch help
You should use the qcloudcli as follow format:
qcloudcli <module> <action> [options and parameters]
The action name you input is error! The module [batch] support the valid action as follows:

DescribeAvailableCvmInstanceTypes       	|DescribeTask
DescribeJob                             	|SubmitJob
DescribeJobs                            	|TerminateTaskInstance
```

## 2. SecretIDとSecretKeyの取得
### I. Tencent Cloud [API 暗号鍵コンソール](https://console.cloud.tencent.com/capi)にログインします。

### II. 新しい暗号鍵を作成するか、または既存のクラウドAPI暗号鍵を使用します。クラウドAPI暗号鍵IDをクリックして詳細ページに移動し、SecretIDとSecretKeyを取得します。

![Alt text](https://main.qcloudimg.com/raw/0fe5e21af0a2f71cffa03b134858d7ee.png)

## 3. COSディレクトリの用意
### I. Bucketとサブフォルダを作成します

![](https://main.qcloudimg.com/raw/c91b6f112908ca94232715f34bd06841.png)

Bucketを作成し、ランダムな名前を付けて、後で使用するためにBucketで3つのフォルダをさらに作成します。フォルダ名は上図に表示されています。

### II. COSアクセスのアドレスを記録します

![](https://main.qcloudimg.com/raw/ce0be493f40d8b19d8b9a4c255b1d8af.png)

まず、上の図でCOS Bucketのアクセスドメイン名を確認して、それから、ドメイン名 + フォルダ名を使って、3つのフォルダのアクセスドメイン名を作成します。先ほど公式アカウントによって作成された3つのフォルダのアクセスアドレスは下記のとおりです：

* cos://batchdemo-1251783334.cosgz.myqcloud.com/logs/
* cos://batchdemo-1251783334.cosgz.myqcloud.com/input/
* cos://batchdemo-1251783334.cosgz.myqcloud.com/output/

``` 自身のBucketアクセスドメイン名に基づいてフォルダアクセスアドレスを作成してください ```

## 4. Batch Demoファイルのダウンロード

[ダウンロードアドレス](http://batchdemo-1251783334.cosgz.myqcloud.com/demo/BatchDemo.zip)、解凍後のディレクトリ構成は以下のとおりです。次の順序でBatchの使用と機能を1つずつ体験してください

* [1_SimpleStart](https://cloud.tencent.com/document/product/599/10551)
* [2_RemoteCodePkg](https://cloud.tencent.com/document/product/599/10552)
* [3_StoreMapping](https://cloud.tencent.com/document/product/599/10983)

``` DemoはPython + Batch CLIの形式で提供され、Batchは多くの機能と構成可能項目を持って、Pythonスクリプトを通してより便利な操作ができます。```

## 5. Demoカスタム情報通用部分の説明
「1_SimpleStart」のカスタム情報部分を例としてします。

```
# custom (Change to your info)
imageId = "img-m4q71qnf"
Application = {
    "DeliveryForm": "LOCAL",
    "Command": " python -c \"fib=lambda n:1 if n<=2 else fib(n-1)+fib(n-2); print(fib(20))\" "
}
StdoutRedirectPath = "your cos path"
StderrRedirectPath = "your cos path"
```

* imageId：内部テストではCloud-initサービスを含むイメージが必要です。クラウド市場でCentOS 7.2バージョンの直接使用可能なイメージを公式に提供し、イメージIDは**img-31tjrtph**です。カスタムイメージはこのイメージに基づいて作成する必要があります
* StdoutRedirectPath、StderrRedirectPath：3番目のステップで準備したCOSディレクトリのlogsフォルダのフルアクセスアドレスを記入してください。例えば、この例ではcos://batchdemo-1251783334.cosgz.myqcloud.com/logs/になりますが、それを自分のアクセスアドレスに置き換えてください
* Application：コマンドラインを起動して、当分の間変更する必要はありません

