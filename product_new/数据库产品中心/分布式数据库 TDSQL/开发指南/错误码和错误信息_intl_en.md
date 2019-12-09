
> If you want to view or download the full set of development documents, see [Development Guide for TDSQL](https://intl.cloud.tencent.com/document/product/1042/33352).


## Error Codes and Error Messages

The following new error codes have been added for TDSQL:
```
	    ER_PROXY_GRAM_ERROR_BEGIN=800,

	    ER_PROXY_SANITY_ERROR,         /*Incorrect SQL type*/
	    ER_PROXY_BAD_COMMAND,          /*Unsupported SQL command*/
	    ER_PROXY_SQL_NOT_SUPPORT,      /*Type not supported by TDSQL*/
	    ER_PROXY_SQLUSE_NOT_SUPPORT,   /*Operation not supported by TDSQL*/
	    ER_PROXY_ERROR_SHARDKEY,       /*The primary and secondary shardkeys was misselected; for example, they should be different and should be certain columns in the table*/

	    ER_PROXY_ERROR_SUB_SHARDKEY,   /*Not used for now*/
	    ER_PROXY_PRE_DEAL_ERROR,       /*Non-compliant join*/
	    ER_PROXY_SHADKEY_ERROR,        /*Complex SQL. The shardkey should be included for a derived table.*/
	    ER_PROXY_COMBINE_SQL_ERROR,    /*SQL recombination error; for example, there is no corresponding secondary sharded table*/
	    ER_PROXY_SQL_ERROR,            /*General SQL error*/
	    ER_PROXY_ONE_SET,              /*count (distinct) must be sent to only one set*/
	    ER_PROXY_STRICT_ERROR,         /*Not used for now*/
	    ER_PROXY_TRANSACTION_ERROR,    /*Transaction error*/


	    ER_PROXY_GRAM_ERROR_END,  /*Syntax error*/

	    ER_PROXY_SYSTEM_ERROR_BEGIN=900,/*System error. When this type of errors occurs, the TDSQL team will receive alarms*/

	    ER_PROXY_SLICING,
	    ER_PROXY_NO_DEFAULT_SET,       /*Set is empty*/
	    ER_PROXY_SOCK_ADDRESS_ERROR,   /*Set address is empty*/
	    ER_PROXY_SOCK_ERROR,           /*Failed to connect to the backend database*/
	    ER_PROXY_STATUS_ERROR,         /*Group status error*/
	    ER_PROXY_UNKNOWN_ERROR,        /*Unknown error*/

      ER_PROXY_LOG_GTID_TIMEOUT,     /*Log write timed out during two-phase commit*/
      ER_PROXY_LOG_GTID_ERROR,       /*Log write timed out during two-phase commit*/
      ER_PROXY_COMMIT_TEMP_ERROR,    /*A temporary error occurred during two-phase commit. The agent will eventually automatically commit the transaction*/
      ER_PROXY_ABORT_TEMP_ERROR,     /*A temporary error occurred when the transaction was rolled back. The agent will eventually automatically roll back the transaction*/
      ER_PROXY_SQL_RETRY,
      ER_PROXY_CONN_BROKEN_ERROR,    /*The connection between the gateway and the backend DB is broken*/
```
