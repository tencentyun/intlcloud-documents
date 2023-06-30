

## Overview
TKE Edge provides the ServiceGroup feature, which only needs two YAML files to implement service deployment in hundreds of regions, without application adaptation or transformation. This document describes how to deploy Nginx services separately within multiple node groups.  

## Directions


### Determining the unique key of ServiceGroup

This step performs logic planning without involving any actual operations. TKE Edge sets the `UniqKey` used as the logical flag of the ServiceGroup to be created to `zone`.  

### Grouping edge nodes by label[](id:Step2)

Label the edge nodes in the TKE Edge console or by using kubectl in the TKE Edge console as instructed below:

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Edge Clusters** on the left sidebar.  
2. Select the target cluster ID to enter the cluster management page.  
3. Click **Node Management** > **Node** to enter the node list page as shown below:
   ![](https://qcloudimg.tencent-cloud.cn/raw/addebe0f7b0f641264b98074ffe6752c.png)
4. Select **More** > **Edit Label** on the right of the target node.  
5. In the **Edit Label** pop-up window, add a label as instructed below:
   ![](https://qcloudimg.tencent-cloud.cn/raw/9ff3586a8bb855b41113cecd52c3cb3c.png)   
   - See the overall architecture chapter. Select `zone=nodeunit1` for nodes 12 and 14 and `zone=nodeunit2` for nodes 21 and 23.  
   - The label `key` needs to be the same as the `UniqKey` of the ServiceGroup. The `value` is a unique key of the NodeUnit. Nodes with the same `value` belong to the same NodeUnit.  
   - If there are multiple ServiceGroups in the same cluster, assign different Uniqkeys to different ServiceGroups.  
6. Click **OK**.  

### Deploying DeploymentGrid

```
apiVersion: superedge.io/v1
kind: DeploymentGrid
metadata:
    name: deploymentgrid-demo
    namespace: default
spec:
    gridUniqKey: zone
    template:
      selector:
        matchLabels:
          appGrid: nginx
      replicas: 2
      template:
        metadata:
          labels:
            appGrid: nginx
        spec:
          containers:
          - name: nginx
            image: nginx:1.7.9
            ports:
            - containerPort: 80
              protocol: TCP
```

### Deploying ServiceGrid

```
apiVersion: superedge.io/v1
kind: ServiceGrid
metadata:
    name: servicegrid-demo
    namespace: default
spec:
    gridUniqKey: zone
    template:
      selector:
        appGrid: nginx
      ports:
      - protocol: TCP
        port: 80
        targetPort: 80
```
>?As shown above, the `gridUniqKey` field is set to `zone`. Therefore, you should also set the label `key` to `zone` when [grouping edge nodes by label](#Step2). If there are three node groups, add three labels respectively: `zone: zone-0`, `zone: zone-1 `, and `zone: zone-2 `.  

At this point, each node group contains the Deployment and corresponding Pod of Nginx. For access to the same `service-name` on a node, the requests will be sent to the node in the target group. The verification method is as follows:

```
[root@VM_1_34_centos ~]# kubectl get deploy
NAME                         READY   UP-TO-DATE   AVAILABLE   AGE
deploymentgrid-demo-zone-0   2/2     2            2           85s
deploymentgrid-demo-zone-1   2/2     2            2           85s
deploymentgrid-demo-zone-2   2/2     2            2           85s
 
[root@VM_1_34_centos ~]# kubectl get svc
NAME                   TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)   AGE
kubernetes             ClusterIP   172.19.0.1     <none>        443/TCP   87m
servicegrid-demo-svc   ClusterIP   172.19.0.177   <none>        80/TCP    80s
```

For node groups added to a cluster after the deployment of DeploymentGrid and ServiceGrid, this feature will automatically create the specified Deployment and Service in the new node groups.  

