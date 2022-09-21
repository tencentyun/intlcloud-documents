## What is TenDI Captcha?
TenDI Captcha provides web and app developers with comprehensive multi-dimensional human verification services through trajectory analysis, characteristic identification, anti-emulator, and other security mechanisms. It safeguards business security in various scenarios like registration and login, marketing offers, commenting/posting/polling, and data protection.

This service helps you solve the following security problems:

- Preventing credential stuffing attacks as well as bulk registration of multiple accounts by bots.
- Preventing click farming and coupon abuse by bots in campaigns.
- Preventing ad spamming, malicious bumping, and poll fraud.
- Preventing from website content and data theft by bots and crawlers.

## Features
### Slider CAPTCHA

This feature allows users to quickly complete verification by simply sliding the knob. Its ease of use and powerful risk control make it suitable for most human verification scenarios.
![](https://qcloudimg.tencent-cloud.cn/raw/869e4bb476380a2845a1eaee58886456.gif) 

### Smart verification

This feature intelligently identifies user characteristics. It requests suspicious users to answer verification questions and allows trusted users to directly proceed. This can greatly improve the experience of human users. The verification process is as follows:

![](https://qcloudimg.tencent-cloud.cn/raw/a9ab053404da39b55aa221c58554dbf6.png)

### Multi-dimensional defense

During the verification, ten security protection mechanisms such as dynamic encryption, virtual machine reinforcement, and anti-emulator are used to defend against malicious activities of the black market.

#### Controllable risk control level

TenDI Captcha supports three risk control levels — Experience-Oriented, Balanced, and Security-Focused.

![](https://qcloudimg.tencent-cloud.cn/raw/5bfbe8fe70ada4e6feb5014ad304f95b.png)

#### Verification results

TenDI Captcha automatically blocks malicious user requests using multiple defense approaches.

| To be verified                                               | Trusted user: Verification successful                        | Malicious user: Verification blocked                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| <img src="https://qcloudimg.tencent-cloud.cn/raw/bc1fdebc5f9affaf7146c45a54ca02de.png" style="zoom:80%;" /> | <img src="https://qcloudimg.tencent-cloud.cn/raw/60827077028e0df8fe82cf5fd1668717.png" style="zoom:80%;" /> | <img src="https://qcloudimg.tencent-cloud.cn/raw/b5d305d285d10ea6b1a4d0b0b3056c65.png" style="zoom:80%;" /> |

### Statistics

TenDI Captcha provides data that is updated every minute so that you can keep track of business security in real time.

<table class="tg">
<thead>
  <tr>
    <th class="tg-0pky">Indicator</th>
    <th class="tg-0pky">Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0pky">Requests</td>
    <td class="tg-0pky">The number of times the client loads verification.</td>
  </tr>
  <tr>
    <td class="tg-0pky">Verifications</td>
    <td class="tg-0pky">The number of verifications initiated after a user responds to the verification question.</td>
  </tr>
  <tr>
    <td class="tg-0pky">Passed verifications</td>
    <td class="tg-0pky">The number of passed verifications.</td>
  </tr>
  <tr>
    <td class="tg-0pky">Failed verifications</td>
    <td class="tg-0pky">The number of failed and blocked verifications.</td>
  </tr>
  <tr>
    <td class="tg-0pky">Failed verifications for wrong responses</td>
    <td class="tg-0pky">The number of verifications blocked due to the wrong responses given by the user.</td>
  </tr>
  <tr>
    <td class="tg-0pky">Verifications blocked by security policies</td>
    <td class="tg-0pky">The number of verifications blocked by security policies.</td>
  </tr>
  <tr>
    <td class="tg-0pky">Ticket verifications</td>
    <td class="tg-0pky">The number of ticket verifications initiated by a server.</td>
  </tr>
  <tr>
    <td class="tg-0pky">Passed ticket verifications</td>
    <td class="tg-0pky">The number of passed ticket verifications.</td>
  </tr>
  <tr>
    <td class="tg-0pky">Failed ticket verifications</td>
    <td class="tg-0pky">The number of failed ticket verifications.</td>
  </tr>
</tbody>
</table>
## Use limits

### QPS limit

1. **Queries Per Second** (QPS) is limited to 1,000 for ticket verification.
2. When QPS exceeds 1,000 for the ticket verification API calls, **an error is returned** (RequestLimitExceeded).
3. To change the limit, submit a ticket or contact us.

## FAQs

If you have any questions when using the service, please see [FAQs About Features](https://intl.cloud.tencent.com/document/product/1159/49691).
