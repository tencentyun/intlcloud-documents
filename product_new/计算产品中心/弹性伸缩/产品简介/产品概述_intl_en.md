
## What is Auto Scaling (AS)?
Auto Scaling (AS) can automatically adjust CVM computing resources according to configured policies and your business needs, ensuring that you always have the correct number of CVM instances available to handle the load of your applications. Intelligent scale-out and scale-in are important for cost control and resource management. When the traffic increases, you need to add more servers to process the additional load. When the traffic decreases, you need to terminate the unnecessary servers.

With AS, you only need to set up the conditions for scale-out and scale-in in advance. When the scale-out conditions are satisfied, AS will automatically add CVMs to maintain performance. When demand decreases, AS will remove CVMs according to the scale-in conditions. 

As shown in the following figures, Auto Scaling can help maintain the appropriate amount of resources, and keep your cluster stay in healthy status. You will get rid of the following troubles in the traditional model: 
 - Insufficient servers due to a surge in business or a CC attack, resulting in no response from your service
 - Estimation of resources based on peak access volume when the access volume rarely peaks, resulting in wasted resources
 - Personal surveillance and frequent handling of capacity alarms, which require multiple manual changes

**Traditional mode:**
![Alt text](https://mc.qcloudimg.com/static/img/92ae76d43c2b490f558490d328b8761a/AS-Product+Introduction%281%29.jpg)

**With AS:**
![Alt text](https://mc.qcloudimg.com/static/img/953c495c4b950e98fd6e360d871bf891/AS-Product+Introduction%282%29.jpg)


## How AS Works

In common Web application services, your cluster usually runs multiple copies of an application to meet client traffic, for example, the frontend server cluster at the access layer, the application server cluster at the logical layer, and the backend cache server cluster. Every instance can process client requests.

These instances are similar or identical and the quantity is usually adjustable. You can add them to one scaling group for easy management:

- Specify the minimum number of instances in each scaling group, and AS will ensure that the number of instances in the group is never less than the minimum.
- Specify the maximum number of instances in each scaling group, and AS will ensure that the number of instances in the group is never more than the maximum.
- Specify a scaling policy, and AS will launch or terminate instances when the demands of an application increase or decrease. There are two kinds of scaling policies:
   a) Dynamic scaling policy: Scale in or out dynamically according to specified conditions (for example, scale out when the CPU utilization of the CVM instances in the scaling group is larger than 60%)
   b) Scheduled scaling policy: Scale in or out at specified times (for example, scale out every day at 21:00) 
- After setting the scaling policy, you can also set the notification policies. When scaling occurs, AS informs you via e-mail, SMS and internal message. Rather than constantly focusing on your service traffic volume changes, you can just check the notifications from AS.
- You can also specify the number of machines required at any time, or add existing machines to the scaling group for joint management.

## Basic concepts of Auto Scaling

**Basic concepts related to Auto Scaling:**

- Scaling group
- Launch configuration
- Scaling policy
- Cooldown period


## 1. Scaling group
A scaling group contains a collection of CVM instances that follow the same policies and have a shared purpose. Scaling groups define attributes such as the maximum and minimum numbers of CVM instances in the group and their associated CLB instances.

## 2. Launch configuration
A launch configuration is the template for the automatic creation of CVMs. It contains the image ID, CVM instance type, system disk/data disk types and capacities, key pair, security group, etc.

When a scaling group is created, it must be specified and cannot be edited once created.

## 3. Scaling policy
A scaling policy defines the conditions for executing a scaling action. The trigger condition can be a time point or an alarm of cloud monitoring, and the action can be removing or adding a CVM.
There are two types of scaling policies:

- **Scheduled scaling policy**
CVM instances are automatically added or removed at a specified point in time, which can be performed on a periodic basis.

- **Dynamic scaling policy**
CVM instances are automatically added or removed based on cloud monitoring metrics such as CPU, memory, and network traffic.

## 4. Cooldown period
Cooldown period refers to the locking duration after one scaling activity (addition or removal of CVM instances) is executed in a scaling group. The scaling group does not perform scaling activities during this duration. The cooldown period can be specified as between 0-999999 (seconds).
