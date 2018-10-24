
The life cycle of CDH refers to the states it experiences from launch to termination. Proper management of the state of a dedicated instance ensures that applications running on the instance provide services efficiently and economically.

### CDH State

| State | Attribute | Description |
|:-----:|:-------:|:-------|
| Creating | Intermediate state | The state after starting creation and before running. |
| Running | Steady state | Normal running state. CVM instances can be assigned on a CDH in this state. |
| Recycled | Steady state | The state when a prepaid CDH is moved into the recycle bin after expiry for more than 7 days. The CDH in this state cannot provide services. After renewed, it will move to the running state. |
| Terminated | Steady state | The termination operation is completed for a CDH which will no longer exist and cannot provide services with all data completely purged. |

### State Transition Graph
![State transition graph](https://main.qcloudimg.com/raw/32937760bb935e64aafe3ef1c770e578.png)
	

## CDH Recycling Mechanism

- Expiration alerts will be sent every other day 7 days before a prepaid CDH expires. The alert message will be sent through email and SMS to the creator of Tencent Cloud account and all collaborators.
- If the account balance is sufficient and you have already set up automatic renewal, the CDH will be automatically renewed upon expiry.
- If the CDH is not renewed before or upon expiry, the system will stop its service upon expiry. The CDH and all the **dedicated CVM instances on it will be shut down and disconnected from the network**, and the instance-related cloud disks will stop serving and only retain the data.
- You can renew and restore the CDH from the recycle bin within 7 days after expiry. If renewed during that period, the dedicated CVM instances on the CDH and associated networks and cloud disks will be available for service.
- If you fail to renew the CDH within 7 days after expiry, the system will release the resources at 00:00 on the 8th day after expiry, **all the dedicated CVM instances on the CDH will be terminated**, and the data in the instance-related local disks and cloud disks **will be irreversibly purged**.
