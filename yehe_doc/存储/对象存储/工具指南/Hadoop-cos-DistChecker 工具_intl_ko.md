## 기능 설명

Hadoop-cos-DistChecker는 마이그레이션 디렉터리의 완전성을 검증하는 툴입니다. 사용자는 `hadoop distcp` 명령어를 사용하여 HDFS에서 COS로 데이터를 마이그레이션한 후, MapReduce의 동시 실행 능력을 기반으로 Hadoop-cos-DistChecker 툴에서 신속하게 **원본 디렉터리**와 **타깃 디렉터리**에 대해 검증 비교합니다.

## 사용 환경

- Hadoop-cos v5.8.2 이상이 요구되며, 자세한 내용은 [hadoop-cos release](https://github.com/tencentyun/hadoop-cos/releases)를 참조하십시오.
- Hadooop MapReduce 실행 환경

>
> - 자체구축한 Hadoop 클러스터인 경우, Hadoop-cos는 최신 버전(GitHub release 버전 5.8.2 이상)을 선택하여 종속되어야만 CRC64 검증 코드를 획득할 수 있습니다.
> - Tencent Cloud ERM 세트를 사용하는 경우 2020년 5월 8일 이후 생성한 클러스터에만 Hadoop-cos 버전이 포함되어 있습니다. 해당 날짜 이전에 생성한 클러스터는 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 처리해야 합니다.

## 사용 설명

Hadoop-cos-distchecker는 Hadoop-cos(CosN 파일 시스템) 문서의 CRC64 검증 값을 획득해야 하므로, 툴 실행 전 fs.cosn.crc64.checksum.enabled 옵션 값을 true로 설정하여 Hadoop-cos 파일의 CRC64 검사합을 획득하고, 툴 실행 완료 후 다시 해당 옵션 값을 false로 변경해 CRC64 검사합 획득을 비활성화해야 합니다.

>Hadoop-COS에서 지원하는 CRC64 검사합과 HDFS 파일 시스템의 CRC32C 검사합은 호환되지 않습니다. 따라서 해당 툴 사용 완료 후 반드시 상기 설정 항목을 비활성화 상태로 복구해야 하며, 그렇지 않을 경우 Hadoop-cos에서 일부 파일 시스템 getFileChecksum 인터페이스 호출 시 실행에 실패할 수 있습니다.

### 매개변수 개념

- **원본 파일 리스트**
  원본 파일 경로 리스트는 사용자가 다음 명령어를 실행해 출력하는 검사할 서브 디렉터리 및 파일 리스트입니다.

```plaintext
hadoop fs -ls -R hdfs://host:port/{source_dir} | awk '{print $8}' > check_list.txt
```

형식 예시는 다음과 같습니다.

```plaintext
/benchmarks/TestDFSIO
/benchmarks/TestDFSIO/io_control
/benchmarks/TestDFSIO/io_control/in_file_test_io_0
/benchmarks/TestDFSIO/io_control/in_file_test_io_1
/benchmarks/TestDFSIO/io_data
/benchmarks/TestDFSIO/io_data/test_io_0
/benchmarks/TestDFSIO/io_data/test_io_1
/benchmarks/TestDFSIO/io_write
/benchmarks/TestDFSIO/io_write/_SUCCESS
/benchmarks/TestDFSIO/io_write/part-00000
```

- **원본 디렉터리**: 원본 파일 리스트가 존재하는 디렉터리를 의미하며, 해당 디렉터리는 일반적으로 `distcp` 명령어를 사용한 데이터 마이그레이션 시 원본 경로로 사용됩니다. `hdfs://host:port/source_dir`를 원본 디렉터리로 한 예시는 다음과 같습니다.

```plaintext
hadoop distcp hdfs://host:port/source_dir cosn://examplebucket-appid/dest_dir
```

또한 해당 경로는 **원본 파일 경로 리스트** 상의 공용 상위 디렉터리이기도 하며, 예를 들어 상기 원본 파일 리스트의 공용 상위 디렉터리는 `/benchmarks`입니다.

- **타깃 디렉터리**: 비교할 타깃 디렉터리입니다.

### 명령 라인 형식

Hadoop-cos-DistChecker는 일종의 MapReduce 작업 프로그램으로, MapReduce 작업에 따라 프로세스를 제출하면 됩니다.

```plaintext
hadoop jar hadoop-cos-distchecker-2.8.5-1.0-SNAPSHOT.jar com.qcloud.cos.hadoop.distchecker.App <원본 파일 리스트의 절대 경로> <원본 디렉터리의 절대 경로 표시> <타깃 디렉터리의 절대 경로 표시> [optional parameters]
```

> Optional parameters는 Hadoop의 옵션 매개변수를 의미합니다.

### 사용 방법

다음과 같이 ` hdfs://10.0.0.3:9000/benchmarks`와 `cosn://hdfs-test-1250000000/benchmarks`의 검증 방법을 예시로 하여 툴 사용 방법을 소개합니다.

먼저 다음 명령어를 실행합니다.

```plaintext
hadoop fs -ls -R hdfs://10.0.0.3:9000/benchmarks | awk '{print $8}' > check_list.txt
```

![](https://main.qcloudimg.com/raw/a2a853be2646b6558983303de805c04e.png)
검사할 원본 경로를 check_list.txt 파일에 내보냅니다. 해당 파일에는 다음과 같이 원본 파일 경로 리스트가 저장됩니다.
![](https://main.qcloudimg.com/raw/216d90b20d383e233e50f497e83c24c3.png)

그리고, 다음을 실행하여 check_list.txt를 HDFS에 넣습니다.

```plaintext
hadoop fs -put check_list.txt hdfs://10.0.0.3:9000/
```

![](https://main.qcloudimg.com/raw/e5b79519dfeac808b64f29e04c35e9a4.png)

마지막으로, Hadoop-cos-DistChecker를 실행해 `hdfs://10.0.0.3:9000/benchmarks`와 `cosn://hdfs-test-1250000000/benchmarks`를 비교한 후, 출력 결과를 `cosn://hdfs-test-1250000000/check_result` 경로에 저장합니다. 명령어 형식은 다음과 같습니다.

```shell
hadoop jar hadoop-cos-distchecker-2.8.5-1.0-SNAPSHOT.jar com.qcloud.cos.hadoop.distchecker.App hdfs://10.0.0.3:9000/check_list.txt hdfs://10.0.0.3:9000/benchmarks cosn://hdfs-test-1250000000/benchmarks cosn://hdfs-test-1250000000/check_result
```

![](https://main.qcloudimg.com/raw/8356bebae88dae96aaecf03ea202df0d.png)

Hadoop-cos-DistChecker에서 원본 파일 리스트와 원본 디렉터리를 읽어 MapReduce 작업을 실행하고 분산형 검사를 진행한 후, 마지막에 검사 보고서를 `cosn://examplebucket-appid/check_result` 경로에 출력합니다.

![](https://main.qcloudimg.com/raw/b49000f8613e41a659df31c19bdab2fa.png)

검사 보고서는 다음과 같습니다.

```plaintext
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO       hdfs://10.0.0.3:9000/benchmarks/TestDFSIO,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO,None,None,None,SUCCESS,'The source file and the target file are the same.'
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_control    hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_control,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO/io_control,None,None,None,SUCCESS,'The source file and the target file are the same.'
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_control/in_file_test_io_0  hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_control/in_file_test_io_0,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO/io_control/in_file_test_io_0,CRC64,1566310986176587838,1566310986176587838,SUCCESS,'The source file and the target file are the same.'
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_control/in_file_test_io_1  hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_control/in_file_test_io_1,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO/io_control/in_file_test_io_1,CRC64,-6584441696534676125,-6584441696534676125,SUCCESS,'The source file and the target file are the same.'
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_data       hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_data,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO/io_data,None,None,None,SUCCESS,'The source file and the target file are the same.'
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_data/test_io_0     hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_data/test_io_0,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO/io_data/test_io_0,CRC64,3534425600523290380,3534425600523290380,SUCCESS,'The source file and the target file are the same.'
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_data/test_io_1     hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_data/test_io_1,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO/io_data/test_io_1,CRC64,3534425600523290380,3534425600523290380,SUCCESS,'The source file and the target file are the same.'
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_write      hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_write,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO/io_write,None,None,None,SUCCESS,'The source file and the target file are the same.'
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_write/_SUCCESS     hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_write/_SUCCESS,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO/io_write/_SUCCESS,CRC64,0,0,SUCCESS,'The source file and the target file are the same.'
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_write/part-00000   hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_write/part-00000,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO/io_write/part-00000,CRC64,-4804567387993776854,-4804567387993776854,SUCCESS,'The source file and the target file are the same.'
```



## 검사 보고서 형식

검사 보고서는 다음 형식으로 출력됩니다.

```plaintext
check_list.txt의 원본 파일 경로, 원본 파일 절대 경로, 타깃 파일 절대 경로, Checksum 알고리즘, 원본 파일의 checksum 값, 타깃 파일의 checksum 값, 검사 결과, 검사 결과 설명
```

여기에서, 검사 결과는 다음 7가지로 나뉩니다.

- SUCCESS: 원본 파일과 타깃 파일이 모두 존재하며 모두 일치함.
- MISMATCH: 원본 파일과 타깃 파일이 모두 존재하지만 일치하지 않음.
- UNCONFIRM: 원본 파일과 타깃 파일의 일치 여부를 확인할 수 없음. 해당 상태는 주로 COS 상의 파일이 CRC64 검증 코드 특성 런칭 전 존재했던 파일이기 때문에 CRC64 검증 값을 획득하지 못하기 때문입니다.
- UNCHECKED: 미검사. 해당 상태는 원본 파일을 읽을 수 없거나 checksum 값을 계산할 수 없기 때문입니다.
- SOURCE_FILE_MISSING: 원본 파일이 존재하지 않음.
- TARGET_FILE_MISSING: 타깃 파일이 존재하지 않음.
- TARGET_FILESYSTEM_ERROR: 타깃 파일 시스템이 CosN 파일 시스템이 아님.



## FAQ

#### 검사 보고서의 CRC64 값이 음수로 표시되는 이유는 무엇입니까?

CRC64 값은 20자리로 표시될 수 있습니다. 이 때 Java long 타입의 표시 범위를 초과하게 되지만 기본 바이트는 일치하므로 long 타입으로 출력 시 음수로 표시되는 것입니다.

