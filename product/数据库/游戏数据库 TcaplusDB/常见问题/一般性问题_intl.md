[//]: # (chinagitpath:XXXXX)

### What is TcaplusDB?
TcaplusDB is a distributed database developed by Tencent independently that features low cost, high availability, high reliability and high performance. TcaplusDB, based on the development characteristics and OPS requirements of games, provides 7x24 game data storage service delivering ease of use, high performance, low cost, high scalability, 99.999% availability and data security, so that game developers no longer worry about data storage.

### What business scenarios is TcaplusDB suitable for?
TcaplusDB is created for games, including mobile games, PC games and browser games. It is also suitable for other storage scenarios, such as social, e-commerce, and government websites and apps.

### Which languages of clients are supported by TcaplusDB?
Linux platform: C++, Java, Erlang; Windows platform: C++, Java, Erlang. Tdr and Protobuf are provided to define business data table structure, and the object-oriented method is adopted. API network communication modes include: message-driven asynchronous operation mode, function callback asynchronous operation mode, coroutine operation mode, and dbproxy proxy mode. Game developers who adopt a language other than C++/Java can access TcaplusDB via RestAPI.

### How is the performance of TcaplusDB?
When the single record size of TcaplusDB is 1 KB, the read/write hybrid model is adopted with the ratio of read and write operations being 9:1, the ratio of memory and disk operations being 50:1, and the performance up to 150,000 QPS.

### How do I use TcaplusDB?
For how to use TcaplusDB, see TcaplusDB product documents [Getting Started](https://intl.cloud.tencent.com/document/product/596/10707) and [Operation Guide](https://intl.cloud.tencent.com/document/product/596/10759).

### How to get the latest SDK of TcaplusDB?
Please download the latest version of Tcaplus API according to your platform, such as Windows and Linux.

### Does TcaplusDB support capacity expansion/reduction?
TcaplusDB's access layer and storage layer support capacity expansion/reduction without non-stop service.

### How is the charge calculated for TcaplusDB?
See TcaplusDB [Purchase Guide](https://intl.cloud.tencent.com/document/product/596/10705).
 
### Who are using TcaplusDB?
TcaplusDB is Tencent's preferred game data storage service. Tencent's game project teams, including Arena of Valor, PUBG Mobile, CFM and QQ Speed Mobile, are all using it.

### Is TcaplusDB stable?
TcaplusDB has a high availability of 99.999%. You can use it without any worry.

### Which regions can TcaplusDB be used?
TcaplusDB is deployed with Tencent Cloud. TcaplusDB is supported in all regions where Tencent Cloud is supported.

### How is the data consistency of TcaplusDB?
The tcapsvr master and slave of TcaplusDB synchronize their data in real time, and are deployed in different IDCs in the same city, with a sync difference within 10 ms. TcaplusDB is being optimized for stronger consistency (implemented by Paxos algorithm).

### How does TcaplusDB implement monitoring statistics?
TcaplusDB has a special process to collect and calculate the metrics of access layer and storage layer nodes and generate alarms, including physical machine metrics, process metrics, access traffic metrics, and latency metrics. With these metrics, problems can be identified quickly and accurately.


