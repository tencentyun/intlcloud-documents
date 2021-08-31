Dear Tencent Cloud User,

The feature of storing Cloud Load Balancer (CLB) access logs in Cloud Object Storage (COS) will be deactivated as per the following schedule.
<table class="table"><thead><tr><th>Time</th><th>Deactivation plan</th></tr></thead>
<tbody><tr><td>00:00:00, April 26, 2020</td><td>The feature of storing access logs in COS will stop accepting <strong>new</strong> enablement requests in <strong>Guangzhou</strong>, while existing logs stored in COS will not be affected.</td></tr>
<tr><td>00:00:00, May 15, 2020</td><td>The feature of storing access logs in COS will stop accepting <strong>new</strong> enablement requests in <strong>Beijing, Shanghai, and Hong Kong (China)</strong>, while existing logs stored in COS will not be affected.</td></tr>
<tr><td>00:00:00, June 30, 2020</td><td><strong>The feature of storing access logs in COS will be officially deactivated in all regions, and all CLB instances will no longer provide this feature.</strong></td></tr></tbody></table>



The feature of [storing access logs in Cloud Log Service (CLS)](https://intl.cloud.tencent.com/document/product/214/34893), an upgrade version of storing access logs in COS, has been officially available. Compared to storing access logs in COS, the feature of storing access logs in CLS provides the following benefits:
- Real-time logging at a minute-level granularity and diversified online search based on full-text, key-value, and fuzzy keywords
- Multi-region coverage and other capabilities, making it more suitable for large-scale use in production environments
- On-demand [shipping of logs from CLS to COS](https://intl.cloud.tencent.com/document/product/614/32940)

As COS and CLS have different service modes, we cannot directly modify the configuration for you. We recommend that you change the access log storage from COS to CLS before 00:00:00, June 30, 2020. Please [configure access log storage in CLS](https://intl.cloud.tencent.com/document/product/214/35063) first and then disable [access log storage in COS](https://intl.cloud.tencent.com/document/product/214/10329).

Tencent Cloud does not store any access logs by default. If you need such logs for your business, please [configure access log storage in CLS](https://intl.cloud.tencent.com/document/product/214/35063) on your own. We are very sorry for any inconvenience caused.

If you have already modified the configuration, please ignore this announcement. Thank you again for your always support and trust.

Sincerely,

Tencent Cloud Team
