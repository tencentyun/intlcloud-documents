## Prerequisites
You have created a cluster, a table group, and the `tb_online` table.

The description file [table_test.proto](https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/table_test.proto) of the `tb_online` table is as follows ([tcaplusservice.optionv1.proto](https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/tcaplusservice.optionv1.proto) is the dependent table):

```
syntax = "proto2";
 
package myTcaplusTable;
 
import "tcaplusservice.optionv1.proto";
 
message tb_online {
    option(tcaplusservice.tcaplus_primary_key) = "openid,tconndid,timekey";
 
    required int32 openid = 1; //QQ Uin
    required int32 tconndid = 2;
    required string timekey = 3;
    required string gamesvrid = 4;
    optional int32 logintime = 5 [default = 1];
    repeated int64 lockid = 6 [packed = true]; // The `repeated` fields should use the `packed` modifier.
    optional pay_info pay = 7;
 
    message pay_info {
        optional uint64 total_money = 1;
        optional uint64 pay_times = 2;
    }
}
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
// Table name "tb_online" of the target business
static const char * TABLE_NAME = "tb_online";
```

## Step 2: Initialize the TcaplusDB API client for Protobuf
```
// TcaplusDB API client for Protobuf
TcaplusAsyncPbApi g_stAsyncApi;
int32_t InitAsyncPbApi()
{
    // TcaplusDB API for Protobuf configuration
    ClientOptions cfg;
    cfg.app_id = APP_ID;
    cfg.zones.push_back(ZONE_ID);
    strcpy(cfg.signature, SIGNATURE);
    for (int32_t i = 0; i < DIR_URL_COUNT; i++)
    {
        cfg.dirs.push_back(DIR_URL_ARRAY[i]);
    }
    // The Protobuf table to be accessed
    cfg.tables.push_back(TABLE_NAME);
    // Log configuration
    strncpy(cfg.log_cfg, "tlogconf.xml", sizeof(cfg.log_cfg));
    // Timeout period for connection initialization: 5 seconds
    cfg.timeout = 5000;
     
    // Initialize connection
    int32_t iRet = g_stAsyncApi.Init(cfg);
    if (0 != iRet)
    {
        cout << "ERROR: g_stAsyncApi.Init failed, log cfg: " << cfg.log_cfg << ", iRet: " << iRet << "." << endl;
        return iRet;
    }
    return iRet;
}
```

## Step 3. Define asynchronous callbacks
```
// Count the number of received response messages
uint32_t g_dwTotalRevNum = 0;
class CommonCallback : public TcaplusPbCallback
{
public:
    CommonCallback()
    {
        cout << "Init CommonCallback." << endl;
    }
     
    ~CommonCallback()
    {
        cout << "Fini ~CommonCallback." << endl;
    }
    // A callback for the received response message, and "msgs" is an array of the received records
    int OnRecv(const std::vector< ::google::protobuf::Message *> &msgs)
    {
        cout << "OnRecv[" << msgs.size() << endl;
        g_dwTotalRevNum++;
        for (size_t idx = 0; idx < msgs.size(); idx++)
        {
            tb_online* t = dynamic_cast<tb_online *>(msgs[idx]);
            if (NULL == t)
            {
                cout << "ERROR: msgs[" << idx << "] not tb_online type." << endl;
                return -1;
            }
             
            cout << "---------- receive a response----------:" << endl;
            cout << "openid=" << t->openid() << endl;
            cout << "tconndid=" << t->tconndid() << endl;
            cout << "timekey=" << t->timekey() << endl;
            cout << "gamesvrid=" << t->gamesvrid() << endl;
            cout << "logintime=" << t->logintime() << endl;
            for (int32_t i = 0; i < t->lockid_size();i++)
            {
                cout << "lockid[" << i << "]=" << t->lockid(i) << endl;
            }
            tb_online_pay_info pay = t->pay();
            cout << "pay total_money=" << pay.total_money() << "; pay_times=" << pay.pay_times() << endl;
             
            // Get the version of the record
            std::string version;
            int iRet = g_stAsyncApi.GetMessageOption(*t, NS_TCAPLUS_PROTOBUF_API::MESSAGE_OPTION_DATA_VERSION, &version);
            cout << "after GetMessageOption iRet= [" << iRet << "] version:" << version.c_str() << " msg:" << t << endl;
        }
         
        return 0;
    }
     
    // A callback for a response error
    int OnError(const std::vector< ::google::protobuf::Message *> &msgs, int errorcode)
    {
        cout << "OnError[" << msgs.size() << endl;
        g_dwTotalRevNum++;
        for (size_t idx = 0; idx < msgs.size(); idx++)
        {
            tb_online* t = dynamic_cast<tb_online *>(msgs[idx]);
            if (NULL == t)
            {
                cout << "ERROR: msgs[" << idx << "] not tb_online type." << endl;
                return -1;
            }
             
            if (TcapErrCode::TXHDB_ERR_RECORD_NOT_EXIST == errorcode)
            {
                cout << "ERROR: openid= " << t->openid() << ", tconndid= " << t->tconndid() << ", timekey= " << t->timekey() << ", record not exists" << endl;
            }
            cout << "ERROR: openid = [" << t->openid() << "], tconndid = [" << t->tconndid() << "], timekey =[" << t->timekey() << "] failed:%d"  << errorcode << endl;
        }
         
        return 0;
    }
 
    // A callback for a timed-out message
    int OnTimeout(const std::vector< ::google::protobuf::Message *> &msgs)
    {
        cout << "OnTimeout[" << msgs.size() << endl;
        for (size_t idx = 0; idx < msgs.size(); idx++)
        {
            tb_online* t = dynamic_cast<tb_online *>(msgs[idx]);
            if (NULL == t)
            {
                cout << "TIMEOUT: msgs[" << idx << "] not tb_online type!" << endl;
                return -1;
            }
             
            cout << "TIMEOUT: openid = [" << t->openid() << "], tconndid = [" << t->tconndid() << "], timekey =[" << t->timekey() << "] timeout" << endl;
        }
         
        return 0;
    }
     
    int OnFinish(const NS_TCAPLUS_PROTOBUF_API::MsgParam &param)
    {
        cout << "OnFinish: " << param.m_nOperation << " req: " << param.m_vecMsgs.size()<< endl;
        return 0;
    }
};
```

## Step 4. Send the delete request
```
int SendDelRequest()
{
    static tb_online t;
    t.set_openid(1);
    t.set_tconndid(1);
    t.set_timekey("test_tcaplus");
 
    static CommonCallback cb;
    std::string version = "-1";
    g_stApi.SetMessageOption(t, NS_TCAPLUS_PROTOBUF_API::MESSAGE_OPTION_DATA_VERSION, version);
    int32_t iRet = g_stAsyncApi.Del(&t, &cb);
    if (iRet != TcapErrCode::GEN_ERR_SUC)
    {
        cout << "ERROR: openid= " << t.openid() << ", tconndid= " << t.tconndid() << ", timekey= " << t.timekey() << ", Delete Error iRet = " << iRet << endl;
        return -1;
    }
    return 0;
}
```

## Samples
```
int main(void) {
 
    // Initialize the API client
    int ret = InitAsyncPbApi();
    if ( ret != 0)
    {
        printf("InitAsyncPbApi failed\n");
        return -1;
    }
 
    // Send the request
    ret = SendDelRequest();
    if (0 != ret)
    {
        printf("SendDelRequest failed\n");
        return -1;
    }
     
    // Receive the response
    do
    {
        // Update and receive the response packet
        g_stAsyncApi.UpdateNetwork();
        usleep(1000 * 10);
    } while (g_dwTotalRevNum != 1);
    return 0;
}
```
