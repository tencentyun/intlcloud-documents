
본문에서는 간단한 예시로 데이터 구독에서 상응하는 리스트를 로컬 파일로 읽어들이는 기능을 설명하며, 간단한 [LocalDemo 다운로드](https://main.qcloudimg.com/raw/f145138da95d16063a3219f030f24625/LocalDemo.zip)를 제공합니다. 다음 작업은 CentOS 운영 체제에서 완료됩니다.

## 설정 환경
- Java 환경 설정
```
 yum install java-1.8.0-openjdk-devel 
```
- [데이터 구독 SDK 다운로드](https://main.qcloudimg.com/raw/2aa7b213535065def5655712c8494182/binlogsdk-2.7.0-official.jar)

## 키 획득
[액세스 관리 콘솔](https://console.cloud.tencent.com/cam/capi)에 로그인해 키를 획득합니다.

## 데이터 구독 선택
1. [DTS 콘솔](https://console.cloud.tencent.com/dtsnew/migrate/page)에 로그인해 왼쪽의 [데이터 구독]을 클릭해 데이터 구독 페이지로 이동합니다.
2. 동기화가 필요한 TencentDB 인스턴스 이름을 선택한 후 실행을 클릭하고 데이터 구독으로 돌아가 생성된 데이터 구독을 클릭합니다. 상세한 소개는 [데이터 구독 방법(https://intl.cloud.tencent.com/document/product/571/8774)을 참조하십시오.
3. 상응하는 DTS 터널, IP와 포트를 조회한 후 이전 키와 결합해 상응하는 LocalDemo.java에 입력합니다.
```
  // Cloud API에서 키를 획득해 이곳에 입력합니다.
        context.setSecretId("AKIDfdsfdsfsdt1331431sdfds"); Cloud API에서 획득하신 secretID를 입력하십시오.
        context.setSecretKey("test111usdfsdfsddsfRkeT"); 
        클라우드 API에서 획득하신 secretKey를 입력하십시오.
	// 데이터 마이그레이션 서비스에서 데이터 구독을 통해 상응하는 ip와 port를 획득해 이곳에 입력합니다.
        context.setServiceIp("10.66.112.181"); 데이터 구독 설정에서 획득한 IP를 입력하십시오.
        context.setServicePort(7507);
        데이터 구독 설정에서 획득한 포트를 입력하십시오.
        final DefaultSubscribeClient client = new DefaultSubscribeClient(context);
	// 동기화할 데이터베이스와 테이블 이름을 입력하고, 해당하는 적용할 스토리지의 파일 이름을 수정합니다.
        final String targetDatabase = "test"; 구독할 데이터베이스 이름을 입력합니다.
        final String targetTable = "alantest"; 구독할 리스트 이름을 입력합니다.

        final String fileName = "test.alan.txt"; 로컬에 저장할 파일 이름을 입력합니다.
        
          client.addClusterListener(listener);
	// 데이터 마이그레이션의 설정 옵션에서 dts-channel의 설정 정보를 획득해 이곳에 입력합니다.
	client.askForGUID("dts-channel-e4FQxtYV3It4test"); 데이터 구독 설정에서 획득한 터널 dts 명칭을 입력해주십시오.
        client.start();
```


##  컴파일 작업과 검증
1.  
```
javac -classpath binlogsdk-2.6.0-release.jar -encoding UTF-8 LocalDemo.java
```
2. 실행한 후에 오류 리포트가 없을 경우는 정상적으로 서비스되고 있는 것입니다. 그 후, 이전에 설정한 적용 파일을 조회합니다.
```
java -XX:-UseGCOverheadLimit -Xms2g -Xmx2g -classpath .:binlogsdk-2.6.0-release.jar LocalDemo
```
3. 이전에 설정한 test.alan.txt를 조회하면 이미 로컬로 데이터를 가져온 것을 볼 수 있습니다.
```
[root@VM_71_10_centos ~]# cat test.alan.txt  
checkpoint:144251@3@357589@317713
record_id:000001000000000004D9110000000000000001
record_encoding:utf8
fields_enc:latin1,utf8
gtid:4f21864b-3bed-11e8-a44c-5cb901896188:1562
source_category:full_recorded
source_type:mysql
table_name:alantest
record_type:INSERT
db:test
timestamp:1523356039
primary:
Field name: id
Field type: 3
Field length: 2
Field value: 26
Field name: name
Field type: 253
Field length: 4
Field value: alan
```

