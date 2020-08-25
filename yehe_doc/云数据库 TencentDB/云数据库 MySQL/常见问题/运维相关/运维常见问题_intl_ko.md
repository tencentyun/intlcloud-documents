
### TencentDB for MySQL에서 pt-online-schema-change 사용에 대한 문제
TencentDB for MySQL5.6 버전은 Online DDL을 지원하게 되었습니다. 5.5 버전으로 테이블 구조 변경 시 테이블 잠금으로 인해 비즈니스에 영향을 주지 않도록 계속해서 pt-online-schema-change 등 오픈 소스 툴로 해당 조작을 완료할 것을 권장하였지만, 사용자가 CVM을 통해 pt-online-schema-change를 사용해 MySQL 테이블 구조를 변경하는 과정에서 적잖은 문제가 발생하고 있습니다.

- 자주 발생하는 오류 정보:
`Use of uninitialized value $host in string eq at /usr/local/percona-toolkit-3.0.3/bin/pt-online-schema-change line 4284.`
- 상응하는 소스 코드 보기:
``` perl
sub _find_slaves_by_processlist {
   my ( $self, $dsn_parser, $dbh, $dsn ) = @_;

   my @slaves = map  {
      my $slave        = $dsn_parser->parse("h=$_", $dsn);
      $slave->{source} = 'processlist';
      $slave;
   }
   grep { $_ }
   map  {
      my ( $host ) = $_->{host} =~ m/^([^:]+):/;
      if ( $host eq 'localhost' ) {
         $host = '127.0.0.1'; # Replication never uses sockets.
      }
      $host;
   } $self->get_connected_slaves($dbh);

   return @slaves;
}
```
코드상에서 보면 processlist 방식으로 slave 정보를 찾을 때, TencentDB에서 계정 복제 관련 정보에 대해 처리함에 따라 processlist로 slave 정보를 획득하지 못한 상황입니다.
- 복구 방식:
pt-osc를 사용할 때 아래와 같은 매개변수를 추가해 slave의 상태를 확인하지 않도록 합니다.
    `--recursion-method=none`
 
### TencentDB 데이터 가져오기 시 Specified key was too long 오류 메시지
**오류 발생 원인:**
사용자가 CVM 명령 라인으로 XXXX.sql 파일을 MySQL로 가져올 때, MySQL에 Specified key was too long이라는 오류 메시지가 출력됩니다.
"ERROR 1071 (42000): Specified key was too long; max key length is 767 bytes"라고 출력되는 오류 메시지는 "인덱스 필드의 길이가 767bytes를 초과해 너무 깁니다."라는 뜻입니다.
- innodb 스토리지 엔진, 멀티 칼럼 인덱스의 길이 제한은 다음과 같습니다.
 각 칼럼의 길이는 767bytes를 초과할 수 없으며, 모든 결합 인덱스 칼럼의 총 길이는 3072bytes를 초과할 수 없습니다.
- myisam 스토리지 엔진, 멀티 칼럼 인덱스 길이 제한은 다음과 같습니다.
각 칼럼의 길이는 1000bytes를 초과할 수 없으며, 모든 결합 인덱스 칼럼의 총 길이는 1000bytes를 초과할 수 없습니다.
>?768 / 2 = 384개 2바이트 또는 767 / 3 = 255개 3바이트의 필드(GBK는 2바이트이고 UTF8는 3바이트, UTF8MB4는 4바이트)

MySQL 5.6 이상 버전의 모든 myisam 테이블은 모두 innodb로 자동 전환됩니다. 따라서, 자체 구축한 데이터베이스에 767bytes를 초과한 결합 인덱스 칼럼이 있을 경우, 자체 구축한 라이브러리에서는 myisam 스토리지 엔진으로 인해 테이블 생성 명령을 정상적으로 실행할 수 있지만 MySQL 5.6 버전 이상에서는 문제가 발생할 수 있습니다.

**솔루션**
1. 백업 파일에서 오류가 발생한 행의 결합 인덱스 칼럼 길이를 수정합니다.
흔히 보는 사례:
`create table test(test varcahr(255) primary key)charset=utf8;`
-- 성공
`create table test(test varcahr(256) primary key)charset=utf8;`
-- 실패
`ERROR 1071（42000）:Specified key was too long; max key length is 767 bytes`
2. TencentDB 5.5 버전을 사용하면 myisam 엔진이 innodb로 자동 전환되지 않습니다.

<span id = "outfile"></span>
### select * from XX into outfile xxxx라고 오류 메시지가 뜨는 원인은 무엇인가요?
플랫폼의 보안성 문제로 file 권한 활성화 및 select into outfile 방식으로 데이터 내보내기를 지원하지 않습니다. 기타 방식으로 내보내시기 바랍니다.

<span id = "emoji"></span>
### MySQL 데이터베이스에 emoji 이모티콘을 삽입할 때 깨짐 현상이 있을 때는 어떻게 해야 하나요?
MySQL 인스턴스 내부, 클라이언트와 MySQL의 인스턴스 연결 등 3가지 방면에 대해 진단하고 모두 utf8mb4 문자 세트를 사용 또는 지원하는지 확인합니다.
MySQL 인스턴스에서 스토리지 emoji 이모티콘을 사용하려면 MySQL 내부, 클라이언트와 MySQL의 인스턴스 연결 3가지 방면에 대해 진단하고 모두 utf8mb4 문자 세트를 사용 또는 지원하는지 확인합니다.
1. 우선 MySQL 인스턴스의 문자 세트를 utf8mb4로 설정한 후, 콘솔에 로그인하여 `character_set_server` 매개변수를 수정합니다.
>!해당 매개변수를 수정하면 데이터베이스가 재시작되므로, 사전에 데이터베이스를 백업해 두어 데이터 손실이 없도록 해주시기 바랍니다.
2. 사용자의 프로그램 클라이언트는 출력된 문자열의 문자 세트가 utf8mb4이도록 보장해야 합니다. 
3. 응용 프로그램의 연결 생성은 지정된 문자 세트를 실행해야 합니다. 흔히 사용하는 jdbc 연결을 예로 듭니다. 
jdbc 연결을 하려면 MySQL Connector/J 5.1.13(포함) 이상의 버전을 사용해야 합니다. 예시 코드는 다음과 같습니다. 
```
String query = “set names utf8mb4”; 
stat.execute(query);
```

