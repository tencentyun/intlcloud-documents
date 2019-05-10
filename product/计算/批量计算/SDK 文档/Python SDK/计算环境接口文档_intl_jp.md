## 開発準備
- [Python SDK](https://cloud.tencent.com/document/sdk/Python)をダウンロードしてインストールします。
- 初めてBatchを使用する場合は、[始める前の準備](https://cloud.tencent.com/document/product/599/10807)を参照してください。
- 計算環境構成パラメータの詳細については、[計算環境の作成APIドキュメント](https://cloud.tencent.com/document/product/599/12691)を参照してください。

## クイックスタート

```
#!/usr/bin/python
# -*- coding: utf-8 -*-

# クラウドAPIエントリモジュールの導入
from QcloudApi.qcloudapi import QcloudApi

# パブリック構成
module = 'batch'

config = {
    'Region': 'ap-beijing',
    'secretId': 'お使いのsecretId',
    'secretKey': 'お使いのsecretKey',
}

service = QcloudApi(module, config)
```

## 計算環境の作成

```
try:
    action = 'CreateComputeEnv'
    action_params = {
        'Version': '2017-03-12',
        "ComputeEnv": {
            "EnvName": "Cluster-A",  #　計算環境名
            "EnvDescription": "first cluster",  #　計算環境の説明
            "EnvType": "MANAGED",
            "MountDataDisks": [
                {
                    "FileSystemType": "NTFS",
                    "LocalPath": J://",  #　データディスクマウントポイント
                    }
                ],
            "EnvData": {
                "InstanceType": "S2.SMALL1", 　#　インスタンスタイプ
                "ImageId": "img-er9shcln",  #　イメージタグ
                "LoginSettings": {
                    "Password": "B1[habcdB1[habcd" 　#　ログインパスワード
                    },
                "InternetAccessible": {
                    "PublicIpAssigned": "TRUE",  # パブリックネットワークIP
                    "InternetMaxBandwidthOut": 50  # パブリックネットワーク帯域幅
                    },
                "SystemDisk": {
                    "DiskType": "LOCAL_BASIC",  # システムディスクのタイプ
                    "DiskSize": 50  # システムディスクのサイズ
                    },
                "DataDisks": [
                    {
                        "DiskType": "LOCAL_BASIC",  # データディスクのタイプ
                        "DiskSize": 50  # データディスクのサイズ
                        }
                    ]
                },
            "DesiredComputeNodeCount": 1  # 計算ノード数
            },
        "Placement": {
            "Zone": "ap-beijing-2"  # Availability Zone
            },
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```
 パラメータの説明とエラーメッセージの詳細については、[計算環境の作成APIドキュメント](https://cloud.tencent.com/document/product/599/12691)を参照してください。
## 計算環境の変更

```
try:
    action = 'ModifyComputeEnv'
    action_params = {
        'Version': '2017-03-12',
        'EnvId': "env-cc44pzme",  # 計算環境タグ
        'DesiredComputeNodeCount': 100,  # 目標ノード数
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```
 パラメータの説明とエラーメッセージの詳細については、[計算環境の変更APIドキュメント](https://cloud.tencent.com/document/product/599/13637)を参照してください。
 
 ## 計算クラスタの削除
 
```
try:
    action = 'DeleteComputeEnv'
    action_params = {
        'Version': '2017-03-12',
        'EnvId': "env-cc44pzme",  # 計算環境タグ
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```
 パラメータの説明とエラーメッセージの詳細については、[計算環境の削除APIドキュメント](https://cloud.tencent.com/document/product/599/12692)を参照してください。
 
 ## 計算環境作成情報の確認
 
```
try:
    action = 'DescribeComputeEnvCreateInfo'
    action_params = {
        'Version': '2017-03-12',
        'EnvId': "",  # 計算環境タグ
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```
 パラメータの説明とエラーメッセージの詳細については、[計算環境作成情報の確認APIドキュメント](https://cloud.tencent.com/document/product/599/14604)を参照してください。
 
 ## 計算環境情報の確認
 
```
try:
    action = 'DescribeComputeEnv'
    action_params = {
        'Version': '2017-03-12',
        'EnvId': "",  # 計算環境タグ
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```
パラメータの説明とエラーメッセージの詳細については、[計算環境情報の確認APIドキュメント](https://cloud.tencent.com/document/product/599/12694)を参照してください。

## 計算環境リストの確認

```
try:
    action = 'DescribeComputeEnvs'
    action_params = {
        'Version': '2017-03-12',
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```
パラメータの説明とエラーメッセージの詳細については、[計算環境リストの確認APIドキュメント](https://cloud.tencent.com/document/product/599/12695)を参照してください。

