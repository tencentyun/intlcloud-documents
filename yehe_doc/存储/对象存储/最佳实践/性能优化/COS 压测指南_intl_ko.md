## COSBench 소개

COSBench는 Intel의 오픈 소스로서 COS의 부하 테스트 툴로 사용됩니다. Tencent Cloud COS는 S3 프로토콜과 호환하는 COS 시스템으로서 COSBench를 사용해 읽기/쓰기 성능에 대한 부하 테스트를 실시할 수 있습니다.


## 시스템 환경

CentOS 7.0 및 이후 버전에서 툴을 실행할 것을 권장하며 ubuntu 환경에서는 예상 밖의 문제가 발생할 수 있습니다.


## 성능 영향 요인

- **기기의 코어 수**: 기기의 코어 수가 적고 활성화한 worker의 수가 많으면, 콘텍스트 전환 시 과도한 오버헤드가 발생하기 쉽습니다. 32나 64코어를 채택하여 부하 테스트를 실시하는 것을 권장합니다.
- **기기 ENI**: 기기에서 발생하는 트래픽은 ENI의 영향을 받습니다. 대용량 파일의 트래픽 부하 테스트 시에는 10기가비트 이상의 ENI 사용을 권장합니다.
- **네트워크 링크 요청**: 외부 네트워크 링크는 품질이 상이하고, 외부 네트워크로 다운로드 시 다운스트림에 따른 트래픽 요금이 발생합니다. 동일 리전 내에서는 내부 네트워크 액세스를 권장합니다.
- **테스트 시간**: 성능 테스트 시간을 적절하게 확보하여 안정된 값을 획득하는 것이 좋습니다.
- **테스트 환경**: 프로그램이 실행하는 JDK 버전 역시 성능에 영향을 미칩니다. 예를 들어 HTTPS를 테스트할 때 낮은 버전의 클라이언트는 암호화 알고리즘의 [GCM BUG](https://bugs.openjdk.java.net/browse/JDK-8201633)로 인해 난수 발생기에 락이 발생하는 등의 문제가 있을 수 있습니다.




## COSBench 실행 단계

1. [COSBench GitHub](https://github.com/intel-cloud/cosbench/releases) 웹 사이트에서 COSBench 0.4.2.c4 zip 압축파일을 다운로드 한 뒤 서버에서 압축을 해제합니다.
2. COSBench의 종속 라이브러리를 설치한 뒤 다음 명령어를 실행합니다.
 - centos 시스템의 경우 다음 명령어를 실행하여 종속 라이브러리를 설치합니다.
```
sudo yum install nmap-ncat java curl java-1.8.0-openjdk-devel -y
```
 - ubuntu 시스템의 경우 다음 명령어를 실행하여 종속 라이브러리를 설치합니다.
```
sudo apt install nmap openjdk-8-jdk 
```
3. s3-config-sample.xml 파일을 편집하여 작업 설정 정보를 추가합니다. 작업 설정 시 다음 다섯 단계를 주로 포함합니다.
   1.   init 단계: 버킷을 생성합니다.
   2.   prepare 단계: worker 스레드, main단계에서 읽어오기 위해 PUT 업로드 시 객체 크기를 지정합니다.
   3.   main 단계: worker 스레드, 읽기/쓰기 객체를 혼합하고, 실행 시간을 지정합니다.
   4.   cleanup 단계: 생성된 객체를 삭제합니다.
   5.   dispose 단계: 버킷을 삭제합니다.

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

| 매개변수                 | 설명                                                         |
| -------------------- | ------------------------------------------------------------ |
|    accesskey, secretkey    |    키 정보, 사용자의 SecretId와 SecretKey로 각각 대체  |
| cprefix              | 버킷 이름 접두사. 예시: examplebucket                            |
| containers           | 버킷 이름 값 구간. 버킷의 마지막 이름은 cprefix와 containers로 구성. 예시: examplebucket1, examplebucket2   |
| csuffix              | 사용자 APPID. APPID 앞에 `-` 입력. 예시: -1250000000      |
| runtime             | 부하 테스트 실행 시간                                                 |
| ratio                | 읽기와 쓰기 비율                                                 |
| workers             | 부하 테스트 스레드 수                                                |

4. cosbench-start.sh 파일을 편집하여 Java에서 다음 매개변수로 행 추가를 실행하고, s3의 md5 인증 기능을 비활성화합니다.
```plaintext
-Dcom.amazonaws.services.s3.disableGetObjectMD5Validation=true
```
5. cosbench 서비스를 실행합니다.
 - centos 시스템의 경우 다음 명령어를 실행합니다. 
```plaintext
sudo bash start-all.sh
```
 - ubuntu 시스템의 경우 다음 명령어를 실행합니다. 
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
7. 다음은 소속 리전이 베이징이며, 32코어, 내부 네트워크 대역폭 17Gbps인 CVM에 대한 업로드 및 다운로드 성능 테스트 예시로, 두 단계를 포함하고 있습니다.
    1. prepare 단계: worker 스레드가 100개이며, 50MB 객체를 1000개 업로드합니다.
    2. main 단계: 100개의 worker 스레드가 300초 동안 읽기/쓰기 객체를 혼합합니다.

위와 같은 두 단계의 성능 테스트 결과는 다음과 같습니다.
![](https://main.qcloudimg.com/raw/e3ac34b6f8340c5cbc834d4f98ba9341.png)

8. 다음 명령어를 실행하여 테스트 서비스를 중지합니다.
```plaintext
sudo bash stop-all.sh
```
