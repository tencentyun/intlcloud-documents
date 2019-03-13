## 1. 事前準備
[事前準備]()の説明に従って準備を完了し、カスタム情報の共通部分の構成方法を確認してください。

## 2. Demoの確認と変更
エディタで1_SimpleStart.pyファイルを開きます
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
カスタム部分customは、Applicationを除いて、すべて事前準備で説明されました。以下は主にApplicationの意味を紹介します
* DeliveryForm：アプリケーションの納品方法。ソフトウェアのパッケージング、コンテナイメージ、およびCVM内部直接実行という3つの方法が含まれています。ここでLOCALはCVM内部直接実行を表します
* Command：タスク起動コマンド。これは1から始まり、フィボナッチ数列の最初の20個数字をStdOutputに合計するPythonスクリプトです

1_SimpleStart.pyは比較的に簡単で、事前準備に従って通用部分を変更するだけで直接実行することができるので、ここでそれを変更する必要はありません

## 3. ジョブ提出
ジョブ提出フローは、DemoのPythonスクリプト + Batch　CLIの形式でカプセル化されています。そのため、以下の例に従ってPythonスクリプトを実行してください
```
$ python 1_SimpleStart.py
{
    "Response": {
        "RequestId": "d069ce2f-abfc-451f-81fd-9327dbf5cf39",
        "JobId": "job-clump52n"
    }
}
```

JobIdフィールドが返された場合は、提出が成功しました。そうではない場合は、エラーのトラブルシューティングのために戻り値を確認するか、[ユーザーフィードバック]()を通して管理者に相談してください。

## 4. ステータス確認

```
$ qcloudcli batch DescribeJob  --Version 2017-03-12 --JobId job-xxx
```
DescribeJobで実行ステータスを確認し、JobIdを実際のJobIdに置き換えてください。よく見られるステータスは以下の通りです
* STARTING  起動中
* RUNNING   実行中
* SUCCEED   実行成功
* FAILED    実行失敗

完全な返却情報は以下の通りです

```
{
    "Response": {
        "JobState": "STARTING",
        "Zone": "ap-guangzhou-2",
        "JobName": "SimpleStart",
        "Priority": 1,
        "RequestId": "8e5ef77c-fa41-4b9f-8c80-107f2546e8ed",
        "TaskSet": [
            {
                "TaskName": "Task1",
                "TaskState": "STARTING"
            }
        ],
        "JobId": "job-n4ohivif",
        "DependenceSet": []
    }
}
```

## 5. 結果確認

結果は、事前準備で構成されたStdoutRedirectPathとStderrRedirectPathディレクトリに保存されます。結果は次のとおりです

![](https://mc.qcloudimg.com/static/img/1038bd36c2c897f7241643995757dd7f/COS_4.png)

成功した場合は標準出力stdout.job-xxx.xxxx.0.logを確認してください。内容は次のとおりです
```
6765
```

失敗した場合は標準エラーstderr.job-xxx.xxxx.0.logを確認してください。可能な内容は次のとおりです
```
/bin/sh: -c: line 0: syntax error near unexpected token `('
/bin/sh: -c: line 0: ` python -c \"fib=lambda n:1 if n<=2 else fib(n-1)+fib(n-2); print(fib(20))\" '
```




