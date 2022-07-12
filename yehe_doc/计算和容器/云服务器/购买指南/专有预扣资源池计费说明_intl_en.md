<dx-alert infotype="explain" title="">
Dedicated Reservation is in the beta test phase now. To try it out, please contact your sales rep.
</dx-alert>


## Billing Mode
- The idle resources in the reservation will incur an idle fee charged at [the price of pay-as-you-go instances](https://intl.cloud.tencent.com/document/product/213/2180). 

## Billing Description
Resource idle fee = [Price of pay-as-you-go instance](https://intl.cloud.tencent.com/document/product/213/2176) × 0.3
<dx-alert infotype="explain" title="">
For the specific price, the "Idle Fee" on the page of creating a reservation shall prevail.
</dx-alert>




## Billing Examples
You can understand the billing rules of **one-time reservation** and **repeated reservation** through the following examples:

<dx-tabs>
::: One-time Reservation
<table>
<tr>
<th width="11%">Date</th><th>Operation</th><th>Billing details</th><th>Remarks</th>
</tr>
<tr>
<td>Jan. 1</td>
<td>Create a reservation containing three instances and valid for one month</td>
<td>After the reservation is successfully created, the three instances will incur an idle fee.</td>
<td>The idle fee will charged by second and settled by hour</td>
</tr>
<tr>
<td>Jan. 2</td>
<td>Use one of the reservation resources to create one instance with the same configuration</td>
<td rowspan=3>The unused two instances continue to incur an idle fee charged by pay-as-you-go mode</td>
<td>- </td>
</tr>
<tr>
<td>Jan. 3</td>
<td>Return the instance created on Jan. 1</td>
<td>The instance will be released</td>
</tr>
<tr>
<td>···</td>
<td>None</td>
<td>-</td>
</tr>
<tr>
<td>Feb. 1</td>
<td>None</td>
<td>The reservation expired. The instances no longer incur an idle fee</td>
<td>The unused two instances will be released</td>
</tr>
</table>
The use of a one-time reservation is shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/cd41ffb0caea8b7b81a71e5d45d45333.png)

:::
::: Repeated Reservation
<table>
<tr>
<th width="11%">Date</th><th>Operation</th><th>Billing details</th><th>Remarks</th>
</tr>
<tr>
<td>Jan. 1</td>
<td>Create a reservation containing three instances and valid for one month</td>
<td>After the reservation is successfully created, the three instances will incur an idle fee.</td>
<td>The idle fee will charged by second and settled by hour</td>
</tr>
<tr>
<td>Jan. 2</td>
<td>Use one of the reservation resources to create one instance with the same configuration</td>
<td>The unused two instances continue to incur an idle fee charged by pay-as-you-go mode</td>
<td>Pay-as-you-go instances can be created</td>
</tr>
<tr>
<td>Jan. 3</td>
<td>Return the instance created on Jan. 1</td>
<td>The three instances in the reservation will incur an idle fee</td>
<td>The instance will be returned to the reservation if the reservation has not expired</td>
</tr>
<tr>
<td>Jan. 4</td>
<td>Use two of the reservation resources to create two instances with the same configuration</td>
<td>The unused one instance continues to incur an idle fee charged by pay-as-you-go mode</td>
<td>Pay-as-you-go instances can be created</td>
</tr>
<tr>
<td>···</td>
<td>None</td>
<td>-</td>
<td>-</td>
</tr>
<tr>
<td>Feb. 1</td>
<td>None</td>
<td>The reservation expired. The remaining one instance no longer incurs an idle fee</td>
<td>The unused one instance will be released</td>
</tr>
<tr>
<td>Feb. 4</td>
<td>Return the two instances created on Jan. 4</td>
<td>The reservation expired. The remaining one instance no longer incurs an idle fee</td>
<td>The three instances will be released</td>
</tr>
</table>

The use of a repeated reservation is shown below:
  
![](https://qcloudimg.tencent-cloud.cn/raw/2647d27ef32cc19b7bb5737c7d58781b.png)


:::
</dx-tabs>



## See Also
- [Dedicated Reservation Overview](https://intl.cloud.tencent.com/document/product/213/43850)
- [Creating Reservation](https://intl.cloud.tencent.com/document/product/213/43851)
- [Viewing Aggregated List of Dedicated Reservation](https://intl.cloud.tencent.com/document/product/213/43852)
- [Viewing the List of Created Reservations](https://intl.cloud.tencent.com/document/product/213/43853)
