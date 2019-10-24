# SDK API

SDK uses several system resources, such as threads and CMQ.

## Data callback function
### API Description

When SDK receives the push data, it notifies the application layer API.

```c
typedef void (*xgAgentRecvDataCB_t)(uint8_t *data, uint32_t len)
```

### Parameter Description
- data: Pass through backend push data field data. This is a json format string.
- len: Number of bytes in the data field.

### Sample Code
```
void testRecvDataCB(uint8_t *data, uint32_t len)
{
    if(NULL != data) {
        printf("[demo Debug]$$$$$$$$$$$$$$$$$$$$$$$\n");
        printf("[demo Debug]Recv data %dByte: %s \n", len, data);
    }
}
```

## Status notification callback feature
### API Description

When SDK status changes, it notifies the application layer API.

```c
typedef void (*xgAgentStatusCB_t)(xgStatus_t status)
```

### Parameter Description
- status: SDK operating status. The details are as follows:

```c
typedef enum {
	STATUS_IDEL,
	STATUS_GET_BROKER_SUCCESS,
	STATUS_CLOUD_CONNECTED,
	STATUS_CLOUD_DISCONNECT
}xgStatus_t;
```
Descriptions:
- STATUS_IDEL: Idle status.
- STATUS_GET_BROKER_SUCCESS: Broker information obtained successfully.
- STATUS_CLOUD_CONNECTED: Connected to the cloud successfully.
- STATUS_CLOUD_DISCONNECT: Disconnected from the cloud.

### Sample Code
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

## SDK Initialization
### API Description
Used for operations such as initializing SDK, applying for resources, and obtaining broker information.

In the config parameter, accessID, accessKey, and deviceName of the application must be passed in. For more information, see the xgAgentConfig_t description.

```c
void xgAgentInit(xgAgentConfig_t *config)
```
### Parameter Description
- config：SDK configuration information.

```c
typedef struct {
	uint8_t accessKey[ACCESS_KEY_LEN+1];
	uint8_t deviceName[DEVICE_NAME_LEN+1];
	uint32_t accessID;
	xgAgentRecvDataCB_t recvCBFunc;
	xgAgentStatusCB_t statusCBFunc;
}xgAgentConfig_t;
```
Descriptions:
- accessID: The application ID is created in the console and has numeric characters.
- accessKey: The application Key is created in the console and has alphabetic characters.
- deviceName: The device name is generally mac but can also be customized.
- recvCBFunc: Backend push data callback notification.
- statusCBFunc: SDK status notification

### Sample Code
```c
xgAgentConfig_t config;

config.accessID = ACCESSID;
config.recvCBFunc = testRecvDataCB;
config.statusCBFunc = testStatusCB;
strcpy(config.accessKey, ACCESSKEY);
strcpy(config.deviceName, DEVICE_NAME);
xgAgentInit(&config);
```

## Exiting the SDK
### API Description
Used to perform operations such as exiting the SDK, releasing resources, and disconnecting from the cloud.
```c
void xgAgentExit(void)
```

### Parameter Description
- No parameter

### Sample Code
```c
xgAgentExit();
```

## Connecting to the cloud
### API Description
Used to connect to the cloud. You can call this after the SDK status becomes STATUS\_GET\_BROKER\_SUCCESS.
```c
void xgAgentConnect(void)
```

### Parameter Description
- No parameter

### Sample Code
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

## Disconnecting from the backend
### API Description

Used to disconnect from the cloud.

```c
void xgAgentDisconnect(void)
```
### Parameter Description
- No parameter

### Sample Code
```c
xgAgentDisconnect();
```
