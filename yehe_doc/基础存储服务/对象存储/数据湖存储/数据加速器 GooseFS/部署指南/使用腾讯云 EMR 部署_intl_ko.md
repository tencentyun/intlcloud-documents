현재 GooseFS는 Tencent Cloud EMR 환경으로 통합되었으며 EMR 최신 버전에 배포될 예정입니다. 사용자는 더 이상 Tencent Cloud EMR 환경을 단독 배포하지 않아도 되며, 기타 EMR 컴포넌트를 사용하는 것과 같이 바로 GooseFS를 사용할 수 있습니다.

아래 문장은 통합되지 않은 GooseFS의 Tencent Cloud EMR 기존 저장 클러스터에 대해 GooseFS의 EMR환경 설정을 배포하는 방법에 대해 소개합니다.

우선, [클러스터 모드 배포 실행](https://intl.cloud.tencent.com/document/product/436/41236#.E9.9B.86.E7.BE.A4.E6.A8.A1.E5.BC.8F.E9.83.A8.E7.BD.B2.E8.BF.90.E8.A1.8C)챕터의 내용을 참고하여 프로덕션 환경에 적합한 배포 아키텍처를 선택하고 클러스터를 배포합니다. 
다음으로, EMR이 컴포넌트를 설정하는 것을 지원하므로 본문은 Hadoop MapReduce, Spark, Flink의 GooseFS에 대한 지원으로 설명합니다. 

## Hadoop MapReduce 지원

Hadoop의 MapReduce 작업이 GooseFS의 데이터를 읽고 쓰게 하기 위해 hadoop-env.sh에서 GooseFS Client의 종속 경로를 HADOOP_CLASSPATH에 추가해야 합니다. 해당 작업은 EMR의 콘솔에서 할 수 있습니다. 예시: 

![](https://main.qcloudimg.com/raw/32b49a221b9a4106a96ab637c7a8a9ba.png)

동시에 core-site.xml에서 GooseFS의 HCFS 구현을 설정해야 하며, 해당 작업도 EMR 콘솔에서 할 수 있습니다. 

fs.AbstractFileSystem.gfs.impl의 설정은 아래와 같습니다. 
```
com.qcloud.cos.goosefs.hadoop.GooseFileSystem
```

![](https://main.qcloudimg.com/raw/1bd4bb9b7871a89b44185dbd88c3a8bc.png)

fs.gfs.impl의 설정은 아래와 같습니다. 
```
com.qcloud.cos.goosefs.hadoop.FileSystem
```

![](https://main.qcloudimg.com/raw/281b9a9021337b5b6fc5a70eb7033c59.png)


설정 전달 후 YARN 관련 컴포넌트를 재시작하면 바로 적용됩니다. 


## Spark 지원

Spark가 goosefs에 액세스하게 하기 위해 GooseFS의 client 종속 패키지를 spark의 executor classpath에 설정해야 하며 spark-defaults.conf에 지정해야 합니다. 

```conf
...
spark.driver.extraClassPath ${GOOSEFS_HOME}/client/goosefs-x.x.x-client.jar
spark.executor.extraClassPath ${GOOSEFS_HOME}/client/goosefs-x.x.x-client.jar
spark.hadoop.fs.gfs.impl com.qcloud.cos.goosefs.hadoop.FileSystem
spark.hadoop.fs.AbstractFileSystem.gfs.impl com.qcloud.cos.goosefs.hadoop.GooseFileSystem
...
```

해당 작업도 EMR 콘솔의 Spark 컴포넌트에서 설정과 전달을 할 수 있습니다. 

![](https://main.qcloudimg.com/raw/0f62582177918a965dd1d231af323830.png)

## Flink 지원

Tencent Cloud EMR의 Flink는 Flink on YARN의 배포 모드를 적용하였기에 원칙적으로 ${FLINK_HOME}/flink-conf.yaml에서 ‘fs.hdfs.hadoopconf’를 hadoop의 설정 경로에 정확하게 설정만 하면 됩니다. Tencent Cloud EMR 클러스터에서 `/usr/local/service/hadoop/etc/hadoop`이 일반적 입니다. 

기타 설정 항목을 설정하지 않고 바로 Flink on YARN의 방식으로 Flink 작업을 제출하면 됩니다. 작업 중 GooseFS의 액세스 경로는 `gfs://master:port/<path>`입니다. 


>! Flink가 GooseFS로 액세스할 경우 반드시 master 와 port를 지정해야 합니다. 
>

## Hive, Impala, HBase, Sqoop, Oozie를 지원합니다. 

Hadoop MapReduce의 환경 지원 설정 후 Hive, Impala, HBase 등 컴포넌트는 별도의 설정 지원 없이 정상 사용 가능합니다. 
  
