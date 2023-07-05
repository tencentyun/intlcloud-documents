## Configuration Scenario
CDN supports configuration of forced HTTPS redirect. If a domain name has been configured with the certificate for HTTPS acceleration, you can specify the 301/302 redirect method to force redirect all HTTP requests at the CDN node to HTTPS requests.
## Configuration Guide
### Viewing configuration
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of the domain name to enter its configuration page. If the domain name has been configured with an HTTPS certificate, you can find **Forced Redirect to HTTPS** switch under the **Advanced Configuration** tab. It is disabled by default:
![](https://main.qcloudimg.com/raw/b138ef26dba5f9ccbec97e592ee334dc.png)

### Modifying configuration
You can click **Edit** on the right to switch 301/302 redirect or directly disable the configuration.
![](https://main.qcloudimg.com/raw/ffbb3a57c19ba1d8a52b25ad66f16508.png)
![](https://main.qcloudimg.com/raw/90aae9a0b02d704dfafd0c080e5972db.png)

>If your domain name is configured for global acceleration, the forced HTTPS redirect configuration will take effect globally. This configuration does not distinguish between requests from and outside of Mainland China.
