## COSBench 소개

COSBench는 Intel의 오픈 소스로서 COS의 부하 테스트 툴로 사용됩니다. Tencent Cloud Object Storage, COS)는 S3 프로토콜과 호환되는 COS 시스템으로서 COSBench를 사용해 읽기/쓰기 성능에 대한 부하 테스트를 실시할 수 있습니다.


## 시스템 환경

CentOS 7.0 이상에서 COSBench를 실행하는 것이 좋습니다. ubuntu에서 실행하면 예상치 못한 문제가 발생할 수 있습니다.


## 성능 영향 요인

- **CPU 코어**: 많은 수의 실행 중인 worker와 결합된 적은 수의 CPU 코어는 컨텍스트 전환에 높은 오버헤드를 유발할 가능성이 큽니다. 따라서 테스트에는 32개 또는 64개의 코어가 권장됩니다.
- **NIC**: 서버로부터의 아웃바운드 트래픽이 제한됩니다. 대용량 파일에 대한 트래픽을 테스트하려면 10GB 이상의 NIC가 권장됩니다.
- **네트워크 링크**: 공중망 링크는 품질이 다릅니다. 공중망을 통한 다운로드를 위한 공중망 다운스트림 트래픽에 대해 요금이 부과됩니다. 따라서 동일한 리전 내에서 액세스하기 위해서는 사설망을 권장합니다.
- **테스트 기간**: 신뢰할 수 있는 값을 얻으려면 더 긴 테스트 기간을 권장합니다.
- **테스트 환경**: 프로그램에서 실행 중인 JDK 버전도 핵심 성능 요소입니다. 예를 들어, 이전 JDK 버전을 사용하여 HTTPS에서 테스트할 때 암호화 알고리즘에 대한 [GCM BUG](https://bugs.openjdk.java.net/browse/JDK-8201633)와 난수 생성기의 잠금 문제가 발생할 수 있습니다.


## COSBench 실행 단계

1. [GitHub](https://github.com/intel-cloud/cosbench/releases/tag/v0.4.2.c4)에서 COSBench 0.4.2.c4.zip을 다운로드하고 서버에서 압축을 해제합니다.
2. COSBench의 종속 라이브러리를 설치한 뒤 다음 명령어를 실행합니다.
 - centos의 경우 다음 명령을 실행하여 종속성을 설치합니다:
```
sudo yum install nmap-ncat java curl java-1.8.0-openjdk-devel -y
```
 - ubuntu의 경우 다음 명령을 실행하여 종속성을 설치합니다.
```
sudo apt install nmap openjdk-8-jdk 
```
3. s3-config-sample.xml 파일을 편집하여 작업 설정 정보를 추가합니다. 작업 설정 시 다음 다섯 단계를 주로 포함합니다.
   1. init 단계: 버킷을 생성합니다.
   2. prepare 단계: worker 스레드, main단계에서 읽어오기 위해 PUT 업로드 시 객체 크기를 지정합니다.
   3. main 단계: worker 스레드, 읽기/쓰기 객체를 혼합하고, 실행 시간을 지정합니다.
   4. cleanup 단계: 생성된 객체를 삭제합니다.
   5. dispose 단계: 버킷을 삭제합니다.

 설정 예시는 다음과 같습니다.
```shell
<?xml version="1.0" encoding="UTF-8" ?>
<workload name="s3-50M-sample" description="sample benchmark for s3">

  <storage type="s3" config="accesskey=AKIDHZRLB9Ibhdp7Y7gyQq6BOk1997xxxxxx;secretkey=YaWIuQmCSZ5ZMniUM6hiaLxHnxxxxxx;endpoint=http://cos.ap-beijing.myqcloud.com" />

  <workflow>

    <workstage name="init">
      <work type="init" workers="10" config="cprefix=examplebucket;csuffix=-1250000000;containers=r(1,10)" />
    </workstage>

    <workstage name="prepare">
      <work type="prepare" workers="100" config="cprefix=examplebucket;csuffix=-1250000000;containers=r(1,10);objects=r(1,1000);sizes=c(50)MB" />
    </workstage>

    <workstage name="main">
      <work name="main" workers="100" runtime="300">
        <operation type="read" ratio="50" config="cprefix=examplebucket;csuffix=-1250000000;containers=u(1,10);objects=u(1,1000)" />
        <operation type="write" ratio="50" config="cprefix=examplebucket;csuffix=-1250000000;containers=u(1,10);objects=u(1000,2000);sizes=c(50)MB" />
      </work>
    </workstage>

    <workstage name="cleanup">
      <work type="cleanup" workers="10" config="cprefix=examplebucket;csuffix=-1250000000;containers=r(1,10);objects=r(1,2000)" />
    </workstage>

    <workstage name="dispose">
      <work type="dispose" workers="10" config="cprefix=examplebucket;csuffix=-1250000000;containers=r(1,10)" />
    </workstage>

  </workflow>

</workload>
```
**매개변수 설명**
<table>
<thead>
<tr><th>매개변수</th><th>설명</th></tr>
</thead>
<tbody>
<tr>
<td>accesskey, secretkey</td>
<td>키 정보. 리스크를 줄이기 위해 서브 계정 키를 사용하고 <a href="https://intl.cloud.tencent.com/document/product/436/32972">최소 권한의 원칙</a>을 따르는 것이 좋습니다. 서브 계정 키를 얻는 방법에 대한 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/598/32675">Access Key</a>를 참고하십시오.</td>
</tr>
<tr>
<td>cprefix</td>
<td>examplebucket과 같은 버킷 이름 접두사</td>
</tr>
<tr>
<td>containers</td>
<td>버킷 이름의 값 범위. 버킷 이름은 examplebucket1 또는 examplebucket2와 같은 cprefix와 containers로 구성됩니다</td>
</tr>
<tr>
<td>csuffix</td>
<td>APPID. APPID에는 -1250000000과 같이 <code>-</code> 접두사가 붙습니다</td>
</tr>
<tr>
<td>runtime</td>
<td>스트레스 테스트 기간</td>
</tr>
<tr>
<td>ratio</td>
<td>읽기 대 쓰기 비율</td>
</tr>
<tr>
<td>workers</td>
<td>스트레스 테스트 스레드 수</td>
</tr>
</tbody>
</table>
4. cosbench-start.sh 파일을 편집하여 Java에서 다음 매개변수로 행 추가를 실행하고, s3의 md5 인증 기능을 비활성화합니다.
```plaintext
-Dcom.amazonaws.services.s3.disableGetObjectMD5Validation=true
```
![](https://qcloudimg.tencent-cloud.cn/raw/ac010bb86f091d709a0776b4e20a5858.png)
5. cosbench 서비스를 시작합니다.
 - centos의 경우 다음 명령을 실행합니다.
```plaintext
sudo bash start-all.sh
```
 - ubuntu의 경우 다음 명령을 실행합니다.
```plaintext
sudo bash start-driver.sh &
sudo bash start-controller.sh &
```
6. 다음 명령어를 실행하여 작업을 제출합니다.
```plaintext
sudo bash cli.sh submit conf/s3-config-sample.xml
```
URL `http://ip:19088/controller/index.html`(ip는 사용자의 부하 테스트 기기 IP로 대체)에서 실행 상태를 조회합니다.
![](https://main.qcloudimg.com/raw/77f1631fa15141332d123fb472bab7ac.png)
이때 다음 이미지와 같이 다섯 단계로 실행되는 것을 확인할 수 있습니다.
![](https://main.qcloudimg.com/raw/3ccb5a60253ceb20c6da9292582c4355.png)
7. 다음은 소속 리전이 베이징이며, 32코어, 사설망 대역폭 17Gbps인 CVM에 대한 업로드 및 다운로드 성능 테스트 예시로, 두 단계를 포함하고 있습니다.
    1. prepare 단계: worker 스레드가 100개이며, 50MB 객체를 1000개 업로드합니다.
    2. main 단계: 100개의 worker 스레드가 300초 동안 읽기/쓰기 객체를 혼합합니다.

 위와 같은 두 단계의 성능 테스트 결과는 다음과 같습니다.
![](https://main.qcloudimg.com/raw/e3ac34b6f8340c5cbc834d4f98ba9341.png)
8. 다음 명령어를 실행하여 테스트 서비스를 중지합니다.
```plaintext
sudo bash stop-all.sh
```
