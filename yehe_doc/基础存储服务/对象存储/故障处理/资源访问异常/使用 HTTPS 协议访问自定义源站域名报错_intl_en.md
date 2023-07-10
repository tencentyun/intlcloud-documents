## Symptom

When I access a custom origin domain over HTTPS, an error is reported.


## Possible Causes

The certificate configuration is incorrect or the custom origin domain is not configured.

## Troubleshooting

### Using a CDN certificate

1. Log in to the [CDN console](https://console.cloud.tencent.com/cdn).
2. On the left sidebar, click **Domain Management**.
3. Click the domain to configure. Then, select the **HTTPS Configuration** tab.
4. In the **HTTPS Configuration** area, click **Configure Certificate**.
For more information, see [HTTPS Configuration Guide](https://intl.cloud.tencent.com/document/product/228/35213).
5. Wait for about 5 minutes. When the CDN domain is deployed again, you can use HTTPS.


### Using a COS certificate 

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Click the name of the target bucket to go to the configuration page.
4. Click **Domains and Transfer** > **Custom Endpoint**.

5. Select the target domain and click **Bind Certificate** to configure the certificate.
6. Click **OK**.

When the value of **HTTPS certificate** is **Uploaded**, you can use HTTPS.

### Using a CVM reverse proxy certificate 

For more information, see [Supporting HTTPS for Custom Endpoints](https://intl.cloud.tencent.com/document/product/436/11142).
