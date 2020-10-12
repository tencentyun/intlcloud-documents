## Background
A gaming company, whose BACKEND service cluster is located in Beijing, expects to connect customers nationwide. However, to save costs, the company does not want to deploy multiple sets of logic and data layers. In this case, a global floating IP is required to serve as the only access entry for global nearby distribution, dynamic traffic distribution, and failure elimination.

## Pain Points
The company's IDC built by customers and the small and medium-sized public cloud vendors cannot schedule the network across regions and do not have the Anycast capability, so it cannot meet the customers’ requirements. As a result, the customers would face the following problems:
1. Use multiple public IPs. Each region is deployed with a cluster, so that multiple logical layers need to be maintained, and data should be read/written across regions, which lead to poor consistency and timeliness.
2. Heavily depending on the linkage quality from Internet Service Providers. For example, service providers A and U suffered BGP network exceptions due to network failures of an ISP in Beijing. As a result, the game could not be accessed in some regions which lead to a serious user loss.
3. All DDoS attacks target at a single IP, which is very dangerous.

## Solution Description
Based on customers’ requirements, Tencent Cloud provides a solution to help solve the problems, as shown in the following figure:
![](https://main.qcloudimg.com/raw/082b373bfa4f9036dedfc4958e25e9f1.png)
The key points of the solution are as follows:
1. Use Anycast EIP. The IP can Anycast in multiple regions at the same time to share one server across the globe.
The user backend maintains one set of clusters and binds the Anycast EIP. The EIP uses Tencent Cloud's private network and POP point to route in multiple regions.
Customers neither need to select a network path nor manually specify the IP publishing location, the traffic will be globally balanced by entering and exiting from the optimal region, simplifying the backend. Meanwhile, customers' IP is converged, and there is no need to configure IP and DNS rules for each region, simplifying ICP filing and management for services in Mainland China.
2. The transmission quality is improved.
Multiple IP publishing sites provide multiple paths, enhancing fault tolerance of the network. In addition, the nearby access leads to Direct Connect transmission, providing a higher reliability, lower latency and improved player experiences than those of the internet. For example, if the network linkage of China Telecom fails between Beijing and Hebei, but the IPs in Guangzhou and Shanghai can still distribute routes, to access Beijing, the traffic of Hebei game users will bypass to Tencent Cloud through the BGP traffic entry of Shanghai or Guangzhou. Therefore, the game company can continue to serve its users while a disruption of services occurs to its competitors.
