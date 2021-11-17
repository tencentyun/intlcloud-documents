

### What problems can be solved by GAAP?
GAAP helps vendors create high-speed network connections between end users and business servers to solve cross-regional access latency and lag.

### What is the coverage of GAAP?
GAAP has more than 50 global nodes deployed across Asia, Europe, South America, North America, and Oceania. It provides stable and efficient high-speed connections for businesses around the globe that require cross-region access or server sharing, avoiding access lag and high latency.

### How does GAAP work?
A peering connection is set up between the acceleration region and the origin server region, so users can avoid unstable public network by using Tencent Cloud's global high-speed private network and optimized access routes. Direct business access through high-speed connections delivers a fast and stable access experience.

### What is an access node and an origin-pull node?
- Access node (formerly acceleration region): a node in the user region or the region closet to the user, i.e., the entry node of the acceleration connection.
- Origin-Pull node (formerly origin server region): a node in the destination server region or the region closest to the destination server, i.e., the origin-pull node of the acceleration connection. 

For example, if your server is located in Hong Kong (China), and you want all users in multiple regions such as West US, East US, Japan, and Korea to access the server through high-speed connections for a fast and stable access experience, then the access nodes will be West US, East US, Japan, and Korea, while the origin-pull node will be Hong Kong (China).

### What protocols and forwarding methods does GAAP support?
GAAP supports TCP/UDP/HTTP/HTTPS protocols at layers 4 and 7 and IP/domain name forwarding.

### Does GAAP support the origin server to get the real user IP?
GAAP supports the origin server to get the real user IP.

### What are some GAAP application scenarios?
GAAP can be used for cross-region business access, such as global e-commerce and globally unified game servers. For more information, please see [Application Scenarios](https://intl.cloud.tencent.com/document/product/608/13760).

### What if the collaborator account does not have permission to access GAAP?
Please contact the administrator of the root account or another account that has the `AdministratorAccess` permission to grant the collaborator GAAP read/write or read-only permission, as instructed in [Configuring Permissions](https://intl.cloud.tencent.com/document/product/608/31510).


