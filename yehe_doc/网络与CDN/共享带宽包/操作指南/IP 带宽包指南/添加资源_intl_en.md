>?BWP is currently in beta. If you want to try it out, please [submit a ticket](https://intl.cloud.tencent.com/apply/p/8o8lmsr5nj8).

After creating a bandwidth package, you need to add EIPs and CLBs to the package to share the bandwidth.

## Restrictions
1. Only bill-by-traffic EIPs and CLBs can be added to the bandwidth package. Monthly subscription EIPs and CLBs cannot be added to the bandwidth package.
2. After an EIP or CLB is added to the bandwidth package, the EIP or CLB will be billed in the package. No additional fees will be charged for the traffic and bandwidth. However, idle EIP fees will still incur.
3. An EIP that is not bound to instances will incur an idle fee, regardless of whether the EIP is added to the bandwidth package. Please bind the EIP to an instance to avoid unnecessary fees.
4. Up to 100 resources, including EIPs and CLBs, can be added to a single bandwidth package.

## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **Bandwidth Package** on the left sidebar.
3. Select a region. Locate the target bandwidth package instance in the list, and click its ID/Name to go to the instance details page.
4. In the "Bandwidth Package Resources" section on the details page, click **Add Resource**.
5. In the pop-up window, select the resource type and resource instance and click **OK**.
![](https://main.qcloudimg.com/raw/f6340c77f748ba0929a87d322e7669e7.png)
