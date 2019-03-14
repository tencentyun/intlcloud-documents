
## 最も簡単な例
この例は、コマンドラインを使用して簡単なジョブを提出する方法を示しています。例はPythonによるフィボナッチ数列の合計で、PythonコードはタスクにおけるApplicationパラメータのCommandフィールドで指定され、結果はタスク構成のstdout出力アドレスに直接出力されます。

## 始める前の準備
始める前に[始める前の準備](
/doc/product/599/10807)ドキュメントのチェックリストに従って準備してください。同時にこの例では、CLIとCOSを使用しますが、ユーザーはまずCLIをインストールして構成し、COS Bucketを作成する必要があります。

### CLIのインストールと構成
CLIの構成については、[CLIの構成](/doc/product/440/6184)を参照してください。インストール後、インストールが成功したことを確認します。
```
qcloudcli batch help

DescribeAvailableCvmInstanceTypes       	|DescribeTask
DescribeJob                             	|SubmitJob
DescribeJobs                            	|TerminateTaskInstance
```

### 結果を保存するCOS Bucketの作成

この簡単な例では、結果はシステムの標準出力に直接出力され、Batchはシステム標準出力のstdoutとstderrを収集し、タスクが完了した後に指定されたCOS Bucketに情報をアップロードできます。事前に情報を保存するためのBucketとサブフォルダを準備する必要があります。

[CLI - 事前準備](/doc/product/599/10548)の第3章**「COSディレクトリの準備」**を参照して、対応するCOS Bucketとサブフォルダを作成してください。

## ジョブ構成の紹介

公式の例を変更して、自分のアカウントで実行可能なBatchジョブ構成にすることができます。その前に、ジョブの各構成項目の意味を確認します。

```
qcloudcli batch SubmitJob --Version 2017-03-12 --Job '{
    "JobName": "TestJob",       // ジョブ名
    "JobDescription": "for test ",    // ジョブの説明
    "Priority": "1",            // ジョブの優先順位
    "Tasks": [                  // タスクリスト（この例ではタスクは1つだけです）
        {
            "TaskName": "Task1",   // タスク1の名前
            "Application": {        // タスク実行コマンド
                "DeliveryForm": "LOCAL",    // ローカルコマンドの実行
                "Command": "python -c \"fib=lambda n:1 if n<=2 else fib(n-1)+fib(n-2); print(fib(20))\" "   // コマンドの具体的な内容（フィボナッチ合計）
            },
            "ComputeEnv": {         // 計算環境構成
                "EnvType": "MANAGED",   // 計算環境のタイプ、ホスト型および非ホスト型
                "EnvData": {        // 具体的な構成（現在はホスト型で、CVMインスタンス作成の説明を参照してください）
                    "InstanceType": "S1.SMALL1",    // CVMインスタンスタイプ
                    "ImageId": "img-m4q71qnf",      // CVMイメージID（置き換える必要あり）
                }
            },
            "RedirectInfo": {       // 標準出力リダイレクト構成           
                "StdoutRedirectPath": "cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/",    // 標準出力（置き換える必要あり）
                "StderrRedirectPath": "cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/"     // 標準エラー（置き換える必要あり）
            }
        }
    ]
}'
--Placement'{
    "Zone": "ap-guangzhou-2"    // Availability Zone（置き換える必要があるかもしれません）
}'
```

BatchのSubmitJobコマンドには3つのパラメータが含まれています
* **Version**：バージョン番号、現在2017-03-12を固定記入します
* **Job**：ジョブ構成、JSONフォーマット、詳細なフィールドの意味は例を参照してください
* **Placement**：ジョブのAvailability Zoneを実行します

``* 1. Jobで置き換えられるフィールドが識別され、実行する前に、カスタムイメージID、VPC関連情報、COS Bucketアドレス、および対応するSecretId、SecretKeyなどをユーザー自身の情報に置き換える必要があります。``

``* 2. 上記の例ではコメントテキストが追加されているため、CLIで直接実行することはできません。実行する前に、以下の例をコピーして「記入待ち」フィールドに入力してください。コマンドが長すぎます。コピーが不完全にならないように、後部のコピーボタンを使用してください。``

``* 3. 詳細なJob構成の説明は`` [ジョブ構成の説明](https://cloud.tencent.com/document/product/599/11040) ``を参照してください。``

```
qcloudcli batch SubmitJob --Version 2017-03-12  --Job '{"JobName": "TestJob",  "JobDescription": "for test", "Priority": "1", "Tasks": [{"TaskName": "Task1",  "TaskInstanceNum": 1,  "Application": {"DeliveryForm": "LOCAL", "Command":  "python -c \"fib=lambda n:1 if n<=2 else fib(n-1)+fib(n-2); print(fib(20))\" "},  "ComputeEnv": {"EnvType":  "MANAGED", "EnvData": {"InstanceType": "S1.SMALL1",  "ImageId": "置き換え待ち" }  }, "RedirectInfo": {"StdoutRedirectPath": "置き換え待ち", "StderrRedirectPath":   "置き換え待ち"}, "MaxRetryCount":  1 } ] }' --Placement '{"Zone": "ap-guangzhou-2"}'
```

### 構成変更

#### 1. ImageIdの記入
```"ImageId": "置き換え待ち"```

内部テストでは、Cloud-initサービスベースの構成されたイメージを使用する必要があります。公式にCentOS 6.5の直接使用可能なイメージを提供して、イメージIDはimg-m4q71qnfです。Windows Server 2012の公式イメージIDはimg-er9shclnです。

#### 2. StdoutRedirectPathとStderrRedirectPathの構成
```"StdoutRedirectPath": "置き換え待ち", "StderrRedirectPath":   "置き換え待ち"```

事前準備でCOS Bucketを作成するアクセスアドレスをStdoutRedirectPathとStderrRedirectPathに入力します。

#### 3. Availability Zoneの変更（オプション）
```
--Placement '{"Zone": "ap-guangzhou-2"}'
```

この例では、広州2区をリソースの申請地域として指定します。CLIで構成したデフォルトの地域に基づいて適切なAvailability Zoneを選択してリソースを申請できます。地域とAvailability Zoneの詳細情報については、[地域とAvailability Zone>>](/doc/product/213/6091)を参照してください。

#### 4. WindowsにおけるコマンドラインによるJSONフォーマットの入力（オプション）
WindowsでCLIによるJSONフォーマットデータの入力はLinuxと異なります。例えば、"は\に置き換える必要があります。詳細については、[Tencent Cloud　CLIのクイック使用](/doc/product/440/6185)の「JSONフォーマットを入力パラメータとする」セクションを参照してください。

## 結果確認

```
{
    "Response": {
        "RequestId": "5d928636-bba2-4ab3-bef3-cf17d7c73c51",
        "JobId": "job-1rqdgnqn"
    }
}
```
JobIdを返すことは、実行が成功したことを示します。

```
$ qcloudcli batch DescribeJob  --Version 2017-03-12 --JobId job-1z4yl2bp
{
    "Response": {
        "JobState": "STARTING",
        "Zone": "ap-guangzhou-2",
        "JobName": "test job",
        "Priority": 1,
        "RequestId": "b116f9b5-410c-4a69-bbe8-b695a2d6a869",
        "TaskSet": [
            {
                "TaskName": "hello2",
                "TaskState": "STARTING"
            }
        ],
        "JobId": "job-1z4yl2bp",
        "DependenceSet": []
    }
}
```
DescribeJobを通して先ほど提出したタスク情報を確認できます。

```
$ qcloudcli batch DescribeJobs  --Version 2017-03-12
```
DescribeJobsを通して現在地域のジョブリストを確認することもできます。

## 次に何ができますか？

これは最も簡単な例で、シングルタスクジョブであり、リモートストレージマッピング機能を使用するのではなく、ユーザーに最も基本的な機能を示すだけです。APIの説明ドキュメントに従って、Batchのより高いレベルの機能をテストし続けることができます。

* **より簡単な操作方法**：Batchには強力な機能と多くの構成項目があり、スクリプトを通して呼び出す方がより簡単かつ迅速です。[事前準備](/doc/product/599/10548)と[1_簡単なスタート](/doc/product/599/10551)からこの方法を試してください。

* **リモートコードパッケージの実行**：Batchは**カスタムイメージ + リモートコードパッケージ + コマンドライン**の方式を提供し、技術的にあらゆる方面でユーザーのビジネスニーズに対応します。詳細については、[2_リモートコードパッケージの実行](/doc/product/599/10552)をご覧ください。

* **リモートストレージマッピング**：Batchはストレージアクセスを最適化し、リモートストレージサービスへのアクセスは、ローカルファイルシステムの操作に簡素化します。詳細については、[3_リモートストレージマッピング](/doc/product/599/10983)をご覧ください。

