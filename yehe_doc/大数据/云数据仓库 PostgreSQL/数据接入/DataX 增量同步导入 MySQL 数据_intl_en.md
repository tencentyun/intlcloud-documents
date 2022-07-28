This document describes how to use [DataX](https://github.com/HashDataInc/DataX) modified by HashData to incrementally sync data from MySQL to CDWPG.

Follow the steps below to use DataX to incrementally sync data from MySQL to CDWPG:
1. Read the `MaxTime` since the last successful sync from the local file (for the initial sync, you can specify an initial time value as required by your business).
2. Use `MaxTime` as the `LastTime` (lower limit of the incremental sync) and `CurTime` as the upper limit.
3. Modify the `datax.json` configuration to specify the time interval (`WHERE` clause in SQL) of the synced table as `[LastTime, CurTime)`.
4. Execute DataX sync. After successful sync, write `CurTime` to the local file for the next sync.
5. Repeat steps 1–4 for multiple incremental syncs.

A sample `datax.json` configuration file is as shown below:
```
{
    "job": {
        "setting": {
            "speed": {
                "channel": 3, 
                "byte": 1048576, 
                "record": 1000
            }, 
            "errorLimit": {
                "record": 2, 
                "percentage": 0.02
            }
        }, 
        "content": [
            {
                "reader": {
                    "name": "mysqlreader", 
                    "parameter": {
                        "username": "******", 
                        "password": "******", 
                        "connection": [
                            {
                                "jdbcUrl": [
                                    "jdbc:mysql://***:***/test?serverTimezone=Asia/Shanghai"
                                ],
                                "querySql": [
                                    "select * from cdw_test_table where updateTime >= '${lastTime}' and updateTime < '${currentTime}'"
                                ]
                            }
                        ]
                    }
                }, 
                "writer": {
                    "name": "gpdbwriter", 
                    "parameter": {
                        "username": "******", 
                        "password": "******", 
                        "column": [
                                 "*"
                        ],
                        "segment_reject_limit": 0, 
                        "copy_queue_size": 2000, 
                        "num_copy_processor": 1, 
                        "num_copy_writer": 1, 
                        "connection": [
                            {
                                "jdbcUrl": "jdbc:postgresql://***:***/***", 
                                "table": [
                                    "ods_cdw_test_table"
                                ]
                            }
                        ]
                    }
                }
            }
        ]
    }
}
```

