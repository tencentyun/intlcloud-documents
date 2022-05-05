
## 메타데이터 가속 개요

메타데이터 가속 기능은 Tencent Cloud Cloud Object Storage(COS) 서비스에서 제공하는 고성능 파일 시스템 기능입니다. 메타데이터 가속 기능의 기본 레이어는 클라우드 HDFS의 우수한 메타데이터 관리 기능을 사용하여, 사용자가 파일 시스템의 시맨틱을 통해 객체 스토리지 서비스에 액세스할 수 있도록 지원합니다. 시스템 설계 지표는 2.4Gb/s 대역폭, 10만 규모 QPS, ms 단위 딜레이에 달합니다. 메타데이터 가속 기능이 활성화되면 버킷은 빅 데이터, 고성능 컴퓨팅, 머신러닝, AI와 같은 시나리오에서 널리 사용될 수 있습니다. 메타데이터 가속 기능에 대한 자세한 내용은 [메타데이터 가속 기능 개요](https://intl.cloud.tencent.com/document/product/436/43305)를 참고하십시오.

## HDFS 액세스의 장점

과거 COS 기반의 빅데이터 접근은 주로 Hadoop-COS 툴 기반으로 구현되었습니다. Hadoop-COS 도구는 내부적으로 HCFS API를 COS Restful API로 조정하여 COS의 데이터에 액세스합니다. COS와 파일 시스템 간의 메타데이터 구성의 차이는 메타데이터 운영 성능의 차이로 이어져 빅데이터 분석 성능에 영향을 미칩니다. 메타데이터 가속 기능이 활성화된 Bucket은 HCFS 프로토콜과 완벽하게 호환되며, 기본 HDFS API를 사용하여 직접 액세스할 수 있으므로 HDFS 프로토콜을 COS 프로토콜로 변환하는 오버헤드를 줄이고 효율적인 디렉터리 Rename(원자 작업), 파일 Atime, Mtime 업데이트, 효율적인 디렉터리 DU 통계, Posix ACL 권한 지원과 같은 기본 HDFS 기능을 제공합니다.


## 준비 작업

1. COS 버킷을 생성하고 이에 대한 메타데이터 가속을 활성화합니다.

2. Bucket이 생성되면 버킷의 **파일 리스트** 페이지로 이동합니다. 콘솔에서 파일을 업로드하거나 다운로드할 수 있습니다.

3. 왼쪽 사이드바에서 **성능 구성 > 메타데이터 가속 기능**을 선택하면 메타데이터 가속이 활성화된 것을 볼 수 있습니다. **메타데이터 가속이 필요한** 버킷을 처음 생성하는 경우 지침에 따라 해당 권한 부여 작업을 수행합니다. 권한 부여를 클릭하면 기본적으로 HDFS 액세스가 활성화되며 기본 Bucket 마운트 포인트의 정보를 볼 수 있습니다.

>?시스템에서 해당 HDFS 파일 시스템을 찾을 수 없다고 표시하면 [티켓 제출](https://console.cloud.tencent.com/workorder/category) 하시기 바랍니다.
>
4. HDFS 액세스가 활성화된 후 VPC 액세스 권한을 구성해야 합니다. HDFS 권한 구성 탭 페이지에서 권한 구성 추가 버튼을 클릭합니다. VPC 이름 열에서 컴퓨팅 클러스터가 있는 VPC의 주소를 선택합니다. 노드 IP 열에 VPC IP 범위에서 열려는 IP 또는 IP 범위를 입력합니다. 액세스 유형을 읽기/쓰기 또는 읽기 전용으로 설정합니다. 그런 다음 저장을 클릭합니다.

>? HDFS 권한 구성은 기본 COS 권한 시스템과 다릅니다. HDFS를 사용하여 COS 버킷에 액세스하는 경우 기본 HDFS와 동일한 권한 환경을 얻기 위해 지정된 VPC의 머신이 COS 버킷에 액세스할 수 있는 권한을 부여하도록 HDFS 권한을 구성하는 것이 좋습니다. 
5. 기본적으로 HDFS 프로토콜은 기본 POSIX ACL 모드를 인증에 사용합니다. Ranger 인증을 사용하려면 HDFS 인증 모드에서 Ranger 인증 모드를 선택하고 Ranger 주소를 구성할 수 있습니다.

>?Ranger 서비스를 구성하고 Ranger 서비스를 사용하여 HDFS를 통해 COS에 액세스하는 방법은 [HDFSranger 인증](https://intl.cloud.tencent.com/document/product/1106/41973)을 참고하십시오.
>
6. 환경을 생성한 후 컴퓨팅 클러스터에 대한 `core-site.xml`을 구성해야 합니다. 자세한 내용은 [HDFS 프로토콜 설정](https://intl.cloud.tencent.com/document/product/1106/41965)을 참고하십시오. Tencent Cloud EMR을 사용하는 경우 추가 구성 없이 기본 EMR 구성을 직접 사용할 수 있습니다.
>!`fs.ofs.bucket.region` 매개변수는 필수입니다. 버킷이 있는 COS 리전(예시: `ap-shanghai`)을 지정합니다.
>
7. HDFS 액세스를 위한 [클라이언트 설치 패키지](https://github.com/tencentyun/chdfs-hadoop-plugin/tree/master/jar)를 다운로드합니다. 설치 패키지가 버전 2.7 이상인지 확인하십시오. 다운로드한 설치 패키지를 Hadoop 클러스터의 각 서버에서 올바른 `classpath` 경로(예시 경로: `/usr/local/service/hadoop/share/hadoop/common/lib/`, 경로는 구성 요소에 따라 다름)에 배치합니다. 그런 다음 `Yarn`, `Hive`, `Presto` 및 `Impala`와 같은 상주 서비스를 다시 시작합니다.
8. 환경 구성이 완료되면 HDFS 파일 시스템이 Hadoop 명령줄 인터페이스(CLI)에서 성공적으로 마운트되었는지 확인할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/90264cdfe35753b95d48db5ab6675629.png)
9. [COS 콘솔](https://console.cloud.tencent.com/cos)에 로그인하여 버킷 파일 리스트의 파일이 디렉터리에 있는지 확인할 수 있습니다.


## HDFS를 통해 COS에 액세스

빅 데이터 시나리오에서 다음 단계를 수행하여 HDFS를 사용하여 메타데이터 가속이 활성화된 버킷에 액세스할 수 있습니다.

1. `core-stie.xml`에서 준비 작업과 같이 HDFS 관련 마운트 포인트 정보를 설정합니다.
2. Hive, MR 및 Spark와 같은 구성 요소를 사용하여 버킷에 액세스합니다. 자세한 내용은 [Mounting a COS Bucket in a Computing Cluster](https://intl.cloud.tencent.com/document/product/436/46199)를 참고하십시오.
3. 기본적으로 기본 `POSIX ACL` 모드가 인증에 채택됩니다. `Ranger1 인증`을 사용해야 하는 경우 [Accessing COS over HDFS in CDH Cluster](https://intl.cloud.tencent.com/document/product/436/46200)를 참고하십시오.


