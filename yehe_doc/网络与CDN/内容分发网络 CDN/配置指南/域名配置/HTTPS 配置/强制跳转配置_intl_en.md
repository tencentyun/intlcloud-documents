## Configuration Overview

Tencent Cloud CDN supports HTTPS/HTTP forced redirection.

- If a domain name is configured with a certificate for HTTPS acceleration, you can specify the 301/302 redirection method to force all HTTP requests at the CDN node to be HTTPS requests.
- You can also specify the 301/302 redirection method to force all HTTPS requests at the CDN node to be HTTP requests.

## Configuration Guide

### Configuration limitations

HTTPS acceleration must be enabled for configuring HTTPS forced redirection.

### Configuration instructions

Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, click **Manage** on the right of a domain name to enter its configuration page, and open the **HTTPS Configuration** tab to find the **Forced Redirection** section. The feature is disabled by default.
<img src="https://main.qcloudimg.com/raw/b11157d848d39d4e4bba540598f35eba.png" style="width:700px"/>
Toggle it on, and configure the redirection type, method:
<img src="https://main.qcloudimg.com/raw/731d7bcb51286683d259691178bf2b39.png" style="width:450px"/>
Finally, click **Confirm** to deploy the configuration:
<img src="https://main.qcloudimg.com/raw/2dcfbacf16b47fe600935f57aadd2e77.png" style="width:700px"/>

