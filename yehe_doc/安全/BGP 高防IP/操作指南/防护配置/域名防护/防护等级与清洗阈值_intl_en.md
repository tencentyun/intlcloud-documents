## Protection Description
In order to improve the protection effect and reduce the risk of false blocking during protection, Anti-DDoS Advanced has three protection levels for CC attacks for your choice, and the "Medium" level is used by default.
- **Loose:** this level can be used when the protected website has no obviously exceptional traffic. It performs a looser human-machine recognition algorithm check on all requests made to the protected website, that is, each visitor is verified and only successfully authenticated visitors are allowed to access the website. As the CC protection policy at this level is relatively loose, there may be a risk of passing a small number of exceptional requests.
- **Medium:** this level is the default CC protection level. It is recommended if you find that the protected website is under CC attacks. Compared with the loose level, the medium level of CC protection can cover most of attack scenarios and defend against most of CC attacks. In addition, it performs a human-machine recognition algorithm check on all requests made to the protected website, that is, each visitor is verified and only successfully authenticated visitors are allowed to access the website.
- **Strict:** the CC attack protection policy is stricter at this level and can defend against more complex CC attacks. In addition, it performs a strict human-machine recognition algorithm check on all requests made to the protected website, that is, each visitor is verified and only successfully authenticated visitors are allowed to access the website. Due to the strict authentication mechanism in this mode, some normal requests may be blocked by mistake.
>!
	>- The protection algorithms used at the above three CC protection levels are only applicable to webpages and HMTL5 pages.
	>- If the business of the visited website is an API or a native app, as such businesses generally cannot respond to algorithm-based authentication normally, there is a great risk of false blocking.
	>- If you need CC protection for API or native app businesses, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for protection policy customization.


## Prerequisites
Purchase an [Anti-DDoS Advanced instance](https://intl.cloud.tencent.com/document/product/297/37241) and set the object to be protected.

## Operation Directions
1. Log in to the [Anti-DDoS console](https://console.cloud.tencent.com/ddos/antiddos-advanced/package) and click **Anti-DDoS Advanced (New)** -> **Configurations** on the left sidebar.
2. Select a domain name under an instance ID from the left list, e.g., **212.64.xx.xx bgpip-000002je** -> **http:80** -> **www.xxx.com**.
![](https://main.qcloudimg.com/raw/9b99b60388bd40282a34316cda196b64.png)
3. In the **CC Protection Policy** section, set the protection level to **Loose**, **Medium**, or **Strict** as needed and set the cleansing threshold.
>?
>- The cleansing threshold is the threshold for Anti-DDoS services to start cleansing traffic. If the number of HTTP requests sent to the specified domain name exceeds the threshold, CC protection will be triggered.
>- If the protection is enabled, the cleansing threshold of your Anti-DDoS Advanced instance will be set to the default value after your business is connected, and the system will generate a baseline cleansing threshold through machine learning based on the historical change patterns of your business traffic. You can also set the cleansing threshold according to your actual business needs.
>- If you have a clear concept about the threshold, set it as required. Otherwise please leave it to the default value. Anti-DDoS will automatically learn through AI algorithms and generate the default threshold for you.
