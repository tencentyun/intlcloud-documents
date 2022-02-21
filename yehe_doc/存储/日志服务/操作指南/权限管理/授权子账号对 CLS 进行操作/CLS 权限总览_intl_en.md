This document introduces the authorization policies for CLS features and corresponding management and read-only permissions. You can configure the corresponding authorization policy statements based on the CLS features to be authorized.

## Authorization Directions

You need to perform 3 steps: use the root account (`CompanyExample`) to create a custom policy, grant the sub-account (`Developer`) all permissions for the log topic (`TopicA`), and then access CLS using the sub-account (`Developer`). The procedure for creating a custom policy using the root account is as follows:

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam) as the root account (`CompanyExample`).
2. On the left sidebar, click **Policies** to go to the policy management page.
3. Click **Create Custom Policy**.
4. In the pop-up window, select **Create by Policy Syntax**.
5. On the **Create by Policy Syntax** page, select **Blank Template** and click **Next**.
6. On the policy editing page, set the policy name and content, and click **Done**.
For example, you can set the policy name to `CLS-TopicA-Access`. Configure the policy content by referring to the following:


## Authorization Policy Statements for Data Collection

### Authorize the minimum permission for log upload via LogListener

```
{
"version": "2.0",
"statement": [
  {
      "action": [
         "cls:pushlog",
         "cls:listLogset",
         "cls:getConfig",
         "cls:agentHeartBeat"
     ],
      "resource": "*",
      "effect": "allow"
  }
]
}
```

### Configure LogListener collection rules

#### Management permission

- Authorization for all log topics
```
{
"version": "2.0",
"statement": [
  {
  "action": [
         "cls:DescribeLogsets",
         "cls:DescribeConfigs",
         "cls:ModifyConfig",
         "cls:DescribeIndex",
         "cls:DescribeIndex",
         "cls:ModifyIndex"
                ],
   "resource": [
                "*"
            ],
   "effect": "allow"
  }
]
}
```
- Authorization for log topics with a specified tag
```
{
    "version": "2.0",
    "statement": [
        {
        "action": [
                     "cls:DescribeLogsets",
                     "cls:DescribeConfigs",
                     "cls:ModifyConfig",
                     "cls:DescribeIndex",
                     "cls:DescribeIndex",
                     "cls:ModifyIndex"
            ],
            "resource": [
                "*"
            ],
             "condition": {
                    "for_any_value:string_equal": {
                         "qcs:resource_tag": [
                             "key&value"
                          ]
                     }
            },
         "effect": "allow"
        }
    ]
}
```

#### Read-only permission

- Authorization for all log topics
```
{
"version": "2.0",
"statement": [
  {
     "action": [
         "cls:DescribeLogsets",
         "cls:DescribeConfigs",
         "cls:DescribeIndex",
         "cls:DescribeIndex"
                ]
   "resource": [
                "*"
            ],
   "effect": "allow"
  }
]
}
```
- Authorization for log topics with a specified tag
```
{
"version": "2.0",
"statement": [
  {
     "effect": "allow",
     "action": [
         "cls:DescribeLogsets",
         "cls:DescribeConfigs",
         "cls:DescribeIndex",
         "cls:DescribeIndex"
                ],
    "resource": [
                "*"
            ],
     "condition": {
        "for_any_value:string_equal": {
           "qcs:resource_tag": [
             "key&value"
                    ]
                }
            }   
  }
]
}
```

### Authorize the minimum permission for log upload via API

```
{
	"version": "2.0",
	"statement": [
  	{
      "action": [
                "cls:CreateTopic",
                "cls:CreateLogset",
                "cls:UploadLog",
            ],
      "resource": "*",
      "effect": "allow"
  	}
]
}
```

## Authorization Policy Statements for Search and Analysis

### Log search via console

#### Management permission

- Authorization for all log topics
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:DescribeAsyncContextResult",
                "cls:DescribeAsyncSearchResult",
                "cls:DescribeExports",
                "cls:DescribeIndex",
                "cls:DescribeLatestJsonLog",
                "cls:DescribeLogContext",
                "cls:DescribeLogFastAnalysis",
                "cls:DescribeLogHistogram",
                "cls:DescribePartitions",
                "cls:DescribeTopics",
                "cls:GetFastAnalysis",
                "cls:GetHistogram",
                "cls:GetLog",
                "cls:SearchLog",
                "cls:ShowContext",
                "cls:getIndex",
                "cls:getLogset",
                "cls:getTopic",
                "cls:searchLog",
                "cls:DescribeAsyncContextTasks",
                "cls:DescribeAsyncSearchTasks",
                "cls:DescribeLogsets",
                "cls:listLogset",
                "cls:listTopic",
                "cls:listPartitions",
                "cls:CreateAsyncContextTask",
                "cls:CreateAsyncSearchTask",
                "cls:CreateExport",
                "cls:CreateIndex",
                "cls:DeleteAsyncContextTask",
                "cls:DeleteAsyncSearchTask",
                "cls:DeleteExport",
                "cls:DeleteIndex",
                "cls:DeleteLogset",
                "cls:DeleteTopic",
                "cls:MergePartition",
                "cls:ModifyIndex",
                "cls:ModifyLogset",
                "cls:ModifyTopic",
                "cls:SplitPartition",
                "cls:deleteLogset",
                "cls:deleteTopic",
                "cls:downloadLog",
                "cls:modifyIndex",
                "cls:modifyLogset",
                "cls:modifyTopic",
                "cls:updatePartition",
                "cls:GetDeliverFunction",
                "cls:CreateLogset",
                "cls:CreateTopic",
                "cls:createLogset",
                "cls:createTopic"
            ],
            "resource": [
                "*"
            ]
        }
    ]
}
```
- Authorization for log topics with a specified tag
>! During configuration, you also need to bind tags to log topics and logsets.
>
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:DescribeAsyncContextResult",
                "cls:DescribeAsyncSearchResult",
                "cls:DescribeExports",
                "cls:DescribeIndex",
                "cls:DescribeLatestJsonLog",
                "cls:DescribeLogContext",
                "cls:DescribeLogFastAnalysis",
                "cls:DescribeLogHistogram",
                "cls:DescribePartitions",
                "cls:DescribeTopics",
                "cls:GetFastAnalysis",
                "cls:GetHistogram",
                "cls:GetLog",
                "cls:SearchLog",
                "cls:ShowContext",
                "cls:getIndex",
                "cls:getLogset",
                "cls:getTopic",
                "cls:searchLog",
                "cls:DescribeAsyncContextTasks",
                "cls:DescribeAsyncSearchTasks",
                "cls:DescribeLogsets",
                "cls:listLogset",
                "cls:listTopic",
                "cls:listPartitions",
                "cls:CreateAsyncContextTask",
                "cls:CreateAsyncSearchTask",
                "cls:CreateExport",
                "cls:CreateIndex",
                "cls:DeleteAsyncContextTask",
                "cls:DeleteAsyncSearchTask",
                "cls:DeleteExport",
                "cls:DeleteIndex",
                "cls:DeleteLogset",
                "cls:DeleteTopic",
                "cls:MergePartition",
                "cls:ModifyIndex",
                "cls:ModifyLogset",
                "cls:ModifyTopic",
                "cls:SplitPartition",
                "cls:deleteLogset",
                "cls:deleteTopic",
                "cls:downloadLog",
                "cls:modifyIndex",
                "cls:modifyLogset",
                "cls:modifyTopic",
                "cls:updatePartition",
                "cls:GetDeliverFunction"
            ],
            "resource": [
                "*"
            ],
            "condition": {
                "for_any_value:string_equal": {
                    "qcs:resource_tag": [
                        "testCAM&test1"
                    ]
                }
            }
        }
    ]
}
```

#### Read-only permission

- Authorization for log topics with a specified tag
>! During configuration, you also need to bind tags to log topics and logsets.
>
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:DescribeAsyncContextResult",
                "cls:DescribeAsyncSearchResult",
                "cls:DescribeExports",
                "cls:DescribeIndex",
                "cls:DescribeLatestJsonLog",
                "cls:DescribeLogContext",
                "cls:DescribeLogFastAnalysis",
                "cls:DescribeLogHistogram",
                "cls:DescribePartitions",
                "cls:DescribeTopics",
                "cls:GetFastAnalysis",
                "cls:GetHistogram",
                "cls:GetLog",
                "cls:SearchLog",
                "cls:ShowContext",
                "cls:getIndex",
                "cls:getLogset",
                "cls:getTopic",
                "cls:searchLog",
                "cls:DescribeAsyncContextTasks",
                "cls:DescribeAsyncSearchTasks",
                "cls:DescribeLogsets",
                "cls:listLogset",
                "cls:listTopic",
                "cls:listPartitions"
            ],
            "resource": [
                "*"
            ],
            "condition": {
                "for_any_value:string_equal": {
                    "qcs:resource_tag": [
                        "key&value"
                    ]
                }
            }
        }
    ]
}
```
- Authorization for all log topics
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:DescribeAsyncContextResult",
                "cls:DescribeAsyncSearchResult",
                "cls:DescribeExports",
                "cls:DescribeIndex",
                "cls:DescribeLatestJsonLog",
                "cls:DescribeLogContext",
                "cls:DescribeLogFastAnalysis",
                "cls:DescribeLogHistogram",
                "cls:DescribePartitions",
                "cls:DescribeTopics",
                "cls:GetFastAnalysis",
                "cls:GetHistogram",
                "cls:GetLog",
                "cls:SearchLog",
                "cls:ShowContext",
                "cls:getIndex",
                "cls:getLogset",
                "cls:getTopic",
                "cls:searchLog",
                "cls:DescribeAsyncContextTasks",
                "cls:DescribeAsyncSearchTasks",
                "cls:DescribeLogsets",
                "cls:listLogset",
                "cls:listTopic",
                "cls:listPartitions"
            ],
            "resource": [
                "*"
            ]
        }
    ]
}
```

### Visual dashboard

#### Management permission

- Authorization for all log topics
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:GetChart",
                "cls:GetDashboard",
                "cls:ListChart",
                "cls:CreateChart",
                "cls:CreateDashboard",
                "cls:DeleteChart",
                "cls:DeleteDashboard",
                "cls:ModifyChart",
                "cls:ModifyDashboard",
                "cls:ListDashboard"
            ],
            "resource": "*"
        },
        {
            "effect": "allow",
            "action": [
                "cls:SearchLog",
                "cls:DescribeTopics",
                "cls:DescribeLogsets"
            ],
            "resource": "*"
        }
    ]
}
```
- Authorization for log topics with a specified tag
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:GetChart",
                "cls:GetDashboard",
                "cls:ListChart",
                "cls:CreateChart",
                "cls:DeleteChart",
                "cls:DeleteDashboard",
                "cls:ModifyChart",
                "cls:ModifyDashboard"
            ],
            "resource": "*"
        },
        {
            "effect": "allow",
            "action": [
                "cls:ListDashboard"
            ],
            "resource": "*"
        },
        {
            "effect": "allow",
            "action": [
                "cls:SearchLog",
                "cls:DescribeTopics"
            ],
            "resource": [
                "*"
            ],
            "condition": {
                "for_any_value:string_equal": {
                    "qcs:resource_tag": [
                        "key&value"
                    ]
                }
            }
        }
    ]
}
```

#### Read-only permission

- Authorization for all log topics
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:GetChart",
                "cls:GetDashboard",
                "cls:ListChart"
            ],
            "resource": "*"
        },
        {
            "effect": "allow",
            "action": [
                "cls:ListDashboard"
            ],
            "resource": "*"
        },
        {
            "effect": "allow",
            "action": [
                "cls:SearchLog",
                "cls:DescribeTopics"
            ],
            "resource": "*"
        }
    ]
}
```
- Authorization for log topics with a specified tag
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:GetChart",
                "cls:GetDashboard",
                "cls:ListChart"
            ],
            "resource": "*"
        },
        {
            "effect": "allow",
            "action": [
                "cls:ListDashboard"
            ],
            "resource": "*"
        },
        {
            "effect": "allow",
            "action": [
                "cls:SearchLog",
                "cls:DescribeTopics"
            ],
            "resource": [
                "*"
            ],
            "condition": {
                "for_any_value:string_equal": {
                    "qcs:resource_tag": [
                        "key&value"
                    ]
                }
            }
        }
    ]
}
```

## Authorization Policy Statements for Monitoring Alarms

#### Management permission

- Authorization for all log topics
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:DescribeLogsets",
                "cls:DescribeTopics"
            ],
            "resource": [
                "*"
            ]
        },
        {
            "effect": "allow",
            "action": [
                "cls:DescribeAlarms",
                "cls:CreateAlarm",
                "cls:ModifyAlarm",
                "cls:DeleteAlarm",
                "cls:DescribeAlarmNotices",
                "cls:CreateAlarmNotice",
                "cls:ModifyAlarmNotice",
                "cls:DeleteAlarmNotice",
                "cam:ListGroups",
                "cam:DescribeSubAccountContacts",
                "cls:GetAlarmLog",
                "cls:DescribeAlertRecordHistory",
                "cls:CheckAlarmRule",
                "cls:CheckAlarmChannel"
            ],
            "resource": "*"
        }
    ]
}
```
- Authorization for log topics with a specified tag (monitoring alarms currently do not fully support permission management by tag)
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:DescribeLogsets",
                "cls:DescribeTopics"
            ],
            "resource": [
                "*"
            ],
            "condition": {
                "for_any_value:string_equal": {
                    "qcs:resource_tag": [
                        "testCAM&test1"
                    ]
                }
            }
        },
        {
            "effect": "allow",
            "action": [
                "cls:DescribeAlarms",
                "cls:CreateAlarm",
                "cls:ModifyAlarm",
                "cls:DeleteAlarm",
                "cls:DescribeAlarmNotices",
                "cls:CreateAlarmNotice",
                "cls:ModifyAlarmNotice",
                "cls:DeleteAlarmNotice",
                "cam:ListGroups",
                "cam:DescribeSubAccountContacts",
                "cls:GetAlarmLog",
                "cls:DescribeAlertRecordHistory",
                "cls:CheckAlarmRule",
                "cls:CheckAlarmChannel"
            ],
            "resource": "*"
        }
    ]
}
```

#### Read-only permission

- Authorization for all log topics
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:DescribeLogsets",
                "cls:DescribeTopics"
            ],
            "resource": [
                "*"
            ]
        },
        {
            "effect": "allow",
            "action": [
                "cls:DescribeAlarms",
                "cls:DescribeAlarmNotices",
                "cls:GetAlarmLog",
                "cls:DescribeAlertRecordHistory",
                "cam:ListGroups",
                "cam:DescribeSubAccountContacts"
            ],
            "resource": "*"
        }
    ]
}
```
- Authorization for log topics with a specified tag (monitoring alarms currently do not fully support permission management by tag)
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:DescribeLogsets",
                "cls:DescribeTopics"
            ],
            "resource": [
                "*"
            ],
            "condition": {
                "for_any_value:string_equal": {
                    "qcs:resource_tag": [
                        "testCAM&test1"
                    ]
                }
            }
        },
        {
            "effect": "allow",
            "action": [
                "cls:DescribeAlarms",
                "cls:DescribeAlarmNotices",
                "cls:GetAlarmLog",
                "cls:DescribeAlertRecordHistory",
                "cam:ListGroups",
                "cam:DescribeSubAccountContacts"
            ],
            "resource": "*"
        }
    ]
}
```

## Authorization Policy Statements for Data Shipping

### Shipping to CKafka

#### Management permission

- Authorization for all log topics
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:DescribeTopics",
                "cls:DescribeLogsets"
            ],
            "resource": "*",
        },
        {
            "effect": "allow",
            "action": [
                "tag:DescribeResourceTagsByResourceIds",
                "tag:DescribeTagKeys",
                "tag:DescribeTagValues",
                "cam:ListAttachedRolePolicies",
                "ckafka:DescribeInstances",
                "ckafka:DescribeTopic",
                "ckafka:DescribeInstanceAttributes",
                "cls:modifyConsumer",
                "cls:getConsumer"
            ],
            "resource": "*"
        }
    ]
}
```
- Authorization for log topics with a specified tag
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:DescribeTopics",
                "cls:DescribeLogsets"
            ],
            "resource": "*",
            "condition": {
                "for_any_value:string_equal": {
                    "qcs:resource_tag": [
                        "age&13",
                        "name&vinson"
                    ]
                }
            }
        },
        {
            "effect": "allow",
            "action": [
                "tag:DescribeResourceTagsByResourceIds",
                "tag:DescribeTagKeys",
                "tag:DescribeTagValues",
                "cam:ListAttachedRolePolicies",
                "ckafka:DescribeInstances",
                "ckafka:DescribeTopic",
                "ckafka:DescribeInstanceAttributes",
                "cls:modifyConsumer",
                "cls:getConsumer"
            ],
            "resource": "*"
        }
    ]
}
```

#### Read-only permission

- Authorization for all log topics
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:DescribeTopics",
                "cls:DescribeLogsets"
            ],
            "resource": "*"
        },
        {
            "effect": "allow",
            "action": [
                "tag:DescribeResourceTagsByResourceIds",
                "tag:DescribeTagKeys",
                "tag:DescribeTagValues",
                "cam:ListAttachedRolePolicies",
                "ckafka:DescribeInstances",
                "ckafka:DescribeTopic",
                "ckafka:DescribeInstanceAttributes",
                "cls:getConsumer"
            ],
            "resource": "*"
        }
    ]
}
```
- Authorization for log topics with a specified tag
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:DescribeTopics",
                "cls:DescribeLogsets"
            ],
            "resource": "*",
            "condition": {
                "for_any_value:string_equal": {
                    "qcs:resource_tag": [
                        "key&value"
                    ]
                }
            }
        },
        {
            "effect": "allow",
            "action": [
                "tag:DescribeResourceTagsByResourceIds",
                "tag:DescribeTagKeys",
                "tag:DescribeTagValues",
                "cam:ListAttachedRolePolicies",
                "ckafka:DescribeInstances",
                "ckafka:DescribeTopic",
                "ckafka:DescribeInstanceAttributes",
                "cls:getConsumer"
            ],
            "resource": "*"
        }
    ]
}
```

### Shipping to COS

#### Management permission

- Authorization for all log topics
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:DescribeTopics",
                "cls:DescribeLogsets",
                "cls:DescribeIndex"
            ],
            "resource": "*"
        },
        {
            "effect": "allow",
            "action": [
                "tag:DescribeResourceTagsByResourceIds",
                "tag:DescribeTagKeys",
                "tag:DescribeTagValues",
                "cls:CreateShipper",
                "cls:ModifyShipper",
                "cls:DescribeShippers",
                "cls:DeleteShipper",
                "cls:DescribeShipperTasks",
                "cls:RetryShipperTask",
                "cam:ListAttachedRolePolicies",
                "cos:GetService",
            ],
            "resource": "*"
        }
    ]
}
```
- Authorization for log topics with a specified tag
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:DescribeTopics",
                "cls:DescribeLogsets",
                "cls:DescribeIndex"
            ],
            "resource": "*", 
            "condition": {
                "for_any_value:string_equal": {
                    "qcs:resource_tag": [
                        "key&value"
                    ]
                }
            }
        },
        {
            "effect": "allow",
            "action": [
                "tag:DescribeResourceTagsByResourceIds",
                "tag:DescribeTagKeys",
                "tag:DescribeTagValues",
                "cls:CreateShipper",
                "cls:ModifyShipper",
                "cls:DescribeShippers",
                "cls:DeleteShipper",
                "cls:DescribeShipperTasks",
                "cls:RetryShipperTask",
                "cam:ListAttachedRolePolicies",
                "cos:GetService",
            ],
            "resource": "*"
        }
    ]
}
```

#### Read-only permission

- Authorization for all log topics
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:DescribeTopics",
                "cls:DescribeLogsets"            ],
            "resource": "*"
        },
        {
            "effect": "allow",
            "action": [
                "tag:DescribeResourceTagsByResourceIds",
                "tag:DescribeTagKeys",
                "tag:DescribeTagValues",
                "cls:DescribeShippers",
                "cls:DescribeShipperTasks",
                "cls:RetryShipperTask",
                "cam:ListAttachedRolePolicies"
            ],
            "resource": "*"
        }
    ]
}
```
- Authorization for log topics with a specified tag
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:DescribeTopics",
                "cls:DescribeLogsets"            ],
            "resource": "*",
            "condition": {
                "for_any_value:string_equal": {
                    "qcs:resource_tag": [
                        "key&value"
                    ]
                }
            }
        },
        {
            "effect": "allow",
            "action": [
                "tag:DescribeResourceTagsByResourceIds",
                "tag:DescribeTagKeys",
                "tag:DescribeTagValues",
                "cls:DescribeShippers",
                "cls:DescribeShipperTasks",
                "cls:RetryShipperTask",
                "cam:ListAttachedRolePolicies"
            ],
            "resource": "*"
        }
    ]
}
```

### Shipping to SCF

#### Management permission

- Authorization for all log topics
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:DescribeTopics",
                "cls:DescribeLogsets"
            ],
            "resource": "*"
        },
        {
            "effect": "allow",
            "action": [
                "tag:DescribeResourceTagsByResourceIds",
                "tag:DescribeTagKeys",
                "tag:DescribeTagValues",
                "cam:ListAttachedRolePolicies",
                "cls:CreateDeliverFunction",
                "cls:DeleteDeliverFunction",
                "cls:ModifyDeliverFunction",
                "cls:GetDeliverFunction",
                "scf:ListFunctions",
                "scf:ListAliases",
                "scf:ListVersionByFunction"
            ],
            "resource": "*"
        }
    ]
}
```
- Authorization for log topics with a specified tag
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:DescribeTopics",
                "cls:DescribeLogsets"
            ],
            "resource": "*",
            "condition": {
                "for_any_value:string_equal": {
                    "qcs:resource_tag": [
                        "key&value"
                    ]
                }
            }
        },
        {
            "effect": "allow",
            "action": [
                "tag:DescribeResourceTagsByResourceIds",
                "tag:DescribeTagKeys",
                "tag:DescribeTagValues",
                "cam:ListAttachedRolePolicies",
                "cls:CreateDeliverFunction",
                "cls:DeleteDeliverFunction",
                "cls:ModifyDeliverFunction",
                "cls:GetDeliverFunction",
                "scf:ListFunctions",
                "scf:ListAliases",
                "scf:ListVersionByFunction"
            ],
            "resource": "*"
        }
    ]
}
```

#### Read-only permission

- Authorization for all log topics
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:DescribeTopics",
                "cls:DescribeLogsets"
            ],
            "resource": "*"
        },
        {
            "effect": "allow",
            "action": [
                "tag:DescribeResourceTagsByResourceIds",
                "tag:DescribeTagKeys",
                "tag:DescribeTagValues",
                "cam:ListAttachedRolePolicies",
                "cls:GetDeliverFunction",
                "scf:ListFunctions",
                "scf:ListAliases",
                "scf:ListVersionByFunction"
            ],
            "resource": "*"
        }
    ]
}
```
- Authorization for log topics with a specified tag
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:DescribeTopics",
                "cls:DescribeLogsets"
            ],
            "resource": "*",
            "condition": {
                "for_any_value:string_equal": {
                    "qcs:resource_tag": [
                        "key&value"
                    ]
                }
            }
        },
        {
            "effect": "allow",
            "action": [
                "tag:DescribeResourceTagsByResourceIds",
                "tag:DescribeTagKeys",
                "tag:DescribeTagValues",
                "cam:ListAttachedRolePolicies",
                "cls:GetDeliverFunction",
                "scf:ListFunctions",
                "scf:ListAliases",
                "scf:ListVersionByFunction"
            ],
            "resource": "*"
        }
    ]
}
```

## Authorization Policy Statements for Developers

### Permission to display on Grafana

- Authorization for all log topics
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:searchLog"
            ],
            "resource": [
                "*"
            ]
        }
    ]
}
```
- Authorization for log topics of a specified tag
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:searchLog"
            ],
            "resource": [
                "*"
            ],
            "condition": {
                "for_any_value:string_equal": {
                    "qcs:resource_tag": [
                        "testCAM&test1"
                    ]
                }
            }
        }
    ]
}
```

