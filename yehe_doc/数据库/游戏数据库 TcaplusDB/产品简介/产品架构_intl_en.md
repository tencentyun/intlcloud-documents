TcaplusDB is a fully hosted distributed NoSQL database service and mainly consists of the management, access, and storage layers. The access and storage layers both consist of multiple connection nodes and storage nodes and support horizontal node scaling. Each layer has its own roles, and the overall architecture is as shown below:
![](https://main.qcloudimg.com/raw/3afc344e14b9f2d2b6eacf46b0751af6.jpg)

#### Management layer
The TcaplusDB management layer is used to store metadata and management information, schedule the TcaplusDB system, and manage TcaplusDB data.

#### Access layer
The TcaplusDB access layer is used to process user requests, interact with data nodes at the storage layer, and get data and return it to users.

#### Storage layer
The storage layer service is the core service of TcaplusDB used to store user data, respond to access-layer requests, and return data information.

### TcaplusDB Logic Structure
The TcaplusDB logic structure consists of clusters, table groups, and tables as shown below:
![](https://main.qcloudimg.com/raw/486543524b9eb422f86682524c7aa3ad.jpg)

