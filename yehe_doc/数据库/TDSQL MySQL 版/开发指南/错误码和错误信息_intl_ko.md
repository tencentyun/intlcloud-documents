
proxy에 대해 다음 오류 코드가 추가되었습니다.

	#define ER_PROXY_GRAM_ERROR_BEGIN 600
	
	#define ER_PROXY_SANITY_ERROR 601           // "Sanity error: %s"
	#define ER_PROXY_GS_NOT_SUPPORT 602         // 지원되지 않는 sql 유형
	#define ER_PROXY_ORDERBY_INDEX_NEG 603      // order by index is negative
	#define ER_PROXY_ORDERBY_INDEX_TOO_BIG 604  // order by index is too big
	#define ER_PROXY_ORDERBY_TYPE_UNSUPPORT 605 // order by 미지원
	#define ER_PROXY_GROUPBY_INDEX_NEG 606      // group by index is negative
	#define ER_PROXY_GROUPBY_INDEX_TOO_BIG 607  // group by index is too big
	#define ER_PROXY_GROUPBY_TYPE_UNSUPPORT 608 // group by 미지원
	#define ER_PROXY_GET_AUTO_ID_FAILED 609     // 자동 증분 id 가져오기 실패
	#define ER_PROXY_TEANS_ROLLED_BACK 610      // 트랜잭션 롤백됨
	#define ER_PROXY_ONE_SET 611                // 현재 sql 문은 하나의 백엔드로 전송되어야 하지만 전송되지 않음
	#define ER_PROXY_CLIENT_HS_ERROR 612        // 클라이언트 핸드셰이크 패킷을 구문 분석하는 동안 오류 발생
	#define ER_PROXY_ACCESS_DENIED_ERROR 613    // the length of readu_auth_switch_result is not 20, 나타나서는 안 됨
	#define ER_PROXY_TRANS_NOT_ALLOWED 614      // 트랜잭션에서 허용되지 않는 명령
	#define ER_PROXY_TRANS_READ_ONLY 615        // 읽기 전용 트랜잭션에서 허용되지 않는 명령
	#define ER_PROXY_TRANS_ERROR_DIFFENT_SET 616    // xa가 아닌 트랜잭션에서 읽기 전용 sql은 여러 백엔드를 사용
	#define ER_PROXY_STRICT_ERROR 617           // strict 모드에서는 한 번에 한 set만 수정 가능
	#define ER_PROXY_SC_TOO_LONG 618            // 백엔드가 오랫동안 연결이 끊어지고 연결이 닫힘
	#define ER_PROXY_START_TRANS_FAILED 619     // 새 xa 트랜잭션 시작 실패
	#define ER_PROXY_SC_RETRY 620               // server 이미 close, 이전 sql 다시 시도
	#define ER_PROXY_SC_TRANS_IN_ROLLBACK_ONLY 621  // server 이미 close, 현재 트랜잭션 rollback
	#define ER_PROXY_SC_COMMIT_LATER 622        // server 이미 close, 트랜잭션은 나중에 커밋됨
	#define ER_PROXY_SC_ROLLBACL_LATER 623      // server 이미 close, 트랜잭션은 나중에 롤백됨
	#define ER_PROXY_SC_IN_COMMIT_OR_ROLLBACK 624   //  트랜잭션이 커밋/롤백될 때 server close
	#define ER_PROXY_SC_NEED_ROLLBACK 625       // server 이미 close, 현재 트랜잭션을 롤백해야 함
	#define ER_PROXY_SC_STATE_WILL_ROLLBACK 626 //  server 이미 close, 롤백이 수행됨
	#define ER_PROXY_XA_UNSUPPORT 627           // 명령은 현재 xa에서 미지원
	#define ER_PROXY_XA_INVALID_COMMAND 628     // 잘못된 xa 명령
	#define ER_PROXY_XA_GTID_INIT_ERROR 629     // gtid log 초기화 실패
	#define ER_PROXY_XA_GET_SET_IP_PORT_FAILED 630  // set 주소 가져오기 실패
	#define ER_PROXY_XA_UPDATE_GTID_LOG_FAILED 631  // gtid log 업데이트 실패
	#define ER_PROXY_MYSQL_PARSER_ERROR 632     // 포함된 데이터베이스 sql을 구문 분석 실패
	#define ER_PROXY_ILLEGAL_ID 633             // 잘못된 kill id
	#define ER_PROXY_NOT_SUPPORT_CURSOR 634     // CURSOR_TYPE_READ_ONLY는 현재 미지원
	#define ER_PROXY_UNKNOWN_PREPARE_HANDLER 635    // 실행된 prepare 불명확
	#define ER_PROXY_SET_PARA_FAIL 636          // Set parameters failed
	#define ER_PROXY_SUBPARTITION_DEAY 637      // 서브 파티션을 처리하는 동안 오류 발생
	#define ER_PROXY_NO_SUBPARTITION_ROUTE 638  // 분할된 테이블에 대한 라우팅 정보 가져오기 실패
	#define ER_PROXY_LOCK_MORE_TABLE 639        // 한 번에 하나의 서브 분할된 테이블만 잠글 수 있음
	#define ER_PROXY_GET_ROUTER_LOCK_FAIL 640   // 경로 잠금 가져오기 실패
	#define ER_PROXY_PART_NAME_EMPTY 641        // 파티션 이름이 비어 있음
	#define ER_PROXY_SUB_PART_TABLE_IS_NONE 642 // 서브 파티션 없음
	#define ER_PROXY_PART_TYPE_DENY 643         // 서브 파티션 유형 미지원
	#define ER_PROXY_PART_NAME_ILLEGAL 644      // 파티션 이름 잘못됨
	#define ER_PROXY_DROP_ALL_PARTITION_FAIL 645    //  모든 파티션 삭제 실패, 테이블 삭제
	#define ER_PROXY_GET_OLD_PART_NUM_FAIL 646  // 테이블의 샤드 수를 가져오기 실패
	#define ER_PROXY_EMPTY_SQL 647              // empty sql, 클라이언트에게 반환되지 않음
	#define ER_PROXY_ERROR_SHARDKEY 648         // sk는 지정된 열이어야 함
	#define ER_PROXY_ERROR_SUB_SHARDKEY 649     // 서브 분할을 위한 Shardkey 실패
	#define ER_PROXY_SQLUSE_NOT_SUPPORT 650     // proxy는 이 사용법 미지원
	#define ER_PROXY_DBFW_WHITE_LIST_DENY 651   // 허용 목록에 없고 방화벽에 의해 차단됨
	#define ER_PROXY_DBFW_DENY 652              // 방화벽에 의해 차단됨
	#define ER_PROXY_INCORRECT_ARGS 653         // stmt 매개변수 잘못됨
	#define ER_PROXY_SYSTABLE_UNSUPPORT_NON_READ_SQL 654    // 읽기 전용이 아닌 sql 문은 시스템 테이블에 액세스 미지원
	#define ER_PROXY_TABLE_NOT_EXIST 655        // 테이블이 존재하지 않음
	#define ER_PROXY_SHARD_JOIN_UNSUPPORT_TYPE 656  // shard join 현재 미지원
	#define ER_PROXY_RECURSIVE_JOIN_DENY 657    // 재귀 join 미지원
	#define ER_PROXY_JOIN_INTERNAL_ERROR 658    // join 작업이 예외적임
	#define ER_PROXY_SQL_TOO_COMPLEX 659        // sql이 너무 복잡함, groupshard는 현재 미지원
	#define ER_PROXY_INVALID_ARG_FOR_GTID_STATE 660 // gtid_state() 매개변수가 잘못됨
	#define ER_PROXY_CANT_SET_GLOBAL_AUTOCOMMIT_GS 661  // Global autocommit cannot be set in groupshard
	#define ER_PROXY_INVALID_VALUE_FOR_AUTOCOMMIT 662   // autocommit 값이 잘못됨
	#define ER_PROXY_XID_ERROR 663              // xid가 잘못됨
	#define ER_PROXY_XID_GENERAT_FAILED 664     // xid는 사용자가 지정할 수 없음
	#define ER_PROXY_CANT_EXEC_IN_INTER_TRANS 665   // "The command cannot be executed in internal transction"
	#define ER_PROXY_XID_TIME_ERROR 666         // "Unexpected time part of xid"
	#define ER_PROXY_XID_TIMEDIFF_TOO_LONG 667  // "timediff > 1800s, it's not safe to execute boost"
	#define ER_PROXY_SAVEPOINT_NOT_EXIST 668    // SAVEPOINT가 존재하지 않음
	#define ER_PROXY_SC_TRANS_IN_ROLLED 669     // serevr가 close되면서 트랜잭션이 롤백됨
	#define ER_PROXY_CANT_BOOST_IN_TRANS 670    // SQLCOM_BOOST는 트랜잭션에서 허용되지 않음
	#define ER_PROXY_TRANS_EXPECTED 671         // "A transaction is expected, this maybe a bug"
	#define ER_PROXY_EXTERNAL_TRANS 672         // 외부 xa 트랜잭션 실행 불가
	#define ER_PROXY_AUTO_INC_FAIL 673          // "Deal auto inc failed"
	#define ER_PROXY_CHECK_JOIN_FAIL 674        // "Check join failed"
	#define ER_PROXY_TABLE_TYPE_NOT_MATCH 675   // "Do not support shard-table operations in noshard instance"
	#define ER_PROXY_UNSUPPORT_NS_IN_INSERT 676 // "Do not support noshard and noshard_allset in insert sql"
	#define ER_PROXY_ALTER_SEQ_ID_FAIL 677      // Alter seq id failed
	#define ER_PROXY_ALTER_ID_ILLEGAL 678       // Alter seq id is illegal
	#define ER_PROXY_CANT_CHANGE_STEP 679       // "Current table use zk to get auto inc, do not support to change step: \'%s\'"
	#define ER_PROXY_ALTER_STEP_FAIL 680        // Alter step failed
	#define ER_PROXY_TOO_MUCH_TABLES 681        // 최대 테이블 수에 도달
	#define ER_PROXY_TABLE_EXISTED 682          // 테이블 이미 존재
	#define ER_PROXY_CREATE_STABLE_FAILED 683   // 복잡한 sql 문을 사용하여 shard 테이블을 생성할 수 없으므로 shard 테이블을 생성 실패
	#define ER_PROXY_DDL_DENY 684               // ddl 작업이 허용되지 않음
	#define ER_PROXY_SHADKEY_ERROR 685          // SQL should not relate to subpartition tables
	#define ER_PROXY_NO_SK 686                  // reject nosk
	#define ER_PROXY_COMBINE_SQL_KEY 687        // Something went wrong
	#define ER_PROXY_GET_SK_ERROR 688           // sk 가져오기 실패
	#define ER_PROXY_SHOW_FAILED 689            // proxy show 명령 오류
	#define ER_PROXY_SET_FAILED 690             // proxy set 명령 오류
	#define ER_PROXY_UNLOCK_FORMAT_ERROR 691    // sql 형식 부정확
	#define ER_PROXY_UNLOCK_ROUTER_FAIL 692     // 경로 잠금 비활성화 실패
	#define ER_PROXY_LOCK_ROUTER_FAIL 693       // 경로 잠금 활성화 실패
	#define ER_PROXY_PROXY_CMD_FAIL 694         // 미지원/*proxy*/ 명령
	#define ER_PROXY_PROCESS_RULE_FILE_FAILED 695   // dump_error
	#define ER_PROXY_GET_AUTO_NUM_ERROR 696     // 자동 증가 값 가져오기 실패
	#define ER_PROXY_SEQUENCE_NOT_EXIST 697     // sequence 존재하지 않음
	#define ER_PROXY_SEQUENCE_ERROR 698         // sequence 잘못됨
	#define ER_PROXY_SEQUENCE_ALREADY_EXIST 699 // sequence 이미 존재
	#define ER_PROXY_SQL_RETRY 700              // sql 문이 커밋되거나 롤백되지 않음
	#define ER_PROXY_XA2PC_ABORT 701            // 2pc 실패, 트랜잭션 롤백됨
	#define ER_PROXY_XA2PC_COMMIT 702           // 2pc 실패, 나중에 커밋됨
	#define ER_PROXY_XA2PC_UNCERTAIN 703        // 알 수 없는 결과로 2pc 실패
	#define ER_PROXY_KILL_ERROR 704             // kill 실패
	#define ER_PROXY_TRACE_DENY705  // trace 모드에서는 sql 문을 실행할 수 없음
	#define ER_PROXY_SQL_IMCOMPLETE 706 // 거래 미완료 상태
	#define ER_PROXY_SHARDKEY_HASH_ERROR 709// sk hash 오류
	
	#define ER_PROXY_GRAM_ERROR_END 799         
	
	// system error -----------------------------------------------------------------------
	#define ER_PROXY_SYSTEM_ERROR_BEGIN 900
	
	#define ER_PROXY_SLICING 901                // slice가 수정되고 확장될 수 있으므로 현재 sql 문이 거부됨
	#define ER_PROXY_NO_DEFAULT_SET 902         // set가 비어 있음
	#define ER_PROXY_GET_ADDRESS_FAILED 903     // 초기화 미완성, 백엔드 주소 가져오기 실패, 나중에 다시 시도
	#define ER_PROXY_SQL_SIZE_ERROR_IN_GET_CANDIDATE_ADDRESS 904 // 백엔드 주소 가져오는 동안 오류 발생(대상 백엔드 번호가 잘못됨)
	#define ER_PROXY_GET_ADDRESS_ERROR 905      // 백엔드 주소 가져오는 동안 오류 발생
	#define ER_PROXY_CANDIDATE_ADDRESS_EMPTY 906 // 백엔드 주소를 얻지 못함
	#define ER_PROXY_CANT_GET_SOCK 907          // socket 가져오기 실패	
	#define ER_PROXY_GET_SET_SOCK_FAIL 908      // socket 가져오기 실패
	#define ER_PROXY_CONNECT_ERROR 909          // 백엔드 연결 실패
	#define ER_PROXY_NO_SQL_ASSIGN_TO_SET 910   // sql 문을 보내는 동안 예외 발생
	#define ER_PROXY_STATUS_ERROR 911           // group 예외 상태이며 연결이 중단됨
	#define ER_PROXY_CONN_BROKEN_ERROR 912      // server close, sql 문이 예외 상태
	#define ER_PROXY_UNKNOWN_ERROR 913          // 알 수 없는 proxy 오류
	#define ER_PROXY_ALL_SLAVES_UNAVAILABLE 914 // 모든 보조 서버를 사용할 수 없음
	#define ER_PROXY_ALL_SLAVES_CHANGE 915      // 보조 서버에 예외가 있음
	
	#define ER_PROXY_ERROR_END 916


>?오류 코드 900 이상은 시스템 오류이며 [클라우드 모니터링 플랫폼](https://console.cloud.tencent.com/monitor/overview)을 통해 알람됩니다.
