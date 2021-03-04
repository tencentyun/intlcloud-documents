## 소개

Hadoop Distcp(Distributed copy)는 주로 Hadoop 파일 시스템 내부 또는 해당 시스템 간의 대규모 데이터 복사에 사용하는 툴이며, Map/Reduce를 기반으로 파일 배치, 오류 처리, 최종 보고서 생성을 실현합니다. Map/Reduce의 동시 처리 능력을 이용하고 모든 Map 작업이 원본 경로의 일부 파일에 대한 복사를 책임지고 완료해, 클러스터 리소스를 충분히 이용할 수 있어 클러스터 또는 Hadoop 파일 시스템 간의 대규모 데이터 마이그레이션을 신속하게 완료할 수 있습니다.

Hadoop-COS는 Hadoop 파일 프로그램의 시맨틱(semantics)을 구현해 Hadoop Distcp 툴을 이용하여 편리하게 COS와 기타 Hadoop 파일 시스템 간에 양방향 데이터 마이그레이션을 진행할 수 있습니다. 본 문서에서는 HDFS를 예시로 Hadoop 파일 시스템과 COS 간에 Hadoop Distcp 툴을 이용하여 데이터 마이그레이션을 진행하는 방법을 소개합니다.

## 전제 조건

1. Hadoop 클러스터에 [Hadoop-COS](https://intl.cloud.tencent.com/document/product/436/6884) 플러그 인이 설치되어 있어야 하며, COS 액세스 키 등이 정확하게 설정되어 있어야 합니다. 다음 Hadoop 명령어를 사용하여 COS의 액세스 정상 여부를 확인할 수 있습니다.
```shell
hadoop fs -ls cosn://examplebucket-1250000000/
```
COS Bucket의 파일 리스트를 정확하게 조회할 수 있는 경우 Hadoop-COS이 정상적으로 설치 및 설정되었다는 의미이며, 다음 실행 순서를 계속해서 진행할 수 있습니다.
2. COS의 액세스 계정은 COS 버킷의 타깃 경로에 대한 읽기 및 쓰기 권한을 보유하고 있어야 합니다.

## 실행 순서

### HDFS의 데이터를 COS 버킷으로 복사하기

Hadoop Distcp를 사용해 로컬 HDFS 클러스터의 `/test` 디렉터리 아래에 있는 파일을 COS의 hdfs-test-1250000000 버킷으로 마이그레이션 합니다.

![](https://main.qcloudimg.com/raw/e20dce07b83846362d02b3c6a1987558.jpg)

1. 다음 명령어를 사용하여 마이그레이션을 실행합니다.

```shell
hadoop distcp hdfs://10.0.0.3:9000/test cosn://hdfs-test-1250000000/
```

Hadoop Distcp는 MapReduce 작업을 실행하여 파일을 복사하며, 완료 후 다음 이미지와 같이 간단한 리포트 정보를 출력합니다.
![](https://main.qcloudimg.com/raw/39e84dcb98386f343ad81fcc48f78af1.jpg)

2. `hadoop fs -ls -R cosn://hdfs-test-1250000000/` 명령어를 실행하여 방금 버킷 hdfs-test-1250000000에 마이그레이션한 디렉터리와 파일을 조회할 수 있습니다.

![](https://main.qcloudimg.com/raw/ca34582214652ad77afe99322e6894fc.png)

### COS의 버킷에 있는 파일을 로컬 HDFS 클러스터로 복사하기

Hadoop Distcp는 서로 다른 클러스터와 파일 시스템 간에 데이터 복사를 제공하는 툴입니다. 따라서 COS 버킷에 있는 객체 경로를 원본 경로로 하고, HDFS 파일 경로를 타깃 경로로 하여 COS에 있는 데이터 파일을 로컬 HDFS로 복사할 수 있습니다.

```shell
hadoop distcp cosn://hdfs-test-1250000000/test hdfs://10.0.0.3:9000/
```

### Distcp 명령 라인 설정 매개변수를 지정하여 HDFS와 COS 간에 데이터 마이그레이션 진행

>해당 명령 라인 설정은 양방향 작업을 지원하며, HDFS 데이터를 COS에 마이그레이션하거나 COS 데이터를 HDFS에 마이그레이션할 수 있습니다.

사용자는 다음 명령어를 직접 설정할 수 있습니다.
```plaintext
hadoop distcp -Dfs.cosn.impl=org.apache.hadoop.fs.CosFileSystem -Dfs.cosn.bucket.region=ap-XXX  -Dfs.cosn.userinfo.secretId=AK**XXX  -Dfs.cosn.userinfo.secretKey=XXXX  -libjars /home/hadoop/hadoop-cos-2.6.5-shaded.jar  cosn://bucketname-appid/test/ hdfs:///test/
```

매개변수 설명은 다음과 같습니다.

- Dfs.cosn.impl: 항상 org.apache.hadoop.fs.CosFileSystem로 설정합니다.
- Dfs.cosn.bucket.region: 버킷의 소재 리전을 입력합니다. COS 콘솔의 버킷 리스트에서 확인할 수 있습니다.
- Dfs.cosn.userinfo.secretId: 버킷 소유자 계정의 SecretId를 입력합니다. [Tencent Cloud API 키](https://console.cloud.tencent.com/capi)에서 획득할 수 있습니다.
- Dfs.cosn.userinfo.secretKey: 버킷 소유자 계정의 secretKey를 입력합니다. [Tencent Cloud API 키](https://console.cloud.tencent.com/capi)에서 획득할 수 있습니다.
- libjars: Hadoop-COS jar 패키지 위치를 지정합니다. Hadoop-COS jar 패키지는 [Github 웨어하우스](https://github.com/tencentyun/hadoop-cos)의 dep 디렉터리에서 다운로드할 수 있습니다.

>기타 매개변수는 [Hadoop 툴](https://intl.cloud.tencent.com/document/product/436/6884) 문서를 참고하십시오.


## Hadoop distcp의 확장 매개변수

Hadoop distcp 툴은 다양한 실행 매개변수를 지원합니다. 예를 들어 `-m`으로 동시 복사에 사용하는 Map 작업 최대 수를 지정할 수 있으며, `-bandwidth`으로 모든 map에서 사용하는 최대 대역폭을 제한할 수 있습니다. 자세한 내용은 Apache Hadoop distcp 툴의 공식 홈페이지 문서 [DistCp Guide](https://hadoop.apache.org/docs/current/hadoop-distcp/DistCp.html)를 참조하십시오.


