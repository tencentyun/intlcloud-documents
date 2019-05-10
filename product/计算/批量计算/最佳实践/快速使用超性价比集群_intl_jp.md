## クラスタをすばやく作成する方法
Batchの計算環境機能を使用して簡単かつ効率的にCVMクラスタを維持することができます。Batchの計算環境は、従来のクラスタの概念に簡単に対応できます。次の例は、計算環境機能を使用して、費用対効果の高いリソースクラスタを迅速に作成/終了する方法を示しています。現在、計算環境はコマンドライン呼び出しのみをサポートしています。まず「始める前の準備」を参照して、CLIをインストールしてください。

## 始める前の準備
始める前に[始める前の準備](/doc/product/599/10807)ドキュメントのチェックリストに従って準備してください。同時にこの例では、CLIを使用しますが、ユーザーはまずCLIをインストールして構成する必要があります。

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

## 計算環境の作成

公式の例を変更して、自分のアカウントで実行可能なBatch計算環境にすることができます。その前に、計算環境の各構成項目の意味を確認します。
[計算環境の作成](/document/api/599/12691)などの計算環境関連のAPIも参照することができます。

次の例では、広州2区で10台のBS1.LARGE8（Batch通用型CPU　4コア、メモリ8GB）タイプのクラスタを迅速に作成します

```
qcloudcli batch CreateComputeEnv --Version 2017-03-12 --ComputeEnv '{
    "EnvName": "batch-env",          //　計算環境名
    "EnvDescription": "batch env demo",   // 計算環境の説明
    "EnvType": "MANAGED",                   // 計算環境のタイプ、ホスト型
    "EnvData": {                            // 具体的な構成（CVMインスタンス作成の説明を参照してください）
        "InstanceType": "BS1.LARGE8",       // 計算環境内CVM インスタンスタイプ
        "ImageId": "img-m4q71qnf",          // 計算環境内CVM イメージID（カスタムイメージに置き換え可能）
        "LoginSettings": {
            "Password": "B1[habcd"          // 計算環境内CVM ログインパスワード
        },
        "InternetAccessible": {
            "PublicIpAssigned": "TRUE",     // 計算環境内CVM パブリックネットワークIPが必要か
            "InternetMaxBandwidthOut": 10   // 計算環境内CVM 帯域幅の上限
        },
        "SystemDisk": {
            "DiskType": "CLOUD_BASIC",      // 計算環境内CVM ディスクタイプ（現在は通常のクラウドディスク）
            "DiskSize": 50                  // 計算環境内CVM ディスクサイズ
        }
    },
    "DesiredComputeNodeCount": 10           // 目標計算ノード数
}'
--Placement'{
    "Zone": "ap-guangzhou-2"                // Availability Zone（現在広州2区は置き換える必要があるかもしれません）
}'
```

#### リクエスト例
```
qcloudcli batch CreateComputeEnv --Version 2017-03-12 --ComputeEnv '{"EnvName":"batch-env","EnvDescription":"batch env demo","EnvType":"MANAGED","EnvData":{"InstanceType":"BS1.LARGE8","ImageId":"img-m4q71qnf","LoginSettings":{"Password":"B1[habcd"},"InternetAccessible":{"PublicIpAssigned":"TRUE","InternetMaxBandwidthOut":50},"SystemDisk":{"DiskType":"CLOUD_BASIC","DiskSize":50}},"DesiredComputeNodeCount":1}' --Placement '{"Zone": "ap-guangzhou-2"}'
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
作成されたCVMは、CVMコンソールで確認することも、Batchの計算環境APIで確認して管理することもできます。これからはBatchのコマンドラインAPIを使用して計算環境と計算環境内のインスタンス情報を確認する方法を説明します。EnvIdが使用され、返されたEnvIdを記録できます。

## 計算環境リストの確認

BatchのコマンドラインAPIを使用して作成されたすべての計算環境のリストを確認できます

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
返される結果に確認する計算環境の情報が含まれています

## 指定された計算環境と含まれるノードリストの確認
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

計算環境全体、および各ノードの詳細情報が含まれています

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

呼び出した後、計算環境は自動的にクラスタ内のすべてのCVMを終了します。

