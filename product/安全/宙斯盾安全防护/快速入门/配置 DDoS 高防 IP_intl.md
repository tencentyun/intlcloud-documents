 The DDoS Protective IP product provides protection and traffic cleansing services against high-traffic DDoS attacks for Internet business servers through proxy forwarding. With simple configuration, you can point business traffic and attack traffic to a DDoS protective IP, so when the attack traffic passes through the protective IP, it will be detected and cleansed by the protection system, and then the clean business traffic will be forwarded to the business server, ensuring business availability in scenarios under DDoS attacks.
 
This document details the steps for configuring and launching a DDoS protective IP. For details on how to purchase a configuration, see [Product Configuration Instructions](https://intl.cloud.tencent.com/document/product/685/18798).

## Flowchart
![0](https://main.qcloudimg.com/raw/b279c094b64ba26eded5623e66a5bd18.png)

## Access Steps
1. **Purchase a DDoS protective IP**
a. Go to the [Aegis Anti-DDoS Console](https://console.cloud.tencent.com/gamesec), click **DDoS Protective IP* in the left pane, and click **Purchase Protective IP** under "Protective IP List".

![1](https://main.qcloudimg.com/raw/be6c1607ce5f3e2ef43c09ba76d81535.png)
b. Select the required configuration according to the business needs, confirm the configuration and click **Purchase Now**.
![2](https://main.qcloudimg.com/raw/b0bed15beeeaf210deed3327f959db72.png)
2. **Add a protective IP forwarding rule group**
a. On the "DDoS Protective IP" page, click **Forwarding rule group** and click **Add forwarding rule group**.
b. Enter "New rule group name", select the "Forwarding mode" and "Project" and click **OK**.
![3](https://main.qcloudimg.com/raw/c797ebc57417de384638fa3bafb5444c.png)
>**Note:**
>60 forwarding rules are provided free of charge by default for each forwarding rule group.

3. **Add a forwarding rule*
a. After creating a forwarding rule group, click a **Forwarding rule group ID** to enter the forwarding rule group details page.
![4](https://main.qcloudimg.com/raw/d2f61f622e130824eefd472635726caf.png)
b. Under **Rule group information**, click **Add Forwarding Rule** to add a rule based on layer 4 port forwarding. Based on the business protocol requirements, select the "Protocol type", configure "Session hold", select the appropriate "Polling policy", and enter the "Forwarding port" number, "Real server port" number and "Real server's public IP and weight" and click **OK**. Forwarding rules can be created and added in batches.
![5](https://main.qcloudimg.com/raw/f3cc98aea65ebf357d23f10fcfd5bc7d.png)
>**Note:**
Each forwarding rule can be configured with 40 public IPs of the real server.

 **Protocol type**: Select the protocol type (TCP or UDP) of the port of the service.
 **Session hold**: Enabling session hold ensures that a series of related access requests are allocated to the same server. When there are multiple real server IPs under the same forwarding rule, if you want the same client's requests to be processed by the same server, you need to enable session hold.
 **Polling policy**: When there are multiple real server IPs under the same forwarding rule, you can select polling by weight or polling by minimum number of connections to allocate the proportion of a backend real server for processing business requests. Polling by weight is to allocate based on the real server's IP weight; while polling by minimum number of connections is to allocate based on the minimum number of public IP connections.
  **Forwarding port**: This refers to the port number that needs to provide services on the protective IP. The client's or user's business requests directly access the port of the protective IP.
  **Real server port**: In contrast with the forwarding port, this refers to the port number that provides services on the real server. The protective IP forwards the user's business requests on the forwarding port to the real server port defined by the real server IP.
 **Real server's public IP and weight**: This refers to the IP address of the backend real server that provides services. When there are multiple public IPs of the real server, the protective IP will poll the business request to each real server IP. The set weight represents the proportion of the requests processed by a real server IP. The bigger the weight, the more requests received.
>**Note:**
> - If there are multiple forwarding rules, they can be created in batches. Enter multiple port numbers in the forwarding port and real server port boxes and separate them with commas. Forwarding rules will created one by one in port order.
> - The following port numbers are reserved for the forwarding cluster and cannot be added as forwarding ports: 843, 3306, 1433, 1434, 36000, 56000 and 3389.
4. **Binding Forwarding Rule Group to Protective IP**
After creating a forwarding rule group, under "DDoS Protective IP", click **Forwarding Rule Group**. In the "Operation" column, click **Bind Protective IP** to bind the forwarding rule group to a protective IP.
![6](https://main.qcloudimg.com/raw/ba0a97d71a426a1cf82507c67cf5719e.png)
You can also click **DDoS Protective IP** and select a protective IP to enter the DDoS protective IP details page. Then, click **Basic Configuration**, click **Bind** under "Forwarding Rule Group Settings" and click **Bind** to bind the forwarding rule group to the protective IP.
![7](https://main.qcloudimg.com/raw/5df4421d7e0964c67fffaba5a1b11923.png)
![8](https://main.qcloudimg.com/raw/377d5e8e0a64953b750755c8913ff2c3.png)
5. **Pointing Business to Protective IP**
 After binding a forwarding rule group to the protective IP, you can verify the connectivity from the protective IP's forwarding port to the real server's real server port. Point the business to the protective IP to complete the protective IP accessing configuration. If your business uses DNS service, you can change the DNS in your business' DNS service provider and replace the original IP address with the bound protective IP address. 
After completing the configuration, your real server is protected by protective IP.
6. **CNAME Protected Domain Name**
You can also create a free protected domain name and resolve to it for access by adding a CNAME record at your business' DNS service provider. For configuration details, see [**Binding a Protected Domain Name to a Protective IP**](https://intl.cloud.tencent.com/document/product/685/18808).
