

To meet diverse requirements in different scenarios, TDMQ for Pulsar provides pro and virtual clusters. We recommend you consider the business scenario, product capabilities, and use costs when purchasing a cluster.


## Product Types

TDMQ for Pulsar product portfolio is as shown below.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/3mS4348_PRELIM__%E6%B6%88%E6%81%AF%E9%98%9F%E5%88%97%20Pulsar%20%E7%89%88_%E4%BA%A7%E5%93%81%E7%9B%AE%E5%BD%95_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US-1.jpg)

## Product Selection Process

We recommend you select a product type based on the following process.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/a7Gg310_PRELIM__%E6%B6%88%E6%81%AF%E9%98%9F%E5%88%97%20Pulsar%20%E7%89%88_%E4%BA%A7%E5%93%81%E7%9B%AE%E5%BD%95_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US-2.jpg)

## Product Selection Analysis

The characteristics of TDMQ for Pulsar cluster types are as compared below:

<table>
  <tr>
    <th class="align-left">Item</th>
    <th class="align-left">Virtual Cluster</th>
    <th class="align-left">Pro Cluster</th>
  </tr>
  <tr>
    <td>Instance type</td>
    <td>Physical resource sharing among logical tenants</td>
    <td>Physical isolation</td>
  </tr>
  <tr>
    <td>Customer group and scenario</td>
    <td>Entry-level customers with a moderate business traffic, short-term testing, and great traffic fluctuations.</td>
    <td>Top customers whose production environment has high requirements for service stability and resource isolation and generates high amounts of business traffic.</td>
  </tr>
  <tr>
    <td>Billing mode</td>
    <td>Pay-as-you-go - postpaid</td>
    <td>Monthly subscription - prepaid</td>
  </tr>
  <tr>
    <td>Billable item</td>
    <td>API call, message storage, and partition topic resource usage.</td>
    <td>Cluster specification, mainly including TPS and bandwidth.</td>
  </tr>
  <tr>
    <td>Messaging TPS limits</td>
    <td>5,000 TPS for production and consumption each per cluster per topic</td>
    <td>On-demand purchase based on different computing and storage specifications (starting from 2,000 TPS)</td>
  </tr>
  <tr>
    <td>SLA</td>
    <td><li>Data reliability: Eight 9s</li><li>Service availability: 99.95%</li></td>
    <td><li>Data reliability: Ten 9s</li><li>Service availability: 99.99%</li></td>
  </tr>
  <tr>
    <td>Pulsar engine version</td>
    <td>2.7.2</td>
    <td>2.9.2</td>
  </tr>
    <tr>
    <td>Upper limit for expansion</td>
    <td>Elastic expansion and use within a certain range</td>
    <td>Up to one million TPS with greater elasticity</td>
  </tr>

  <tr>
    <td>High availability</td>
    <td>Multi-AZ deployment in the same region is not supported.</td>
    <td>Custom multi-AZ deployment in the same region is supported to enhance disaster recovery capabilities.</td>
  </tr>
  <tr>
    <td>Event support and expert service</td>
    <td>The standard ticket service of Tencent Cloud is provided.</td>
    <td>Event support is provided for major events such as product upgrade, business launch, and promotion campaign to ensure smooth business operations.</td>
  </tr>

</table>


## Capacity Estimation

After selecting the cluster type, you need to estimate the computing and storage specifications actually needed by your business.

- **Computing specification**: In a TDMQ for Pulsar pro cluster, the computing specification indicates the upper limits on messaging TPS and bandwidth of the instance, which you can select as needed.
- **Storage specification**: You can calculate the required storage space based on the estimated message volume and size of your business.

Note that the TDMQ for Pulsar pro cluster adopts the three-copy mode for message storage.


### Purchasing a cluster

Select a region and create/purchase a cluster [here](https://buy.cloud.tencent.com/tdmq).



