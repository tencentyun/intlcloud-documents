

## Server Fleet 

A server fleet consists of multiple CVM instances, each of which runs multiple game server sessions. GSE can manage and assign game server sessions. In general, each session is a process.

![](https://main.qcloudimg.com/raw/31e41eec195bf98521120c5e71e5d9b2.jpg)




#### CVM auto scaling

- Auto scaling based on game server session buffer   
You can configure the game server session buffer, i.e., the ratio of reserved idle server processes, to expand when the idle processes are insufficient, and to reduce when they are sufficient.

- Stateful reduction  
GSE will not remove instances where game server sessions are running. During reduction, GSE will notify the game server sessions, which can determine whether or not to reduce immediately. If you selected full protection on the product configuration page and the game server sessions keep running and rejecting reduction, reduction will never be performed.





## Game Server Queue

A game server queue is actually a queue of server fleets with configured priorities. It can include server fleets around the world to implement nearby scheduling and disaster recovery.

![](https://main.qcloudimg.com/raw/bb7598376dbe1b0e72f8e08d0522dfa3.jpg)



#### How disaster recovery works 
GSE supports cross-region deployment, in which server fleets built in multiple regions make up a queue. When a region fails, the latency of requests from clients to servers in the region will become very high. In this case, the system will automatically switch to a region with low latency to implement disaster recovery. You can also manually adjust the fleet priority to delete faulty regions from the queue.

#### How nearby assignment works 
GSE provides a speed test tool that you can use to test the latency of requests from a client to a server. In battle games, GSE will assign a server in the region nearest to all players in the room as a whole.



## Alias 

A client can request a server in a server fleet through an alias. When the version is updated, you can create a server fleet and point the alias to the new fleet so that the client can still call the same alias and implement non-stop update.
![](https://main.qcloudimg.com/raw/b3c8b0b7d529e4c0d29288f69978d868.png)





