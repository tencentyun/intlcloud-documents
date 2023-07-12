## 준비 작업

1. Tencent Cloud 공식 홈페이지에 CHDFS 파일 시스템 및 CHDFS 마운트 포인트를 생성하고，권한 정보를 설정합니다. 
2. Tencent Cloud VPC 환경의 CVM으로 생성 완료된 CHDFS에 액세스합니다. 자세한 내용은[CHDFS 생성](https://intl.cloud.tencent.com/document/product/1106/41961)을 참고하십시오. 
3. 마운트 완료 후, hadoop 명령행 툴을 열고 다음 명령어를 실행하여 CHDFS 기능이 정상 작동되는지 확인합니다. 
```bash
hadoop fs -ls ofs://f4xxxxxxxxxxxxxxx.chdfs.ap-beijing.myqcloud.com/
```
다음과 같은 내용이 출력된다면, 클라우드 HDFS 기능이 정상임을 의미합니다. 
![](https://main.qcloudimg.com/raw/3be9476976dd7da027ea6e634652c00b.png)

## 마이그레이션 

준비 작업이 완료되면 hadoop 커뮤니티 표준의 Distcp 툴로 전체 또는 증분 HDFS 데이터를 마이그레이션할 수 있습니다. 자세한 내용은 [Distcp 공식 홈페이지 가이드 문서](https://hadoop.apache.org/docs/r1.0.4/cn/distcp.html)를 참고하십시오. 

#### 주의사항

hadoop distcp 툴에서 제공하는 일부 매개변수는 CHDFS와 호환되지 않습니다. 다음 테이블의 일부 매개변수를 지정할 경우 적용되지 않습니다. 

| 매개변수| 설명                                        | 상태 |
| -------- | ----------------------------------------------- | -------- |
| -p[rbax] | r：replication，b：block-size，a：ACL，x：XATTR | 적용 안됨   |

#### 사례 소개

1. CHDFS 준비가 완료되면 다음 hadoop 명령어를 실행하여 데이터 마이그레이션를 진행합니다. 
```bash
hadoop distcp hdfs://10.0.1.11:4007/testcp ofs://f4xxxxxxxx-xxxx.chdfs.ap-beijing.myqcloud.com/
```
`f4xxxxxxxx-xxxx.chdfs.ap-beijing.myqcloud.com`은 마운트 포인트 도메인이며 실제 신청한 마운트 포인트 정보에 맞게 변경해야 합니다. 
2. Hadoop 명령어 실행이 완료되면 다음과 같이 로그에 마이그레이션 상세 정보가 출력됩니다. 
```plaintext
2019-12-31 10:59:31 [INFO ] [main:13300] [org.apache.hadoop.mapreduce.Job:] [Job.java:1385]
 Counters: 38
    File System Counters
        FILE: Number of bytes read=0
        FILE: Number of bytes written=387932
        FILE: Number of read operations=0
        FILE: Number of large read operations=0
        FILE: Number of write operations=0
        HDFS: Number of bytes read=1380
        HDFS: Number of bytes written=74
        HDFS: Number of read operations=21
        HDFS: Number of large read operations=0
        HDFS: Number of write operations=6
        OFS: Number of bytes read=0
        OFS: Number of bytes written=0
        OFS: Number of read operations=0
        OFS: Number of large read operations=0
        OFS: Number of write operations=0
    Job Counters
        Launched map tasks=3
        Other local map tasks=3
        Total time spent by all maps in occupied slots (ms)=419904
        Total time spent by all reduces in occupied slots (ms)=0
        Total time spent by all map tasks (ms)=6561
        Total vcore-milliseconds taken by all map tasks=6561
        Total megabyte-milliseconds taken by all map tasks=6718464
    Map-Reduce Framework
        Map input records=3
        Map output records=2
        Input split bytes=408
        Spilled Records=0
        Failed Shuffles=0
        Merged Map outputs=0
        GC time elapsed (ms)=179
        CPU time spent (ms)=4830
        Physical memory (bytes) snapshot=1051619328
        Virtual memory (bytes) snapshot=12525191168
        Total committed heap usage (bytes)=1383071744
    File Input Format Counters
        Bytes Read=972
File Output Format Counters
        Bytes Written=74
    org.apache.hadoop.tools.mapred.CopyMapper$Counter
        BYTESSKIPPED=5
        COPY=1
        SKIP=2
```

