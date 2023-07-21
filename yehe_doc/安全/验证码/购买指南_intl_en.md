## Billing overview
### Billing prerequisites

Both the business client and server have completed corresponding code integration. Captcha will be billed based on the **number of ticket verifications** initiated by the server.

### Free trial

When new users log in to the [Captcha console](https://console.cloud.tencent.com/captcha/graphical) and activates the service, they can get a free quota of 100 times of ticket verification.

>! Each Tencent Cloud primary account can get the free quota only once.

### Billing mode

After the free quota is used up, you will be billed on a **postpaid daily** basis according to our cumulative tiered pricing structure.

#### Pay-as-you-go tiered price table

<table>
<thead>
<tr>
<th align="left">Ticket Verifications (Times/day)</th>
<th>USD/Time</th>
</tr>
</thead>
<tbody><tr>
<td>(0,100]</td>
<td>0.005</td>
</tr>
<tr>
<td>(100,1000]</td>
<td>0.002</td>
</tr>
<tr>
<td>(1000,10000]</td>
<td>0.0008</td>
</tr>
<tr>
<td>(10000,100000]</td>
<td>0.0002</td>
</tr>
<tr>
<td>(100000,1000000]</td>
<td>0.0001</td>
</tr>
<tr>
<td>> 1000000</td>
<td>0.00005</td>
</tr>
</tbody></table>

#### Billing example

For example, if the number of ticket verifications on a day is 200, according to the pay-as-you-go tiered price table, some ticket verifications fall within the range of (0,100], and some fall within the range of (100,1000]. Based on the cumulative tiered pricing mode, the fees for that day would be 0.005 × 100 + 0.002 × 100 = USD 0.7. The pay-as-you-go bill will be output the next day and the fees will be deducted directly from the account balance.

## Overdue payment policy

**Service suspension upon a 7-day overdue payment**: If your account has an overdue payment for more than 7 days, the Captcha service will be suspended. After the service is suspended, you will be unable to use the Captcha console and calling the ticket verification API will return an error.

>! If you are a customer of a Tencent Cloud partner, the rules regarding resources when there are overdue payments are subject to the agreement between you and the partner.

## FAQs

For more information, please see [Billing FAQs](https://intl.cloud.tencent.com/document/product/1159/49690).
