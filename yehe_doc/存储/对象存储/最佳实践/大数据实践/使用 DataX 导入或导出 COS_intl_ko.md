## 환경 종속

- [HADOOP-COS](https://github.com/tencentyun/hadoop-cos/releases) 및 해당 버전의 [cos_api-bundle](https://github.com/tencentyun/hadoop-cos/releases).
- DataX 버전: DataX-3.0.

## 다운로드 및 설치

#### HADOOP-COS 다운로드

공식 Github에서 [HADOOP-COS](https://github.com/tencentyun/hadoop-cos/releases) 및 해당 버전의 [cos_api-bundle](https://github.com/tencentyun/hadoop-cos/releases)을 다운로드하십시오.

#### DataX 소프트웨어 패키지 다운로드

운영사 Github에서 [DataX](http://datax-opensource.oss-cn-hangzhou.aliyuncs.com/datax.tar.gz)를 다운로드하십시오. 

#### HADOOP-COS 설치

HADOOP-COS 다운로드 후 `hadoop-cos-2.x.x-${version}.jar` 및 `cos_api-bundle-${version}.jar`를 Datax 압축 해제 경로 `plugin/reader/hdfsreader/libs/` 및`plugin/writer/hdfswriter/libs/`에 복사하십시오.

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

설정은 다음 내용을 참조하십시오.
- hadoopConfig 설정은 cosn에서 필요한 설정입니다.
- defaultFS는 cosn 경로로 작성합니다. 예를 들어 `cosn://examplebucket-1250000000/`와 같이 쓸 수 있습니다.
- fs.cosn.userinfo.region을 버킷이 속한 리전(`ap-beijing` 등)으로 변경합니다. 자세한 내용은 [리전과 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오.
- COS_SECRETID와 COS_SECRETKEY를 COS 키로 변경합니다.

다른 항목은 hdfs 설정 항목과 동일하게 설정합니다.

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
