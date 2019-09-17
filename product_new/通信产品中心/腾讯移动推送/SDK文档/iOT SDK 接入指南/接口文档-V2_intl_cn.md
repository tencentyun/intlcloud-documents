# SDK API

SDK使用了一些系统资源，如线程、消息队列等。

## 数据接收回调函数
### 接口说明

SDK接收到推送数据时，通知给上层应用接口。

```c
typedef void (*xgAgentRecvDataCB_t)(uint8_t *data, uint32_t len)
```

### 参数说明
- data：透传后台推送的data字段数据，为json格式字符串。
- len：data字段所占字节数。

### 示例代码
```
void testRecvDataCB(uint8_t *data, uint32_t len)
{
    if(NULL != data) {
        printf("[demo Debug]$$$$$$$$$$$$$$$$$$$$$$$\n");
        printf("[demo Debug]Recv data %dByte: %s \n", len, data);
    }
}
```

## 状态通知回调函数
### 接口说明

SDK状态变化时，通知给上层应用接口。

```c
typedef void (*xgAgentStatusCB_t)(xgStatus_t status)
```

### 参数说明
- status：SDK的运行状态，详细信息如下：

```c
typedef enum {
	STATUS_IDEL,
	STATUS_GET_BROKER_SUCCESS,
	STATUS_CLOUD_CONNECTED,
	STATUS_CLOUD_DISCONNECT
}xgStatus_t;
```
说明：
- STATUS_IDEL：空闲状态
- STATUS_GET_BROKER_SUCCESS：获取broker信息成功。
- STATUS_CLOUD_CONNECTED：连接云端成功
- STATUS_CLOUD_DISCONNECT：与云端断开连接

### 示例代码
```c
void testStatusCB(xgStatus_t status)
{
    switch(status) {
        case STATUS_GET_BROKER_SUCCESS:
            printf("[demo Debug]We will go to connect xg cloud\n");
            xgAgentConnect();
            break;
        case STATUS_CLOUD_CONNECTED:
            printf("[demo Debug]We connect xg cloud success\n");
            break;
        case STATUS_CLOUD_DISCONNECT:
            printf("[demo Debug]We disconnect xg cloud\n");
            break;
        default:
            break;
    }
}
```

## SDK初始化
### 接口说明
用于SDK初始化、资源申请、获取云端broker信息等操作。

应用的accessID、accessKey、deviceName信息都需要在config参数中传入，更多说明见xgAgentConfig_t描述。

```c
void xgAgentInit(xgAgentConfig_t *config)
```
### 参数说明
- config：SDK的配置信息

```c
typedef struct {
	uint8_t accessKey[ACCESS_KEY_LEN+1];
	uint8_t deviceName[DEVICE_NAME_LEN+1];
	uint32_t accessID;
	xgAgentRecvDataCB_t recvCBFunc;
	xgAgentStatusCB_t statusCBFunc;
}xgAgentConfig_t;
```
说明：
- accessID：数字型，控制台创建的应用ID
- accessKey：字符型，控制台创建的应用Key
- deviceName：设备名称，一般使用mac或自行定义
- recvCBFunc：后台推送数据的回调通知
- statusCBFunc：SDK状态通知

### 示例代码
```c
xgAgentConfig_t config;

config.accessID = ACCESSID;
config.recvCBFunc = testRecvDataCB;
config.statusCBFunc = testStatusCB;
strcpy(config.accessKey, ACCESSKEY);
strcpy(config.deviceName, DEVICE_NAME);
xgAgentInit(&config);
```

## SDK退出
### 接口说明
用于SDK退出、资源释放、断开云端连接等操作。
```c
void xgAgentExit(void)
```

### 参数说明
- 无参数

### 示例代码
```c
xgAgentExit();
```

## 连接云端
### 接口说明
用于连接云端，需要在SDK状态为STATUS\_GET\_BROKER\_SUCCESS后调用。
```c
void xgAgentConnect(void)
```

### 参数说明
- 无参数

### 示例代码
```c
void testStatusCB(xgStatus\_t status)
{
switch(status) {
	case STATUS\_GET\_BROKER\_SUCCESS:
		printf("We will go to connect xg cloud\n";);
		xgAgentConnect();
	break;
	...
	default:
	break;
	}
}
```

## 与后台断开连接
### 接口说明

用于与云端断开连接。

```c
void xgAgentDisconnect(void)
```
### 参数说明
- 无参数

### 示例代码
```c
xgAgentDisconnect();
```
