DataX is an open-source CLI that supports importing full or incremental data from TencentDB to CDWPG. The tool is developed in Java and uses JDBC to connect the source database to the target database. It can run on Windows and Linux. Install the Java environment before use.

**DataX installation:**
1. Download the source code [here](https://github.com/HashDataInc/DataX) and compile it.
2. Directly use [datax-v1.0.4-hashdata.tar.gz](https://www.tencentcloud.com/document/product/1138/45015), an already compiled version.

The following section introduces [DataX](https://github.com/HashDataInc/DataX) modified by HashData, which is more efficient to import data to CDWPG. Tests show that it can import more than 100,000 entries per second. The following is the configuration file to import data from MySQL to CDWPG:
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
                        "username": "****", 
                        "password": "****", 
                        "column": [
                            "*"
                        ], 
                        "splitPk": "id", 
                        "connection": [
                            {
                                "table": [
                                    "test1"
                                ], 
                                "jdbcUrl": [
                                    "jdbc:mysql://***:***/db1?serverTimezone=Asia/Shanghai"
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
                        "preSql": [
                            "truncate table test1"
                        ], 
                        "postSql": [
                            "select count(*) from test2"
                        ], 
                        "segment_reject_limit": 0, 
                        "copy_queue_size": 2000, 
                        "num_copy_processor": 1, 
                        "num_copy_writer": 1, 
                        "connection": [
                            {
                                "jdbcUrl": "jdbc:postgresql://****:**/db1", 
                                "table": [
                                    "test1"
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

**Parameter description:**
1. The `writer` should be `gpdbwriter`. `postgresqlwriter` can also be used to write data to CDWPG, with a poor insertion efficiency though.
2. For specific meanings and parameter tuning, see [DataX](https://github.com/HashDataInc/DataX).
3. We recommend you add the `serverTimezone=Asia/Shanghai` parameter to the JDBC URL of `mysqlreader` to avoid data inconsistency caused by time zone issues.


