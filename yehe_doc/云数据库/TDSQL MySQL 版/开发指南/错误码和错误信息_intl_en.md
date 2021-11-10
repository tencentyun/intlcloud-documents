
The following error codes have been added for the proxy:

	#define ER_PROXY_GRAM_ERROR_BEGIN 600
	
	#define ER_PROXY_SANITY_ERROR 601           // "Sanity error: %s"
	#define ER_PROXY_GS_NOT_SUPPORT 602         // Unsupported SQL type
	#define ER_PROXY_ORDERBY_INDEX_NEG 603      // order by index is negative
	#define ER_PROXY_ORDERBY_INDEX_TOO_BIG 604  // order by index is too big
	#define ER_PROXY_ORDERBY_TYPE_UNSUPPORT 605 // ORDER BY is not supported
	#define ER_PROXY_GROUPBY_INDEX_NEG 606      // group by index is negative
	#define ER_PROXY_GROUPBY_INDEX_TOO_BIG 607  // group by index is too big
	#define ER_PROXY_GROUPBY_TYPE_UNSUPPORT 608 // GROUP BY is not supported
	#define ER_PROXY_GET_AUTO_ID_FAILED 609     // Failed to obtain auto-increment ID
	#define ER_PROXY_TEANS_ROLLED_BACK 610      // The transaction has been rolled back
	#define ER_PROXY_ONE_SET 611                // The current SQL statement should have been sent to one backend but it has not
	#define ER_PROXY_CLIENT_HS_ERROR 612        // An error occurred while parsing the client handshake packet
	#define ER_PROXY_ACCESS_DENIED_ERROR 613    // The length of readu_auth_switch_result is not 20, which should not happen
	#define ER_PROXY_TRANS_NOT_ALLOWED 614      // Command not allowed in the transaction
	#define ER_PROXY_TRANS_READ_ONLY 615        // Command not allowed in the read-only transaction
	#define ER_PROXY_TRANS_ERROR_DIFFENT_SET 616    // In the non-XA transaction, the read-only SQL uses multiple backends
	#define ER_PROXY_STRICT_ERROR 617           // In the strict mode, only one set can be modified at a time
	#define ER_PROXY_SC_TOO_LONG 618            // The backend is disconnected for a long time and the connection is closed
	#define ER_PROXY_START_TRANS_FAILED 619     // Failed to start a new XA transaction
	#define ER_PROXY_SC_RETRY 620               // The server is closed. Please retry the previous SQL statement.
	#define ER_PROXY_SC_TRANS_IN_ROLLBACK_ONLY 621  // The server is closed. The current transaction is being rolled back.
	#define ER_PROXY_SC_COMMIT_LATER 622        // The server is closed. The transaction will be committed later.
	#define ER_PROXY_SC_ROLLBACL_LATER 623      // The server is closed. The transaction will be rolled back later.
	#define ER_PROXY_SC_IN_COMMIT_OR_ROLLBACK 624   // The server was closed when the transaction was being committed/rolled back
	#define ER_PROXY_SC_NEED_ROLLBACK 625       // The server is closed. The current transaction needs to be rolled back.
	#define ER_PROXY_SC_STATE_WILL_ROLLBACK 626 // The server is closed. Rollback will be performed.
	#define ER_PROXY_XA_UNSUPPORT 627           // Command is not supported by XA currently.
	#define ER_PROXY_XA_INVALID_COMMAND 628     // The XA command is invalid.
	#define ER_PROXY_XA_GTID_INIT_ERROR 629     // GTID log initialization failed
	#define ER_PROXY_XA_GET_SET_IP_PORT_FAILED 630  // Failed to obtain the set address
	#define ER_PROXY_XA_UPDATE_GTID_LOG_FAILED 631  // Failed to update GTID log
	#define ER_PROXY_MYSQL_PARSER_ERROR 632     // Failed to parse the embedded database SQL
	#define ER_PROXY_ILLEGAL_ID 633             // Kill ID is invalid
	#define ER_PROXY_NOT_SUPPORT_CURSOR 634     // CURSOR_TYPE_READ_ONLY is currently not supported
	#define ER_PROXY_UNKNOWN_PREPARE_HANDLER 635    // The executed prepare is unknown
	#define ER_PROXY_SET_PARA_FAIL 636          // Set parameters failed
	#define ER_PROXY_SUBPARTITION_DEAY 637      // An error occurred while handling subpartitions
	#define ER_PROXY_NO_SUBPARTITION_ROUTE 638  // No routing information was obtained for the subpartitioned table
	#define ER_PROXY_LOCK_MORE_TABLE 639        // Only one subpartitioned table can be locked at a time
	#define ER_PROXY_GET_ROUTER_LOCK_FAIL 640   // Failed to obtain the route lock
	#define ER_PROXY_PART_NAME_EMPTY 641        // Partition name is empty
	#define ER_PROXY_SUB_PART_TABLE_IS_NONE 646 // There is no subpartition
	#define ER_PROXY_PART_TYPE_DENY 643         // The subpartition type is not supported
	#define ER_PROXY_PART_NAME_ILLEGAL 644      // The partition name is invalid
	#define ER_PROXY_DROP_ALL_PARTITION_FAIL 645    // Failed to delete all partitions. Please try deleting the table.
	#define ER_PROXY_GET_OLD_PART_NUM_FAIL 646  // Failed to obtain the number of shards of the table
	#define ER_PROXY_EMPTY_SQL 647              // Empty SQL, which will not be returned to the client
	#define ER_PROXY_ERROR_SHARDKEY 648         // The shardkey must be a specified column
	#define ER_PROXY_ERROR_SUB_SHARDKEY 649     // Shardkey for subpartitioning failed
	#define ER_PROXY_SQLUSE_NOT_SUPPORT 650     // The proxy does not support this usage
	#define ER_PROXY_DBFW_WHITE_LIST_DENY 651   // Not in the allowlist and blocked by the firewall
	#define ER_PROXY_DBFW_DENY 652              // Blocked by the firewall
	#define ER_PROXY_INCORRECT_ARGS 653         // The "stmt" parameter is incorrect
	#define ER_PROXY_SYSTABLE_UNSUPPORT_NON_READ_SQL 654    // Non-read-only SQL statements cannot access system tables
	#define ER_PROXY_TABLE_NOT_EXIST 655        // The table does not exist
	#define ER_PROXY_SHARD_JOIN_UNSUPPORT_TYPE 656  // Shard join is currently not supported
	#define ER_PROXY_RECURSIVE_JOIN_DENY 657    // Recursive join is not supported
	#define ER_PROXY_JOIN_INTERNAL_ERROR 658    // The join operation is exceptional
	#define ER_PROXY_SQL_TOO_COMPLEX 659        // The SQL statement is too complex and groupshard is currently not supported
	#define ER_PROXY_INVALID_ARG_FOR_GTID_STATE 660 // The "gtid_state()" parameter is invalid
	#define ER_PROXY_CANT_SET_GLOBAL_AUTOCOMMIT_GS 661  // Global autocommit cannot be set in groupshard
	#define ER_PROXY_INVALID_VALUE_FOR_AUTOCOMMIT 662   // The "autocommit" value is invalid
	#define ER_PROXY_XID_ERROR 663              // xid is invalid
	#define ER_PROXY_XID_GENERAT_FAILED 664     // xid cannot be specified by the user
	#define ER_PROXY_CANT_EXEC_IN_INTER_TRANS 665   // "The command cannot be executed in internal transction"
	#define ER_PROXY_XID_TIME_ERROR 666         // "Unexpected time part of xid"
	#define ER_PROXY_XID_TIMEDIFF_TOO_LONG 667  // "timediff > 1800s, it's not safe to execute boost"
	#define ER_PROXY_SAVEPOINT_NOT_EXIST 668    // The SAVEPOINT does not exist
	#define ER_PROXY_SC_TRANS_IN_ROLLED 669     // The transaction has been rolled back as the server is closed
	#define ER_PROXY_CANT_BOOST_IN_TRANS 670    // SQLCOM_BOOST is not allowed in the transaction
	#define ER_PROXY_TRANS_EXPECTED 671         // "A transaction is expected, this maybe a bug"
	#define ER_PROXY_EXTERNAL_TRANS 672         // An external XA transaction cannot be executed
	#define ER_PROXY_AUTO_INC_FAIL 673          // "Deal auto inc failed"
	#define ER_PROXY_CHECK_JOIN_FAIL 674        // "Check join failed"
	#define ER_PROXY_TABLE_TYPE_NOT_MATCH 675   // "Do not support shard-table operations in noshard instance"
	#define ER_PROXY_UNSUPPORT_NS_IN_INSERT 676 // "Do not support noshard and noshard_allset in insert sql"
	#define ER_PROXY_ALTER_SEQ_ID_FAIL 677      // Alter seq id failed
	#define ER_PROXY_ALTER_ID_ILLEGAL 678       // Alter seq id is illegal
	#define ER_PROXY_CANT_CHANGE_STEP 679       // "Current table use zk to get auto inc, do not support to change step: \'%s\'"
	#define ER_PROXY_ALTER_STEP_FAIL 680        // Alter step failed
	#define ER_PROXY_TOO_MUCH_TABLES 681        // The maximum number of tables has been reached
	#define ER_PROXY_TABLE_EXISTED 682          // The table already exists
	#define ER_PROXY_CREATE_STABLE_FAILED 683   // Failed to create the sharded table, as complex SQL statements cannot be used to create a sharded table
	#define ER_PROXY_DDL_DENY 684               //The DDL operation is not allowed
	#define ER_PROXY_SHADKEY_ERROR 685          // SQL should not relate to subpartition tables
	#define ER_PROXY_NO_SK 686                  // reject nosk
	#define ER_PROXY_COMBINE_SQL_KEY 687        // Something went wrong
	#define ER_PROXY_GET_SK_ERROR 688           // Failed to get the shardkey
	#define ER_PROXY_SHOW_FAILED 689            // The "proxy show" command is incorrect
	#define ER_PROXY_SET_FAILED 690             // The "proxy set" command is incorrect
	#define ER_PROXY_SET_FAILED 690             // The SQL statement format is incorrect
	#define ER_PROXY_UNLOCK_ROUTER_FAIL 692     // Failed to disable route lock
	#define ER_PROXY_LOCK_ROUTER_FAIL 693       // Failed to enable route lock
	#define ER_PROXY_PROXY_CMD_FAIL 694         // The "/*proxy*/" command is not supported
	#define ER_PROXY_PROCESS_RULE_FILE_FAILED 695   // dump_error
	#define ER_PROXY_GET_AUTO_NUM_ERROR 696     // Failed to obtain the auto-increment value
	#define ER_PROXY_SEQUENCE_NOT_EXIST 697     // The sequence does not exist
	#define ER_PROXY_SEQUENCE_ERROR 698         // The sequence is invalid
	#define ER_PROXY_SEQUENCE_ALREADY_EXIST 699 // The sequence already exists
	#define ER_PROXY_SQL_RETRY 700              // The SQL statement has not been committed or rolled back
	#define ER_PROXY_XA2PC_ABORT 701            // 2PC failed and the transaction will be rolled back
	#define ER_PROXY_XA2PC_COMMIT 702           // 2PC failed and it will be committed later
	#define ER_PROXY_XA2PC_UNCERTAIN 703        // 2PC failed with unknown result
	#define ER_PROXY_KILL_ERROR 704             // Failed to kill
	#define ER_PROXY_TRACE_DENY705  // The SQL statement cannot be executed in the trace mode
	#define ER_PROXY_SQL_IMCOMPLETE 706 // The transaction is in the incomplete status
	#define ER_PROXY_SHARDKEY_HASH_ERROR 709// Shardkey hash error
	
	#define ER_PROXY_GRAM_ERROR_END 799         
	
	// system error -----------------------------------------------------------------------
	#define ER_PROXY_SYSTEM_ERROR_BEGIN 900
	
	#define ER_PROXY_SLICING 901                // The slice is modified and possibly being scaled, causing the current SQL statement to be rejected
	#define ER_PROXY_NO_DEFAULT_SET 902         // The set is empty
	#define ER_PROXY_GET_ADDRESS_FAILED 903     // Initialization has not been completed yet. Failed to obtain the backend address. Please try again later.
	#define ER_PROXY_SQL_SIZE_ERROR_IN_GET_CANDIDATE_ADDRESS 904 // An error occurred while obtaining the backend address (the number of destination backend is incorrect)
	#define ER_PROXY_GET_ADDRESS_ERROR 905      // An error occurred while obtaining the backend address
	#define ER_PROXY_CANDIDATE_ADDRESS_EMPTY 906 // No backend address has been obtained
	#define ER_PROXY_CANT_GET_SOCK 907          // Failed to obtain the socket	
	#define ER_PROXY_GET_SET_SOCK_FAIL 908      // Failed to obtain the socket
	#define ER_PROXY_CONNECT_ERROR 909          // Backend connection failed
	#define ER_PROXY_NO_SQL_ASSIGN_TO_SET 910   // An exception occurred while sending SQL statements
	#define ER_PROXY_STATUS_ERROR 911           // The group is in an exceptional status and disconnected
	#define ER_PROXY_CONN_BROKEN_ERROR 912      // The server is closed and the SQL statement is in an exceptional status
	#define ER_PROXY_UNKNOWN_ERROR 913          // Unknown proxy error
	#define ER_PROXY_ALL_SLAVES_UNAVAILABLE 914 // All secondary servers are unavailable
	#define ER_PROXY_ALL_SLAVES_CHANGE 915      // The secondary server has an exception
	
	#define ER_PROXY_ERROR_END 916


>?Error code 900 and higher are system errors, which will be alarmed through the [Cloud Monitor platform](https://console.cloud.tencent.com/monitor/overview).
