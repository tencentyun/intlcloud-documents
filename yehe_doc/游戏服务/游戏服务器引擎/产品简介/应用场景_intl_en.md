GSE can be applied in different scenarios in different games, as detailed below:


### Battle server
On a battle server, a battle usually lasts for several to tens of minutes (no more than one hour), and traffic peaks at noon and in the evenings. During off-peak hours, some servers do not need to be used. Therefore, you can use GSE to add/remove servers instantly during peak/off-peak hours and greatly reduce your server costs. In addition, GSE can assign the nearest access region for each battle to guarantee network stability and fair play.

GSE is suitable for table, turn-based/strategy, and real-time battle games. You can create a game server session that represents a room or service where players can battle or chat with each other.




### Message push 
In commonly used game frameworks, a client needs to sustain a persistent connection with a server so that the server can push messages to the client instantly. Therefore, message push is a core module in many games.

Message push may encounter the following problems during deployment:
- A high number of messages fail to be pushed due to network failures.
- Most messages are pushed by only several servers with high specifications. Therefore, a faulty server will have an overly large service impact.

Through GSE, you can implement cross-region disaster recovery with minimal costs. When a region fails, you can quickly switch to another region. The message push service is distributed among multiple servers so that even if a server fails, the affected scope will be small, and you can quickly switch to another server.



