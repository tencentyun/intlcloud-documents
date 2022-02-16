
- [How does the game server kick out an invalid tcaproxy (access layer) node?](#52)
- [How does the game server choose the tcaproxy (access layer) node?](#53)
- [Does TcaplusDB have the compression feature?](#59)
- [Is the TcaplusDB API thread-safe?](#61)
- [How does tcapsvr (storage layer) achieve disaster recovery?](#63)
- [How does tcaproxy (access layer) achieve disaster recovery?](#62)
- [Does TcaplusDB have overload protection?](#66)
- [What is the principle of cold and hot data exchange for TcaplusDB?](#71)
- [How does tcaproxy (access layer) choose tcapsvr (storage layer)?](#81)
- [What is the level of the lock in TcaplusDB?](#84)

<span id="52"></span>
### How does the game server kick out an invalid tcaproxy (access layer) node?
TcaplusDB API supports disaster recovery in case of any tcaproxy exceptions. There are two main ways in which the API kicks out invalid tcaproxy processes:

1. The API physically considers that a tcaproxy is not available. The API sends heartbeat detection packets to all connected tcaproxy every second. If a game server does not receive the corresponding heartbeat return packets from tcaproxy within 10 seconds, the API will actively disconnect the TCP connection to the tcaproxy and actively connect the tcaproxy at the next onupdate.
2. The API logically considers that a tcaproxy is not available. The API calculates the request and response ratio of a tcaproxy every 10 seconds as a basis for judgment. The timeout threshold for a request packet is 3 seconds. If a tcaproxy times out more than 3 times, the tcaproxy is considered unavailable and no request will be sent to it. A `getmetdata` request is sent to the tcaproxy 60 seconds later. If the tcaproxy can correctly handle the `getmetadata` request, the API considers the tcaproxy available and requests will be sent to it again.

If the game server finds that a tcaproxy is not available within 10s, it will not send data to the tcaproxy node.

<span id="53"></span>
### How does the game server choose the tcaproxy (access layer) node?
The game server maintains a consistent Hash ring locally. Once a tcaproxy (access layer) node has been verified, it will be added to the Hash ring. If a tcaproxy (access layer) node reduces capacity or the TCP link between game server and tcaproxy (access layer) has been disconnected due to machine abnormalities, the game server will remove the tcaproxy (access layer) node from the Hash ring. The game server calculates hash values based on the primary key in the request (if it is a `batchget` request, it randomly selects a single tcaproxy (access layer) node), and then selects a single tcaproxy (access layer) node from the consistent Hash ring.

<span id="59"></span>
### Does TcaplusDB have the compression feature?
TcaplusDB has a compression feature based on the Google snappy compression algorithm, including protocol compression (i.e., compression of the request/response packet between game server and tcaproxy (access layer) and data compression (i.e., compression of the data that needs to be stored by tcapsvr (storage layer)). If you want to reduce the network traffic costs between game server and tcaproxy (access layer), we recommend that you enable the protocol compression. You can also call the `SetCompressSwitch` function of TcaplusDB API to enable the tcapsvr (storage layer) compression, which can save disk space, improve IO disk performance, and reduce the CPU resources used for compression and decompression.

<span id="61"></span>
### Is the TcaplusDB API thread-safe?
TcaplusDB API is non-thread-safe, mainly because components such as tlog and tdr are not thread-safe. It is recommended that a single thread uses a single API object and a single game region uses a single API object. If you need to interact across game regions, it is recommended to maintain multiple API objects with a single game server.

<span id="62"></span>
### How does tcaproxy (access layer) achieve disaster recovery?
Tcaproxy (access layer) adopts a peer-to-peer design scheme, that is, all tcaproxy (access layer) nodes under a single game region contain routing information of all tables under a single game region. If a tcaproxy (access layer) fails, as long as the remaining tcaproxy (access layer) nodes are not overloaded, the game server will kick out the abnormal tcaproxy (access layer) node, which will not affect the use of game server. There is no single point of failure risk for the tcaproxy (access layer).

<span id="63"></span>
### How does tcapsvr (storage layer) achieve disaster recovery?
The tcapsvr (storage layer) runs in a primary-secondary mode (primary tcapsvr and secondary tcapsvr). Primary and secondary tcapsvr synchronize data in real time, and are deployed at the different IDCs in the same city, ensuring that primary-secondary synchronization latency is less than 10 ms. If the secondary tcapsvr is abnormal, it will not affect the use of game server (if the read request offloading is not enabled, the requests of game server are processed by the primary tcapsvr. If the read request offloading is enabled, the secondary tcapsvr will assist in processing part of the read requests), and the DBA will rebuild the secondary tcapsvr; if the primary tcapsvr is abnormal, the secondary tcapsvr will perform failure recovery and the DBA will apply for a new machine to rebuild the secondary tcapsvr. There is no single point of failure risk for the tcapsvr (storage layer).

<span id="66"></span>
### Does TcaplusDB have overload protection?
Both the access layer and the storage layer have process-level overload protection measures to ensure that services will not collapse during peak hours.

<span id="71"></span>
### What is the principle of cold and hot data exchange for TcaplusDB?
TcaplusDB uses memory + SSD disk storage. The first GB data of a single engine file is mapped in memory. The hot data is placed in the memory and the cold data is placed on the disk. The LRU algorithm is used for hot and cold data exchange. The `get` operation of game server triggers the LRU swap-in operation, and the LRU thread of tcapsvr (storage layer) is responsible for the LRU swap-out operation. Try to ensure that the hot data is stored in the memory, thus ensuring high cache hit rate and low single read and write latency.

<span id="81"></span>
### How does tcaproxy (access layer) choose tcapsvr (storage layer)?
Each table defines a shardkey. If no shardkey is defined, the shardkey defaults to the primary key. Tcaproxy (access layer) selects the corresponding tcapsvr (storage layer) according to `hash (shardkey) % 10000` (where % is the remainder operator), so the shardkey should be highly discrete.

<span id="84"></span>
### What is the level of the lock in TcaplusDB?
The granularity of the lock in TcaplusDB is logging level.
