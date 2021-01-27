## Protection Description
In order to improve the protection effect and reduce the risk of false blocking during protection, Anti-DDoS Advanced has three protection levels for CC attacks for your choice, and the "normal" level is used by default.
- **Loose**: this level can be used when the protected website has no obviously exceptional traffic. It performs a looser human-machine recognition algorithm check on all requests made to the protected website, that is, each visitor is verified and only successfully authenticated visitors are allowed to access the website. As the CC protection policy at this level is relatively loose, there may be a risk of passing through a small number of exceptional requests.
- **Normal**: this level is the default CC protection level. It is recommended if you find that the protected website is under CC attacks. Compared with the loose level, the normal level of CC protection can cover most of attack scenarios and defend against most of CC attacks. In addition, it performs a human-machine recognition algorithm check on all requests made to the protected website, that is, each visitor is verified and only successfully authenticated visitors are allowed to access the website.
- **Strict**: the CC attack protection policy is stricter at this level and can defend against more complex CC attacks. In addition, it performs a strict human-machine recognition algorithm check on all requests made to the protected website, that is, each visitor is verified and only successfully authenticated visitors are allowed to access the website. Due to the strict authentication mechanism in this mode, some normal requests may be blocked by mistake.
>!
	- The protection algorithms used at the above three CC protection levels are only applicable to webpages and HMTL5 pages.
	- If the business of the visited website is an API or a native app, as such businesses generally cannot respond to algorithm-based authentication normally, there is a great risk of false blocking.
	- If you need CC protection for API or native app businesses, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for protection policy customization.

## Directions
By default, the normal level of CC protection is used for domain names of websites protected by Anti-DDoS Advanced instances. You can freely adjust the protection mode according to your actual business needs.
1. Log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/bgp_v2), select **Anti-DDoS Advanced** > **Protection Configuration** on the left sidebar, and click **CC Protection** on the protection policy page.
2. On the CC protection page, find the HTTP CC protection and HTTPS CC protection section at the bottom of the page, select the domain name that requires CC protection under the corresponding protocol, and set the CC protection level.
>!
	- The CC protection level policy only takes effect for domain names with the access configured as website business (layer-7 access).
	- If you haven't connected the website domain name to be configured to an Anti-DDoS Advanced instance, please connect it first as instructed in [Connecting Website Business](https://intl.cloud.tencent.com/document/product/297/34102).

For more information, please see [Managing CC Protection Policy](https://intl.cloud.tencent.com/document/product/297/34095).
