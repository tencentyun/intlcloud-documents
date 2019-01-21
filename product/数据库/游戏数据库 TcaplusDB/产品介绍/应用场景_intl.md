[//]: # (chinagitpath:XXXXX)

### Mobile games

As mobile games are characterized by fragmented play time, high player interaction, support for both all-server/all-region and multi-server/multi-region modes, fast iteration rate, and multiple operational activities, data requirement is massive and thus low latency is very important for data storage. TcaplusDB can support and optimize mobile games accordingly by leveraging technologies such as batch operation, automatic server merging, capacity expansion/reduction with non-stop service, and cold and hot data exchange. In addition, TcaplusDB also provide targeted support and optimization with regard to frequent data rollbacks, high availability, data updates and other data-related features.

### PC games

PC game players are often logged in for extended periods of time, and PC games have a long lifecycle. Most PC games run in the multi-server/multi-region mode, so there are large amounts of data records and thus high requirements for low latency. TcaplusDB can support and optimize PC games by using technologies such as automatic disaster recovery, data partitioning, automatic record packeting, and cache combined with SSD disk storage.

### Browser games

Browser games feature frequent server launching/merging, and usually run 7x24 non-stop. As browsers have limited ability to cache data, high requirements are imposed on the backend data storage system. TcaplusDB can support and optimize browser games by means of automatic server merging, capacity expansion/reduction with non-stop service, and cache combined with high-speed disk storage.

### Social apps

In social apps, data can be created freely by users, and comments are used frequently. Contents are aggregated by topic, and fields such as Text, Link, and Time are of fixed length. Data activity is determined by time, and more data is read and less data is written. TcaplusDB can support and optimize social apps by using technologies such as list storage, heterogeneous datatype support, hot and cold data exchange, and read/write separation.

