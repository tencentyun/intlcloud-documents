### How can I configure live push acceleration outside Chinese mainland?
Go to the CSS console > [Domain Management](https://console.cloud.tencent.com/live/domainmanage), where the default push domain name is pre-configured with push acceleration outside Chinese mainland. If you want to use your own push domain name, add one and then complete CNAME-related operations as instructed to configure acceleration outside Chinese mainland for it.
		
### How can I accelerate push for a playback domain name outside Chinese mainland?
Go to the CSS console > [Domain Management](https://console.cloud.tencent.com/live/domainmanage) > Add Playback Domain, where you can select one of the two acceleration types as needed: **Global Acceleration**, which requires the domain name to have obtained ICP filing in Chinese mainland; otherwise, configuration will fail; **Acceleration in Hong Kong/Macao/Taiwan (China Region) and other regions**, which can be configured just as instructed, but playback is unavailable in Chinese mainland in this case.
	 
### How can I check whether acceleration outside Chinese mainland has been configured for my domain name?
You can use a server outside Chinese mainland to run the `ping` command on the push and playback domain names; if the server IP is a nearest node IP, acceleration outside Chinese mainland has been configured. You can also use [this tool](https://tools.ipip.net/dns.php) to test your domain name and check whether the resolved IP corresponds to the acceleration region.
	 
### How can I troubleshoot failures of live playback outside Chinese mainland?
Currently, playback outside Chinese mainland supports HTTP-FLV, HLS, and RTMP. You can troubleshoot playback issues in the following way:
1. **Is the domain name pingable?**
If not, check the current network environment.
2. **Is the obtained HTTP status code 200?**
	If it is not 200, there are several possible reasons for the failure. Generally, if the status code is 403, which indicates authentication failure, you need to check whether the calculation format of hotlink protection complies with the requirements. If the status code is 404, which indicates that the stream played back is not on the platform, you need to check whether the push is normal. For other error codes, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
	 
### What protocols does live push outside Chinese mainland support?
Currently, only RTMP is supported.
	 
### Does live playback outside Chinese mainland support HTTPS?
Yes. Go to the CSS console > [Domain Management](https://console.cloud.tencent.com/live/domainmanage) > Playback Domain > Manage > Advanced Configuration > HTTPS Configuration, where you can add an HTTPS certificate to the domain name for which you want to configure HTTPS pull.
	 
### Can I modify the region of live playback acceleration outside Chinese mainland?
Yes. You can do so in the CSS console > Domain Management. It takes about 15 minutes for the change to take effect.
	 
### Does push acceleration outside Chinese mainland support HttpDNS scheduling?
Yes, but you need to [submit a ticket](https://console.cloud.tencent.com/workorder/category) for configuration in the backend.
