Cloud Log Service (CLS) is a one-stop log data solution. After quickly and easily connecting to it (which takes about 5 minutes), you can enjoy comprehensive, stable, and reliable log services such as log capture, storage, content search, statistics collection, and analysis with no need to care about resource scaling. It helps you locate business problems, monitor metrics, perform security audit, and solve other log problems, greatly lowering your log OPS threshold.

CLS operations supported by CloudAudit are as shown below:

| Operation Name | Resource Type | Event Name |
|-----------|------|---------------------------|
| Consumer heartbeat     | cls  | consumerGroupHeartBeat    |
| Creating chart      | cls  | CreateChart               |
| Creating consumer group     | cls  | createConsumerGroup       |
| Creating dashboard     | cls  | CreateDashboard           |
| Creating logset     | cls  | createLogset              |
| Creating server group     | cls  | createMachineGroup        |
| Creating shipping configuration    | cls  | createShipper             |
| Creating log topic    | cls  | createTopic               |
| Deleting chart      | cls  | DeleteChart               |
| Deleting consumer group     | cls  | deleteConsumerGroup       |
| Deleting dashboard     | cls  | DeleteDashboard           |
| Deleting logset     | cls  | deleteLogset              |
| Deleting server group     | cls  | deleteMachineGroup        |
| Deleting shipping configuration    | cls  | deleteShipper             |
| Deleting log topic    | cls  | deleteTopic               |
| Getting consumer group cursor   | cls  | getConsumerGroupCursor    |
| Getting log cursor    | cls  | getCursor                 |
| Getting dashboard information   | cls  | GetDashboard              |
| Getting fast analysis result  | cls  | GetFastAnalysis           |
| Getting the histogram of the number of logs | cls  | GetHistogram              |
| Getting index configuration    | cls  | getIndex                  |
| Getting logset details   | cls  | getLogset                 |
| Getting server group details   | cls  | getMachineGroup           |
| Getting server status    | cls  | getMachineStatus          |
| Getting shipping configuration details  | cls  | getShipper                |
| Getting log topic details  | cls  | getTopic                  |
| Getting chart list    | cls  | ListChart                 |
| Getting consumer group list   | cls  | listConsumerGroup         |
| Getting dashboard list   | cls  | ListDashboard             |
| Getting logset list   | cls  | listLogset                |
| Getting server group list   | cls  | listMachineGroup          |
| Getting topic partition list  | cls  | listPartitions            |
| Getting shipping configuration list  | cls  | listShipper               |
| Getting shipping task list  | cls  | listShipperTask           |
| Getting log topic list  | cls  | listTopic                 |
| Modifying chart      | cls  | ModifyChart               |
| Modifying consumer group     | cls  | modifyConsumerGroup       |
| Modifying consumer group cursor   | cls  | modifyConsumerGroupCursor |
| Modifying index configuration    | cls  | modifyIndex               |
| Modifying logset     | cls  | modifyLogset              |
| Modifying server group     | cls  | modifyMachineGroup        |
| Modifying shipping configuration    | cls  | modifyShipper             |
| Modifying log topic    | cls  | modifyTopic               |
| Splitting/Merging topic partition | cls  | updatePartition           |
