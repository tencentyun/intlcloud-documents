CloudAudit has two features: Operation Record and Tracking Set.
## Operation Record  
This feature records the operations a user performed under the Tencent Cloud account in the last 7 days.
- **Operation Record List**
You can view the operation record list as well as the operation event time, user name, event name, resource type, resource name and other information via the console.
- **Operation Record Details**
You can also obtain the details of a single operation record, including access key, region, error code, event ID, event name, event source, event time, request ID, source IP address and user name.

## Tracking Set  
Tracking set is an enhanced feature of operation record. It allows customers to ensure the traceability and security of enterprise personnel's operations on assets. It includes such information as operation log type and path. When your tracking set is in a normal state, it stores the operation log records under your account to the bucket configured for the tracking set; when your tracking set is closed, the operation log will not be stored to the bucket. 



### Tracking set operations  
You can perform the following operations on tracking set: create and delete tracking set; edit the configuration of tracking set; disable the tracking set's logging feature.
> **Note:**
> You can only create one tracking set during trial period of CloudAudit.

### Advanced features of tracking set  
#### Set log file prefix
This is the log file prefix stored in COS.
It is used to specify the parent directory of TencentLogs.
If you specify a prefix of "test", the log path becomes: `/test/Year/Month/Day`, for example:
```
/test/2017/11/02
```
Log file naming convention: `year/month/day/time (down to the hash value of minute).gz
`, for example:
```
201711021635_26c6f84d-bd41-4211-a9d4-2c223e31295d_0.gz
```




  


