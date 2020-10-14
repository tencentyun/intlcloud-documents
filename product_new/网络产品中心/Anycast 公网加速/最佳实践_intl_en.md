## Background
A gaming company whose backend service cluster is in Beijing expects customers nationwide to connect to the game. However, at the same time, to save costs, the company does not want to deploy multiple sets of logic and data layers. In this case, a global floating IP is required to serve as the only access entry for global nearby distribution, dynamic traffic distribution, and failure elimination.

## Pain Points
Because the company's on-premise IDC and small and medium-sized public cloud vendors do not have the cross-region network scheduling capability and the Anycast capability, the gaming company cannot meet the customers’ requirements. As a result, its customers face the following problems:

1. Customers must use multiple public IPs. Because each region is deployed with a cluster, multiple logical layers need to be maintained and data needs to be read/written across regions, which lead to poor consistency and real-time performance.
2. Customers are heavily dependent on the linkage quality of internet service providers (ISPs). For example, service providers A and U suffered BGP network exceptions due to the network failures of an ISP in Beijing. As a result, the game could not be accessed in certain regions, which led to a serious loss of players for the game.
3. All DDoS attacks would target a single IP, which represents a serious security threat for the game.

## Solution Plan
Tencent Cloud provides a solution to help resolve the problems experienced by customers, as shown in the following figure:

![](https://main.qcloudimg.com/raw/36436ad0b04b1e709226ab20f7fee74f.png)

The key points of the solution are as follows:

1. The solution uses the Anycast EIP. The IP can Anycast in multiple regions at the same time to establish one server shared by game players worldwide.
The user backend maintains one set of clusters and binds the Anycast EIP. The EIP uses Tencent Cloud's private network and PoPs to route in multiple regions.
Customers do not need to select a network path or manually specify the IP publishing location. By entering and exiting from the optimal region, the nearby traffic will be globally balanced and backend processes will be simplified. In addition, customers’ IPs will be converged, eliminating the need to configure IP and DNS rules for each region and simplifying ICP filing and management.
2. The solution improves the transmission quality.
Multiple IP publishing sites provide multiple paths, enhancing the fault tolerance of the network. In addition, nearby access uses Direct Connect, providing higher reliability and lower latency than the public network and improving the player experience. For example, if China Telecom's network linkage between Beijing and Hebei fails but the IPs in Guangzhou and Shanghai can still distribute routes, the traffic of Hebei game users who access Beijing will bypass to Tencent Cloud through the BGP traffic entry of Shanghai or Guangzhou. As a result, the game company can continue to serve its customers while its competitors experience service disruptions.
