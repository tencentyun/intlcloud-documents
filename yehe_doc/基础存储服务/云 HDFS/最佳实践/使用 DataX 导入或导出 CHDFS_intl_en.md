## Environment Dependencies

- [CHDFS_JAR](https://github.com/tencentyun/chdfs-hadoop-plugin).
- DataX version: DataX 3.0

## Download and Installation

#### Getting CHDFS JAR

Download [CHDFS JAR](https://github.com/tencentyun/chdfs-hadoop-plugin).

#### Getting DataX package

Download [DataX](http://datax-opensource.oss-cn-hangzhou.aliyuncs.com/datax.tar.gz).

#### Installing CHDFS JAR

After downloading the CHDFS JAR, copy `chdfs_hadoop_plugin_network-1.7.jar` to the DataX decompression path `plugin/reader/hdfsreader/libs/` and `plugin/writer/hdfswriter/libs/`.

## Directions

### Configuring DataX

#### Modifying `datax.py` script

Open the `bin/datax.py` script in the DataX decompression directory and modify the `CLASS_PATH` variable in it as follows:

```plaintext
CLASS_PATH = ("%s/lib/*:%s/plugin/reader/hdfsreader/libs/*:%s/plugin/writer/hdfswriter/libs/*:.") % (DATAX_HOME, DATAX_HOME, DATAX_HOME)
```

#### Configuring `hdfsreader` and `hdfswriter` in JSON configuration file

Below is a JSON sample:

```json
{
	"job": {
		"setting": {
			"speed": {
				"byte": 10485760
			},
			"errorLimit": {
				"record": 0,
				"percentage": 0.02
			}
		},
		"content": [{
			"reader": {
				"name": "hdfsreader",
				"parameter": {
					"path": "testfile",
					"defaultFS": "ofs://f4xxxxxxxxx-hxT9.chdfs.ap-beijing.myqcloud.com/",
					"column": ["*"],
					"fileType": "text",
					"encoding": "UTF-8",
					"hadoopConfig": {
						"fs.AbstractFileSystem.ofs.impl": "com.qcloud.chdfs.fs.CHDFSDelegateFSAdapter",
						"fs.ofs.impl": "com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter",
						"fs.ofs.tmp.cache.dir": "/data/chdfs_tmp_cache",
						"fs.ofs.user.appid": "1250000000"
					},
					"fieldDelimiter": ","
				}
			},
			"writer": {
				"name": "hdfswriter",
				"parameter": {
					"path": "/user/hadoop/",
					"fileName": "testfile1",
					"defaultFS": "ofs://f4xxxxxxxxx-hxT9.chdfs.ap-beijing.myqcloud.com/",
					"column": [{
							"name": "col",
							"type": "string"
						},
						{
							"name": "col1",
							"type": "string"
						},
						{
							"name": "col2",
							"type": "string"
						}
					],
					"fileType": "text",
					"encoding": "UTF-8",
					"hadoopConfig": {
						"fs.AbstractFileSystem.ofs.impl": "com.qcloud.chdfs.fs.CHDFSDelegateFSAdapter",
						"fs.ofs.impl": "com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter",
						"fs.ofs.tmp.cache.dir": "/data/chdfs_tmp_cache",
						"fs.ofs.user.appid": "1250000000"
					},
					"fieldDelimiter": ":",
					"writeMode": "append"
				}
			}
		}]
	}
}
```

Here, configure `hadoopConfig` as the configuration required by the CHDFS instance and enter the path of the CHDFS instance as `defaultFS`, such as `ofs://f4xxxxxxxxx-hxT9.chdfs.ap-beijing.myqcloud.com/`. Other configuration items are the same as the HDFS configuration items.

### Performing data migration

Save the configuration file as `hdfs_job.json`, place it in the `job` directory, and run the following command:
```bash
bin/datax.py job/hdfs_job.json
```

You can see that the output is as follows:

```plaintext
2020-03-09 16:49:59.543 [job-0] INFO  JobContainer - 
         [total cpu info] => 
                averageCpu                     | maxDeltaCpu                    | minDeltaCpu                    
                -1.00%                         | -1.00%                         | -1.00%
                        

         [total gc info] => 
                 NAME                 | totalGCCount       | maxDeltaGCCount    | minDeltaGCCount    | totalGCTime        | maxDeltaGCTime     | minDeltaGCTime     
                 PS MarkSweep         | 1                  | 1                  | 1                  | 0.024s             | 0.024s             | 0.024s             
                 PS Scavenge          | 1                  | 1                  | 1                  | 0.014s             | 0.014s             | 0.014s             

2020-03-09 16:49:59.543 [job-0] INFO  JobContainer - PerfTrace not enable!
2020-03-09 16:49:59.543 [job-0] INFO  StandAloneJobContainerCommunicator - Total 2 records, 33 bytes | Speed 3B/s, 0 records/s | Error 0 records, 0 bytes |  All Task WaitWriterTime 0.000s |  All Task WaitReaderTime 0.033s | Percentage 100.00%
2020-03-09 16:49:59.544 [job-0] INFO  JobContainer - 
Task start time                    : 2020-03-09 16:49:48
Task end time                    : 2020-03-09 16:49:59
Total task duration                    :                 11s
Average task traffic                    :                3 B/s
Record write speed                    :              0 rec/s
Read records                    :                   2
Failed reads/writes                    :                   0
```


