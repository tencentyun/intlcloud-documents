CTSDB supports two configuration modes: QuickConfig and CustomConfig, as detailed below. We recommend you select an appropriate instance specification based on your needs in three aspects: performance, capacity, and other factors. For instance performance data, please see [Performance](https://intl.cloud.tencent.com/document/product/1100/40938).

Go to the [CTSDB purchase page](https://intl.buy.cloud.tencent.com/ctsdb) and select the mode as desired.

## QuickConfig
CTSDB provides the QuickConfig mode, where you only need to select the volume of data to be stored, and the system will automatically create an instance with three nodes and two replicas. In addition, when the system automatically selects the node configuration, under the premise that the nodes have the same storage capacity, it will preferably use the node configuration with fewer CPU cores and smaller memory for the instance.

## CustomConfig
In CustomConfig mode, you can select the number of nodes, node specification, and node capacity as desired as shown below:
![](https://main.qcloudimg.com/raw/59103f74ee45b5438add945e58b4a295.png)
>!Be cautious when selecting a two-node instance, as it cannot fully ensure data integrity due to the characteristics of a distributed system.
