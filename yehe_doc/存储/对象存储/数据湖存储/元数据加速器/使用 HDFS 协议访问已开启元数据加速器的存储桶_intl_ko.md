## 메타데이터 가속 개요

메타데이터 가속 기능은 Tencent Cloud Cloud Object Storage(COS) 서비스에서 제공하는 고성능 파일 시스템 기능입니다. 메타데이터 가속 기능의 기본 레이어는 클라우드 HDFS의 우수한 메타데이터 관리 기능을 사용하여, 사용자가 파일 시스템의 시맨틱을 통해 객체 스토리지 서비스에 액세스할 수 있도록 지원합니다. 시스템 설계 지표는 2.4Gb/s 대역폭, 10만 규모 QPS, ms 단위 딜레이에 달합니다. 메타데이터 가속 기능이 활성화되면 버킷은 빅 데이터, 고성능 컴퓨팅, 머신러닝, AI와 같은 시나리오에서 널리 사용될 수 있습니다. 메타데이터 가속 기능에 대한 자세한 내용은 [메타데이터 가속 기능 개요](https://intl.cloud.tencent.com/document/product/436/43305)를 참고하십시오.

## HDFS 액세스의 장점

과거에는 COS 기반의 빅데이터 액세스가 주로 Hadoop-COS 툴을 통해 구현되었습니다. Hadoop-COS 도구는 내부적으로 HCFS API를 COS Restful API에 적용하여 COS의 데이터에 액세스합니다. COS와 파일 시스템 간의 메타데이터 구성의 차이로 인해 메타데이터 운영 성능이 달라지며, 이는 빅데이터 분석 성능에 영향을 미칩니다. 메타데이터 가속 기능이 활성화된 Bucket은 HCFS 프로토콜과 완벽하게 호환되며, 기본 HDFS API를 사용하여 직접 액세스할 수 있으므로 HDFS 프로토콜을 COS 프로토콜로 변환하는 오버헤드를 줄이고 효율적인 디렉터리 Rename(원자 작업), 파일 Atime, Mtime 업데이트, 효율적인 디렉터리 DU 통계, Posix ACL 권한 지원과 같은 기본 HDFS 기능을 제공합니다.

<span id="1"></span>
## 버킷 생성 및 HDFS 프로토콜 구성

1. COS 버킷을 생성하고 이에 대한 메타데이터 가속을 활성화합니다.

버킷이 생성되면 버킷의 **파일 목록** 페이지로 이동하여 파일을 업로드 및 다운로드할 수 있습니다.
2. 왼쪽 사이드바에서 **성능 구성 > 메타데이터 가속**을 클릭하면 메타데이터 가속이 활성화된 것을 확인할 수 있습니다.
**메타데이터 가속을 활성화해야 하는** 버킷을 생성하는 경우 메시지에 따라 해당 **권한 부여** 작업을 수행해야 합니다. 인증을 클릭하면 HDFS 프로토콜이 자동으로 활성화되고 기본 버킷 마운트 대상 정보를 볼 수 있습니다.
>?시스템에서 해당 HDFS 파일 시스템을 찾을 수 없다고 표시하면 [티켓 제출](https://console.cloud.tencent.com/workorder/category) 하시기 바랍니다.
>
3. HDFS 권한 구성 열에서 **권한 구성 추가**를 클릭합니다.

4. VPC 이름 열에서 컴퓨팅 클러스터가 있는 VPC를 선택하고 노드 IP 열에서 열어야 하는 IP 주소 또는 범위를 입력하고 액세스 유형으로 편집 가능 또는 읽기 전용을 선택하고 **저장**을 클릭합니다.
>? HDFS 권한 구성은 기본 COS 권한 시스템과 다릅니다. HDFS를 사용하여 COS 버킷에 액세스하는 경우 기본 HDFS와 동일한 권한 환경을 얻기 위해 지정된 VPC의 머신이 COS 버킷에 액세스할 수 있는 권한을 부여하도록 HDFS 권한을 구성하는 것이 좋습니다. 


## COS에 액세스하도록 컴퓨팅 클러스터 구성

### EMR 환경

EMR 환경은 이미 COS와 완벽하게 통합되었으며 다음 단계만 완료하면 됩니다.
1. EMR 서버를 찾아 다음 명령을 실행하여 EMR 환경에서 HDFS 클라이언트 패키지 버전을 확인합니다. 버전이 2.7 이상인지 확인하십시오.
```
find / -name "chdfs*"
```
검색 결과의 chdfs 패키지 버전이 2.7 이상인지 확인하십시오.
2. 클라이언트 패키지를 업데이트해야 하는 경우 다음 단계를 수행합니다.
 1. 다음 위치에서 업데이트된 jar 패키지의 스크립트 파일을 다운로드합니다.
    - [update_cos_jar.sh](https://hadoop-jar-beijing-1259378398.cos.ap-beijing.myqcloud.com/hadoop_plugin_network/2.7/update_cos_jar.sh)
    - [update_cos_jar_common.sh](https://hadoop-jar-beijing-1259378398.cos.ap-beijing.myqcloud.com/hadoop_plugin_network/2.7/update_cos_jar_common.sh)
 2. 다음 명령을 실행하여 서버의 /root 디렉터리에 두 개의 스크립트를 넣어 update_cos_jar.sh에 대한 실행 권한을 추가합니다.
```
sh update_cos_jar.sh  https://hadoop-jar-beijing-1259378398.cos.ap-beijing.myqcloud.com/hadoop_plugin_network/2.7  
```
매개변수를 해당 리전의 버킷으로 교체합니다(예시: 광저우 리전의 `https://hadoop-jar-guangzhou-1259378398.cos.ap-guangzhou.myqcloud.com/hadoop_plugin_network/2.7`).
모든 jar 패키지가 교체될 때까지 각 EMR 노드에서 위의 단계를 수행합니다.
3. 새 구성 항목 `fs.ofs.bucket.region`을 추가하여 EMR 콘솔에서 core-site.xml을 구성합니다. 버킷이 상주하는 COS 리전(예시: `ap-shanghai`)을 지정합니다.
>!`fs.ofs.bucket.region` 매개변수는 필수입니다. 버킷이 있는 COS 리전(예시: `ap-shanghai`)을 지정합니다.
>
4. Yarn, Hive, Presto 및 Impala와 같은 상주 서비스를 다시 시작합니다.


### 자체 구축된 Hadoop/CDH 환경
1. HDFS 프로토콜을 통한 액세스를 위해 [클라이언트 설치 패키지](https://github.com/tencentyun/chdfs-hadoop-plugin/tree/master/jar) 2.7 이상 버전을 다운로드합니다.
2. Hadoop 클러스터에 있는 각 서버의 'classpath' 경로에 설치 패키지를 배치합니다. 예시: `/usr/local/service/hadoop/share/hadoop/common/lib/` (컴포넌트에 따라 다를 수 있음)
2. [CHDFS 마운트](https://intl.cloud.tencent.com/document/product/1106/41965)에 설명된 대로 컴퓨팅 클러스터에서 `core-site.xml`을 구성합니다.
3. Yarn, Hive, Presto 및 Impala와 같은 상주 서비스를 다시 시작합니다.

>!`fs.ofs.bucket.region` 매개변수는 필수입니다. 버킷이 있는 COS 리전(예시: `ap-shanghai`)을 지정합니다.
>

### 환경 확인

모든 환경 구성 단계가 완료되면 다음과 같은 방법으로 환경을 확인할 수 있습니다.
- 클라이언트에서 Hadoop 명령줄을 사용하여 마운트가 성공했는지 확인합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/90264cdfe35753b95d48db5ab6675629.png)
- [COS 콘솔](https://console.cloud.tencent.com/cos)에 로그인하여 버킷 파일 목록의 파일과 디렉터리가 일치하는지 확인합니다.


## Ranger 권한 구성

기본적으로 기본 POSIX ACL 모드는 HDFS 프로토콜에 대한 인증에 채택됩니다. Ranger 인증을 사용해야 하는 경우 다음과 같이 구성합니다.

### EMR 환경

1. EMR 환경에 COSRanger 서비스가 통합되어 있어 EMR 클러스터 구매 시 선택하실 수 있습니다.
2. HDFS 프로토콜의 HDFS 인증 모드에서 Ranger 인증 모드를 선택하고 해당 Ranger 주소 정보를 설정합니다.
 - CHDFS의 경우 core-site.xml에 새 구성 항목 fs.ofs.ranger.enable.flag를 추가하고 true로 설정합니다.
 - COSN의 경우 새 구성 항목 fs.cosn.credentials.provider를 추가하고 org.apache.hadoop.fs.auth.RangerCredentialsProvider로 설정합니다.
 - Ranger에 대해 궁금한 사항은 [CHDFS FAQ](https://intl.cloud.tencent.com/document/product/1106/41958)를 참고하십시오.

### 자체 구축된 Hadoop/CDH 환경

1. HDFS 프로토콜을 통해 COS에 액세스하도록 Ranger 서비스를 구성합니다. 자세한 내용은 [CHDFS Ranger 권한 시스템 솔루션](https://intl.cloud.tencent.com/document/product/1106/41973)을 참고하십시오.
2. HDFS 프로토콜의 HDFS 인증 모드에서 Ranger 인증 모드를 선택하고 해당 Ranger 주소 정보를 설정합니다.
 - CHDFS의 경우 core-site.xml에 새 구성 항목 fs.ofs.ranger.enable.flag를 추가하고 true로 설정합니다.
 - COSN의 경우 새 구성 항목 fs.cosn.credentials.provider를 추가하고 org.apache.hadoop.fs.auth.RangerCredentialsProvider로 설정합니다.
 - Ranger에 대해 궁금한 사항은 [CHDFS FAQ](https://intl.cloud.tencent.com/document/product/1106/41958)를 참고하십시오.

## 기타

빅 데이터 시나리오에서는 다음 단계에서 HDFS 프로토콜을 통해 활성화된 메타데이터 가속을 사용하여 버킷에 액세스할 수 있습니다.

1. [버킷 생성 및 HDFS 프로토콜 구성](#1)의 설명에 따라 `core-stie.xml`에 HDFS 마운트 대상 정보를 설정합니다.
2. Hive, MR 및 Spark와 같은 컴포넌트가 있는 버킷에 액세스합니다. 자세한 내용은 [컴퓨팅 클러스터에 COS 버킷 마운트](https://intl.cloud.tencent.com/document/product/436/46199)를 참고하십시오.
3. 기본적으로 기본 `POSIX ACL` 모드가 인증에 채택됩니다. `Ranger 인증`을 사용해야 하는 경우 [CHDFS Ranger 권한 시스템 솔루션](https://intl.cloud.tencent.com/document/product/1106/41973)을 참고하십시오.



