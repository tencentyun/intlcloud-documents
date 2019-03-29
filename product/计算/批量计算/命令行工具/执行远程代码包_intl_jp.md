BatchはHTTPの方式で、.tgzフォーマットのファイルからコードパッケージを取得することをサポートします。ユーザーはコードをパッケージ化してCOSにアップロードできるため、LOCALモードよりもコードの整理が容易になります

## 1. 事前準備
[事前準備](https://cloud.tencent.com/document/product/599/10548)の説明に従って準備を完了し、カスタム情報の通用部分の構成方法を確認してください。

## 2. Demoの確認と変更
エディタで2_RemoteCodePkg.pyファイルを開きます
```
# custom (Change to your info)
imageId = "img-m4q71qnf"
Application = {
    "DeliveryForm": "PACKAGE",
    "Command": "python ./codepkg/fib.py",
    "PackagePath": "http://batchdemo-1251783334.cosgz.myqcloud.com/codepkg/codepkg.tgz"
}
StdoutRedirectPath = "your cos path"
StderrRedirectPath = "your cos path"
```
カスタム部分customは、Applicationを除いて、すべて事前準備で説明されました。以下は主にApplicationの意味を紹介します
* DeliveryForm：アプリケーションの納品方法。ソフトウェアのパッケージング、コンテナイメージ、およびCVM内部直接実行という3つの方法が含まれています。ここでPACKAGEはソフトウェアのパッケージング方式を表します
* PackagePath：パッケージのアドレス。HTTP方式で提供され、それは.tgzフォーマットでなければなりません。そして、BatchはこのパッケージをスケジューリングされたCVMのあるディレクトリにダウンロードし、そのディレクトリでCommandを実行します
* Command：タスク起動コマンド。ここでパッケージ内のPythonスクリプトファイルを直接呼び出します。パッケージをダウンロードして内部のファイル構造と内容を確認することができます。

fib.pyの内容は以下のとおりです
```
fib = lambda n:1 if n<=2 else fib(n-1)+fib(n-2)
print("Remote Code Package : %d"%(fib(20)))
```

2_RemoteCodePkg.pyは比較的に簡単で、事前準備に従って通用部分を変更するだけで直接実行することができるので、ここでそれを変更する必要はありません

## 3. ジョブ提出
ジョブ提出フローは、DemoのPythonスクリプト + Batch内部テストバージョンCLIの形式でカプセル化されています。そのため、以下の例に従ってPythonスクリプトを実行してください
```
$ python 2_RemoteCodePkg.py
{
    "Response": {
        "RequestId": "d069ce2f-abfc-451f-81fd-9327dbf5cf39",
        "JobId": "job-clump52n"
    }
}
```

JobIdフィールドが返された場合は、提出が成功しました。そうではない場合は、エラーのトラブルシューティングのために戻り値を確認するか、[ユーザーフィードバック](https://cloud.tencent.com/document/product/599/10806)のコミュニケーショングループに加入して、管理者に相談してください。

## 4. ステータス確認
[簡単なスタート](https://cloud.tencent.com/document/product/599/10551)の同名の章を参照してください

## 5. 結果確認
[簡単なスタート](https://cloud.tencent.com/document/product/599/10551)の同名の章を参照してください

2_RemoteCodePkg.pyの実行結果は以下のとおりです
```
Remote Code Package : 6765
```

