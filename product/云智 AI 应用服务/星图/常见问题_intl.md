### What is a graph database?
Derived from graph theory, a graph database is also known as graph-oriented/based database with the basic concept to store and query data in the structure of "graph" rather than storing images. Its data model is mainly represented by nodes and relationships (edges) and can also process key-value pairs. In short, a graph is a collection of nodes and relationships that correlate those nodes, which presents entities as nodes and their correlations with other entities as relationships. This versatile and expressive structure can be used to model various scenarios.
	 
### Is SKG just a graph database?
SKG features the efficient storage and query capabilities of a graph database, based on which it further builds a graph engine. Simply put, SKG is an integrated platform for graph database and graph engine. Its intelligence is reflected in its abilities to integrate cross-industry data, govern heterogeneous data and normalize complex relationships. It can be said that SKG's capabilities to process and mine trillions of data entries in quasi-real time are something that cannot be found in general graph database systems.


### What are the advantages and disadvantages of a graph database?
A graph database has complete advantages in dealing with correlated relationships, especially in the era of the Internet with ever-growing social networks. For example, it can help us know who LIKES who (this can be one-way or two-way), who is FRIEND_OF who or who is LEADER_OF everyone. In addition to the obvious superiority in correlated queries, a graph database has the following benefits:
- It enables user to think in an object-oriented manner where each query used by the user has explicit semantics;
- It enables user to update and query the data entries in real time;
- It can elastically respond to massive changes in relationships, such as adding and deleting relationships and entities.
- It facilitates visualization of real-time big data mining results.

Although a graph database makes up for the defects of many relational databases, it is not applicable in some fields at present, such as:
- Recording a large amount of event-based data (e.g., log entries);
- Storing binary data.

### What is the system performance of SKG?
The SKG platform uses a server with 24-core CPUs (2.4 GHz clock rate per core), 128 GB MEM and 3 TB SSD, which can complete the execution of algorithms such as PageRank (for significance scoring and ranking) and Fast Unfolding (for community delineating) in dozens of hours in a complex social network containing 2 billion entities and 200 billion edges.
> **Note:**
> The processing time decreases as the number of processing cluster nodes increases.
