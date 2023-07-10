## 환경 종속

- [CHDFS_JAR](https://github.com/tencentyun/chdfs-hadoop-plugin).
- DataX 버전: DataX-3.0.

## 다운로드 및 설치

#### CHDFS JAR 다운로드

운영사 Github에서 [CHDFS_JAR](https://github.com/tencentyun/chdfs-hadoop-plugin)을 다운로드하십시오.

#### DataX 소프트웨어 패키지 다운로드

운영사 Github에서 [DataX](http://datax-opensource.oss-cn-hangzhou.aliyuncs.com/datax.tar.gz)를 다운로드하십시오. 

#### CHDFS JAR 설치

CHDFS JAR을 다운로드한 후，`chdfs_hadoop_plugin_network-1.7.jar`을 Datax 압축 해제 경로`plugin/reader/hdfsreader/libs/` 및 `plugin/writer/hdfswriter/libs/`로 복사하십시오.

## 사용 방법

### DataX 설정

#### datax.py 스크립트 수정

DataX의 압축 해제 디렉터리에 속한 bin/datax.py 스크립트를 열어 스크립트의 CLASS_PATH 변수를 아래와 같이 수정하십시오.

```plaintext
CLASS_PATH = ("%s/lib/*:%s/plugin/reader/hdfsreader/libs/*:%s/plugin/writer/hdfswriter/libs/*:.") % (DATAX_HOME, DATAX_HOME, DATAX_HOME)
```

#### JSON 설정 파일에 hdfsreader 및 hdfswriter 설정

JSON 파일 예시는 아래와 같습니다.

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

hadoopConfig 설정은 CHDFS에 필요한 설정으로，defaultFS는 CHDFS 경로로 작성합니다. 예를 들어 `ofs://f4xxxxxxxxx-hxT9.chdfs.ap-beijing.myqcloud.com/`과 같이 쓸 수 있으며 기타 설정은 hdfs 설정과 같게 작성하면 됩니다. 

### 데이터 마이그레이션 실행

구성 파일 이름을 hdfs_job.json으로 설정하고 job 디렉터리에 저장해 아래와 같이 명령 라인을 실행합니다.
```bash
bin/datax.py job/hdfs_job.json
```

스크린에서 보이는 정상적인 결과 출력은 아래와 같습니다.

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
작업 활성화 시간                    : 2020-03-09 16:49:48
작업 종료 시간                    : 2020-03-09 16:49:59
작업 총 소요 시간                    :                 11s
작업 평균 트래픽                    :                3B/s
기록 입력 속도                    :              0rec/s
읽은 기록 총 횟수                    :                   2
읽기/쓰기 실패 총 횟수                     :                   0
```


