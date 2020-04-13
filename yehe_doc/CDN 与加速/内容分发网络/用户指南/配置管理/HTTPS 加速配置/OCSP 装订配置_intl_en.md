## Configuration Scenario
OCSP stapling is a TLS certificate status request extension. An OCSP stapling server can send the cached OCSP query result to the client during TLS handshake for verification by the user, eliminating the need for the client to contact the CA. OCSP stapling greatly improves the efficiency of TLS handshake and reduces verification time.

Tencent Cloud CDN allows you to enable/disable OCSP Stapling.

## Configuration Guide
### Viewing configuration
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of the domain name to enter its configuration page. Under the **Advanced Configuration** tab, find the **OCSP Stapling Configuration**, which is disabled by default:
![](https://main.qcloudimg.com/raw/a0f84d254848ea7c28a0642b3ab1866a.png)

### Modifying configuration
If a domain name has been configured with HTTPS acceleration, you can directly switch to enable/disable OCSP stapling. After the certificate configuration is deleted, OCSP stapling will be automatically invalidated:
![](https://main.qcloudimg.com/raw/af090e9a10a99f552c2a57378d0b46ff.png)

>If your domain name is configured for global acceleration, the OCSP stapling configuration will take effect globally. This configuration does not distinguish between requests from and outside of Mainland China.

