### Auto Scaling 
Auto Scaling is a managerial service that automatically adjusts elastic compute resources based on user's business needs and policies.
### Scaling Group 
A scaling group contains a collection of CVM instances that follow the same policies and have a shared purpose. It defines attributes such as the maximum and minimum numbers of CVM instances in the group and their associated CLB instances.
### Launch Configuration 
A launch configuration is a template for automatically creating a CVM instance, containing information about the image ID, CVM instance type, types and capacities of system and data disks, key pair, and security group.

When a scaling group is created, it must be specified and cannot be edited once created.

### Alarm-based Scaling 
The automatic addition and removal of CVM instances based on Cloud Monitor metrics such as CPU, memory, and network traffic.

### Scheduled Action
Scheduled Action is one of the ways to perform automatic scaling. CVM instances will be automatically added or removed at a specified time point, which can be performed on a periodic basis.
### Scaling Policy 
A Scaling Policy is a triggering condition (e.g., a time point or an alarm from Cloud Monitor) for performing a scaling action such as removing or adding a CVM instance
### Scheduled Scaling Policy 
The automatic addition and removal of CVM instances at a specified time point, which can be performed on a periodic basis.

### Cooldown Period 
A cooldown period refers to the period of lockdown after a scaling action is completed in the same scaling group.




