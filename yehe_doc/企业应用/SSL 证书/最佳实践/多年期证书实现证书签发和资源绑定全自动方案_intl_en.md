## Overview
The multi-year certificate is an automatic SSL certificate review and delivery feature powered by Tencent Cloud. If you buy a multi-year certificate for two years or more and complete the review, Tencent Cloud will automatically review information and issue the next SSL certificate for you one month before your existing SSL certificate expires, simplifying the application process.
Tencent Cloud also supports SSL certificate management by cloud resources, where a new SSL certificate can be deployed as the original one in cloud resources such as Tencent Cloud CLB and CDN.
This document describes how to realize the automatic certificate issuance and resource binding of a multi-year certificate by combining the above two features.

>? Take the GeoTrust OV multi-year certificate and the Tencent Cloud CDN as examples here.
>
## Directions
### Step 1. Purchase a multi-year certificate
1. Log in to the SSL Certificate Service buy page.
2. Select and purchase a multi-year SSL certificate based on your needs.

3. Complete the SSL certificate application process.

### Step 2. Deploy the SSL certificate to cloud resources
After the certificate is obtained, you can deploy it to Tencent Cloud resources (such as CDN) using the quick SSL certificate deployment feature.
1. Log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl), select a target multi-year certificate, and click **Deploy**.

2. In the “Select deployment type” pop-up window, select a target type and corresponding resource instance.

3. Click **OK** to deploy the SSL certificate to selected cloud resources.


### Step 3. Enable certificate management by cloud resources
1. Click a **certificate name** to go to the "Certificate Details" page.
2. In the Basic Info module, click **View** to check certificate management by cloud resources.

3. In the “Management by cloud resource” pop-up window, select target cloud resources.

4. Click **OK** to complete the operation.
















