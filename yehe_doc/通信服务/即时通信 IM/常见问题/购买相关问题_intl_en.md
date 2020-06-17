### Do IM Pro Edition and IM Flagship Edition have a DAU limit?
Pro Edition and Flagship Edition do not have an upper limit on DAU. The first 10,000 DAU per month is free. DAU over free quota will be charged at USD149.99/10,000 DAU per month, with counts less than 10,000 billed as 10,000. The DAU fee is pay-as-you-go on a monthly basis. Fees incurred within a calendar month will be deducted on the third day of the next month.
If the DAU of each day within a calendar month is lower than 10,000, no DAU fees will be incurred for that month. If for any day within a calendar month, the DAU is higher than 10,000, you will be charged based on the highest DAU value in that month. 
For more information on billing rules, see [Billing Overview](https://intl.cloud.tencent.com/document/product/1047/34350).

### What should I do if I received an error when creating 100 accounts in IM?
You can create up to 100 accounts in the Trial Edition. If you need to use the accounts in a production environment, you need to configure a standard billing plan for each SDKAppID. In addition, you can call the [API for deleting accounts](https://intl.cloud.tencent.com/document/product/1047/34955) to delete unwanted accounts in the Trial Edition. **User data cannot be recovered once the account is deleted**, so proceed with caution.

### Does IM support global access?
IM provides reliable and secure network connections with global coverage. With its proprietary multi-level optimal addressing algorithm, IM can perform scheduling across the entire network. When terminals log in from outside Mainland China, the IM SDK connects to the nearest access nodes or cache nodes. Global access and cache nodes include the following:
- China: South China, North China, East China, and Hong Kong
- Global:
 - Asia: Singapore, Indonesia, UAE, Thailand, Japan, Vietnam, and India
 - Europe: United Kingdom, Netherlands, Germany, Italy, Norway, France, and Russia
 - South America: Brazil
 - North America: United States, Canada, and Mexico
 - Oceania: Australia
 - Africa: South Africa

### IM allows the creation of up to 50 audio-video chat rooms. How many audio-video chat rooms can be created after I created 3 and then disbanded 3?
If you created 3 audio-video chat rooms and then disbanded 3, you can still create 50. The number of audio-video chat rooms you can create is a net value. Disbanded chat rooms do not count against the quota. If you have an audio-video chat room that has no members but has not been disbanded, it is still included in the quota.

### What’s the maximum number of groups I can create?
The number of groups that you can create is unrestricted, but if you create more than 100,000 groups, you will need to pay certain resource fees. The cumulative group count is a net value. If you disband a group, it is not included in the total group count.
The fees are as follows: 149.99 USD/month per 10,000 groups (counts less than 100,000 will be billed as 100,000) if the cumulative group count exceeds 100,000. For more information, see the [Price Specification](https://intl.cloud.tencent.com/document/product/1047/34350).