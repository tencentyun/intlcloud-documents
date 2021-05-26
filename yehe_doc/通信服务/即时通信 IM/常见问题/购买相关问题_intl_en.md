### Do IM Pro edition and IM Flagship edition have a DAU limit?
Pro edition and Flagship edition do not have an upper limit on DAU. The first 10,000 DAU per month is free. DAU over free quota will be charged at 149.99 USD/10,000 DAU per month, with counts less than 10,000 billed as 10,000. The DAU fee is pay-as-you-go on a monthly basis. Fees incurred within a month will be deducted on the third day of the next month.
If the DAU of each day within a month is lower than 10,000, no DAU fees will be incurred for that month. If for any day within a month, the DAU is higher than 10,000, you will be charged based on the highest DAU value in that month. 
For more information on billing rules, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

### What should I do if I received an error when creating 100 accounts in IM?
You can create up to 100 accounts in the Trial edition. To use the accounts in a production environment, you need to configure a standard billing plan for each SDKAppID. In addition, you can call the [v4/im_open_login_svc/account_delete](https://intl.cloud.tencent.com/document/product/1047/34955) API to delete unwanted accounts in the Trial edition. **User data cannot be recovered once the account is deleted**, so proceed with caution.

### Does IM support global access?
IM provides reliable, secure network connections with global coverage. With its proprietary multi-level optimal addressing algorithm, IM can perform scheduling across the entire network. When terminals log in, the IM SDK connects to the nearest access nodes. IM access nodes include the following:

- China: South China, North China, East China, Hong Kong, and Taiwan
- Other regions:
 - Asia: Singapore, Indonesia, UAE, Thailand, Japan, Vietnam, India, South Korea, and Philippines
 - Europe: United Kingdom, Netherlands, Germany, Italy, Norway, France, Russia, and Spain
 - South America: Brazil
 - North America: United States, Canada, and Mexico
 - Oceania: Australia
 - Africa: South Africa and Nigeria


### IM allows the creation of up to 50 audio-video groups. How many audio-video groups can be created after I created 3 and then deleted 3?
If you created 3 audio-video groups and then deleted 3, you can still create 50. The number of audio-video groups you can create is a net value. Deleted groups do not count against the quota. If you have an audio-video group that has no members but has not been deleted, it is still included in the quota.

### How many groups can I create?
The number of groups that you can create is unrestricted, but if you create more than 100,000 groups, you will need to pay certain resource fees. The total group count is a net value. If you delete a group, it is not included in the total group count.
The fees are as follows: 149.99 USD/month per 100,000 groups (counts less than 100,000 will be billed as 100,000) if the total group count exceeds 100,000. For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).
