## Prerequisites
You have created a cluster, a table group and the `PLAYERONLINECNT` table.

The description file [table_test.xml](https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/table_test.xml) of the `PLAYERONLINECNT` table is as follows:
```
<?xml version="1.0" encoding="GBK" standalone="yes" ?>
<metalib name="tcaplus_tb" tagsetversion="1" version="1">
<struct name="PLAYERONLINECNT" version="1" primarykey="TimeStamp,GameSvrID" splittablekey="TimeStamp">
    <entry name="TimeStamp"         type="uint32"     desc="Measured in minutes" />
    <entry name="GameSvrID"         type="string"     size="64" />
    <entry name="GameAppID"         type="string"     size="64" desc="gameapp id" />
    <entry name="OnlineCntIOS"      type="uint32"     defaultvalue="0" desc="The number of iOS online users" />
    <entry name="OnlineCntAndroid"  type="uint32"     defaultvalue="0" desc="The number of Android online users" />
    <entry name="BinaryLen"         type="smalluint" defaultvalue="1" desc="Data length of the data source; skip the source check when the length is 0."/>
    <entry name="binary"            type="tinyint"     desc="Binary" count= "1000" refer="BinaryLen" />
    <entry name="binary2"           type="tinyint"     desc="Binary 2" count= "1000" refer="BinaryLen" />
    <entry name="strstr"            type="string"     size="64" desc="String"/>
    <index name="index_id"  column="TimeStamp"/>
</struct>
</metalib>
```

## Step 1: Define configuration parameters
```
// Access address of the target cluster
static const char DIR_URL_ARRAY[][TCAPLUS_MAX_STRING_LENGTH] =
{
   "tcp://10.191.***.99:9999",
   "tcp://10.191.***.88:9999"
};
// The number of target cluster addresses
static const int32_t DIR_URL_COUNT = 2;
// Cluster ID of the target business
static const int32_t APP_ID = 3;
// Table group ID of the target business
static const int32_t ZONE_ID = 1;
// Target business password
static const char * SIGNATURE = "*******";
// Table name "PLAYERONLINECNT" of the target business
static const char * TABLE_NAME = "PLAYERONLINECNT";
```

## Step 2: Initialize TcaplusAPI log handles
Log configuration file: [tlogconf.xml](https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/tlogconf.xml)
```
// TCaplus service log class
TcaplusService::TLogger* g_pstTlogger;
LPTLOGCATEGORYINST g_pstLogHandler;
LPTLOGCTX g_pstLogCtx;
int32_t InitLog()
{
    // Absolute path of the log configuration file
    const char* sLogConfFile = "tlogconf.xml";
    // Log class name
    const char* sCategoryName = "mytest";
    // Initialize the log handle using the configuration file
    g_pstLogCtx = tlog_init_from_file(sLogConfFile);
    if (NULL == g_pstLogCtx)
    {
        fprintf(stderr, "tlog_init_from_file failed.\n");
        return -1;
    }
    // Get the log class
    g_pstLogHandler = tlog_get_category(g_pstLogCtx, sCategoryName);
    if (NULL == g_pstLogHandler)
    {
        fprintf(stderr, "tlog_get_category(mytest) failed.\n");
        return -2;
    }
    // Initialize the log handle
    g_pstTlogger = new TcaplusService::TLogger(g_pstLogHandler);
    if (NULL == g_pstTlogger)
    {
        fprintf(stderr, "TcaplusService::TLogger failed.\n");
        return -3;
    }
 
    return 0;
}
```

## Step 3: Initialize TcaplusAPI client
```
// The client main class of the TCaplus service API
TcaplusService::TcaplusServer g_stTcapSvr;
// Meta information for the table
extern unsigned char g_szMetalib_tcaplus_tb[];
LPTDRMETA g_szTableMeta = NULL;
int32_t InitServiceAPI()
{
    // Initialize
    int32_t iRet = g_stTcapSvr.Init(g_pstTlogger, /*module_id*/0, /*app id*/APP_ID, /*zone id*/ZONE_ID, /*signature*/SIGNATURE);
    if (0 != iRet)
    {
        tlog_error(g_pstLogHandler, 0, 0, "g_stTcapSvr.Init failed, iRet: %d.", iRet);
        return iRet;
    }
 
    // Add the directory server
    for (int32_t i = 0; i< DIR_URL_COUNT; i++)
    {
        iRet = g_stTcapSvr.AddDirServerAddress(DIR_URL_ARRAY[i]);
        if (0 != iRet)
        {
            tlog_error(g_pstLogHandler, 0, 0, "g_stTcapSvr.AddDirServerAddress(%s) failed, iRet: %d.", DIR_URL_ARRAY[i], iRet);
            return iRet;
        }
    }  
 
    // Get the meta description of the table
    g_szTableMeta = tdr_get_meta_by_name((LPTDRMETALIB)g_szMetalib_tcaplus_tb, TABLE_NAME);
    if(NULL == g_szTableMeta)
    {
        tlog_error(g_pstLogHandler, 0, 0,"tdr_get_meta_by_name(%s) failed.", TABLE_NAME);
        return -1;
    }
 
    // Register the data table (connect to the directory server, verify the password, and get the table routing) with 10-second timeout period
    iRet = g_stTcapSvr.RegistTable(TABLE_NAME, g_szTableMeta, /*timeout_ms*/10000);
    if(0 != iRet)
    {
        tlog_error(g_pstLogHandler, 0, 0, "g_stTcapSvr.RegistTable(%s) failed, iRet: %d.", TABLE_NAME, iRet);
        return iRet;
    }
 
    // Connect to all TcaplusDB proxy servers corresponding to the table
    iRet = g_stTcapSvr.ConnectAll(/*timeout_ms*/10000, 0);
    if(0 != iRet)
    {
        tlog_error(g_pstLogHandler, 0, 0, "g_stTcapSvr.ConnectAll failed, iRet: %d.", iRet);
        return iRet;
    }
 
    return 0;
}
```

## Step 4. Send a delete request via the API
```
int32_t SendDeleteRequest()
{
    // Request object class
    TcaplusService::TcaplusServiceRequest* pstRequest = g_stTcapSvr.GetRequest(TABLE_NAME);
    if (NULL == pstRequest)
    {
        tlog_error(g_pstLogHandler, 0, 0, "g_stTcapSvr.GetRequest(%s) failed.", TABLE_NAME);
        return -1;
    }
 
    // Initialize the request object
    int iRet = pstRequest->Init(TCAPLUS_API_DELETE_REQ, NULL, 0, 0, 0, 0);
    if(0 != iRet)
    {
        tlog_error(g_pstLogHandler, 0, 0, "pstRequest->Init(TCAPLUS_API_DELETE_REQ) failed, iRet: %d.", iRet);
        return iRet;
    }
 
    // Add a record to the table according to the request
    TcaplusService::TcaplusServiceRecord* pstRecord = pstRequest->AddRecord();
    if (NULL == pstRecord)
    {
        tlog_error(g_pstLogHandler, 0, 0, "pstRequest->AddRecord() failed.");
        return -1;
    }
 
    PLAYERONLINECNT stPLAYERONLINECNT;
    memset(&stPLAYERONLINECNT, 0, sizeof(stPLAYERONLINECNT));
 
    // Specify the information of the key to be deleted
    stPLAYERONLINECNT.dwTimeStamp = 1;
    snprintf(stPLAYERONLINECNT.szGameSvrID, sizeof(stPLAYERONLINECNT.szGameSvrID), "%s", "mysvrid");
 
         
    // Set the record based on the TDR description
    iRet = pstRecord->SetData(&stPLAYERONLINECNT, sizeof(stPLAYERONLINECNT));
    if(0 != iRet)
    {
        tlog_error(g_pstLogHandler, 0, 0, "pstRecord->SetData() failed, iRet: %d.", iRet);
        return iRet;
    }
 
    // Send the request packet
    iRet= g_stTcapSvr.SendRequest(pstRequest);
    if(0 != iRet)
    {
        tlog_error(g_pstLogHandler, 0, 0, "g_stTcapSvr.SendRequest failed, iRet: %d.", iRet);
        return iRet;
    }
    return 0;
}
```

## Step 5. Receive the response via the API
```
int RecvResp(TcaplusServiceResponse*& response)
{
    // Block the reception of response packets 5,000 times with each block lasting for 1 ms
    unsigned int sleep_us = 1000;
    unsigned int sleep_count = 5000;
    do
    {
        usleep(sleep_us);
        response = NULL;
        int ret = g_stTcapSvr.RecvResponse(response);
        if (ret < 0)
        {
            tlog_error(g_pstLogHandler, 0, 0, "tcaplus_server.RecvResponse failed. ret:%d", ret);
            return ret;
        }
 
        // Receive a response packet
        if (1 == ret)
        {
             break;
        }
    } while ((--sleep_count) > 0);
 
    // Timeout period: 5 seconds
    if (0 == sleep_count)
    {
        tlog_error(g_pstLogHandler, 0, 0, "tcaplus_server.RecvResponse wait timeout.");
        return -1;
    }
    return 0;
}
```

## Samples
Please refer to [main.cpp](https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/main_tdr.cpp).
```
int main(void) {
    // Initialize the log
    int ret = InitLog();
    if ( ret != 0)
    {
        printf("init log failed\n");
        return -1;
    }
 
    // Initialize the API client
    ret = InitServiceAPI();
    if ( ret != 0)
    {
        printf("init InitServiceAPI failed\n");
        return -1;
    }
 
    // Send the request
    ret = SendDeleteRequest();
    if (0 != ret)
    {
        printf("SendDeleteRequest failed\n");
        return -1;
    }
     
    // Receive the response
    TcaplusServiceResponse* response = NULL;
    ret = RecvResp(response);
    if (0 != ret)
    {
        printf("RecvResp failed\n");
        return -1;
    }
     
    // Get the result, where "0" indicates success
    int32_t result = response->GetResult();
    if (0 != result)
    {
        printf("the result is %d\n", result);
        return -1;
    }
     
    return 0;
}
```
