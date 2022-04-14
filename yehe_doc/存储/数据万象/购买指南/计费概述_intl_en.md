## Billing Mode

CI is pay-as-you-go (postpaid).

- **Pay-as-you-go (postpaid) billing mode**: Fees are charged by the **actual usage**. Amounts are deducted and the bill for the previous month is generated on the first day of each month. When you start using CI, it will be pay-as-you-go by default, so you do not need to purchase it.


## Pricing

For CI pricing details, see Pricing Overview.

As the data storage service of CI is based on COS, the storage fees will be listed on COS bills. For more information, see COS Pricing Overview.


## Amount Freezing Mechanism
After the bill for the current month is settled, 120% of its amount will be frozen for the next month. During settlement the next month, this frozen amount will be unfrozen first for deduction.




## Billable Items

CI billable items include image processing, content recognition, content moderation, media processing, file processing, and traffic.

## Billing Cycles

The billing cycles and sequence of CI billable items are as detailed below:

<table>
   <tr>
      <th colspan=2>Billable Item</td>
      <th>Billing Cycle</td>
      <th>Description</td>
      <th>Billing Sequence</td>
   </tr>
   <tr>
      <td rowspan=4>Image processing</td>
      <td>Basic image processing</td>
      <td rowspan=4>Monthly</td>
      <td rowspan=21>Amounts are deducted and the bill for the previous month is generated on the first day of each month</td>
      <td rowspan=4>Free tier > resource pack > pay-as-you-go, or only pay-as-you-go in case of no free tier</td>
   </tr>
   <tr>
      <td>Advanced image compression</td>
   </tr>
   <tr>
      <td>Guetzli image compression</td>
   </tr>
   <tr>
      <td>Blind watermarking</td>
   </tr>
   <tr>
      <td rowspan=4>Content moderation</td>
      <td>Image moderation</td>
      <td rowspan=4><li>Monthly for automatic moderation<li>Daily for human moderation</td>
      <td rowspan=4>Free tier > resource pack > pay-as-you-go, or only pay-as-you-go in case of no free tier</td>
   </tr>
   <tr>
      <td>Video moderation</td>
   </tr>
   <tr>
      <td>Audio moderation</td>
   </tr>
   <tr>
      <td>Text moderation</td>
   </tr>
   <tr>
      <td rowspan=4>Content recognition</td>
      <td>Image tagging (displayed as content recognition on bills)</td>
      <td rowspan=4>Monthly</td>
      <td rowspan=4>Free tier > resource pack > pay-as-you-go, or only pay-as-you-go in case of no free tier</td>
   </tr>
   <tr>
      <td>QR code recognition</td>
   </tr>
   <tr>
      <td>Speech recognition</td>
   </tr>
   <tr>
      <td>Face effect</td>
   </tr>
   <tr>
      <td rowspan=6>Media processing</td>
      <td>Video frame capturing</td>
      <td rowspan=6>Monthly</td>
      <td rowspan=9>Free tier > resource pack > pay-as-you-go, or only pay-as-you-go in case of no free tier</td>
   </tr>
   <tr>
      <td>Video metadata acquisition</td>
   </tr>
   <tr>
      <td>Animated image generation</td>
   </tr>
   <tr>
      <td>Intelligent thumbnail generation</td>
   </tr>
   <tr>
      <td>File transcoding (audio/video transcoding)</td>
   </tr>
   <tr>
      <td>Audio/Video splicing</td>
   </tr>
   <tr>
      <td rowspan=2>File processing</td>
      <td>File preview</td>
      <td rowspan=2>Monthly</td>
   </tr>
   <tr>
      <td>Privacy and compliance protection</td>
   </tr>
   <tr>
      <td colspan=2>Traffic</td>
      <td>Monthly</td>
   </tr>
</table>

## Related Topics

1. Currently, CI offers free tiers for various features such as image processing, content moderation, content recognition, media processing, and file processing. For more information, see Free Tier. For feature or discount details, [contact us](https://intl.cloud.tencent.com/contact-sales).
2. For more information on the COS overdue policy (data retention and destruction), see COS [Payment Overdue](https://intl.cloud.tencent.com/document/product/436/10044).
