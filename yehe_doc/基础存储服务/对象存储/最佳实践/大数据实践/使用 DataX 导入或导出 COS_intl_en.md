## Environmental Dependencies

- [HADOOP-COS](https://github.com/tencentyun/hadoop-cos/releases) and the corresponding [cos_api-bundle](https://github.com/tencentyun/hadoop-cos/releases).
- DataX version: DataX 3.0

## Download and Installation

#### Downloading HADOOP-COS

Download [HADOOP-COS](https://github.com/tencentyun/hadoop-cos/releases) and the corresponding [cos_api-bundle](https://github.com/tencentyun/hadoop-cos/releases) on Github.

#### Downloading DataX package

Download [DataX](http://datax-opensource.oss-cn-hangzhou.aliyuncs.com/datax.tar.gz) on Github.

#### Installing HADOOP-COS

After HADOOP-COS is downloaded, copy `hadoop-cos-2.x.x-${version}.jar` and `cos_api-bundle-${version}.jar` to the Datax decompression paths `plugin/reader/hdfsreader/libs/` and `plugin/writer/hdfswriter/libs/`.

## How to Use

### DataX configuration

#### Modifying datax.py script

Open the `bin/datax.py` script in the DataX decompression directory, and modify the CLASS_PATH variable in the script as follows:

```plaintext
CLASS_PATH = ("%s/lib/*:%s/plugin/reader/hdfsreader/libs/*:%s/plugin/writer/hdfswriter/libs/*:.") % (DATAX_HOME, DATAX_HOME, DATAX_HOME)
```

#### Configuring `hdfsreader` and `hdfswriter` in JSON configuration file

A sample JSON file is as shown below:
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
					"defaultFS": "cosn://examplebucket-1250000000/",
					"column": ["*"],
					"fileType": "text",
					"encoding": "UTF-8",
					"hadoopConfig": {
						"fs.cosn.impl": "org.apache.hadoop.fs.CosFileSystem",
						"fs.cosn.userinfo.region": "ap-beijing",
						"fs.cosn.tmp.dir": "/tmp/hadoop_cos",
						"fs.cosn.userinfo.secretId": "COS_SECRETID",
						"fs.cosn.userinfo.secretKey": "COS_SECRETKEY"
					},
					"fieldDelimiter": ","
				}
			},
			"writer": {
				"name": "hdfswriter",
				"parameter": {
					"path": "/user/hadoop/",
					"fileName": "testfile1",
					"defaultFS": "cosn://examplebucket-1250000000/",
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
						"fs.cosn.impl": "org.apache.hadoop.fs.CosFileSystem",
						"fs.cosn.userinfo.region": "ap-beijing",
						"fs.cosn.tmp.dir": "/tmp/hadoop_cos",
						"fs.cosn.userinfo.secretId": "COS_SECRETID",
						"fs.cosn.userinfo.secretKey": "COS_SECRETKEY"
					},
					"fieldDelimiter": ":",
					"writeMode": "append"
				}
			}
		}]
	}
}
```

Notes:
- Configure `hadoopConfig` as required for cosn.
- Use `defaultFS` to specify the cosn path, e.g. `cosn://examplebucket-1250000000/`.
- In `fs.cosn.userinfo.region`, enter the region where your bucket resides, such as `ap-beijing`. For more information, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224).
- For `COS_SECRETID` and `COS_SECRETKEY`, use your own COS key information.

The other fields can be the same as those for hdfs.

### Migrating data

Save the configuration file as `hdfs_job.json` in the `job` directory by running

```bash
bin/datax.py job/hdfs_job.json
```

The resulting output is as shown below:

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
Job start time                    : 2020-03-09 16:49:48
Job end time                    : 2020-03-09 16:49:48
Job duration                    :                 11s
Average job traffic                    :                3B/s
Recorded write speed                    :              0rec/s
Recorded read count                    :                   2
Read/Write failure count                    :                   0
```
