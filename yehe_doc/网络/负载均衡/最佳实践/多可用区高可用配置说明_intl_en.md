## Implementing HA Across Multiple AZs
CLB instance supports disaster recovery across availability zones. For example, multiple clusters can be deployed in two availability zones in the same region: Hong Kong (China) Zone 1 and Hong Kong (China) Zone 2. This achieves disaster recovery across availability zones in the same region. With this feature, a CLB instance can forward frontend access traffic to other availability zones in the same region within 10 seconds if the entire availability zone fails, restoring service capability.

## FAQs and Use Cases
#### Question 1: If CLB instance `test1` is configured for Hong Kong (China) Zone 1 and Zone 2, what is the policy for inbound public network traffic of the client?
Hong Kong (China) Zone 1 and Zone 2 have a pair of IP resource pools, which can be seen as IP resources with equivalent load balancing capability. Developers do not need to figure out between master cluster and slave cluster. When they purchase a CLB instance and bind it to CVM, two sets of rules will be generated and written into the two clusters, achieving high availability.

#### Question 2: Suppose that CLB instance test1 is configured for Hong Kong (China) Zones 1 and 2, and bound to 100 real servers in each availability zone. During business operation, 1 million HTTP persistent connections (with TCP connection kept alive) are established in each zone. If the entire CLB cluster in Zone 1 fails and becomes unavailable, what will happen to the business?
When CLB instance in Hong Kong (China) Zone 1 fails, all current persistent connections will be closed, while non-persistent connections will not be affected. The disaster recovery architecture will automatically bind the 100 servers in each zone to CLB instance in Hong Kong (China) Zone 2 within 10s, immediately restoring business capability with no manual intervention required.

#### Question 3: Which type of CLB is compatible with multi-AZ disaster recovery? Does it cost extra fees?
Multi-AZ disaster recovery is free of charge. This feature is available for both public network and private network CLB instances, except for private network CLB instances created in Guangzhou before April 29, 2020, in Shanghai before December 19, 2019, and in Beijing before December 18, 2019.

