腾讯云用户可以使用支付方式模块查询，添加，删除和设置默认支付方式，用户需保留至少一个支付方式，账号未绑定支付方式可参照下方流程进行绑定。

## 付款方式页面
在 [付款方式页面](https://console.intl.cloud.tencent.com/accountv1/paymentmethods) 中，用户可以查询其现有的付款方式，包括付款类型，帐户ID，付款人姓名，状态和操作。
 ![](https://qcloudimg.tencent-cloud.cn/raw/2227c55e715d1e1c5601bd17bfd13e51.png)

>! 
>- 用户可以单击“Current Default”将其标记为默认付款方式。
>- 用户只能使用一种默认付款方式，系统按月于到期还款日（每月10号）或可用额度不足时，对您账户的默认支付方式进行托收还款。

## 添加付款方式
 ![](https://qcloudimg.tencent-cloud.cn/raw/e25dc2b3158cfa06d9565cf87d4fdcb7.png)
- 登录腾讯云官网**费用中心** > **资金管理** > <b>[支付方式](https://console.intl.cloud.tencent.com/accountv1/paymentmethods)</b>，单击**添加付款方式**按钮跳转到添加付款方式页面，输入信用卡或借记卡信息绑定支付方式。
 ![](https://staticintl.cloudcachetci.com/yehe/backend-news/BYnm001_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_1685432126964.png)
- 成功添加付款帐户后，用户的腾讯云帐户将与该付款帐户关联，然后用户可以使用该付款帐户进行充值和付款。

## 删除付款方式
- 用户可以单击“Delete”来删除所选的付款方式。但是无法删除默认付款方式，您可以选择有效的付款方式或添加有效的付款方式，然后点击"Set as default"以将其标记为默认付款方式。之后，先前的默认付款方式将成为可以保留或删除的通用付款方式。
![](https://main.qcloudimg.com/raw/69550d8f13d6df0e35225712d9dc614c.png)

## 常见问题
1.未绑卡的如何绑定付款卡？
可直接在 [付款方式页面](https://console.intl.cloud.tencent.com/accountv1/paymentmethods) 中添加付款方式。

2.绑定了PayPal 的如何绑定付款卡？
需前往在 [付款方式页面](https://console.intl.cloud.tencent.com/accountv1/paymentmethods) 中添加新的付款方式，点击"Set as default"以将其标记为默认付款方式，针对先前绑定的PayPal付款方式可单击“Delete”来进行删除所选的付款方式。

3.目前支持几种付款方式？
腾讯云目前支持信用卡、借记卡付款。

4.我可以设置多少个付款帐户？
平台最多支持绑定5张付款卡，如若超出将无法添加新卡，您可通过删除不用的付款卡后再添加新的付款账户，但是默认付款账户仅有一个。

5.目前支持哪种信用卡？
支持六种信用卡：VISA，万事达，JCB，DISCOVER，AMEX和银联。



