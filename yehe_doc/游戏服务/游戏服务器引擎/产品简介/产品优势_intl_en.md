### Real-time scalability for reduced costs
All games have peak and off-peak hours. With GSE, you can set a selected instance type and a scaling scope, and GSE will auto-scale game servers according to player traffic within the specified scope, enabling you to meet peak demand while eliminating the need to pay for idle servers during off-peak hours. 

### Stateful scaling mode 
GSE will not remove instances where game server sessions are running. When the server load drops and reduction is triggered, GSE will inform the game processes that the server is being removed and prevent new game server sessions from being assigned to said server. However, it will not forcibly terminate the instance, which may cut client connections. The instance will be removed only after the game processes initiate an end command. 


### Health check for guaranteed service stability 
- Health check is performed on servers, and the runtime environment is monitored in real time. If a server fails, it will be deallocated, and traffic will be rescheduled to other servers in a matter of seconds. 
- No manual OPS is required. If a massive failure occurs, the region can be automatically switched based on the speed test result. You can also manually remove the faulty region.

### Cross-region deployment for effective disaster recovery 
GSE supports cross-region deployment, where server fleets built in multiple regions make up a queue. When the queue is requested, the system will automatically select a server fleet in a region for player access. When a region fails, the service will be quickly switched to another region.

### Zero downtime updates for a smooth gaming experience 
GSE supports zero downtime updates. A client can request a server in a server fleet through an alias. When the version is updated, you can create a server fleet and point the alias to the new fleet to implement an update with zero downtime.

### Global release and nearby access 
GSE is available in multiple regions such as Shanghai and North America. It provides a speed test tool to test the latency between a game client and each region and can assign the nearest server fleet to the client based on the test data.  

### Cross-platform call for easier use 
GSE can be called across platforms such as PCs, mobile devices, and game consoles. It supports C++ and C# client engines and custom gaming server frameworks.

### Pay-as-you-go billing for lower costs 
You can set the server instance type and scaling scope in GSE, and instances will be scaled within this scope. Since access traffic to a game has peak and off-peak hours, GSE can perform the auto scaling of servers based on the player access request volume to prepare your business for access peaks and eliminate your need to pay for idle servers during off-peak hours.


