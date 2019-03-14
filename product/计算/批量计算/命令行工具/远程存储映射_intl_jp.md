リモートマッピングは、Batchがストレージに関連する補助的な機能を使用して、COS、CFSなどのリモートストレージをローカルフォルダにマッピングすることができます

## 1. 事前準備
[事前準備]()の説明に従って準備を完了し、カスタム情報の共通部分の構成方法を確認してください。

## 2. 入力データファイルのアップロード
number.txtの内容は次のとおりです
```
1
2
3
4
5
6
7
8
9
```

ファイルを事前準備で作成したinputフォルダにアップロードします

![](https://mc.qcloudimg.com/static/img/02738c821f14ed132fef76c466c79d08/COS_5.png)

## 3. Demoの確認と変更
エディタで3_StoreMapping.pyファイルを開きます
```
# custom (Change to your info)
imageId = "img-m4q71qnf"
Application = {
    "DeliveryForm": "PACKAGE",
    "Command": "python ./codepkg/countnum.py",
    "PackagePath": "http://batchdemo-1251783334.cosgz.myqcloud.com/codepkg/codepkg.tgz"
}
StdoutRedirectPath = "your cos path"
StderrRedirectPath = "your cos path"
InputMapping = {
    "SourcePath": "your input remote path",
    "DestinationPath": "/data/input/"
}
OutputMapping = {
    "SourcePath": "/data/output/",
    "DestinationPath": "your output remote path"
}
```
2_RemoteCodePkg.pyと比較すると、カスタム部分は次のように変更されています
* ApplicationのCommandはcountnum.py実行に変更します 
* InputMapping：入力マッピング、SourcePath：リモートストレージアドレス（事前準備のinputフォルダのアドレスに変更）、DestinationPath：ローカルディレクトリ（変更なし）
* OutputMapping：出力マッピング、SourcePath：ローカルディレクトリ（変更なし）、DestinationPath：リモートストレージアドレス（事前準備のoutputフォルダのアドレスに変更）

countnum.pyの内容は以下のとおりです
```
import os

inputfile = "/data/input/number.txt"
outputfile = "/data/output/result.txt"

def readFile(filename):
    total = 0
    fopen = open(filename, 'r')
    for eachLine in fopen:
        total += int(eachLine)
    fopen.close()
    print "total = ",total
    fwrite = open(outputfile, 'w')
    fwrite.write(str(total))
    fwrite.close()

print("Local input file is ",inputfile)
readFile(inputfile)
```
ファイルinput/number.txtを開き、各行の数字を加えて、結果をoutput/Result.txtに書き込みます

## 4. ジョブ提出
ジョブ提出フローは、DemoのPythonスクリプト + Batch内部テストバージョンCLIの形式でカプセル化されています。そのため、以下の例に従ってPythonスクリプトを実行してください
```
$ python 3_StoreMapping.py
{
    "Response": {
        "RequestId": "d069ce2f-abfc-451f-81fd-9327dbf5cf39",
        "JobId": "job-clump52n"
    }
}
```

JobIdフィールドが返された場合は、提出が成功しました。そうではない場合は、エラーのトラブルシューティングのために戻り値を確認するか、[ユーザーフィードバック]()を通して管理者に相談してください。

## 5. ステータス確認
[簡単なスタート]()の同名の章を参照してください。

## 6. 結果確認
Batchは出力データをローカルディレクトリからリモートストレージディレクトリにコピーします。3_StoreMapping.pyの実行結果はresult.txtに保存され、このファイルは自動的にCOSに同期されます
![pic](https://mc.qcloudimg.com/static/img/aee7138e589378eea48851dd1649b711/COS_6.png)
```
45
```
