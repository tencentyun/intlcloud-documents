> After creating a bandwidth package, you need to add the desired EIPs to the package to share bandwidth.

## Restrictions
1. Only bill-by-traffic and bill-by-hour EIPs can be added to the bandwidth package. Monthly subscription EIPs cannot be added to the shared bandwidth package.
2. After an EIP is added to the bandwidth package, the original billing mode of EIP is changed to “bill with bandwidth package”. No additional fees are charged for the traffic and bandwidth, but if the EIP is idle, you still need to pay the idle fee.
3. No matter whether the EIP is added to a bandwidth package, an idle fee will incur if the EIP is not bound with any instances. You can bind the EIP to an instance to avoid incurring of the idle fee. 
4. Up to 100 EIPs can be added to a single bandwidth package.

## Directions
1. Log in to the [Virtual Private Cloud Console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **Bandwidth Package** on the left sidebar.
3. Select a region, find the target bandwidth package instance in the list, and click its instance ID to go to the instance details page.
4. In the "Bandwidth Pack Resources" section on the details page, click **+ Add Resource**.
5. In the pop-up window, select the resource type and resource instance and click **Confirm**.
