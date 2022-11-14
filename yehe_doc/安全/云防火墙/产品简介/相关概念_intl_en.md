## **Network perimeter**
The network perimeter is the boundary between the Internet and Tencent Cloud's internal network. The network perimeter traffic, also known as north-south traffic, is the traffic generated during communication between cloud assets and the Internet.
North-south traffic is the traffic between public IP addresses and can be divided into "outbound traffic" and "inbound traffic" according to the direction.
- **Outbound traffic**: The traffic generated when cloud assets communicate with the Internet through the bound public IP address.
- **Inbound traffic**: The traffic generated when the Internet communicates with the cloud assets.

## **Edge firewall**
The edge firewall is a firewall for clusters that monitors north-south traffic. It defends the boundary between the assets associated with your EIP and the Internet, as shown in the image below:


![](https://qcloudimg.tencent-cloud.cn/raw/8cf4091e3eb39aab49476b758282c5af.jpg)

The edge firewall offers access control and log audit. Thanks to its built-in intrusion defense module and default cluster deployment, the firewall is out-of-the-box and easy to scale without complex network configurations and image installation.

## Virtual Private Cloud

Virtual Private Cloud (VPC) is a custom and logically isolated network space on Tencent Cloud. Similar to a traditional network running in an IDC, your VPC hosts your cloud resources including CVM, CLB, and CDB.

A VPC offers you:
- **EIP**: Used to access the Internet.
- **Peering Connection**: Supports communication between VPCs. For more information, please see [Peering Connection Documentation](https://intl.cloud.tencent.com/document/product/553).
- **Cloud Connect Network (CCN)**: Supports communication between VPCs. For more information, please see [Cloud Connect Network Documentation](https://intl.cloud.tencent.com/document/product/1003).

Cloud VPC connection can be achieved with Peering Connection and CCN, and the traffic between 2 VPCs is called east-west traffic. For more information, please see [Virtual Private Cloud Documentation](https://intl.cloud.tencent.com/document/product/215).

## Inter-VPC firewall
The inter-VPC firewall is a distributed firewall that monitors east-west traffic between VPCs. It defends the boundary between two VPCs, as shown in the image below: 

![](https://qcloudimg.tencent-cloud.cn/raw/046aa53505739449cca390720292b5fe.jpg)

Inter-VPC firewall is deployed between two VPCs connected through Peering Connection and CCN, and offers access control, topology visualization, log audit, exclusive resource configuration, and other features. Besides, it is out-of-the-box without complex routing configurations and image installation.

## Access control
Access control is a collection of traffic filtering rules. An access control list contains all the rules for the same type of traffic. Each access control rule is composed of the rule body and description:
- **Rule body**: Allow or block communication from the port of a specified address to the port of another address over a specific protocol.
  - **Access source**: The address of the source, and it is usually an IP address.  
  - **Access destination**: The address of the destination, and it can be an IP address or a domain name.
  - **Destination port**: The destination port of the communication.
  - **Protocol**: The network protocol used for the communication.
  - **Policy**: For traffic that matches the above 4 conditions specified in a rule, one of the following operations is performed according to the policy of the rule.
    - **Allow**: Allows access, and will record traffic logs, but not rule hit logs.
    - **Observe**: Allows access, and will record both traffic and rule hit logs.
    - **Block**: Denies access, and will record rule hit logs, but not traffic logs.
- **Rule description**: Describes the purpose of this access control rule.

>!A reasonable and standard rule description makes the rule more readable, while reducing maintenance costs and improving efficiency.

## Rule priorities

The priority indicates a rule's position in the list and 1 indicates the top priority. For any data flows that go through the firewall, Cloud Firewall (CFW) matches them with the rules according to the list from top to bottom:

- If a data flow matches a rule, matching will stop and the corresponding policy is applied.
- If a data flow does not match the current rule, CFW will try to match it with the next rule.
- If a data flow does not match any of the rules, it is allowed.
- In an access control list, the priority is an integer that ranges from 1 to n, where 1 indicates the highest priority and n is the total number of rules or the lowest priority in the current rule list. Generally, the priority of a general rule with wildcards is set to n.
- The priorities conform to the principles of <strong>continuity and uniqueness</strong>.
  - Continuity: The priorities must be consecutive positive integers. If the total number of rules is n, the maximum priority value is n.
  - Uniqueness: A rule list cannot contain duplicate priorities.
  - The following rules ensure the continuity and uniqueness of priorities:
    - If a new rule is added to the list, its priority is n+1.
    - If a new rule is inserted into the list, its priority is set to that of the original rule at the position, and the priorities of all the following rules automatically increase by 1.
    - When you edit a rule, you can move the rule by modifying its priority to that of the rule at the target position within the range of 1 to n. After you enter the new priority, the rule is moved to that position, and the priorities of all the following rules automatically increase by 1.



## Intrusion defense

Intrusion defense is designed to monitor network transmission and detect suspicious activities. When a suspicious event is detected, the system will send an alert or take proactive measures. CFW has integrated Tencent Cloud's threat intelligence, basic protection, and virtual patching features. By performing real-time monitoring, statistics, and analysis on your network perimeter traffic, it can help detect intrusion, malicious outgoing requests, and other unknown risks, and offer real-time protection and alerts.

## Logs
- **Rule hit logs**: Records the rule hits to help O&M specialists with security audit. The rule matching logs display the 5-tuple information of all the data flows that are allowed, observed, or blocked, and allow you to view the rule applied by clicking a button.
- **Operation logs**: CFW operation logs are divided into user login logs, toggle operation logs, and rule operation logs.
  - **User login logs**: Records the login activities of all the accounts of a given user.
  - **Toggle operation logs**: Records the enabling and disabling of firewalls.
  - **Rule operation logs**: Records users' add, delete, and edit operations on the access control rules.