## Outbound Bandwidth Cap (Downstream Bandwidth)

The public network bandwidth cap refers to the upper limit of outbound bandwidth by default, i.e. the bandwidth going out from CVM instances. The public bandwidth cap varies for different network billing mode. See below for details:
- The following rules apply to instances created before 00:00, February 24, 2020:
<table>
<tr><th rowspan="2">Network Billing Mode</th><th colspan="2">Instance</th><th rowspan="2">Bandwidth Cap Range (Mbps)</th></tr>
<tr><th>Instance Billing Mode</th><th>Instance Configuration</th></tr>
<tr><td>Bill-by-traffic</td><td>Pay-as-you-go instances</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>Bill-by-bandwidth</td><td>Pay-as-you-go instances</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>Bandwidth package</td><td colspan="2">All</td><td>0 - 1,000 or uncapped</td></tr>
</table>

- The following rules apply to instances created after 00:00, February 24, 2020:
<table>
<tr><th rowspan="2">Network Billing Mode</th><th colspan="2">Instance</th><th rowspan="2">Bandwidth Cap Range (Mbps)</th></tr>
<tr><th style="width: 18.5607%;">Instance Billing Mode</th><th style="width: 24.5814%;">Instance Configuration</th></tr>
<tr><td>Bill-by-traffic</td><td>Pay-as-you-go instances</td><td>All</td><td>0 - 100</td></tr>
<tr><td>Bill-by-bandwidth</td><td>Pay-as-you-go instances</td><td>All</td><td>0 - 100</td></tr>
<tr><td>Bandwidth package</td><td colspan="2">All</td><td>0 - 1,000 or uncapped</td></tr>
</table>


## Inbound Bandwidth Cap (Upstream Bandwidth)

The inbound bandwidth of the public network refers to the bandwidth that flows into CVM instances.
- If the fixed bandwidth purchased by users is greater than 10 Mbps, Tencent Cloud assigns a public network inbound bandwidth that is equal to the purchased bandwidth.
- If the fixed bandwidth purchased by users is less than 10 Mbps, Tencent Cloud assigns 10 Mbps public network inbound bandwidth.

## Increasing the Bandwidth Cap

You can choose one of the following adjustment methods based on your needs:
- [Adjusting the network billing mode (bill-by-bandwidth)](#AdjustNetworkModeByBandwidth)
- [Adjusting the network billing mode (bill-by-bandwidth-package)](#AdjustNetworkModeByBandwidthPackage)

If you cannot adjust your instance or network billing mode, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%20CVM&step=1) to request to increase the bandwidth cap. We will get back to you as soon as possible.

<span id="AdjustNetworkModeByBandwidth"></span>
### Adjusting the network billing mode (bill-by-bandwidth)

1. Change the billing mpde of bill-by-traffic instances to bill-by-bandwidth. For detailed operations, see [Adjusting the Network Configuration](https://intl.cloud.tencent.com/document/product/213/15517).
2. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
3. Locate the instance for which you want to adjust the bandwidth and choose **More** > **Resource Adjustment** > **Adjust Network** on the right.
4. In the **Adjust Network** window that appears, set the target bandwidth cap and click **OK**, as shown in the following figure.

<span id="AdjustNetworkModeByBandwidthPackage"></span>
### Adjusting the network billing mode (bill-by-bandwidth-package)

1. Change the billing mode of bill-by-traffic instances to bill-by-bandwidth-package.
> Uncapped bandwidth is supported for instances in the bandwidth package.
>
2. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
3. Locate the instance for which you want to adjust the bandwidth and choose **More** > **Resource Adjustment** > **Adjust Network** on the right.
4. In the **Adjust Network** window that appears, set the target bandwidth cap and click **OK**, as shown in the following figure.
![](https://main.qcloudimg.com/raw/4e6a0a6556532e91d7b3101c97c62b77.png) 

