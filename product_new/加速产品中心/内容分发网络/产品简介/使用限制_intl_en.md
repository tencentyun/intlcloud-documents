## ICP filing for domain name
You need to obtain ICP filing for your domain name connected to CDN for acceleration. If you have not done so, use the [ICP filing registration](https://intl.cloud.tencent.com/product/icp) service of Tencent Cloud.

## Credit Check
When connecting your domain name to CDN, CDN will check its credibility. If your domain name has had the following situations, it will have a low credibility and be blacklisted.
- The accelerated domain name has published content via Tencent Cloud CDN that severely violates regulations.
- The account to which the accelerated domain name belongs has generated a large amount of outstanding fees.
- The accelerated domain name is listed as a malicious domain name by Tencent PC Manager.

## Content Check
CDN regularly scans contents delivered over the entire internet. If your domain name has the following illegal contents, CDN will block the contents and no longer provide acceleration service in severe cases.
- Unauthorized gaming server
- Pirated game/software/video websites
- Illegal hospital and medicine websites
- Pornographic contents
- Drug-related contents
- Gambling advertising contents and gambling-related games

## Acceleration Service
| Type | Limit |
| -------- | ------------------------------------------------ |
| Accelerated domain name | Wildcard domain names can be connected <br/>Up to 100 ones are supported |
| Data statistics | Statistics generated in the past 90 days can be queried by default |
| Content purge | URL purger: 1,000 per day <br/>Directory purge: 200 per day |
| Access log | Access logs are retained for 30 days by default |

## Domain name repossession
If your domain name does not generate any website access traffic within three months after connection, CDN will automatically close the acceleration service. If you want to use the service again, log into the CDN console to enable it manually.

