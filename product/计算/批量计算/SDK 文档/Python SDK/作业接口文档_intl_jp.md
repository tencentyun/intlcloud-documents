## 開発準備
- [Python SDK](https://cloud.tencent.com/document/sdk/Python)をダウンロードしてインストールします。
- 初めてBatchを使用する場合は、[始める前の準備](https://cloud.tencent.com/document/product/599/10807)を参照してください。
- ジョブ構成パラメータの詳細については、[ジョブ提出APIドキュメント](https://cloud.tencent.com/document/product/599/12683)を参照してください。

## クイックスタート

```
#!/usr/bin/python
# -*- coding: utf-8 -*-

# クラウドAPIエントリモジュールの導入
from QcloudApi.qcloudapi import QcloudApi

# パブリック構成
module = 'batch'

config = {
    'Region': 'ap-guangzhou',  # ターゲット地域
    'secretId': ‘お使いのsecretId',
    'secretKey': ‘お使いのsecretKey',
}

service = QcloudApi(module, config)
```

## ジョブ提出

```
try:
    action = 'SubmitJob'
    action_params = {
        'Version': '2017-03-12',
        'Job': {
            'JobName': 'batch-job', # ジョブ名
            'JobDescription': 'batch job',  # ジョブの説明
            'Priority': '1',  # ジョブの優先順位
            'Tasks': [
                {
                    'TaskName': 'task1',  # タスク名
                    'TaskInstanceNum':  1,  # タスクインスタンス数
                    'FailedAction': 'FAST_INTERRUPT',  # 失敗したジョブの処理方法
                    'Application': {
                        'DeliveryForm': 'LOCAL',  # パッケージソース
                        'Command': 'echo hello',  # コマンドライン
                        },
                    'EnvId': 'env-gbyctcy9',  # 計算環境タグ
                    'RedirectInfo': {
                        'StdoutRedirectPath': 'cos://bucketgz-1251783334.cos.ap-guangzhou.myqcloud.com/stdout/',  # 標準出力ストレージパス
                        'StderrRedirectPath': 'cos://bucketgz-1251783334.cos.ap-guangzhou.myqcloud.com/stderr/',  # 標準エラーストレージパス
                        }
                    }
                ]
            },
        'Placement': {
            'Zone': 'ap-guangzhou-2'  # Availability Zone
            },
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```
パラメータの説明とエラーメッセージの詳細については、[ジョブ提出APIドキュメント](https://cloud.tencent.com/document/product/599/12683)を参照してください。

## ジョブ終了

```
try:
    action = 'TerminateJob'
    action_params = {
        'Version': '2017-03-12',
        'JobId': 'job-8kwnzki7',  # ジョブタグ
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```
パラメータの説明とエラーメッセージの詳細については、[ジョブ終了APIドキュメント](https://cloud.tencent.com/document/product/599/12689)を参照してください。

## ジョブ削除

```
try:
    action = 'DeleteJob'
    action_params = {
        'Version': '2017-03-12',
        'JobId': 'job-8kwnzki7',  # ジョブタグ
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```
パラメータの説明とエラーメッセージの詳細については、[ジョブ削除APIドキュメント](https://cloud.tencent.com/document/product/599/12682)を参照してください。

## ジョブ提出情報の確認

```
try:
    action = 'DescribeJobSubmitInfo'
    action_params = {
        'Version': '2017-03-12',
        'JobId': 'job-8kwnzki7',  # ジョブタグ
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```
パラメータの説明とエラーメッセージの詳細については、[ジョブ提出情報の確認APIドキュメント](https://cloud.tencent.com/document/product/599/12687)を参照してください。

## ジョブ情報の確認

```
try:
    action = 'DescribeJob'
    action_params = {
        'Version': '2017-03-12',
        'JobId': 'job-8kwnzki7',  # ジョブタグ
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```
パラメータの説明とエラーメッセージの詳細については、[ジョブ情報の確認APIドキュメント](https://cloud.tencent.com/document/product/599/12685)を参照してください。

## ジョブリストの確認

```
try:
    action = 'DescribeJobs'
    action_params = {
        'Version': '2017-03-12'
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```
パラメータの説明とエラーメッセージの詳細については、[ジョブリストの確認APIドキュメント](https://cloud.tencent.com/document/product/599/12686)を参照してください。

## タスク情報の確認

```
try:
    action = 'DescribeTask'
    action_params = {
        'Version': '2017-03-12',
	'JobId': 'job-8kwnzki7',  # ジョブタグ
	'TaskName': 'task A'  # タスク名
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```
パラメータの説明とエラーメッセージの詳細については、[タスク情報の確認APIドキュメント](https://cloud.tencent.com/document/product/599/12684)を参照してください。

## タスクインスタンスの終了

```
try:
    action = 'TerminateTaskInstance'
    action_params = {
        'Version': '2017-03-12',
	'JobId': 'job-8kwnzki7',  # ジョブタグ
	'TaskName': 'task A',  # タスク名
	'TaskInstanceIndex': 1  # 最初のインスタンス
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```
パラメータの説明とエラーメッセージの詳細については、[タスクインスタンスの終了APIドキュメント](https://cloud.tencent.com/document/product/599/12688)を参照してください。

