## Feature Overview
Tencent Cloud implements custom management of your resource bills from the perspective of statistical analysis by leveraging its tag tool and cost allocation capabilities. This well meets your need for multidimensional management and analysis of bills and costs. If you want to allocate your costs from the perspective of an EMR cluster or a user of certain nodes in the cluster, you can use [Cost Allocation Tags](https://intl.cloud.tencent.com/document/product/555/32276).

- **Cost allocation by cluster**: This feature allows you to view cluster bills by business department. When different departments use different EMR clusters, it is necessary to allocate costs by department. Cluster tags can be set for different departments for cost allocation and associated with other resources in the EMR cluster, such as EMR nodes, cloud disks, and metadata.
- **Cost allocation by node**: This feature allows you to view node bills by business department. When multiple departments share the same EMR cluster, it is necessary to allocate costs by task node used by different departments. Node tags can be set for different departments for cost allocation and associated with other resources on the EMR node, such as CVM, system disks, and data disks.

## Prerequisites
You have set **Tag** to a cost allocation tag as described in [Cost Allocation Tags](https://intl.cloud.tencent.com/document/product/555/32276). After the cost allocation tag takes effect, it will be displayed in bills within 24 hours, subject to the data caching mechanism.

## Directions
### Cost allocation by cluster
1. Configure a cost allocation tag.
	- Configure a cost allocation tag for a new cluster:
		- Create a cluster: Log in to the [EMR console](https://console.cloud.tencent.com/emr) and select **Create Cluster** on the **Cluster list** page as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/7402372e02b50580d7e430444aa473ff.png)

		- Select a cost allocation tag: In **Basic configuration** > **Advanced settings**, select the configured cost allocation tag as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/e2fb8777b122379a6b263eb34523e49c.png)
	- Configure a cost allocation tag for an existing cluster:
		- Add a cost allocation tag for a cluster: Log in to the [EMR console](https://console.cloud.tencent.com/emr), select the target cluster on the **Cluster list** page, and click **More** > **Edit tag** at the top as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/93bb213f6e6c4b6947529a3fa3fb86f9.png)
		- Add, modify, or delete cost allocation tags as needed in the **Edit tag** pop-up window.
![](https://qcloudimg.tencent-cloud.cn/raw/f0af8b0ff374614d42dca5dfb59a687f.png)

>? You can batch edit tags for up to 20 clusters at a time.

2. View the cluster's cost allocation tag.
	- Set the **Tag** field in the list: Click the **set** icon in the **Cluster list**.
![](https://qcloudimg.tencent-cloud.cn/raw/851508fd0c37c847f5744804e7eb0221.png)
Select the **Tag** field as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/d331f5321af853cac31f6e370ad5b3e6.png)
	- View the cluster's cost allocation tag as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/fb542f6be94dfb569e0a122d7cdf09ac.png)

3. View the node's cost allocation tag.
A cost allocation tag assigned to a cluster will be automatically inherited by CDB (such as TencentDB for MySQL), CBS (system disks and data disks), and CVM in the cluster.
	- Set the **Tag** field of a node: Select **Cluster list** > **Cluster name** > **Resource Management** > **Node List** and click the **set** icon.
![](https://qcloudimg.tencent-cloud.cn/raw/5fd76595e1fe389c499977f74eaa0e3f.png)
Select the **Tag** field as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/df84ccd0cb1a396199926398e68deca7.png)
	- View the node's cost allocation tag as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/63c9b964742c1d16a7444b712dbc632e.png)

4. Configure a cost allocation tag for an added node.
After a cluster is created, new MetaDB instances or manually /automatically added nodes will not automatically inherit the cluster's cost allocation tag; instead, they need to be manually associated with the tag.
	- Configure a cost allocation tag for an added node: Click **Cluster name** > **Resource Management** > **Scale Out** > **Configure tag (cluster-level tag)** to associate an added node with the cluster's cost allocation tag as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/d9966b6cbcfb8575c2ec2f8cdbc44f4e.png)
	- Configure a cost allocation tag for a MetaDB instance: Click **Cluster name** > **Cluster Service** > **Add Component**, select the Hive component for example, and select the cost allocation tag (cluster-level tag) to associate the new MetaDB instance with the cluster's cost allocation tag as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/05a35054e9db5746258d0e49b5592bdd.png)

>? Cluster fees = fees incurred by existing resources + fees incurred by new resources; therefore, new resources must be associated with the cluster's cost allocation tag in order to be included in the calculation of cluster fees.

5. View the cluster's bills.
On the **Bill Overview** page in the [Billing Center](https://console.cloud.tencent.com/expense/bill/overview), select the bill for the target month and select **By Tag** and **Cluster level** to view the cluster fees.
![](https://qcloudimg.tencent-cloud.cn/raw/2d4cef56755710fefb2f737e656fc42f.png)

>? 
>- As you have selected the Hive metadata storage location for association with MetaDB when creating the cluster, the fees here consist of the fees of nodes, CBS, and TencentDB for MySQL.
>- As a new pay-as-you-go cluster is billed by hour, its billing data will start to be displayed after one hour.

6. Download bills.
In the [Billing Center](https://console.cloud.tencent.com/expense/bill/overview), select **Bills** > **Download Center** to select bills for different months by bill type (L0, L1, L2, or L3).
![](https://qcloudimg.tencent-cloud.cn/raw/7c9f987e12de7b78474178efc39e46f1.png)

>? 
>- L0: Electronic bill in PDF format, which can be easily used for requesting payments or archiving bills.
>- L1: Multidimensional consolidated bill, which provides billing data by product, project, region, or tag for you to view bills easily.
>- L2: Resource bill, which provides billing data by resource ID (instance).
>- L3: Detailed bill, which provides billing data at the finest granularity. For example, if a product is billed by hour, a new billing data entry will be displayed per hour per component. For all bills except L3 bills, the billing data for the previous month can be queried in the current month, while the billing data for the current month can be queried only after the first day of the next month.

### Cost allocation by node
1. Configure a cost allocation tag for a node.
Click **Resource Management** > **Node List** > **Select node** > **Edit tag**.
![](https://qcloudimg.tencent-cloud.cn/raw/9705069ecff82539bbc045f46ee19b58.png)
You can add, modify, or delete a cost allocation tag for a node as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/cd81df662f930b488c949456fd447892.png)
2. Set the **Tag** field of a node.
Select **Cluster list** > **Cluster name** > **Resource Management** > **Node List** and click the **set** icon.
![](https://qcloudimg.tencent-cloud.cn/raw/aaff1123125d0f6e69c5f6a30c3eec57.png)
Select the **Tag** field as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/19af9c6bdb22fde097f8770f489e713d.png)
3. View the node's cost allocation tag as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/aebe90c2ab7af63ce88f35573b685442.png)
4. View the node's bill.
    On the **Bill Overview** page in the **Billing Center**, select the bill for the target month and select **By Tag** and the cost allocation tag of the added node to view the node fees.
    ![](https://qcloudimg.tencent-cloud.cn/raw/09d7b4a0014a474d08e0f30a8a47716b.png)
5. Download bills.
The steps are the same as those for downloading cluster bills.





