Snova supports the management and OPS of clusters in the Cloud Console and through the Cloud API. The following describes how to operate in the console. Cloud API is temporarily unavailable during the product trial.

## Creating a Cluster

This function is temporarily unavailable in the console during the trial period. After your trial qualification is approved, you need to provide the following information to the product team for activating your cluster. The following regions are supported for the trial: Beijing, Shanghai, Guangzhou and Singapore. The following information items are required for activating an trial cluster:

| Information item | Value range | Note |
| --------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| User UIN         | /                                                            | /                                                            |
| User APPID       | /                                                            | /                                                            |
| Activated regions and availability zones | Guangzhou Zone 1 or Guangzhou Zone 3 | During the internal trial period, only Beijing, Shanghai, Guangzhou and Shenzhen regions are supported |
| Cluster name | Default | The initial default value is xxx which can be modified in the Cloud Console |
| VPC | Example: vpc-aejsd98p | Enter the information of the VPC and subnet you wish to connect to Snova, which can be queried and adjusted in the [VPC Console](https://console.cloud.tencent.com/vpc/vpc?rid=5) |
| User subnet | Example: [subnet-83knqldq](https://console.cloud.tencent.com/vpc/subnet?regionId=-1&subnetId=subnet-83knqldq) | Available in [VPC - Subnet](https://console.cloud.tencent.com/vpc/subnet?rid=1) |
| Storage capacity | Initialized storage capacity in TB: storage capacity after 3 months in TB: | / |
| Number of compute nodes | / | Generally, over 3 compute nodes are required |
| Username | / | The initial login username. <br>1. Only lowercase letters, underscores and digits are allowed <br>2. It must start with a letter or underscore <br>3. Length: 6-32 characters |
| User password | / | Cluster login password. <br> 1. Length: 8-16 characters <br>2. At least two of the following three types of characters are required: [a-z,A-Z], [0-9] and [-!@#$%&^*+=_:;,.?] |

## Modifying Information

From the cluster list page, enter the basic cluster information page to modify the cluster name, network, and admin password.

> **Note:**
> Modifying the network address will change the cluster access link, so the calling address needs to be modified accordingly.

## Real-time Querying

Go to the real-time query subpage of the cluster details page to view the ongoing queries in three types of states: querying, blocked and waiting for execution. 

 The queries in the list can be terminated by clicking the **Terminate Query** button.

## Querying the History

Go to the history query subpage of the cluster details page to view the completed or terminated queries.

## Monitoring Events

Cluster-sensitive operational events can be queried using the event monitoring module on the cluster details page and the separate event monitoring module.
