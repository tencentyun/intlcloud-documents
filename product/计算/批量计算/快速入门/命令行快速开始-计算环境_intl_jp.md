## 計算環境の使用例
この例では、コマンドラインを使用して計算環境を作成してから、指定した計算環境にジョブを提出し、最後に計算環境を終了する方法を示します。

## 始める前の準備
始める前に[始める前の準備](/doc/product/599/10807)ドキュメントのチェックリストに従って準備してください。同時にこの例では、CLIとCOSを使用しますが、ユーザーはまずCLIをインストールして構成し、COS Bucketを作成する必要があります。

### CLIのインストールと構成
CLIの構成については、[CLIの構成](/doc/product/440/6184)を参照してください。インストール後、インストールが成功したことを確認します。
```
qcloudcli batch help

CreateComputeEnv                        	|DescribeJobSubmitInfo
CreateTaskTemplate                      	|DescribeJobs
DeleteComputeEnv                        	|DescribeTask
DeleteJob                               	|DescribeTaskTemplates
DeleteTaskTemplates                     	|ModifyTaskTemplate
DescribeAvailableCvmInstanceTypes       	|SubmitJob
DescribeComputeEnv                      	|TerminateJob
DescribeComputeEnvs                     	|TerminateTaskInstance
DescribeJob
```

### 結果を保存するCOS Bucketの作成

この簡単な例では、結果はシステムの標準出力に直接出力され、Batchはシステム標準出力のstdoutとstderrを収集し、タスクが完了した後に指定されたCOS Bucketに情報をアップロードできます。事前に情報を保存するためのBucketとサブフォルダを準備する必要があります。

[CLI - 事前準備](/doc/product/599/10548)の第3章**「COSディレクトリの準備」**を参照して、対応するCOS Bucketとサブフォルダを作成してください。


## 計算環境の作成

公式の例を変更して、自分のアカウントで実行可能なBatch計算環境にすることができます。その前に、計算環境の各構成項目の意味を確認します。
[計算環境の作成](/document/api/599/12691)などの計算環境関連のAPIも参照することができます。

```
qcloudcli batch CreateComputeEnv --Version 2017-03-12 --ComputeEnv '{
    "EnvName": "test compute env",          //　計算環境名
    "EnvDescription": "test compute env",   // 計算環境の説明
    "EnvType": "MANAGED",                   // 計算環境のタイプ、ホスト型
    "EnvData": {                            // 具体的な構成（CVMインスタンス作成の説明を参照してください）
        "InternetAccessible": {
            "PublicIpAssigned": "TRUE",
            "InternetMaxBandwidthOut": 50
        },
        "LoginSettings": {
            "Password": "B1[habcd"
        },
        "InstanceType": "S1.SMALL1",        // CVMインスタンスタイプ
        "ImageId": "img-xxxxyyyy"           // CVMイメージID（置き換える必要あり）
    },
    "DesiredComputeNodeCount": 2            // 目標計算ノード数
}'
--Placement'{
    "Zone": "ap-guangzhou-2"                // Availability Zone（置き換える必要があるかもしれません）
}'
```


#### リクエスト例
```
qcloudcli batch CreateComputeEnv --Version 2017-03-12  --ComputeEnv '{"EnvName": "test compute env", "EnvDescription": "test compute env", "EnvType": "MANAGED", "EnvData": {"InstanceType": "S1.SMALL2", "ImageId": "置き換え待ち", "LoginSettings": {"Password": "置き換え待ち"}, "InternetAccessible": {"PublicIpAssigned": "TRUE", "InternetMaxBandwidthOut": 50}, "SystemDisk": {"DiskType": "CLOUD_BASIC", "DiskSize": 50 } }, "DesiredComputeNodeCount": 2 }' --Placement '{"Zone": "ap-guangzhou-2"}'
```

#### 戻り例
戻り値。ここで、EnvIdはBatch計算環境の唯一のIDです。
```
{
    "Response": {
        "EnvId": "env-c96rwhnf",
        "RequestId": "bead16d4-b33b-47b5-9b86-6a02b4bed1b2"
    }
}
```

## 計算環境リストの確認
#### リクエスト例
```
qcloudcli batch DescribeComputeEnvs --Version 2017-03-12
```

#### 戻り例
```
{
    "Response": {
        "TotalCount": 1,
        "ComputeEnvSet": [
            {
                "EnvId": "env-c96rwhnf",
                "Placement": {
                    "Zone": "ap-guangzhou-2"
                },
                "EnvType": "MANAGED",
                "EnvName": "test compute env",
                "ComputeNodeMetrics": {
                    "CreatedCount": 0,
                    "DeletingCount": 0,
                    "CreationFailedCount": 0,
                    "SubmittedCount": 0,
                    "CreatingCount": 0,
                    "AbnormalCount": 0,
                    "RunningCount": 2
                },
                "CreateTime": "2017-11-27T07:10:02Z"
            }
        ],
        "RequestId": "bac76f1c-06cd-4ef4-82a9-f230fa5a1992"
    }
}
```


## 指定した計算環境の確認
#### リクエスト例
```
qcloudcli batch DescribeComputeEnv --Version 2017-03-12 --EnvId env-c96rwhnf
```

#### 戻り例
```
{
    "Response": {
        "EnvId": "env-c96rwhnf",
        "Placement": {
            "Zone": "ap-guangzhou-2"
        },
        "EnvType": "MANAGED",
        "EnvName": "test compute env",
        "RequestId": "12dc7dba-f33b-4d5a-8cd6-ebd1df17ebf7",
        "ComputeNodeMetrics": {
            "CreatedCount": 0,
            "DeletingCount": 0,
            "CreationFailedCount": 0,
            "SubmittedCount": 0,
            "CreatingCount": 0,
            "AbnormalCount": 0,
            "RunningCount": 2
        },
        "ComputeNodeSet": [
            {
                "ComputeNodeId": "node-838udz1w",
                "ComputeNodeState": "RUNNING",
                "Mem": 2,
                "ResourceCreatedTime": "2017-11-27T07:10:46Z",
                "ComputeNodeInstanceId": "ins-q09nyg5g",
                "AgentVersion": "1.0.7",
                "TaskInstanceNumAvailable": 1,
                "Cpu": 1
            },
            {
                "ComputeNodeId": "node-c4z8f8xc",
                "ComputeNodeState": "RUNNING",
                "Mem": 2,
                "ResourceCreatedTime": "2017-11-27T07:10:41Z",
                "ComputeNodeInstanceId": "ins-fgqcau4q",
                "AgentVersion": "1.0.7",
                "TaskInstanceNumAvailable": 1,
                "Cpu": 1
            }
        ],
        "CreateTime": "2017-11-27T07:10:02Z"
    }
}
```

## 指定した計算環境へのタスクの提出
#### リクエスト例
```
qcloudcli batch SubmitJob --Version 2017-03-12  --Job '{"JobName": "test job", "JobDescription": "xxx", "Priority": "1", "Tasks": [{"TaskName": "hello2", "TaskInstanceNum": 1,  "Application": {"DeliveryForm": "LOCAL", "Command": "python -c \"fib=lambda n:1 if n<=2 else fib(n-1)+fib(n-2); print(fib(20))\" "}, "EnvId": "置き換え待ち", "RedirectInfo": {"StdoutRedirectPath": "cos://dondonbatch-1251783334.cosgz.myqcloud.com/hello2/logs/", "StderrRedirectPath":  "cos://dondonbatch-1251783334.cosgz.myqcloud.com/hello2/logs/"} } ] }' --Placement '{"Zone": "ap-guangzhou-2"}'

```

#### 戻り例
```
{
    "Response": {
        "RequestId": "cf821ae0-71d6-42b1-b878-6ecdeec15796",
        "JobId": "job-lhi5agkh"
    }
}
```

## 計算環境の終了
#### リクエスト例
```
qcloudcli batch DeleteComputeEnv --Version 2017-03-12 --EnvId env-c96rwhnf
```

#### 戻り例
```
{
    "Response": {
        "RequestId": "389f011a-7dbd-4993-82fe-334ac923ff88"
    }
}
```

