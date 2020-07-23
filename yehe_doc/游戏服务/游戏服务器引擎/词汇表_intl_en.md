### Server Fleet
A server fleet is a group of managed resources in the form of CVM instances capable of auto scaling and health check. The managed server fleet is used to deploy game servers.

### Alias
An alias is used to abstract the name of a fleet. By using an alias instead of a specific fleet ID, you can change the server fleet associated with the alias to switch player traffic from one fleet to another fleet more easily and seamlessly for zero downtime updates.

### Asset Package
An asset package is a zip package deployed on a CVM instance. Its directory must contain all the components necessary for running your game server, including executable files, dependent packages, and installation scripts of the game server.

### Queue
A queue is a group of server fleets running in regions of a game asset package. You can use a queue to create a cross-region fleet group and allow placing game server sessions in any fleet in the queue, so as to minimize the latency, deliver a better player experience, use more fleet capacity more efficiently, provide high capacity for new games more swiftly, and make the game more elastically available.

### Instance
An instance is a CVM instance provided by GSE. The specific type can be viewed in the console “Create Fleet > Deployment Configuration”.