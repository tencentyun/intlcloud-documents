### Do IM pro edition and IM flagship edition have DAU limits?
Fees charged for usage exceeding the free quota of the professional or flagship package are based on DAU and peak group count that exceed the free quota. Fees are charged according to their peak values within a calendar month on a postpaid basis. Fees incurred will be deducted on the third day of the next month.
If the DAU of each day within a calendar month is lower than 10,000, no DAU fees are incurred for that month. If the DAU is higher than 10,000 on any day within a calendar month, you will be charged based on the highest DAU value in that month. 
For more billing information, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

### What should I do if an error occurs after I have created 100 accounts in IM?
You can create up to 100 accounts in the trial edition. To use the accounts in a production environment, you need to configure a standard billing plan for each SDKAppID. In addition, you can call the [API for deleting accounts](https://intl.cloud.tencent.com/document/product/1047/34955) to delete unwanted accounts in the trial edition. **User data cannot be recovered after the accounts are deleted**, so proceed with caution.

### Does IM support global access?
IM provides highly interconnected, reliable, and secure global network connections and proprietary multi-level optimal addressing algorithms to implement scheduling across private and public networks. When terminals log in, the IM SDK connects to the nearest access nodes or cache nodes. Global access and cache nodes include the following:

- China: South China, North China, East China, Hong Kong, Taiwan regions, etc.
- Other countries (regions):
 - Asia: Singapore, Indonesia, UAE, Thailand, Japan, Vietnam, and India
 - Europe: United Kingdom, Netherlands, Germany, Italy, Norway, France, and Russia
 - South America: Brazil
 - North America: United States, Canada, and Mexico
 - Oceania: Australia
 - Africa: South Africa

### Since IM allows the creation of up to 50 AVChatRooms, how many AVChatRooms can be created after I create 3 and then disband 3?
If you create 3 AVChatRooms and then disband 3, you can still create 50. The number of AVChatRooms you can create is a net value. Disbanded AVChatRooms do not count against the quota. If you have an AVChatRoom that has no members but has not been disbanded, it is still included in the quota.

### What is the maximum number of groups I can create?
The number of groups that you can create is unrestricted, but if you create more than 100,000 groups, you will need to pay certain resource fees. The cumulative group count is a net value. If you disband a group, it is not included in the total group count.
The fees are as follows: if the cumulative group count exceeds 100,000, the excessive part will be charged 149.99 USD/month per 100,000 groups (counts less than 100,000 will be billed as 100,000). For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).
