## 1. API説明

APIリクエストドメイン名： cdb.tencentcloudapi.com 。

このAPI（DescribeDBZoneConfig）は作成可能なデータベースの各地域での販売可能な仕様構成を照合するために使用されます。

デフォルトのAPIリクエスト頻度制限：20回/秒。

注意：このAPIは金融区地域をサポートします。金融区と非金融区は分離されており、相互運用できないため、共通パラメータRegionが金融区地域（例えば、ap-shanghai-fsi）の場合は、金融区地域のドメイン名を同時に指定する必要があります。Region地域と一致するようにするのは一番です。例えば：cdb.ap-shanghai-fsi.tencentcloudapi.com 。



## 2. 入力パラメータ

次のリクエストパラメータリストには、APIリクエストパラメータと一部の共通パラメータのみがリストされています。完全な共通パラメータのリストについては、[共通リクエストパラメータ](/document/api/236/15833)を参照してください。

| パラメータ名 | 必須項目 | タイプ | 説明 |
|---------|---------|---------|---------|
| Action | はい | String | 共通パラメータ、このAPIの値：DescribeDBZoneConfig |
| Version | はい | String | 共通パラメータ、該当APIの値：2017/03/20 |
| Region | はい | String | 共通パラメータ。詳細について製品がサポートする[地域リスト](/document/api/236/15833#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)を参照してください。 |

## 3. 出力パラメータ

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| TotalCount | Integer | 販売可能な地域の構成数量|
| Items | Array of [RegionSellConf](/document/api/236/15878#RegionSellConf) | 販売可能な地域の構成詳細|
| RequestId | String | 唯一のリクエストID、リクエストごとに返します。問題を特定するときに、このリクエストのRequestIdが必要です。|

## 4. 例

### 例1 データベースの販売可能な仕様の取得

#### 入力例

```
https://cdb.tencentcloudapi.com/?Action=DescribeDBZoneConfig
&<共通リクエストパラメータ>
```

#### 出力例

```
{
    "Response": {
        "TotalCount": 17,
        "Items": [
            {
                "RegionName": "広州",
                "Area": "中国華南",
                "IsDefaultRegion": 0,
                "Region": "ap-guangzhou",
                "ZonesConf": [
                    {
                        "Status": 1,
                        "ZoneName": "広州2区",
                        "IsCustom": true,
                        "IsSupportDr": true,
                        "IsSupportVpc": true,
                        "HourInstanceSaleMaxNum": 30,
                        "IsDefaultZone": false,
                        "IsBm": false,
                        "PayType": [
                            "0",
                            "1",
                            "2"
                        ],
                        "DrZone": [
                            "ap-shanghai-1",
                            "ap-shanghai-2",
                            "ap-beijing-1",
                            "ap-beijing-2",
                            "ap-guangzhou-open-1",
                            "ap-guangzhou-3",
                            "ap-guangzhou-4",
                            "ap-chengdu-1",
                            "ap-chengdu-2"
                        ],
                        "ProtectMode": [
                            "0",
                            "1",
                            "2"
                        ],
                        "ZoneConf": {
                            "DeployMode": [
                                0
                            ],
                            "MasterZone": [
                                "ap-guangzhou-2"
                            ],
                            "SlaveZone": [
                                "ap-guangzhou-2"
                            ],
                            "BackupZone": [
                                "ap-guangzhou-2"
                            ]
                        },
                        "Zone": "ap-guangzhou-2",
                        "SellType": [
                            {
                                "TypeName": "Z3",
                                "EngineVersion": [
                                    "5.5",
                                    "5.6",
                                    "5.7"
                                ],
                                "Configs": [
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 1000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 1000,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が1万人に達する小型ゲームアプリケーションまたは100万人レベルのツール類アプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 2000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 2400,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が1万人に達する小型ゲームアプリケーションまたは100万人レベルのツール類アプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 4000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 4400,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が10万人レベルに達する中型ゲームアプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 8000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 7200,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が100万人レベルに達する大型ゲームアプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 16000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 18000,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が100万人レベルに達する大型ゲームアプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 32000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 25000,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が100万人レベルに達する大型ゲームアプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 64000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 37689,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が100万人レベルに達する大型ゲームアプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 96000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 40919,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が100万人レベルに達する大型ゲームアプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 128000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 61378,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が100万人レベルに達する大型ゲームアプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 244000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 122755,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が100万人レベルに達する大型ゲームアプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 488000,
                                        "Cpu": 0,
                                        "VolumeMin": 6000,
                                        "VolumeMax": 6000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 245509,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が100万人レベルに達する大型ゲームアプリケーション",
                                        "Status": 0
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Status": 1,
                        "ZoneName": "広州3区",
                        "IsCustom": true,
                        "IsSupportDr": true,
                        "IsSupportVpc": true,
                        "HourInstanceSaleMaxNum": 30,
                        "IsDefaultZone": false,
                        "IsBm": false,
                        "PayType": [
                            "0",
                            "1"
                        ],
                        "DrZone": [
                            "ap-shanghai-1",
                            "ap-shanghai-2",
                            "ap-beijing-1",
                            "ap-beijing-2",
                            "ap-guangzhou-open-1",
                            "ap-guangzhou-2",
                            "ap-guangzhou-4",
                            "ap-seoul-1",
                            "ap-chengdu-1",
                            "ap-chengdu-2"
                        ],
                        "ProtectMode": [
                            "0",
                            "1",
                            "2"
                        ],
                        "ZoneConf": {
                            "DeployMode": [
                                0
                            ],
                            "MasterZone": [
                                "ap-guangzhou-3"
                            ],
                            "SlaveZone": [
                                "ap-guangzhou-3"
                            ],
                            "BackupZone": [
                                "ap-guangzhou-3"
                            ]
                        },
                        "Zone": "ap-guangzhou-3",
                        "SellType": [
                            {
                                "TypeName": "Z3",
                                "EngineVersion": [
                                    "5.5",
                                    "5.6",
                                    "5.7"
                                ],
                                "Configs": [
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 1000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 1000,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が1万人に達する小型ゲームアプリケーションまたは100万人レベルのツール類アプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 2000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 2400,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が1万人に達する小型ゲームアプリケーションまたは100万人レベルのツール類アプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 4000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 4400,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が10万人レベルに達する中型ゲームアプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 8000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 7200,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が100万人レベルに達する大型ゲームアプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 16000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 18000,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が100万人レベルに達する大型ゲームアプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 32000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 25000,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が100万人レベルに達する大型ゲームアプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 64000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 37689,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が100万人レベルに達する大型ゲームアプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 96000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 40919,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が100万人レベルに達する大型ゲームアプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 128000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 61378,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が100万人レベルに達する大型ゲームアプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 244000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 122755,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が100万人レベルに達する大型ゲームアプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 488000,
                                        "Cpu": 0,
                                        "VolumeMin": 6000,
                                        "VolumeMax": 6000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 245509,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が100万人レベルに達する大型ゲームアプリケーション",
                                        "Status": 0
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Status": 4,
                        "ZoneName": "広州1区",
                        "IsCustom": true,
                        "IsSupportDr": false,
                        "IsSupportVpc": true,
                        "HourInstanceSaleMaxNum": 30,
                        "IsDefaultZone": false,
                        "IsBm": false,
                        "PayType": [
                            "0",
                            "1",
                            "2"
                        ],
                        "ProtectMode": [
                            "0",
                            "1",
                            "2"
                        ],
                        "ZoneConf": {
                            "DeployMode": [
                                0
                            ],
                            "MasterZone": [
                                "ap-guangzhou-1"
                            ],
                            "SlaveZone": [
                                "ap-guangzhou-1"
                            ],
                            "BackupZone": [
                                "ap-guangzhou-1"
                            ]
                        },
                        "Zone": "ap-guangzhou-1",
                        "SellType": [
                            {
                                "TypeName": "Z3",
                                "EngineVersion": [
                                    "5.5",
                                    "5.6",
                                    "5.7"
                                ],
                                "Configs": [
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 360,
                                        "Cpu": 0,
                                        "VolumeMin": 10,
                                        "VolumeMax": 500,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 120,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が1万人に達する小型ゲームアプリケーションまたは100万人のツール類アプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 1000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 500,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 1000,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が1万人に達する小型ゲームアプリケーションまたは100万人レベルのツール類アプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 2000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 500,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 2400,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が1万人に達する小型ゲームアプリケーションまたは100万人レベルのツール類アプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 4000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 1000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 4400,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が10万人レベルに達する中型ゲームアプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 8000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 1000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 7200,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が100万人レベルに達する大型ゲームアプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 12000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 1000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 15000,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が100万人レベルに達する大型ゲームアプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 16000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 1000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 18000,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が100万人レベルに達する大型ゲームアプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 24000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 1000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 23000,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が100万人レベルに達する大型ゲームアプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 48000,
                                        "Cpu": 0,
                                        "VolumeMin": 1000,
                                        "VolumeMax": 1000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 37000,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が100万人レベルに達する大型ゲームアプリケーション",
                                        "Status": 0
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Status": 2,
                        "ZoneName": "広州4区",
                        "IsCustom": true,
                        "IsSupportDr": true,
                        "IsSupportVpc": true,
                        "HourInstanceSaleMaxNum": 30,
                        "IsDefaultZone": true,
                        "IsBm": false,
                        "PayType": [
                            "0",
                            "1",
                            "2"
                        ],
                        "DrZone": [
                            "ap-shanghai-1",
                            "ap-shanghai-2",
                            "ap-shanghai-3",
                            "ap-beijing-1",
                            "ap-beijing-2",
                            "ap-guangzhou-open-1",
                            "ap-guangzhou-2",
                            "ap-guangzhou-3",
                            "na-ashburn-1",
                            "ap-chengdu-1",
                            "ap-chengdu-2",
                            "ap-bangkok-1"
                        ],
                        "ProtectMode": [
                            "0",
                            "1",
                            "2"
                        ],
                        "ZoneConf": {
                            "DeployMode": [
                                0
                            ],
                            "MasterZone": [
                                "ap-guangzhou-4"
                            ],
                            "SlaveZone": [
                                "ap-guangzhou-4"
                            ],
                            "BackupZone": [
                                "ap-guangzhou-4"
                            ]
                        },
                        "Zone": "ap-guangzhou-4",
                        "SellType": [
                            {
                                "TypeName": "Z3",
                                "EngineVersion": [
                                    "5.5",
                                    "5.6",
                                    "5.7"
                                ],
                                "Configs": [
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 1000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 1000,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が1万人に達する小型ゲームアプリケーションまたは100万人レベルのツール類アプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 2000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 2400,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が1万人に達する小型ゲームアプリケーションまたは100万人レベルのツール類アプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 4000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 4400,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が10万人レベルに達する中型ゲームアプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 8000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 7200,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が100万人レベルに達する大型ゲームアプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 16000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 18000,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が100万人レベルに達する大型ゲームアプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 32000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 25000,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が100万人レベルに達する大型ゲームアプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 64000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 37689,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が100万人レベルに達する大型ゲームアプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 96000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 40919,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が100万人レベルに達する大型ゲームアプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 128000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 61378,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が100万人レベルに達する大型ゲームアプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 244000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 122755,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が100万人レベルに達する大型ゲームアプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 488000,
                                        "Cpu": 0,
                                        "VolumeMin": 6000,
                                        "VolumeMax": 6000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 245509,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が100万人レベルに達する大型ゲームアプリケーション",
                                        "Status": 0
                                    }
                                ]
                            }
                        ]
                    }
                ]
            },
            {
                "RegionName": "バンコク",
                "Area": "アジア太平洋地区",
                "IsDefaultRegion": 0,
                "Region": "ap-bangkok",
                "ZonesConf": [
                    {
                        "Status": 2,
                        "ZoneName": "バンコク1区",
                        "IsCustom": true,
                        "IsSupportDr": true,
                        "IsSupportVpc": true,
                        "HourInstanceSaleMaxNum": 30,
                        "IsDefaultZone": true,
                        "IsBm": false,
                        "PayType": [
                            "0",
                            "1"
                        ],
                        "DrZone": [
                            "ap-guangzhou-4"
                        ],
                        "ProtectMode": [
                            "0",
                            "1",
                            "2"
                        ],
                        "ZoneConf": {
                            "DeployMode": [
                                0
                            ],
                            "MasterZone": [
                                "ap-bangkok-1"
                            ],
                            "SlaveZone": [
                                "ap-bangkok-1"
                            ],
                            "BackupZone": [
                                "ap-bangkok-1"
                            ]
                        },
                        "Zone": "ap-bangkok-1",
                        "SellType": [
                            {
                                "TypeName": "Z3",
                                "EngineVersion": [
                                    "5.5",
                                    "5.6",
                                    "5.7"
                                ],
                                "Configs": [
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 1000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 1000,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が1万人に達する小型ゲームアプリケーションまたは100万人レベルのツール類アプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 2000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 2400,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が1万人に達する小型ゲームアプリケーションまたは100万人レベルのツール類アプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 4000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 4400,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が10万人レベルに達する中型ゲームアプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 8000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 7200,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が100万人レベルに達する大型ゲームアプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 16000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 18000,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が100万人レベルに達する大型ゲームアプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 32000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 25000,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が100万人レベルに達する大型ゲームアプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 64000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 37689,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が100万人レベルに達する大型ゲームアプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 96000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 40919,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が100万人レベルに達する大型ゲームアプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 128000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 61378,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が100万人レベルに達する大型ゲームアプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 244000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 122755,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が100万人レベルに達する大型ゲームアプリケーション",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "高可用性バージョン",
                                        "CdbType": "CUSTOM",
                                        "Memory": 488000,
                                        "Cpu": 0,
                                        "VolumeMin": 6000,
                                        "VolumeMax": 6000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 245509,
                                        "Iops": 0,
                                        "Info": "1日のアクティブユーザー数が100万人レベルに達する大型ゲームアプリケーション",
                                        "Status": 0
                                    }
                                ]
                            }
                        ]
                    }
                ]
            }
        ],
        "RequestId": "f1ccdafe-6803-455e-bb84-e33c08ba8247"
    }
}
```


## 5. 開発者リソース

### API Explorer

**このツールは、オンライン呼び出し、署名検証、SDKコードの生成、およびクイック検索APIなどの機能を提供し、クラウドAPIの使用難しさを大幅に軽減することができますので、お勧めします。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cdb&Version=2017-03-20&Action=DescribeDBZoneConfig)

### SDK

クラウドAPI 3.0は、API呼び出しを容易にするために複数のプログラミング言語をサポートする、関連開発ツールセット（SDK）を提供します。

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. エラーコード

以下に、APIビジネスロジックに関連するエラーコードのみをリストします。その他のエラーコードについては、[共通エラーコード](/document/api/236/15835#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)を参照してください。

| エラーコード | 説明 |
|---------|---------|
| CdbError | バックエンドエラーまたはプロセスエラー。 |
| InvalidParameter | パラメータエラー。 |

