## ICP Filing for Domain Name in Mainland China
When connecting your domain name to Tencent Cloud CDN for acceleration, if you select Chinese mainland or global as the acceleration region, the ICP filing for services in Mainland China should be obtained from the MIIT for your domain name.

## Credibility Check
1. Tencent Cloud CDN will conduct an **account credibility check** when you activate the CDN service. If your Tencent Cloud account has too many violation records, your account will have low credibility and will be blocked. Tencent Cloud CDN will prohibit service activation for these accounts.

2. Tencent Cloud CDN will conduct a **domain name credibility check** when you connect your domain name after activating the CDN service. If there exist records of the following behaviors for your account, your account will have low credibility and will be blocked. Tencent Cloud CDN will not allow domain name connection for these accounts.
 - The acceleration domain name has published content through Tencent Cloud CDN that severely violates regulations.
 - The account to which the acceleration domain name belongs has incurred a large amount of outstanding fees.
 - The acceleration domain name is listed as a malicious domain name by Tencent PC Manager.

## Content Check
When you use the Tencent Cloud CDN service in Chinese mainland, you are responsible to stay in compliance with applicable local laws, regulations, and policies for your contents, qualifications, capabilities, and behaviors.

If the following contents, among others, appear under your domain name, we will block the non-compliant contents and terminate acceleration services in severe cases:
- Unauthorized gaming server
- Pirated game/software/video websites
- Unauthorized hospital and pharmaceutical websites
- Pornographic contents
- Drug-related contents
- Gambling advertisements and games

## Acceleration Service
| Type | Limit |
| -------- | ------------------------------------------------ |
| Acceleration domain name | Wildcard domain names can be connected <br/>Up to 100 ones are supported |
| Data statistics | Statistics generated in the last 90 days can be queried by default |
| Content purge | URL purge: 10,000 per day <br/>Directory purge: 100 per day |
| Access log | Access logs are retained for 30 days by default |

## Domain Name Repossession
If your domain name does not generate any website access traffic within three months after connection, CDN will automatically close the acceleration service. If you want to use the service again, log in to the CDN Console to enable it manually.
