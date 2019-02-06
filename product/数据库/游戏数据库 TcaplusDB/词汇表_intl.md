[//]: # (chinagitpath:XXXXX)

### Protobuf

Google Protocol buffer (Protobuf) is a lightweight and efficient structured data storage format developed by Google for the serialization of structured data. It is suitable for data storage or RPC data exchange. TcaplusDB defines table structures and serializes data records through Protobuf.

### TcaplusDB table

For the tables used for data storage, the structure is defined using the Protobuf file that conforms to the TcaplusDB semantics. For more information, see [Proto Table Creation File](https://intl.cloud.tencent.com/document/product/596/31661).

### App

It is the App unit of TcaplusDB, which corresponds to the game App. AppID is displayed on the configuration information page, and is used as a connection parameter for the TcaplusDB SDK connection table.

### AppKey

It is the App unit key of TcaplusDB. AppKey is displayed on the configuration information page, and is used as a connection parameter for the TcaplusDB SDK connection table.

### Deployment Unit (Zone)

It is the data deployment unit within a TcaplusDB App unit, which can be interpreted as a zone. Multiple zones can be created in an App, and tables with the same name must be created in different zones. ZoneID is displayed in the **Deployment Unit** column of the list, and is used as a connection parameter for the TcaplusDB SDK connection table.

### Access via VPC network

The access point of the TcaplusDB directory service is the entry for users to access TcaplusDB tables via Tcaplus SDK. The VPC network URL is displayed on the configuration information page, and is used as a connection parameter for the TcaplusDB SDK connection table.

### Access via HTTP

The access point of the TcaplusDB RESTful API service is the entry for users to access TcaplusDB tables via the HTTP client. The URL for access via HTTP is displayed on the configuration information page, and is used as a connection parameter for the HTTP client connection table.




