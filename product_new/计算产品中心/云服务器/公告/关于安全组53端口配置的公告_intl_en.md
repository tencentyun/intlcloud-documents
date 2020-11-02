## Overview
Port 53 is Domain Name Server’s (DNS) open port. It is primarily used for domain name resolution. The DNS acts as a translator between the domain name and IP address, so users only need to remember the domain name to quickly access the website.

The “Classified Catalogue of Telecommunications Businesses” (2015 Edition) has categorized recursive Internet domain name resolution services as telecommunications services (Code number: B26-1). To manage recursive domain name services, the telecommunications services permit must be obtained.

## Related policies and regulations

**1. Internet domain resolution services are not permitted without a business license.**
If you or your company is involved in this business, you must apply for a “Code and Protocol Conversion License”. For specific details, contact your local telecommunications administration.
**“Administrative Measures for the Licensing of Telecommunication Business Operations” Article 46:** Whoever violates the provisions of Paragraph 1 of Article 16 and Paragraph 1 of Article 28, whereby arbitrarily engages in telecommunications services or engages in telecommunications services beyond the permitted scope, shall be punished in accordance with Article 69 of the “Telecommunication Regulation of the People's Republic of China”. For serious misconduct, an order will be given to suspend the business for rectification, which will be included in the list of untrustworthy telecommunications services providers.
**“Internet Domain Name Regulations” of the Ministry of Industry and Information Technology, Article 36:** To provide domain name resolution services, businesses shall comply with relevant laws, regulations and standards, and have the relevant technical, services, network and information security safeguard capacities. Businesses shall put in place network and information security safeguard measures, record and store domain name resolution logs, O&M logs, and change records in accordance with the law, to ensure the service quality of resolution and the security of the resolution system. Where telecommunications services are involved, businesses shall obtain the telecommunications operations licenses in accordance with the law.
**2. Tencent Cloud will not provide services, such as access or billing, for individuals or entities who have not obtained business licenses or ICP filings for non-commercial Internet information services in Mainland China.**
**“Administrative Measures for the Licensing of Telecommunication Business Operations” Article 24, value-added telecommunications businesses providing access services must comply with the following regulation:** (Three) The provision of services, such as access or billing, for entities or individuals that have not obtained business licenses or ICP filings for non-commercial Internet information services in Mainland China in accordance with the law is not permitted.
If you or your company does not engage in **Internet domain name resolution services**, we recommended you adjust the security group policy of your server, and disable port 53 via inbound rules.

## Disabling port 53 via inbound rules

1. Log in to the [Tencent Cloud CVM Console](https://console.cloud.tencent.com/cvm/index).
2. In the instance management page, select the instance where port 53 is to be disabled, and click the **ID/Name**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/186bd6ec5c69b12b3ea9645ff1dbb22b.png)
3. In the instance details page, select the **Security Groups** tab, to enter the security group management page for this instance. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/7eb1b0b56520701fc8d28a14cfecd7f1.png)
4. In the **Bound to security group** field, select the **Security Group ID/Name** of the inbound rule that is to be modified.
5. In the **Security Group Rule** page, select the **Inbound Rule** tab. Click **Add a Rule**. This is shown in the following figure.
![](https://main.qcloudimg.com/raw/f1f7f9ce6d3e259e06542bf19d797022.png)
6. In the **Add Inbound Rule** window that pops up, enter the following information. This is shown in the following figure:
![Add inbound rules-disable port 53](https://main.qcloudimg.com/raw/f3890575ef22f31f67c0c6902f6df55a.png)
 - Type: Select “Custom”.
 - Source: Enter “0.0.0.0/0”.
 - Protocol port: Enter “UDP:53”.
 - Policy: Select “Reject”.
7. Click **Complete** to disable port 53.

## FAQs

### What is the Internet domain name resolution service?
**Internet Domain Name Resolution** establishes the relationship between an Internet domain name and its corresponding IP address.
**Internet domain name resolution service** builds domain name resolution servers and related software on the Internet to translate Internet domain names to their corresponding IP addresses. There are two types of domain name resolution services: authoritative and recursive resolution services.
- Authoritative resolution: This service provides domain name resolution for root domain names, top-level domain names, and other levels of domain names.
- Recursive resolution: This service establishes the correspondence between domain names and IP addresses by querying the local cache or the authoritative resolution service system.

Internet domain name resolution service here specifically refers to recursive resolution service. For more information, see “Classification Catalog of Telecommunications Services” (2015 Edition): B26-1 Internet domain name resolution services.

 
### How will disabling port 53 through inbound rules impact my server?
If you do not engage in Internet domain name resolution services, disabling port 53 through inbound rules does not impact your server or business.

### Can individual engage in domain name resolution services?
Telecommunications services providers must have established businesses in accordance with the law. An individual cannot engage in this type of service. You must obtain an “Code and Protocol Conversion License” before carrying out Internet domain name resolution services businesses. For more information about obtaining a license, you can contact your local telecommunications administration office.

### What are the impacts of carrying out Internet domain name resolution services without the permit?
According to the “Telecommunications Regulations of the People's Republic of China” Article 69: (One) Whoever violates Article 7 Paragraph 3 or perform acts listed in Article 58 Item 1, whereby operates a telecommunications business without authorization or operates beyond the permitted scope, is subject to rectification by the Ministry of Industry and Information Technology, the telecommunications regulatory agency of the province, autonomous region, or municipality, including the confiscation of illegal income and a fine between 3 to 5 times the illegal income. If there is no illegal income or the illegal income does not exceed 50,000 RMB, the penalty will be between 100,000 RMB and 1,000,000 RMB. For serious misconduct, an order will be given to suspend the business for rectification.
