## 메타데이터 가속 개요

메타데이터 가속 기능은 Tencent Cloud COS(Cloud Object Storage) 서비스에서 제공하는 고성능 파일 시스템 기능입니다. 메타데이터 가속 기능의 기본 레이어는 클라우드 HDFS의 우수한 메타데이터 관리 기능을 사용하여, 사용자가 파일 시스템의 시맨틱을 통해 객체 스토리지 서비스에 액세스할 수 있도록 지원합니다. 시스템 설계 지표는 100GB/s 대역폭, 10만 규모 QPS, ms 단위 딜레이에 달합니다. 메타데이터 가속 기능이 활성화되면 버킷은 빅 데이터, 고성능 컴퓨팅, 머신러닝, AI와 같은 시나리오에서 널리 사용될 수 있습니다. 메타데이터 가속 기능에 대한 자세한 내용은 [메타데이터 가속 기능 개요](https://intl.cloud.tencent.com/document/product/436/43305)를 참고하십시오.

## HDFS 액세스의 장점

과거에는 COS 기반의 빅데이터 액세스가 주로 Hadoop-COS 툴을 통해 구현되었습니다. Hadoop-COS 도구는 내부적으로 HCFS API를 COS Restful API에 적용하여 COS의 데이터에 액세스합니다. COS와 파일 시스템 간의 메타데이터 구성의 차이로 인해 메타데이터 운영 성능이 달라지며, 이는 빅데이터 분석 성능에 영향을 미칩니다. 메타데이터 가속 기능이 활성화된 Bucket은 HCFS 프로토콜과 완벽하게 호환되며, 기본 HDFS API를 사용하여 직접 액세스할 수 있으므로 HDFS 프로토콜을 COS 프로토콜로 변환하는 오버헤드를 줄이고 효율적인 디렉터리 Rename(원자 작업), 파일 Atime, Mtime 업데이트, 효율적인 디렉터리 DU 통계, Posix ACL 권한 지원과 같은 기본 HDFS 기능을 제공합니다.

<span id="1"></span>

## 버킷 생성 및 HDFS 프로토콜 구성

1. [COS 버킷 생성](https://intl.cloud.tencent.com/document/product/436/13309)하고 이에 대한 메타데이터 가속을 활성화합니다.
버킷이 생성되면 버킷의 **파일 목록** 페이지로 이동하여 파일을 업로드 및 다운로드할 수 있습니다.
2. 왼쪽 사이드바에서 **성능 구성 > 메타데이터 가속**을 클릭하면 메타데이터 가속이 활성화된 것을 확인할 수 있습니다.
**메타데이터 가속을 활성화해야 하는** 버킷을 생성하는 경우 메시지에 따라 해당 **권한 부여** 작업을 수행해야 합니다. 인증을 클릭하면 HDFS 프로토콜이 자동으로 활성화되고 기본 버킷 마운트 대상 정보를 볼 수 있습니다.

>?시스템에서 해당 HDFS 파일 시스템을 찾을 수 없다고 표시하면 [티켓 제출](https://console.cloud.tencent.com/workorder/category) 하시기 바랍니다.
>
3. HDFS 권한 구성 열에서 **권한 구성 추가**를 클릭합니다.


4. VPC 이름 열에서 컴퓨팅 클러스터가 있는 VPC를 선택하고 노드 IP 열에서 열어야 하는 IP 주소 또는 범위를 입력하고 액세스 유형으로 편집 가능 또는 읽기 전용을 선택하고 **저장**을 클릭합니다.
>? **HDFS 권한 구성**은 기본 COS 권한 시스템과 다릅니다. HDFS를 사용하여 COS 버킷에 액세스하는 경우 기본 HDFS와 동일한 권한 환경을 얻기 위해 지정된 VPC의 머신이 COS 버킷에 액세스할 수 있는 권한을 부여하도록 HDFS 권한을 구성하는 것이 좋습니다. 

## COS에 액세스하도록 컴퓨팅 클러스터 구성

### 환경 종속

|     종속성         | chdfs-hadoop-plugin                               | COSN（hadoop-cos）                                | cos_api-bundle                                               |
| ------------ | ------------------------------------------------- | ------------------------------------------------- | ------------------------------------------------------------ |
| 버전     | ≥ v2.7                                         | ≥ v8.1.5                                       | 버전이 [tencentyun/hadoop-cos](https://github.com/tencentyun/hadoop-cos/releases)에 나열된 COSN 버전과 일치하는지 확인하십시오. |
| 다운로드 주소 | [Github](https://github.com/tencentyun/chdfs-hadoop-plugin)   | [Github](https://github.com/tencentyun/hadoop-cos/releases) | [Github](https://github.com/tencentyun/hadoop-cos/releases)            |

### EMR 환경

[EMR 환경](https://console.cloud.tencent.com/emr)은 이미 COS와 원활하게 통합되었으며 다음 단계만 완료하면 됩니다.

1. EMR 서버를 찾아 다음 명령을 실행하여 EMR 환경에 필요한 서비스 폴더의 패키지 버전이 환경 종속성에 대한 요구 사항을 충족하는지 확인합니다.
```plaintext
find / -name "chdfs*" 
find / -name "temrfs_hadoop*" 
```
![](https://qcloudimg.tencent-cloud.cn/raw/cb73bf879c1b7c0aa3304392c6845c2d.png)
![](https://qcloudimg.tencent-cloud.cn/raw/654573077995cb16701af9635d7db351.png)


검색 결과에 있는 두 jar 패키지의 버전이 위의 환경 종속성 요구 사항을 충족하는지 확인합니다.

2. chdfs-hadoop-plugin을 업데이트해야 하는 경우 다음 단계를 진행합니다.

   다음 위치에서 업데이트된 jar 패키지의 스크립트 파일을 다운로드합니다.

   - [update_cos_jar.sh](https://hadoop-jar-beijing-1259378398.cos.ap-beijing.myqcloud.com/hadoop_plugin_network/2.7/update_cos_jar.sh)
   - [update_cos_jar_common.sh](https://hadoop-jar-beijing-1259378398.cos.ap-beijing.myqcloud.com/hadoop_plugin_network/2.7/update_cos_jar_common.sh)

   다음 명령을 실행하여 서버의 /root 디렉터리에 두 개의 스크립트를 넣어 update_cos_jar.sh에 대한 실행 권한을 추가합니다.
```
sh update_cos_jar.sh  https://hadoop-jar-beijing-1259378398.cos.ap-beijing.myqcloud.com/hadoop_plugin_network/2.7  
```
매개변수를 해당 리전의 버킷으로 교체합니다(예시: 광저우 리전의 `https://hadoop-jar-guangzhou-1259378398.cos.ap-guangzhou.myqcloud.com/hadoop_plugin_network/2.7`).
모든 jar 패키지가 교체될 때까지 각 EMR 노드에서 위의 단계를 수행합니다.

3. hadoop-cos 패키지 또는 cos_api-bundle 패키지를 업데이트해야 하는 경우 다음 단계를 진행합니다.
 - /usr/local/service/hadoop/share/hadoop/common/lib/hadoop-temrfs-1.0.5.jar을 temrfs_hadoop_plugin_network-1.1.jar로 바꿉니다.
 - core-site.xml에 다음 구성 항목을 추가합니다.
    -  emr.temrfs.download.md5=822c4378e0366a5cc26c23c88b604b11
    -  emr.temrfs.download.version=2.7.5-8.1.5-1.0.6 (2.7.5를 hadoop 버전으로 바꾸고 8.1.5를 필요한 hadoop-cos 패키지 버전(8.1.5 이상이어야 함)으로 바꿉니다. cos_api-bundle 버전은 자동으로 조정됩니다)
    -  emr.temrfs.download.region=sh
    -  emr.temrfs.tmp.cache.dir=/data/emr/hdfs/tmp/temrfs 
 - core-site.xml에서 구성 항목 fs.cosn.impl=com.qcloud.emr.fs.TemrfsHadoopFileSystemAdapter를 수정합니다.

4. 새 구성 항목 `fs.cosn.bucket.region` 및 `fs.cosn.trsf.fs.ofs.bucket.region`을 추가하여 버킷이 상주하는 COS 리전(예시: `ap-shanghai`)을 지정하여 [EMR 콘솔](https://console.cloud.tencent.com/emr)에서 core-site.xml을 구성합니다.
>!버킷이 상주하는 COS 리전(예시: `ap-shanghai`)을 지정하려면 `fs.cosn.bucket.region` 및 `fs.cosn.trsf.fs.ofs.bucket.region`이 필요합니다.
>
5. Yarn, Hive, Presto 및 Impala와 같은 상주 서비스를 다시 시작합니다.


###  자체 구축된 Hadoop/CDH 환경

1. [CDH 설치](https://docs.cloudera.com/csp/2.0.1/deployment/topics/csp-install-cdh.html)에 설명된 자체 구축 환경에서는 환경 종속성에서 버전 요구 사항을 충족하는 3개의 jar 패키지를 다운로드해야 합니다.
2. Hadoop 클러스터에 있는 각 서버의 'classpath' 경로에 위의 세 가지 설치 패키지를 배치합니다. 예시: `/usr/local/service/hadoop/share/hadoop/common/lib/` (컴포넌트에 따라 다를 수 있음)
3. hadoop-env.sh 파일을 수정합니다. `$HADOOP_HOME/etc/hadoop` 디렉터리에 들어가 hadoop-env.sh 파일을 편집하고, 다음 내용을 추가하여 cosn 관련 jar 패키지를 Hadoop 환경 변수에 추가합니다.
   ```shell
   for f in $HADOOP_HOME/share/hadoop/tools/lib/*.jar; do
     if [ "$HADOOP_CLASSPATH" ]; then
       export HADOOP_CLASSPATH=$HADOOP_CLASSPATH:$f
     else
       export HADOOP_CLASSPATH=$f
     fi
   done
   ```
4. 컴퓨팅 클러스터의 `core-site.xml`에 다음 구성 항목을 추가합니다.

   ```xml
   <!--cosn의 구현 클래스-->
   <property>
           <name>fs.cosn.impl</name>
           <value>org.apache.hadoop.fs.CosFileSystem</value>
   </property>
   
   <!--ap-guangzhou 형식의 사용자 버킷 리전 정보-->    
   <property>
           <name>fs.cosn.bucket.region</name>
           <value>ap-guangzhou</value>
   </property>
   
   <!--ap-guangzhou 형식의 사용자 버킷 리전 정보-->    
   <property>
           <name>fs.cosn.trsf.fs.ofs.bucket.region</name>
           <value>ap-guangzhou</value>
   </property>
   
   <!-- SecretId 및 SecretKey를 얻는 방법 구성-->
   <property>
           <name>fs.cosn.credentials.provider</name>
           <value>org.apache.hadoop.fs.auth.SimpleCredentialProvider</value>
   </property>
   
   <!--계정에 대한 API Keys 정보입니다. [액세스 관리 콘솔](https://console.cloud.tencent.com/capi)에 로그인하면 Tencent Cloud API 키를 조회할 수 있습니다. -->
   <property>
           <name>fs.cosn.userinfo.secretId</name>
           <value>XXXXXXXXXXXXXXXXXXXXXXXX</value>
   </property>
   
   <!--계정에 대한 API Keys 정보입니다. [액세스 관리 콘솔](https://console.cloud.tencent.com/capi)에 로그인하면 Tencent Cloud API 키를 조회할 수 있습니다. -->
   <property>
           <name>fs.cosn.userinfo.secretKey</name>
           <value>XXXXXXXXXXXXXXXXXXXXXXXX</value>
   </property>
   
   <!-- 계정의 appid 구성-->
   <property>
           <name>fs.cosn.trsf.fs.ofs.user.appid</name>
           <value>125XXXXXX</value>
   </property>
   
   <!--실행 중 생성된 임시 파일을 저장하는 데 사용되는 로컬 임시 디렉터리-->     
   <property>
           <name>fs.cosn.trsf.fs.ofs.tmp.cache.dir</name>
           <value>/tmp</value>
   </property>
   ```

5. Yarn, Hive, Presto 및 Impala와 같은 상주 서비스를 다시 시작합니다.

### 환경 확인

모든 환경 구성 단계가 완료되면 다음과 같은 방법으로 환경을 확인할 수 있습니다.

- 클라이언트에서 Hadoop 명령줄을 사용하여 마운트가 성공했는지 확인합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/3dbfa5004cf6a3b9183fae20cfaa4e49.png)
- [COS 콘솔](https://console.cloud.tencent.com/cos)에 로그인하여 버킷 파일 목록의 파일과 디렉터리가 일치하는지 확인합니다.

## Ranger 권한 구성

기본적으로 기본 POSIX ACL 모드는 HDFS 프로토콜에 대한 인증에 채택됩니다. Ranger 인증을 사용해야 하는 경우 다음과 같이 구성합니다.

### EMR 환경

1. EMR 환경에 COSRanger 서비스가 통합되어 있어 EMR 클러스터 구매 시 선택하실 수 있습니다.
2. HDFS 프로토콜의 **HDFS 인증 모드**에서 **Ranger 인증 모드**를 선택하고 해당 Ranger 주소 정보를 설정합니다.
 - core-site.xml에 새 구성 항목 fs.cosn.credentials.provider를 추가하고 org.apache.hadoop.fs.auth.RangerCredentialsProvider로 설정합니다.
 - Ranger에 대해 궁금한 사항은 [COS Ranger 권한 시스템 솔루션](https://intl.cloud.tencent.com/document/product/436/39144)을 참고하십시오.

### 자체 구축된 Hadoop/CDH 환경

1. HDFS 프로토콜을 통해 COS에 액세스하도록 Ranger 서비스를 구성합니다. 자세한 내용은 [COS Ranger 권한 시스템 솔루션](https://intl.cloud.tencent.com/document/product/436/39144)을 참고하십시오.
2. HDFS 프로토콜의 **HDFS 인증 모드**에서 **Ranger 인증 모드**를 선택하고 해당 Ranger 주소 정보를 설정합니다.
 - core-site.xml에 새 구성 항목 fs.cosn.credentials.provider를 추가하고 org.apache.hadoop.fs.auth.RangerCredentialsProvider로 설정합니다.


## 기타

빅 데이터 시나리오에서는 다음 단계에서 HDFS 프로토콜을 통해 활성화된 메타데이터 가속을 사용하여 버킷에 액세스할 수 있습니다.

1. [버킷 생성 및 HDFS 프로토콜 구성](#1)의 설명에 따라 `core-stie.xml`에 HDFS 마운트 대상 정보를 설정합니다.
2. Hive, MR 및 Spark와 같은 컴포넌트가 있는 버킷에 액세스합니다. 자세한 내용은 [컴퓨팅 클러스터에 COS 버킷 마운트](https://intl.cloud.tencent.com/document/product/436/46199)를 참고하십시오.
3. 기본적으로 기본 `POSIX ACL` 모드가 인증에 채택됩니다. `Ranger 인증`을 사용해야 하는 경우 [COS Ranger 권한 시스템 솔루션](https://intl.cloud.tencent.com/document/product/436/39144)을 참고하십시오.

