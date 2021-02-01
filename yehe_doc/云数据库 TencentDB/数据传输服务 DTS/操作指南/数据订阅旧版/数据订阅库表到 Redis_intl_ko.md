본문에서는 간단한 예시로 데이터 구독에서 상응하는 리스트를 로컬 파일로 읽어들이는 기능을 설명하며, 간단한 [RedisDemo 다운로드](https://main.qcloudimg.com/raw/0a3b560fad57a27440f9445039552d2b/RedisDemo.zip)를 제공합니다. 다음 작업은 CentOS 운영 체제에서 완료됩니다.

## 설정 환경
- Java 환경 설정 
```
yum install java-1.8.0-openjdk-devel 
```
- [데이터 구독 SDK 다운로드](https://main.qcloudimg.com/raw/2aa7b213535065def5655712c8494182/binlogsdk-2.7.0-official.jar)
- [jedis-2.9.0.jar 다운로드](https://main.qcloudimg.com/raw/130e0f114f84e6e7eb9cc16d2fecd58c/jedis-2.9.0.zip)

## 키 획득
[액세스 관리 콘솔](https://console.cloud.tencent.com/cam/capi)에 로그인해 키를 획득합니다.

## 데이터 구독 선택
1. [DTS 콘솔](https://console.cloud.tencent.com/dtsnew/migrate/page)에 로그인해 왼쪽의 [데이터 구독]을 클릭해 데이터 구독 페이지로 이동합니다.
2. 동기화가 필요한 TencentDB 인스턴스 이름을 선택한 후 실행을 클릭하고 데이터 구독으로 돌아가 생성된 데이터 구독을 클릭합니다. 상세한 소개는 [데이터 구독 방법(https://intl.cloud.tencent.com/document/product/571/8774)을 참조하십시오.
3. 상응하는 DTS 터널, IP와 포트를 조회한 후 이전 키와 결합해 상응하는 RedisDemo.java에 입력합니다.

```
 context.setSecretId("AKIDfdsfdsfsdt1331431sdfds"); Cloud API에서 획득하신 secret ID를 입력합니다.
        context.setSecretKey("test111usdfsdfsddsfRkeT"); Cloud API에서 획득하신 secretKey를 입력합니다.
    // 데이터 마이그레이션 서비스에서 데이터 구독을 통해 상응하는 ip와 포트를 획득해 이곳에 입력합니다.
        context.setServiceIp("10.66.112.181"); 데이터 구독 설정에서 획득한 IP를 입력합니다.
        context.setServicePort(7507); 데이터 구독 설정에서 획득한 포트를 입력합니다.

        // 소비자 생성
        //SubscribeClient client=new DefaultSubscribeClient(context,true);
        final DefaultSubscribeClient client = new DefaultSubscribeClient(context);

        final Jedis jedis = new Jedis("127.0.0.1", 6379); 상응하는 redis 호스트와 포트를 입력합니다.

        final String targetDatabase = "test"; 구독할 데이터베이스 이름을 입력합니다.
        final String targetTable = "alantest"; 구독할 리스트 이름을 입력합니다. 표는 id와 name, 2개의 필드로 나뉘며, id가 기본 키입니다.

        // 구독 listener 생성
        ClusterListener listener = new ClusterListener() {
            @Override
            public void notify(List<ClusterMessage> messages) throws Exception {
		//                System.out.println("--------------------:" + messages.size());
                for(ClusterMessage m:messages){
                    DataMessage.Record record = m.getRecord();
                    //관심 없는 구독 정보 필터링
	            if(!record.getDbName().equalsIgnoreCase(targetDatabase) || !record.getTablename().equalsIgnoreCase(targetTable)){
                        //주의사항: 관심 없는 정보에도 응답을 보내야 합니다.
                        m.ackAsConsumed();
                        continue;
                    }

                    if(record.getOpt() != DataMessage.Record.Type.BEGIN && record.getOpt() != DataMessage.Record.Type.COMMIT){
                        List<DataMessage.Record.Field> fields = record.getFieldList();

                        //INSERT RECORD
                        //String pk = record.getPrimaryKeys();
			
                        if(record.getOpt() == DataMessage.Record.Type.INSERT){
			    
			    String keyid="";
			    String value="";
                            for (DataMessage.Record.Field field : fields) {

                                //우선 id값을 획득해야 하며, primary key가 있어야 합니다. 그 후 name이라는 이름의 리스트를 찾아 redis에 key와 name에 대응되는 value를 삽입합니다.
				if(field.getFieldname().equalsIgnoreCase("id")){
                                    keyid=field.getValue();
               continue;
                                }
				if(field.getFieldname().equalsIgnoreCase("name")){
				    value=field.getValue();
                                  
                                }
				jedis.set(keyid, value);
                            }

                        }
  
```


##  컴파일 작업과 검증
1.  
```
[root@VM_71_10_centos ~]# javac -classpath binlogsdk-2.6.0-release.jar:jedis-2.9.0.jar -encoding UTF-8 RedisDemo.java 
```
2. 실행 시 오류 리포트가 없을 경우는 정상적으로 서비스되고 있는 것입니다. 그 후, 이전에 설정한 적용 파일을 조회합니다.
```
 java -XX:-UseGCOverheadLimit -Xms2g -Xmx2g -classpath .:binlogsdk-2.6.0-release.jar:jedis-2.9.0.jar RedisDemo
```
3. 데이터베이스 삽입과 업데이트 작업을 조회한 후, redis 모니터링으로 삽입과 수정이 성공한 것을 확인하고 나서 마지막으로 삭제 작업을 진행하며, redis의 상응하는 데이터도 삭제됩니다.

```
MySQL [test]> insert into alantest values(1001,'alan1');
Query OK, 1 row affected (0.00 sec)

MySQL [test]> update alantest set name='alan2' where id=1001;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

------------------------
127.0.0.1:6379> get 1001
"alan2"


MySQL [test]> update alantest set name='alan3' where id=1001;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

------------------------
127.0.0.1:6379> get 1001
"alan3"

MySQL [test]> delete from alantest where id=1001;
Query OK, 1 row affected (0.00 sec)

-----------------------

127.0.0.1:6379> get 1001
(nil)

```
