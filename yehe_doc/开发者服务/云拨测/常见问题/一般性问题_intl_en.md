[](id:que1)
### Will accessing an application from lots of testing nodes affect the application performance?
Yes. Accessing an application from lots of testing nodes at the same time puts more pressure on the application server, as long as you need to spend a lot of money in purchasing a large number of widespread testing nodes. CAT has a testing frequency of no shorter than one minute. It still has much to do to support instantaneous high concurrency compared with professional stress test tools.

[](id:que2)
### How do I select a node type (IDC, LastMile, or mobile) for my scenario?
**Node types:**
IDC: It is the IDC testing node deployed on the backbone line.
LastMile: It is the testing node deployed on the end user's PC to test the end user's experience on the PC.
Mobile: It is the testing node deployed on the mobile phone to test the mobile user experience.
**Suggestions for selection:**
- To test the business availability, you can select the more stable **IDC**.
- To check the access experience and network conditions of end users, we recommend you select **LastMile** or **Mobile** to simulate the user access to an application.

[](id:que3)
### Why do testing nodes in and outside the Chinese mainland need to be configured separately for global businesses?
Compared to testing nodes in the Chinese mainland, those outside the Chinese mainland may be subject to poor network quality due to ISP, geographical location, and other factors. If these two types of testing nodes are tested at the same time, the data will be averaged and therefore inaccurate. Thus, we recommend you configure them separately for business issue analysis.


[](id:que4)
### How does CAT work? With what technology?
How it works: CAT's global monitoring network spreads across different regions (in and outside the Chinese mainland), ISPs (China Mobile, China Unicom, China Telecom, etc.), terminals (IDC, LastMile, and mobile), and network conditions (3G, 4G, and Wi-Fi). It actively tests application experience to get different performance metrics during application running.
Technology: Non-intrusive without code nesting.

[](id:que5)
### Will modifying the application content affect monitoring?
The monitoring data will change accordingly.

