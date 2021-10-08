## Scenarios
When users visit your website with an expired certificate, there will be a warning sign displayed; if an API has been called by your domain name, an error will be reported. To avoid business interruption, update your certificate on the console in a timely manner.

## Directions
### Example 1: External certificate
1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/waf/overview) and select **Instance Management** -> **Domain Name Connection** on the left sidebar.
2. On the domain name connection page, select a domain name and click **Edit**.
3. On the pop-up page, click **Reassociate** in the web server configurations to display a pop-up window for certificate configuration.
4. In the pop-up window, select "External Certificate" for the certificate type, enter the certificate and private key, and then click **Save**.

### Example 2: Tencent Cloud hosting certificate
1. On the [domain name connection](https://console.cloud.tencent.com/guanjia/instance/domain) page, select a domain name and click **Edit**.
2. On the pop-up page, click **Reassociate** in the web server configurations to display a pop-up window for certificate configuration.
2. In the pop-up window, select "Tencent Cloud Hosting Certificate" for the certificate type and then click **Save**. The SSL certificate will be used.
>?This method only applies to certificates uploaded for SSL certificate management.

### Example 3: One-click configuration
1. Enter the [SSL Certificate](https://console.cloud.tencent.com/guanjia/waf/overview) and click **My Certificate**.
2. On the pop-up page, select an ID prior to clicking **Deploy**.
3. In the pop-up window, select "Web Application Firewall" for the deployment type, select a WAF instance, and then click **OK**.

## Certificate Validity Check
You can check the effective and expiration dates of the certificate by accessing the domain name via a browser. If the certificate does not take effect, please [contact us](https://intl.cloud.tencent.com/contact-us) for help.
