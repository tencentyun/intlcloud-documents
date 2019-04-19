## 概要情報
Batchは、ジョブおよび計算環境内で生成されたイベントをメッセージサービス（CMQ）の形式でスローされることをサポートします。例えば、ジョブ実行の成功/失敗、計算環境ノード作成の成功/失敗/異常などのイベント発生は、CMQのトピック購読メカニズムを通じて通知およびコールバックできます。

## 使用ガイド
例えば、計算環境関連のイベントをリスニングするには、次の3つの手順で計算環境関連のイベントを登録できます。

### 1. CMQトピックを作成します
[メッセージサービスCMQコンソール](https://console.cloud.tencent.com/mq/topic?rid=1)にログインして、新しいトピックを作成します。
![](https://main.qcloudimg.com/raw/9434883b7843df9bd3f1ec392ad26e36.png)
### 2.　計算環境を作成して、CMQトピックを関連付けます
ジョブを提出するとき（SubmitJob）または計算環境を作成するとき（Create）に**notifications**フィールドを追加し、リスニングするイベント**event_name**を指定します。複数のイベントを指定することが可能です。
```
"notifications": [
    {
      "event_configs": [
        {
          "event_name": "JobFailed" // イベント名
        },
        {
          "event_name": "JobSucceed",
          "event_vars": [           // カスタムイベントパラメータ
            {
              "name": "jobSucceed",
              "value": "Success"
            }
          ]
        }
      ],
      "topic_name": "job-message"   // CMQ Topic Name
    }
  ],
```

* 現在、APIまたはCLIを介して計算環境を作成するときにのみCMQトピックを関連付けることが可能です。これからは、コンソール操作による方法でもサポートされる予定です。
* event_vars：イベントによって生成された固定メッセージ本体に加えて、カスタムパラメータの追加もサポートします。
* topic_name：関連付けられたCMQトピックのName（**注意：IDではありません**）。すべてのイベントメッセージはそのトピックに配信され、トピックはすべての購読者にメッセージを転送します。

### 3.　購読者を設定してテストします
[メッセージサービスCMQコンソール](https://console.cloud.tencent.com/mq/topic?rid=1)で新規作成したトピックに購読者を追加します。すばやく簡単に確認するために、すでに作成されているメッセージキューを指定できます。
![](https://main.qcloudimg.com/raw/d6746fa9bad7c8f16fa4e427c7476458.png)
メッセージ構造は次のとおりです。購読者がメッセージキューを指定した場合は、[メッセージサービスCMQコンソール - メッセージ受信](https://console.cloud.tencent.com/mq/receive)を通して、Batchからトピックに送信されたイベントメッセージ（メッセージ受信でのメッセージ内容はBase64処理が必要です）をすばやく確認することができます。
```
{
	"Events": [{
		"EventVersion": "1.0",
		"EventTime": "2018-06-15T14:43:17Z",
		"Region": "ap-guangzhou",
		"Batch": {
			"ComputeNodeId": "node-0iy7wxyo",
			"EnvId": "env-ptoxdb1t",
			"ComputeNodeState": "CREATED",
			"Mem": 8,
			"ResourceCreatedTime": "2018-06-15T14:43:18Z",
			"EnvName": "batch-env",
			"ComputeNodeInstanceId": "ins-9rikj9kw",
			"Cpu": 4
		},
		"EventName": "COMPUTE_NODE_CREATED",
		"EventVars": []
	}]
}
```

### ジョブ関連のイベント
タイプ | 説明
-----|------
JOB_RUNNING | ジョブ実行
JOB_SUCCEED | ジョブ完了
JOB_FAILED | ジョブ失敗
JOB_FAILED_INTERRUPTED | ジョブ失敗中断
TASK_RUNNING | タスク実行
TASK_SUCCEED | タスク完了
TASK_FAILED | タスク失敗
TASK_FAILED_INTERRUPTED | タスク失敗中断
TASK_INSTANCE_RUNNING | タスクインスタンス実行
TASK_INSTANCE_SUCCEED | タスクインスタンス完了
TASK_INSTANCE_FAILED | タスクインスタンス失敗
TASK_INSTANCE_FAILED_INTERRUPTED | タスクインスタンス失敗中断

最新の定義とジョブ提出API Demoについては、[ジョブ提出 >>](https://cloud.tencent.com/document/product/599/12683)を参照してください

### 計算環境関連のイベント
タイプ | 説明
-----|------
COMPUTE_ENV_CREATED | 計算環境の作成
COMPUTE_ENV_DELETED | 計算環境の削除
COMPUTE_NODE_CREATED | 計算ノード作成成功
COMPUTE_NODE_CREATION_FAILED |  計算ノード作成失敗
COMPUTE_NODE_RUNNING | 計算ノード実行中
COMPUTE_NODE_ABNORMAL | 計算ノード異常
COMPUTE_NODE_DELETING | 計算ノード終了中 

最新の定義と計算環境作成API Demoについては、[計算環境の作成 >>](https://cloud.tencent.com/document/product/599/12683)を参照してください

