Dear Tencent Cloud User,

The feature of storing CLB access logs in COS will be deactivated in the following schedule:
<table class="table"><thead><tr><th>Time</th><th>Deactivation Plan</th></tr></thead>
<tbody><tr><td>00:00:00, April 26, 2020 </td><td>The feature of storing access logs in COS will stop accepting new enablement requests in <strong>Guangzhou</strong>, while existing logs stored in COS will not be effected.</td></tr>
<tr><td>00:00:00, May 15, 2020 </td><td>The feature of storing access logs in COS will stop accepting new enablement requests in <strong>Beijing, Shanghai, and Hong Kong (China)</strong>, while existing logs stored in COS will not be effected.</td></tr>
<tr><td>00:00:00, June 30, 2020 </td><td>The feature of storing access logs in COS will be <strong>officially deactivated</strong> in all regions, and all CLB instance will no longer provide this feature.</td></tr></tbody></table>



The feature of [storing CLB access logs in CLS](https://intl.cloud.tencent.com/document/product/214/34893), an upgrade version of storing access logs in COS, has been officially available. Compared to the former, the latter can provide:
- Real-time logging at a minute-level granularity and diversified online search based on full-text, key-value, and fuzzy keywords.
- Multi-region coverage and other capabilities, making it more suitable for large-scale use in production environments.

As COS and CLS have different service modes, we cannot help you directly modify the configuration. We recommend that you change the existing access log storage location from COS to CLS before 00:00:00, June 30, 2020. Please [configure access log storage in CLS](https://intl.cloud.tencent.com/document/product/214/35063) first and then disable [access log storage in COS](https://intl.cloud.tencent.com/document/product/214/10329).

By default, Tencent Cloud does not promise to store access logs. If you need such logs for your business, please [configure access log storage in CLS](https://intl.cloud.tencent.com/document/product/214/35063) on your own. We are very sorry for any inconvenience caused.

If you have already modified the configuration, please ignore this notice. Thank you again for your always support and trust!

Sincerely,

Tencent Cloud Team
