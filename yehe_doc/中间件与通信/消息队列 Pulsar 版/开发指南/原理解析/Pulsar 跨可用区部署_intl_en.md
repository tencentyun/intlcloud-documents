
## Pulsar Multi-AZ Deployment

Pulsar supports multi-AZ deployment, which means when you purchase a Pulsar cluster in a region with at least three AZs, you can select up to three AZs for multi-AZ deployment. Partition replicas of this cluster will be forcibly distributed across the nodes in all AZs, which ensures that your cluster can normally provide services even if it is unavailable in a single AZ.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/wSbv048_PRELIM__%E6%B6%88%E6%81%AF%E9%98%9F%E5%88%97%20Pulsar%20%E7%89%88_%E4%BA%A7%E5%93%81%E7%9B%AE%E5%BD%95_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US.jpg)

### How multi-AZ deployment works

Pulsar implements cross-AZ disaster recovery based on rack awareness. Although the service nodes of different components are deployed in different racks in different AZs, they are essentially in a single Pulsar cluster.

As a kind of ensemble placement policy, rack awareness is the algorithm that the BookKeeper client uses to select ensembles based on the network topology attribute.

#### How to select bookie

When a bookie cluster is deployed for the first time, each bookie will register a temporary zk-node to the current ZooKeeper, and the BookKeeper client will discover the bookie list via ZooKeeper. When a bookie changes or fails, the ensemble placement policy will be notified of this through the `onClusterChanged (Set, Set)` API and reconstruct a new network topology. Subsequent operations, such as newEnsemble, will be generated based on the new network topology.


#### Network topology

Network topology shows the bookie node information in a cluster in a tree-like hierarchical structure. A bookie cluster may consist of many data centers in different regions. A data center contains bookie nodes distributed on different racks. In the tree-like structure, the leaf nodes show the bookie information.

-  **Example 1:** There are three bookies: bk1, bk2, and bk3 in region A. Their network locations are /region-a/rack-1/bk1, /region-a/rack-1/bk2, and /region-a/rack-2/bk3, respectively, as shown in the network topology below:
```
         root
          |
      region-a
        /  \
  rack-1  rack-2
    /  \      \
 bk1  bk2     bk3

```
- **Example 2:** There are four bookies: bk1, bk2, bk3, and bk4 in region A and region B. Their network locations are /region-a/rack-1/bk1, /region-a/rack-1/bk2, /region-b/rack-2/bk3, and /region-b/rack-2/bk4, respectively, as shown in the network topology below:
```

              root
            /      \
      region-a      region-b
        |              |  
     rack-1          rack-2
      /  \           /    \
   bk1  bk2         bk3   bk4

```

The network locations are resolved with the DNSToSwitchMapping method from domain names or IP addresses. They must be in the format of “/region/rack”, where the first slash (/) represents root, “region” represents data center, and “rack” represents rack information.

>?The DNSToSwitchMapping method implemented in Pulsar is the BookieRackAffinityMapping method. This method stores rack information through ZookKeeper, and only has the rack awareness capability currently.

## Notes

Currently, Pulsar virtual clusters don’t support multi-AZ deployment, and only exclusive clusters do. To use this feature, [contact us](https://www.tencentcloud.com/contact-us).

>?This feature is currently in beta testing and is free of charge.
