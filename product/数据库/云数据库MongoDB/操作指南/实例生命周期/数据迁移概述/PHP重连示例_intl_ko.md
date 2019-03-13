## 설명

TencentDB for MongoDB는 쉬운 mongos 액세스만 제공하는 것이 아니라 액세스용 로드밸런싱 IP도 제공합니다. 그 후에 해당 IP의 연결 대상은 mongos와 같은 라우팅 액세스 레이어입니다.
클라이언트 드라이브는 로드밸런싱 IP를 통하여 접속 서버와 지속적인 연결을 구축합니다. 이 연결이 장시간 동안 액티브 상태일 때, 당사는 이에 대해 어떠한 간섭도 하지 않습니다. 그러나 지속적인 연결의 휴면 시간이 1일(이 시간은 버전의 최적화에 따라 조정될 수 있음)을 초과할 경우, 라우팅 액세스 레이어는 이 연결을 끊을 수 있습니다.
일반적으로 클라이언트 드라이브는 자동 이중 연결 과정을 구현합니다. 그러나 일부 언어의 드라이브는 구현되지 못합니다. 자동 재연결을 구현할 수 없는 언어의 드라이브일 경우 사용자가 이미 끊긴 연결을 TencentDB for MongoDB에 시도하면 "Remote server has closed the connection"라는 메시지가 나타날 수도 있습니다. 따라서, 수동으로 재연결해야 합니다. 다음은 PHP 재연결의 Demo입니다.

## PHP Mongo 기반 드라이브의 재연결 구현
```
<?php

function getConnection() {
    $connection = false;
    $uri = 'mongodb://rwuser:1234567a@10.66.148.142:27017/admin?authMechanism=MONGODB-CR';
    $maxRetries = 5;
    for( $counts = 1; $counts <= $maxRetries; $counts++ ) {
        try {
            $connection = new MongoClient($uri);
        } catch( Exception $e ) {
     // 또는 수요에 따라 다음의 Catch 코드행을 사용하십시오. 주의: 일부 아키텍처가 이름 스페이스를 사용할 때는 "\"이 필요합니다.
     // } catch( \Exception $e ) {
            continue;
        }
        break;
    }
    return $connection;
}

$connection = getConnection();

if($connection) {
		$db = $connection->testdb;
		$collection = $db->testcollection;

		$one = $collection->findOne();

		var_dump($one);
}
```
