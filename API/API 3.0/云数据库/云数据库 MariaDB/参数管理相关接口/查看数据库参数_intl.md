## 1. API Description

Domain name for API request: mariadb.tencentcloudapi.com

This API (DescribeDBParameters) is used to obtain the current parameter settings of the database.

Default request rate limit: 20/sec.

Note: This API supports Finance regions. Finance and non-Finance regions are isolated from each other. Therefore, if the common parameter Region is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region specified in the Region field, for example: mariadb.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/237/16147).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: DescribeDBParameters. |
| Version | Yes | String | Common parameter. The value used for this API: 2017-03-12. |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/237/16147#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceId | Yes | String | Instance ID, such as tdsql-ow728lmc. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| InstanceId | String | Instance ID, such as tdsql-ow728lmc. |
| Params | Array of [ParamDesc](/document/api/237/16191#ParamDesc) | Requests the current parameter values of the DB |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Obtain the current parameters of the database

#### Input example

```
https://mariadb.tencentcloudapi.com/?Action=DescribeDBParameters
&InstanceId=tdsql-ige1a5k3
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "InstanceId": "tdsql-ige1a5k3",
    "Params": [
      {
        "Constraint": {
          "Range": {
            "Max": "65535",
            "Min": "1"
          },
          "Type": "section"
        },
        "Default": "1",
        "Param": "auto_increment_increment",
        "SetValue": "",
        "Value": "1"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "65535",
            "Min": "1"
          },
          "Type": "section"
        },
        "Default": "1",
        "Param": "auto_increment_offset",
        "SetValue": "",
        "Value": "1"
      },
      {
        "Constraint": {
          "Enum": "ON,OFF",
          "Type": "enum"
        },
        "Default": "ON",
        "Param": "autocommit",
        "SetValue": "",
        "Value": "ON"
      },
      {
        "Constraint": {
          "Enum": "ROW,STATEMENT,MIXED",
          "Type": "enum"
        },
        "Default": "ROW",
        "Param": "binlog_format",
        "SetValue": "",
        "Value": "ROW"
      },
      {
        "Constraint": {
          "Enum": "utf8,latin1,gbk,utf8mb4",
          "Type": "enum"
        },
        "Default": "utf8",
        "Param": "character_set_server",
        "SetValue": "",
        "Value": "utf8"
      },
      {
        "Constraint": {
          "Enum": "latin1_general_cs,latin1_general_ci,latin1_bin,latin1_swedish_ci,gbk_chinese_ci,gbk_bin,utf8_general_ci,utf8_bin,utf8_unicode_ci,utf8mb4_general_ci,utf8mb4_bin,utf8mb4_unicode_ci",
          "Type": "enum"
        },
        "Default": "",
        "Param": "collation_server",
        "SetValue": "",
        "Value": "utf8_general_ci"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "3600",
            "Min": "1"
          },
          "Type": "section"
        },
        "Default": "10",
        "Param": "connect_timeout",
        "SetValue": "",
        "Value": "10"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "7",
            "Min": "0"
          },
          "Type": "section"
        },
        "Default": "0",
        "Param": "default_week_format",
        "SetValue": "",
        "Value": "0"
      },
      {
        "Constraint": {
          "Enum": "ON,OFF,ALL",
          "Type": "enum"
        },
        "Default": "ON",
        "Param": "delay_key_write",
        "SetValue": "",
        "Value": "ON"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "4294967295",
            "Min": "1"
          },
          "Type": "section"
        },
        "Default": "100",
        "Param": "delayed_insert_limit",
        "SetValue": "",
        "Value": "100"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "3600",
            "Min": "1"
          },
          "Type": "section"
        },
        "Default": "300",
        "Param": "delayed_insert_timeout",
        "SetValue": "",
        "Value": "300"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "4294967295",
            "Min": "1"
          },
          "Type": "section"
        },
        "Default": "1000",
        "Param": "delayed_queue_size",
        "SetValue": "",
        "Value": "1000"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "30",
            "Min": "0"
          },
          "Type": "section"
        },
        "Default": "4",
        "Param": "div_precision_increment",
        "SetValue": "",
        "Value": "4"
      },
      {
        "Constraint": {
          "Enum": "ON,OFF",
          "Type": "enum"
        },
        "Default": "OFF",
        "Param": "event_scheduler",
        "SetValue": "",
        "Value": "OFF"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "18446744073709547520",
            "Min": "4"
          },
          "Type": "section"
        },
        "Default": "1024",
        "Param": "group_concat_max_len",
        "SetValue": "",
        "Value": "1024"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "10000",
            "Min": "100"
          },
          "Type": "section"
        },
        "Default": "5000",
        "Param": "innodb_concurrency_tickets",
        "SetValue": "",
        "Value": "5000"
      },
      {
        "Constraint": {
          "Enum": "OFF,ON",
          "Type": "enum"
        },
        "Default": "OFF",
        "Param": "innodb_large_prefix",
        "SetValue": "",
        "Value": "ON"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "1073741824",
            "Min": "1"
          },
          "Type": "section"
        },
        "Default": "50",
        "Param": "innodb_lock_wait_timeout",
        "SetValue": "",
        "Value": "20"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "90",
            "Min": "10"
          },
          "Type": "section"
        },
        "Default": "10",
        "Param": "innodb_max_dirty_pages_pct",
        "SetValue": "",
        "Value": "70.000000"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "95",
            "Min": "5"
          },
          "Type": "section"
        },
        "Default": "37",
        "Param": "innodb_old_blocks_pct",
        "SetValue": "",
        "Value": "37"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "1000",
            "Min": "0"
          },
          "Type": "section"
        },
        "Default": "1000",
        "Param": "innodb_old_blocks_time",
        "SetValue": "",
        "Value": "1000"
      },
      {
        "Constraint": {
          "Enum": "4096,8192,16384,32768,65536",
          "Type": "enum"
        },
        "Default": "4096",
        "Param": "innodb_page_size",
        "SetValue": "",
        "Value": "16384"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "1024",
            "Min": "1"
          },
          "Type": "section"
        },
        "Default": "300",
        "Param": "innodb_purge_batch_size",
        "SetValue": "",
        "Value": "1000"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "64",
            "Min": "0"
          },
          "Type": "section"
        },
        "Default": "56",
        "Param": "innodb_read_ahead_threshold",
        "SetValue": "",
        "Value": "56"
      },
      {
        "Constraint": {
          "Enum": "nulls_equal,nulls_unequal,nulls_ignored",
          "Type": "enum"
        },
        "Default": "nulls_equal",
        "Param": "innodb_stats_method",
        "SetValue": "",
        "Value": "nulls_equal"
      },
      {
        "Constraint": {
          "Enum": "ON,OFF",
          "Type": "enum"
        },
        "Default": "OFF",
        "Param": "innodb_stats_on_metadata",
        "SetValue": "",
        "Value": "OFF"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "4294967296",
            "Min": "1"
          },
          "Type": "section"
        },
        "Default": "8",
        "Param": "innodb_stats_sample_pages",
        "SetValue": "",
        "Value": "8"
      },
      {
        "Constraint": {
          "Enum": "ON,OFF",
          "Type": "enum"
        },
        "Default": "OFF",
        "Param": "innodb_strict_mode",
        "SetValue": "",
        "Value": "OFF"
      },
      {
        "Constraint": {
          "Enum": "ON,OFF",
          "Type": "enum"
        },
        "Default": "ON",
        "Param": "innodb_table_locks",
        "SetValue": "",
        "Value": "ON"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "128",
            "Min": "0"
          },
          "Type": "section"
        },
        "Default": "0",
        "Param": "innodb_thread_concurrency",
        "SetValue": "",
        "Value": "64"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "3600000",
            "Min": "1"
          },
          "Type": "section"
        },
        "Default": "10000",
        "Param": "innodb_thread_sleep_delay",
        "SetValue": "",
        "Value": "0"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "86400",
            "Min": "10"
          },
          "Type": "section"
        },
        "Default": "28800",
        "Param": "interactive_timeout",
        "SetValue": "",
        "Value": "28800"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "18446744073709547520",
            "Min": "128"
          },
          "Type": "section"
        },
        "Default": "262144",
        "Param": "join_buffer_size",
        "SetValue": "",
        "Value": "2097152"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "4294967295",
            "Min": "100"
          },
          "Type": "section"
        },
        "Default": "300",
        "Param": "key_cache_age_threshold",
        "SetValue": "",
        "Value": "300"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "16384",
            "Min": "512"
          },
          "Type": "section"
        },
        "Default": "1024",
        "Param": "key_cache_block_size",
        "SetValue": "",
        "Value": "1024"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "100",
            "Min": "1"
          },
          "Type": "section"
        },
        "Default": "100",
        "Param": "key_cache_division_limit",
        "SetValue": "",
        "Value": "100"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "31536000",
            "Min": "1"
          },
          "Type": "section"
        },
        "Default": "5",
        "Param": "lock_wait_timeout",
        "SetValue": "",
        "Value": "5"
      },
      {
        "Constraint": {
          "Enum": "ON,OFF",
          "Type": "enum"
        },
        "Default": "OFF",
        "Param": "log_queries_not_using_indexes",
        "SetValue": "",
        "Value": "OFF"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "10",
            "Min": "0.05"
          },
          "Type": "section"
        },
        "Default": "1.000000",
        "Param": "long_query_time",
        "SetValue": "",
        "Value": "1.000000"
      },
      {
        "Constraint": {
          "Enum": "OFF,ON",
          "Type": "enum"
        },
        "Default": "OFF",
        "Param": "low_priority_updates",
        "SetValue": "",
        "Value": "OFF"
      },
      {
        "Constraint": {
          "Enum": "0,1",
          "Type": "enum"
        },
        "Default": "1",
        "Param": "lower_case_table_names",
        "SetValue": "",
        "Value": "0"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "1073741824",
            "Min": "16384"
          },
          "Type": "section"
        },
        "Default": "134217728",
        "Param": "max_allowed_packet",
        "SetValue": "",
        "Value": "1073741824"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "4096",
            "Min": "1"
          },
          "Type": "section"
        },
        "Default": "2000",
        "Param": "max_connect_errors",
        "SetValue": "",
        "Value": "2000"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "32768",
            "Min": "1"
          },
          "Type": "section"
        },
        "Default": "4096",
        "Param": "max_connections",
        "SetValue": "",
        "Value": "10000"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "1048576",
            "Min": "0"
          },
          "Type": "section"
        },
        "Default": "16382",
        "Param": "max_prepared_stmt_count",
        "SetValue": "",
        "Value": "200000"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "16777216",
            "Min": "262144"
          },
          "Type": "section"
        },
        "Default": "4194304",
        "Param": "myisam_sort_buffer_size",
        "SetValue": "",
        "Value": "4194304"
      },
      {
        "Constraint": {
          "Enum": "4096,8192,16384,32768,65536,1048576",
          "Type": "enum"
        },
        "Default": "16384",
        "Param": "net_buffer_length",
        "SetValue": "",
        "Value": "16384"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "3153600",
            "Min": "1"
          },
          "Type": "section"
        },
        "Default": "30",
        "Param": "net_read_timeout",
        "SetValue": "",
        "Value": "30"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "4294967295",
            "Min": "1"
          },
          "Type": "section"
        },
        "Default": "10",
        "Param": "net_retry_count",
        "SetValue": "",
        "Value": "10"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "3153600",
            "Min": "1"
          },
          "Type": "section"
        },
        "Default": "60",
        "Param": "net_write_timeout",
        "SetValue": "",
        "Value": "60"
      },
      {
        "Constraint": {
          "Type": "string"
        },
        "Default": "index_merge=on,index_merge_union=on,index_merge_sort_union=on,index_merge_intersection=on,optimize_join_buffer_size=on",
        "Param": "optimizer_switch",
        "SetValue": "",
        "Value": "batched_key_access=off,block_nested_loop=on,condition_fanout_filter=on,derived_merge=on,duplicateweedout=on,engine_condition_pushdown=on,firstmatch=on,index_condition_pushdown=on,index_merge=on,index_merge_intersection=on,index_merge_sort_union=on,index_merge_union=on,loosescan=on,materialization=on,mrr=on,mrr_cost_based=on,semijoin=on,subquery_materialization_cost_based=on,use_index_extensions=on"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "16384",
            "Min": "1024"
          },
          "Type": "section"
        },
        "Default": "8192",
        "Param": "query_alloc_block_size",
        "SetValue": "",
        "Value": "16384"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "1048576",
            "Min": "1"
          },
          "Type": "section"
        },
        "Default": "1048576",
        "Param": "query_cache_limit",
        "SetValue": "",
        "Value": "1048576"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "104857600",
            "Min": "0"
          },
          "Type": "section"
        },
        "Default": "0",
        "Param": "query_cache_size",
        "SetValue": "",
        "Value": "0"
      },
      {
        "Constraint": {
          "Enum": "OFF,ON,DEMAND",
          "Type": "enum"
        },
        "Default": "OFF",
        "Param": "query_cache_type",
        "SetValue": "",
        "Value": "OFF"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "1048576",
            "Min": "8192"
          },
          "Type": "section"
        },
        "Default": "8192",
        "Param": "query_prealloc_size",
        "SetValue": "",
        "Value": "24576"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "16383",
            "Min": "0"
          },
          "Type": "section"
        },
        "Default": "10",
        "Param": "slave_parallel_threads",
        "SetValue": "",
        "Value": ""
      },
      {
        "Constraint": {
          "Range": {
            "Max": "1024",
            "Min": "1"
          },
          "Type": "section"
        },
        "Default": "2",
        "Param": "slow_launch_time",
        "SetValue": "",
        "Value": "2"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "1073741824",
            "Min": "32768"
          },
          "Type": "section"
        },
        "Default": "2097152",
        "Param": "sort_buffer_size",
        "SetValue": "",
        "Value": "2097152"
      },
      {
        "Constraint": {
          "Type": "string"
        },
        "Default": "",
        "Param": "sql_mode",
        "SetValue": "",
        "Value": "NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "100",
            "Min": "10"
          },
          "Type": "section"
        },
        "Default": "10",
        "Param": "sqlasyntimeout",
        "SetValue": "",
        "Value": "30"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "2048",
            "Min": "400"
          },
          "Type": "section"
        },
        "Default": "400",
        "Param": "table_definition_cache",
        "SetValue": "",
        "Value": "400"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "524288",
            "Min": "400"
          },
          "Type": "section"
        },
        "Default": "1024",
        "Param": "table_open_cache",
        "SetValue": "",
        "Value": "10240"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "65536",
            "Min": "1"
          },
          "Type": "section"
        },
        "Default": "3",
        "Param": "thread_pool_oversubscribe",
        "SetValue": "",
        "Value": "30"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "67108864",
            "Min": "262144"
          },
          "Type": "section"
        },
        "Default": "33554432",
        "Param": "tmp_table_size",
        "SetValue": "",
        "Value": "33554432"
      },
      {
        "Constraint": {
          "Enum": "REPEATABLE-READ,SERIALIZABLE,READ-COMMITTED,READ-UNCOMMITTED",
          "Type": "enum"
        },
        "Default": "REPEATABLE-READ",
        "Param": "tx_isolation",
        "SetValue": "",
        "Value": "REPEATABLE-READ"
      },
      {
        "Constraint": {
          "Range": {
            "Max": "259200",
            "Min": "60"
          },
          "Type": "section"
        },
        "Default": "28800",
        "Param": "wait_timeout",
        "SetValue": "",
        "Value": "28800"
      }
    ],
    "RequestId": "914db412-d6e6-47ad-8e62-d06e02e52a56"
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick indexing of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=mariadb&Version=2017-03-12&Action=DescribeDBParameters)

### SDK

Cloud API 3.0 comes with the software development kit (SDK) that supports multiple programming languages and makes it easier to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### Command line tools

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following only lists the error codes related to the API business logic. For other error codes, see [Common Error Codes](/document/api/237/16149#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError.CamAuthFailed | CAM authentication request failed |
| InternalError.DbOperationFailed | Failed to query the database |
| InternalError.GetDbConfigFailed | Failed to obtain instance parameters in the database |
| InvalidParameter.GenericParameterError | Failed to pass the parameter validity verification |
| ResourceUnavailable.InstanceAlreadyDeleted | The database instance has been deleted |
| ResourceUnavailable.InstanceStatusAbnormal | The database instance is in an invalid status and cannot be operated |
| UnauthorizedOperation.PermissionDenied | No permission to perform operations on the API or resource |

