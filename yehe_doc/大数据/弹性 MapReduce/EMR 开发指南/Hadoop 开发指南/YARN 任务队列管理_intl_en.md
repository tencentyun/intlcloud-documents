You can log in to the YARNwebUI, which is the web user interface of YARN, through the shortcut entry provided in EMR. For more information, please see the product documentation. After logging in, you will see the following:

![YARN](https://mc.qcloudimg.com/static/img/df3b8ca1dc152d28f7f84caa87613e53/5-1-3.png)  

You can see some monitoring information of the entire cluster here:

- Apps: 67 submitted apps, including 9 pending ones, 7 running ones, and 51 completed ones, where 15 containers are running.
- Memory: 36 GB in total with 30 GB used and 10 GB reserved.
- Virtual cores: 20 cores in total with 15 used ones and 5 reserved ones.
- Nodes: 5 available nodes, 0 decommissioned ones, 0 lost ones, 0 unhealthy ones, and 0 rebooted ones.
- Scheduler: Fair Scheduler, including maximum and minimum memory size and CPU allocation information.

The Application Queues section contains job queuing information of the cluster. Take the root.hadoop queue as an example:
- Used resources: 30,720 MB (30 GB) memory, 15 virtual cores.
- Active applications: 7.
- Pending applications: 9.
- Minimum memory occupied: 0 MB, 0 cores.
- Maximum memory occupied: 36,860 MB, 20 cores.
- Steady fair share.
- Instantaneous fair share.
- The proportion of memory occupied by this queue is 83.3%.
