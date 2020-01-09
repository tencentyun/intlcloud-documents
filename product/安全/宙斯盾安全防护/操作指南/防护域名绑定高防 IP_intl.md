
In the [Aegis Anti-DDoS Console](https://console.cloud.tencent.com/gamesec), select "Business Domain Name List" in the left pane, and click "Create a business and a domain name" in the right to automatically generate a protected domain name. You can access the protection service by pointing the CNAME of your business domain name to a protected domain name.

## Flowchart
![](https://main.qcloudimg.com/raw/fbb9f8966ec2657da0eca193a02a5759.png)

## Process for Binding a Protected Domain Name to a Protective IP
1. **Create a business**
a. Click **Business Domain Name List** and then click **Create a business and a domain name**.
![1](https://main.qcloudimg.com/raw/26808fa32108113f2ab584deeca6426b.png)
b. Enter the relevant information and click **Create**. After successful creation, the business and the free protected domain name are generated in "Business Domain Name List".
![2](https://main.qcloudimg.com/raw/d5b8306d4884245e470120490b0d4ac4.png)
2. **Add a protective IP**
a. In the business domain name list management page, click "Add IP" to go to the business details page.
![3](https://main.qcloudimg.com/raw/224f702e08ca2d2d2d90ea98a0a83616.png)
b. Click "Add IP" under "Settings of IP resources and resolution" in the "Business Details" page.
![4](https://main.qcloudimg.com/raw/db021706af6b3986fd284825634ad3d4.png)
c. Select a protective IP and click **OK**.
![5](https://main.qcloudimg.com/raw/69a94067fe25cc514bb66001936ad313.png)
3. **Enable domain name resolution**
After adding a protective IP, enable "Domain Name Resolution". The protected domain name provides intelligent resolution, i.e. the source IP of the end user is resolved to the IP of the corresponding line. For example, China Telecom users will be resolved to the protective IP for China Telecom, while China Unicom users will be resolved to the protective IP for China Unicom. If the protective IP of a line is blocked due to excessive attacks, it will be automatically resolved to another available protective IP.
If "BGP Line First" is enabled, and a BGP line IP is bound, the protected domain name will preferentially schedule all business requests to be resolved to the BGP IP address. (Other non-BGP IPs with resolution enabled are in stand by.) If the BGP protective IP is jammed due to heavy-traffic attacks, the system will intelligently schedule business requests to non-BGP protective IPs with resolution enabled to provide high-bandwidth protection. After the BGP protective IP is unblocked, the system will schedule all business requests to it.
![](https://main.qcloudimg.com/raw/545082a6e322da966ac0dd8b640dbf6b.png)
4. **Point the CNAME of the primary domain name to the protected domain name**
After line resolution is enabled, the business' primary domain name can be intelligently resolved to the protective IP by pointing the CNAME to the protected domain name.
You can verify whether the domain name can be resolved to the protective IP using ping or nslookup locally.
