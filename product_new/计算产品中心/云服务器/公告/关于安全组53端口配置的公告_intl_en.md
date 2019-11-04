## Overview
Port 53 is the Domain Name Server’s (DNS) open port. It is primarily used for domain name resolution. The DNS acts as a translator between the domain name and the IP address, so users only need to remember the domain name to quickly access the web site.

The “Classified Catalogue of Telecommunications Businesses” (2015 Edition) has incorporated the recursive Internet domain name resolution service into telecommunications services (Code number: B26-1). This means that to handle recursive domain name service, the telecommunications services permit for this category must be obtained.

## Related Policies and Regulations

**1. Conducting of Internet domain resolution services business is not permitted without a business license.**
If the company (you) are involved in this business, you must apply for a “Code and Rules Conversion Service License”. For specific details, contact your local telecommunications administration.
**”Measures for the Administration of Telecommunications Business Licenses” Article 46:**  Whoever violates the provisions of Paragraph 1 of Article 16, and Paragraph 1 of Article 28 of these Measures, and arbitrarily engages in telecommunications services or engages in telecommunications services beyond the permitted scope, shall be punished in accordance with Article 69 of the “Regulation of the People's Republic of China on Telecommunications”. If the circumstances are serious and an order is given to suspend business for rectification and punishment, the business will be directly included in the list of untrustworthy telecommunications service businesses.
**”Internet Domain Name Management Measures” of the Ministry of Industry and Information Technology, Article 36:** To provide domain name resolution services, businesses shall comply with relevant laws, regulations and standards, and have the corresponding technologies, services, and network and information security assurance capabilities. Businesses must implement network and information security measures, and must record and retain domain name resolution logs, O&M logs, and change records in accordance with the law, to ensure the resolution of service quality and resolution system security. Where the business involves the operation of telecommunications services, it shall obtain the telecommunications business operation license in accordance with the law.
**2. Tencent Cloud will not provide services, such as access or billing, for individuals or entities who have not obtained business licenses or the non-operational Internet information services ICP filing.**
**”Measures for the Administration of Telecommunications Business Licenses” Article 24, Value-added telecommunications service businesses that provide access services must comply with the following regulation:** (Three) The provision of services, such as access or billing, for entities or individuals that have not obtained business licenses or a non-operational Internet information services ICP filing in accordance with the law is not permitted.
If you (entity) do not engage in **Internet domain name resolution services**, it is recommended that you adjust the security group policy of your server, and disable port 53 in the inbound rules.

## Disabling Port 53 Through Inbound Rules

1. Log in to the [Tencent Cloud CVM Console](https://console.cloud.tencent.com/cvm/index).
2. In the instance management page, select the instance where port 53 is to be disabled, and click the **ID/Instance Name**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/186bd6ec5c69b12b3ea9645ff1dbb22b.png)
3. In the instance details page, select the **Security Group** tab, to enter the security group management page for this instance. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/7eb1b0b56520701fc8d28a14cfecd7f1.png)
4. In the **Bound Security Groups** field, select the **Security Group ID/Name** of the inbound rule that is to be modified.
5. In the **Security Group Rules** page, select the **Inbound Rules** tab. Click **Add a Rule**. This is shown in the following figure.
![](https://main.qcloudimg.com/raw/f1f7f9ce6d3e259e06542bf19d797022.png)
6. In the **Add Inbound Rules** window that pops up, enter the following information. This is shown in the following figure:
![Add inbound rules-Disable port 53](https://main.qcloudimg.com/raw/f3890575ef22f31f67c0c6902f6df55a.png)
 - Type: Select “Custom”.
 - Source: Enter “0.0.0.0/0”.
 - Protocol port: Enter “UDP:53”.
 - Policy: Select “Reject”.
7. Click **Complete** to disable port 53.

## FAQs

### What is the Internet Domain Name Resolution Service?
**Internet Domain Name Resolution** is the process of implementing the relationship between an Internet domain name and its corresponding IP address.
**Internet domain name resolution service business** is a service that creates a domain name resolution server and related software on the Internet to implement conversion of Internet domain names to their corresponding IP addresses. There are two types of domain name resolution services: authoritative resolution services and recursive resolution services.
- Authoritative resolution: This is the service providing domain name resolution for root domain names, top-level domain names, and other levels of domain names.
- Recursive resolution: This is the service implementing the correspondence between the domain names and IP addresses through querying the local cache or the authoritative resolution service system.

Internet domain name resolution service here specifically refers to the recursive resolution service. For more information, see [“Classified Catalogue of Telecommunications Businesses” (2015 Edition): B26-1 Internet domain name resolution service business](http://www.miit.gov.cn/n1146285/n1146352/n3054355/n3057709/n3057714/c4564270/content.html).


### What Effect Does Disabling Port 53 Through Inbound Rules Have on My Server?
If you do not perform Internet domain name resolution services business, disabling port 53 in inbound rules does not have an effect on your server or business.

### Can an Individual Engage in Domain Name Resolution Services Business?
Telecommunications business operators must have a business established in accordance with the law. Individuals cannot carry out this type of service. You must obtain an “Code and Rules Conversion Business License” before you can carry out Internet domain name resolution services business. For more information about obtaining a license, you can contact your local telecommunications administration office.

### What Impact Will Carrying Out Internet Domain Name Resolution Services Without the Related Permit?
According to the “Regulation of the People's Republic of China on Telecommunications” Article 69: (One) Those who violate Article 7 Paragraph 3, or perform the acts listed in Article 58 Item 1, operating a telecommunications business without authorization, or operating beyond the scope of the telecommunications business, are subject to corrections according to the Ministry of Industry and Information Technology, or the telecommunications regulatory agency of the province, autonomous region, or municipality, including the confiscation of illegal income and a fine of 3 to 5 times the amount of the illegal income. If there is no illegal income or the illegal income does not exceed 50,000 RMB, the penalty will be between 100,000 RMB and 1,000,000 RMB. If the circumstances are serious, the entity shall be ordered to suspend business for rectification.

