

### Access ID
Unique identifier of an application; cannot be modified.

### Access Key
Client authentication key, used together with an access ID to verify whether a call is valid; cannot be modified.


### Tag
Tag configured for a certain user or a group of users. Custom tags can be configured through client or server calls and then used at the frontend.

### System Preset Tag
Tag that TPNS presets for specific users directly by sorting data. System preset tags are for use only and cannot be edited or deleted.


### Push Content
A message command is the code that is received and executed by an application. The specific code format is defined by application developers. By using message commands, you can remotely control application activities. For example, you can use message commands to download applications, change the startup flickering screen, modify item prices in mobile games, and silently update text or images in applications.

### Immediate/Scheduled Push
Immediate push is suitable for push testing. Scheduled push is often used for official external push.

### Additional Parameters
You can customize key-value pairs to implement custom requirements.

### Offline Retention
Content pushed when users are offline can be retained for a specified period of time, which is called the offline retention period. The users can receive the pushed content only if they get online within the offline retention period. For activities that do not have time limits, it is highly recommended that you set the offline retention period to 72 hours.

 
 

### Click Event
Response action performed after a user clicks a notification. The action can be directly opening the application, opening a feature page of the application, or accessing a URL with browser.

### Multi-Package Name Push
In multi-package name push mode, all applications on devices that use the same access ID to register with the push service will receive messages. This feature is used to differentiate applications from different channels and with different package names.



### Message ID
ID of a push task.

### Push Time
Time to start push.

 
 



### Planned Push Count
Number of pushes sent within the past 30 days to devices that were connected to the server. If offline retention is configured for the message, the number of effective pushes will increase over time as users go online, which means that users who just get online also receive this push.

### Online Device Count
Number of devices connected to the server within the push validity period (messages can be successfully pushed only after the devices are connected to the server).

### Device Arrival Count
Number of users to whom a message is pushed successfully. There is a 5-minute delay before real-time data is generated.

### Display Count
Number of messages that are displayed via the system's message display API.

### Click Count
Total number of clicks on a message that is successfully pushed. Devices need to call a specific function to report the click count.

### Clear Count
Number of messages that are cleared via the system’s message clearing API.


