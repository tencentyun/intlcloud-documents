## Access Policies for Data Collection

### Collecting data using LogListener

Users can collect data and upload logs using the LogListener agent. The example below grants users the minimum access to uploading logs via LogListener.

```
{
	"version": "2.0",
	"statement": [{
		"action": [
			"cls:pushLog",
			"cls:getConfig",
			"cls:agentHeartBeat"
		],
		"resource": "*",
		"effect": "allow"
	}]
}
```

>? If your LogListener version is earlier than v2.6.5, you need to add "cls:listLogset" to the above content.
>

### Uploading data using an API

Users can upload logs to CLS using an API. The example below grants users the minimum access to uploading logs using an API.

```
{
	"version": "2.0",
	"statement": [{
		"action": [
			"cls:UploadLog"
		],
		"resource": "*",
		"effect": "allow"
	}]
}
```

### Uploading data using Kafka

Users can upload logs to CLS using the Kafka protocol. The example below grants users the minimum access to upload logs using the Kafka protocol.

```
{
	"version": "2.0",
	"statement": [{
		"action": [
			"cls:RealtimeProducer"
		],
		"resource": "*",
		"effect": "allow"
	}]
}
```

### Managing collection configurations and machine groups

Users can create, modify, and delete collection configurations and machine groups.

```
{
	"version": "2.0",
	"statement": [{
		"action": [
			"cls:DescribeLogsets",
			"cls:DescribeTopics",
			"cls:CreateConfig",
			"cls:CreateConfig",
			"cls:DeleteConfig",
			"cls:DescribeConfigs",
			"cls:ModifyConfig",
			"cls:CreateMachineGroup",
			"cls:DeleteMachineGroup",
			"cls:DescribeMachineGroups",
			"cls:ModifyMachineGroup"
		],
		"resource": "*",
		"effect": "allow"
	}]
}
```

## Access Policies for Search and Analysis

### Searching for logs via the console

#### Managing all log topics

Users can search for and manage all log topics, including creating/deleting log topics and modifying index configurations, not including configuring collection, shipping log data, or processing logs.

```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:CreateLogset",
                "cls:CreateTopic",
                "cls:CreateExport",
                "cls:CreateIndex",
                "cls:DeleteLogset",
                "cls:DeleteTopic",
                "cls:DeleteExport",
                "cls:DeleteIndex",
                "cls:ModifyLogset",
                "cls:ModifyTopic",
                "cls:ModifyIndex",
                "cls:MergePartition",
                "cls:SplitPartition",
                "cls:DescribeLogsets",
                "cls:DescribeTopics",
                "cls:DescribeExports",
                "cls:DescribeIndex",
                "cls:DescribeIndexs",
                "cls:DescribePartitions",
                "cls:SearchLog",
                "cls:DescribeLogHistogram",
                "cls:DescribeLogContext",
                "cls:DescribeLogFastAnalysis",
                "cls:DescribeLatestJsonLog"
            ],
            "resource": [
                "*"
            ]
        }
    ]
}
```

#### Managing specific log topics

Users can search for and manage specific log topics, including creating/deleting log topics and modifying index configurations, not including configuring collection, shipping log data, or processing logs.

```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:CreateLogset",
                "cls:CreateTopic",
                "cls:CreateExport",
                "cls:CreateIndex",
                "cls:DeleteLogset",
                "cls:DeleteTopic",
                "cls:DeleteExport",
                "cls:DeleteIndex",
                "cls:ModifyLogset",
                "cls:ModifyTopic",
                "cls:ModifyIndex",
                "cls:MergePartition",
                "cls:SplitPartition",
                "cls:DescribeLogsets",
                "cls:DescribeTopics",
                "cls:DescribeExports",
                "cls:DescribeIndex",
                "cls:DescribeIndexs",
                "cls:DescribePartitions",
                "cls:SearchLog",
                "cls:DescribeLogHistogram",
                "cls:DescribeLogContext",
                "cls:DescribeLogFastAnalysis",
                "cls:DescribeLatestJsonLog"
            ],
            "resource": [
                "qcs::cls:ap-guangzhou:100007***827:logset/1c012db7-2cfd-4418-****-7342c7a42516",
                "qcs::cls:ap-guangzhou:100007***827:topic/380fe1f1-0c7b-4b0d-****-d514959db1bb"
            ]
        }
    ]
}
```

#### Managing log topics with specific tags

Users can search for and manage log topics with specific tags, including creating/deleting log topics and modifying index configurations, not including configuring collection, shipping log data, or processing logs. When you tag a log topic, you need to also tag its logset.

```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:CreateLogset",
                "cls:CreateTopic",
                "cls:CreateExport",
                "cls:CreateIndex",
                "cls:DeleteLogset",
                "cls:DeleteTopic",
                "cls:DeleteExport",
                "cls:DeleteIndex",
                "cls:ModifyLogset",
                "cls:ModifyTopic",
                "cls:ModifyIndex",
                "cls:MergePartition",
                "cls:SplitPartition",
                "cls:DescribeLogsets",
                "cls:DescribeTopics",
                "cls:DescribeExports",
                "cls:DescribeIndex",
                "cls:DescribeIndexs",
                "cls:DescribePartitions",
                "cls:SearchLog",
                "cls:DescribeLogHistogram",
                "cls:DescribeLogContext",
                "cls:DescribeLogFastAnalysis",
                "cls:DescribeLatestJsonLog"
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

#### Reading all log topics

Users can search for logs in all log topics.

```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:DescribeLogsets",
                "cls:DescribeTopics",
                "cls:DescribeExports",
                "cls:DescribeIndex",
                "cls:DescribeIndexs",
                "cls:DescribePartitions",
                "cls:SearchLog",
                "cls:DescribeLogHistogram",
                "cls:DescribeLogContext",
                "cls:DescribeLogFastAnalysis",
                "cls:DescribeLatestJsonLog"
            ],
            "resource": [
                "*"
            ]
        }
    ]
}
```

#### Reading specific log topics

Users can search for logs in specific log topics.

```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:DescribeLogsets",
                "cls:DescribeTopics",
                "cls:DescribeExports",
                "cls:DescribeIndex",
                "cls:DescribeIndexs",
                "cls:DescribePartitions",
                "cls:SearchLog",
                "cls:DescribeLogHistogram",
                "cls:DescribeLogContext",
                "cls:DescribeLogFastAnalysis",
                "cls:DescribeLatestJsonLog"
            ],
            "resource": [
                "qcs::cls:ap-guangzhou:100007***827:logset/1c012db7-2cfd-4418-****-7342c7a42516",
                "qcs::cls:ap-guangzhou:100007***827:topic/380fe1f1-0c7b-4b0d-****-d514959db1bb"
            ]
        }
    ]
}
```

#### Reading log topics with specific tags

Users can search for logs in log topics with specific tags.

```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:DescribeLogsets",
                "cls:DescribeTopics",
                "cls:DescribeExports",
                "cls:DescribeIndex",
                "cls:DescribeIndexs",
                "cls:DescribePartitions",
                "cls:SearchLog",
                "cls:DescribeLogHistogram",
                "cls:DescribeLogContext",
                "cls:DescribeLogFastAnalysis",
                "cls:DescribeLatestJsonLog"
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

### Searching for and analyzing logs via APIs

#### Searching for and analyzing all log topics

Users can search for and analyze all log topics via APIs.

```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:SearchLog"
            ],
            "resource": [
                "*"
            ]
        }
    ]
}
```

#### Searching for and analyzing specific log topics

Users can search for and analyze specific log topics via APIs.

```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:SearchLog"
            ],
            "resource": [
                "qcs::cls:ap-guangzhou:100007***827:logset/1c012db7-2cfd-4418-****-7342c7a42516",
                "qcs::cls:ap-guangzhou:100007***827:topic/380fe1f1-0c7b-4b0d-****-d514959db1bb"
            ]
        }
    ]
}
```

#### Searching for and analyzing log topics with specific tags

Users can search for and analyze log topics with specific tags via APIs.

```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:SearchLog"
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



### Analyzing logs using dashboards

#### Managing all dashboards

Users can manage (including create, edit, and delete) all dashboards and view the data of all log topics via dashboards.

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
                "cls:DescribeDashboards"
            ],
            "resource": "*"
        },
        {
            "effect": "allow",
            "action": [
                "cls:SearchLog",
                "cls:DescribeTopics",
                "cls:DescribeLogFastAnalysis",
                "cls:DescribeIndex",
                "cls:DescribeLogsets"
            ],
            "resource": "*"
        }
    ]
}
```

#### Managing log topics and dashboards with specific tags

Users can manage (including create, edit, and delete) dashboards with specific tags and view the data of log topics with specific tags via dashboards.

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
	                "cls:DescribeDashboards"
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
	                "cls:SearchLog",
	                "cls:DescribeTopics",
	                "cls:DescribeLogFastAnalysis",
	                "cls:DescribeIndex",
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
	        }
	    ]
	}

#### Managing the log topics and dashboards of specific resources

Users can manage (including create, edit, and delete) specific dashboards and view the data of specific log topics via dashboards.

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
                "cls:DescribeDashboards"
            ],
            "resource": [
                "qcs::cls::uin/100000***001:dashboard/dashboard-0769a3ba-2514-409d-****-f65b20b23736"
            ]
        },
        {
            "effect": "allow",
            "action": [
                "cls:SearchLog",
                "cls:DescribeTopics",
                "cls:DescribeLogFastAnalysis",
                "cls:DescribeIndex",
                "cls:DescribeLogsets"
            ],
            "resource": [
                "qcs::cls::uin/100000***001:topic/174ca473-50d0-4fdf-****-2ef681a1e02a"
            ]
        }
    ]
}
```

#### Viewing all dashboards

Users can view all dashboards and the data of all log topics via dashboards.

	{
	    "version": "2.0",
	    "statement": [
	         {
	            "effect": "allow",
	            "action": [
	                "cls:GetChart",
	                "cls:GetDashboard",
	                "cls:ListChart",
	                "cls:DescribeDashboards"
	            ],
	            "resource": "*"
	        },
	        {
	            "effect": "allow",
	            "action": [
	                "cls:SearchLog",
	                "cls:DescribeTopics",
	                "cls:DescribeLogFastAnalysis",
	                "cls:DescribeIndex",
	                "cls:DescribeLogsets"
	            ],
	            "resource": "*"
	        }
	    ]
	}

#### Viewing log topics and dashboards with specific tags

Users can view dashboards with specific tags and view the data of log topics with specific tags via dashboards.

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
                "cls:DescribeDashboards"
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
                "cls:SearchLog",
                "cls:DescribeTopics",
                "cls:DescribeLogFastAnalysis",
                "cls:DescribeIndex",
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
        }
    ]
}
```

#### Viewing the log topics and dashboards of specific resources

Users can view specific dashboards and the data of specific log topics via dashboards.

	{
	    "version": "2.0",
	    "statement": [
	         {
	            "effect": "allow",
	            "action": [
	                "cls:GetChart",
	                "cls:GetDashboard",
	                "cls:ListChart",
	                "cls:DescribeDashboards"
	            ],
	            "resource": [
	                "qcs::cls::uin/100000***001:dashboard/dashboard-0769a3ba-2514-409d-****-f65b20b23736"
	            ]
	        },
	        {
	            "effect": "allow",
	            "action": [
	                "cls:SearchLog",
	                "cls:DescribeTopics",
	                "cls:DescribeLogFastAnalysis",
	                "cls:DescribeIndex",
	                "cls:DescribeLogsets"
	            ],
	            "resource": [
	                "qcs::cls::uin/100000***001:topic/174ca473-50d0-4fdf-****-2ef681a1e02a"
	            ]
	        }
	    ]
	}

## Access Policies for Alarms

#### Managing all alarm policies

Users can manage all alarm policies, including create and view alarm policies and create notification groups.

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

#### Viewing all alarm policies

Users can view all alarm policies.

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



## Access Policies for Data Processing

#### Managing all data processing tasks

Users can manage the data processing tasks of all log topics.

```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:DescribeLogsets",
                "cls:DescribeDataTransformPreviewDataInfo",
                "cls:DescribeTopics",
                "cls:DescribeIndex",
                "cls:CreateDataTransform"
            ],
            "resource": [
                "*"
            ]
        },
        {
            "effect": "allow",
            "action": [
                "cls:DescribeFunctions",
                "cls:CheckFunction",
                "cls:DescribeDataTransformFailLogInfo",
                "cls:DescribeDataTransformInfo",
                "cls:DescribeDataTransformPreviewInfo",
                "cls:DescribeDataTransformProcessInfo",
                "cls:DeleteDataTransform",
                "cls:ModifyDataTransform"
            ],
            "resource": [
                "*"
            ]
        }
    ]
}
```

#### Viewing all data processing tasks

Users can view the data processing tasks of all log topics, which does not require DSL function authorization.

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
                "cls:DescribeDataTransformFailLogInfo",
                "cls:DescribeDataTransformInfo",
                "cls:DescribeDataTransformPreviewDataInfo",
                "cls:DescribeDataTransformPreviewInfo",
                "cls:DescribeDataTransformProcessInfo"
            ],
            "resource": [
                "*"
            ]
        }
    ]
}
```

## Access Policies for Data Shipping/Consumption

### Shipping to CKafka

#### Managing the CKafka shipping of all log topics

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
                "cls:modifyConsumer",
                "cls:getConsumer"
            ],
            "resource": "*"
        }
    ]
}
```

#### Managing the CKafka shipping of log topics with specific tags

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

#### Viewing the CKafka shipping of all log topics

Users can view the CKafka shipping of all log topics.

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

#### Viewing the CKafka shipping of log topics with specific tags

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

#### Managing the COS shipping of all log topics

Users can manage the COS shipping of all log topics.

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
                "cos:GetService"
            ],
            "resource": "*"
        }
    ]
}
```

#### Managing the COS shipping of log topics with specific tags

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
                "cos:GetService"
            ],
            "resource": "*"
        }
    ]
}
```

#### Viewing the COS shipping of all log topics

```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:DescribeTopics",
                "cls:DescribeLogsets" ],
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

#### Viewing the COS shipping of log topics with specific tags

```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:DescribeTopics",
                "cls:DescribeLogsets"],
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

#### Managing the SCF shipping of all log topics

Users can manage the SCF shipping of all log topics.

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

#### Managing the SCF shipping of log topics with specific tags

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

#### Viewing the SCF shipping of all log topics

Users can view the SCF shipping of all log topics.

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

#### Viewing the SCF shipping of log topics with specific tags

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

### Real-time consumption

#### Consuming all log topics in real time

Users can consume all log topics in real time.

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
                "cls:DescribeKafkaConsume",
                "cls:OpenKafkaConsume",
                "cls:GetDeliverFunction",
                "cam:ListAttachedRolePolicies"
            ],
            "resource": [
                "*"
            ]
        }
    ]
}
```

#### Consuming log topics with specific tags in real time

Users can manage the real-time consumption of log topics with specific tags.

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
                        "group&group3"
                    ]
                }
            }
        },
        {
            "effect": "allow",
            "action": [
                "cls:DescribeKafkaConsume",
                "cls:OpenKafkaConsume",
                "cls:GetDeliverFunction",
                "cam:ListAttachedRolePolicies"
            ],
            "resource": [
                "*"
            ]
        }
    ]
}
```

## Access Policies for Developers 

### CLS connection to Grafana

#### Displaying the data of all log topics via Grafana

```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:SearchLog"
            ],
            "resource": [
                "*"
            ]
        }
    ]
}
```

#### Displaying the data of log topics with specific tags via Grafana

```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:SearchLog"
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

