
This document describes how to send custom messages by using API.

## Sending Custom Messages
To invoke this API, the room type must be **Standard** (ITMG_ROOM_TYPE_STANDARD) or **High quality** (ITMG_ROOM_TYPE_HIGHQUALITY). The mic of the sender must be turned on, and the receiver allows downstream.

### API Prototype

```
//iOS API
-(int) SendCustomData:(NSData *)data repeatCout:(int)reaptCout;
//Unity API
public abstract int SendCustomData(byte[] customdata,int repeatCout);
```

### Parameter description

| Parameter   | Type   | Description   |
|----------|-------|-------|
|data       |NSData *   |Message to be delivered|
|reaptCout  |int        |Repeat times. `-1` indicates to resend unlimitedly|

### Return value
**QAV_OK**: The call is successful.

**1004**: Parameter error. **1201**: The room does not exist.

For more error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/607/33223).

### Sample code

**Executed statements**

```
-(IBAction)SendCustData:(UIButton*)sender {
    int ret = 0;
    NSString *typeString;
    switch (sender.tag) {
        case 1:
            ret = [[[ITMGContext GetInstance] GetRoom] SendCustomData:[NSData dataWithBytes:_shareRoomID.text.UTF8String length:_roomIdText.text.length] repeatCout:_shareOpenID.text.intValue];
            typeString = @"sendCustData";
            break;
          case 2:
            ret = [[[ITMGContext GetInstance] GetRoom] StopSendCustomData];
            typeString = @"recvCustData";
            break;
        default:
            break;
    }
    if(ret != 0) {
        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"set fail" message:[NSString stringWithFormat:@"%@:errorcode :%d",typeString,ret] delegate:NULL cancelButtonTitle:@"OK" otherButtonTitles:nil];
        [alert show];
    }
}
```

**Callback**
```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSString* log =[NSString stringWithFormat:@"OnEvent:%d,data:%@", (int)eventType, data];
    switch (eventType) {
                 case   ITMG_MAIN_EVENT_TYPE_CUSTOMDATA_UPDATE: {
            if (ITMG_CUSTOMDATA_AV_SUB_EVENT_UPDATE == ((NSNumber *)data[@"sub_type"]).intValue) {
                UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"customdata" message:[NSString stringWithFormat:@"content:%@,from:%@ ",data[@"content"],data[@"senderid"]] delegate:NULL cancelButtonTitle:@"OK" otherButtonTitles:nil];
                                    [alert show];
            }
        }
            break;
    }
}
```


## Stop Sending Custom Messages
Call this API to stop sending custom messages

### API Prototype

```
//iOS API
-(int) StopSendCustomData;
//Unity API
public abstract int StopSendCustomData();
```

### Return value

**1003**: There is an ongoing task.
