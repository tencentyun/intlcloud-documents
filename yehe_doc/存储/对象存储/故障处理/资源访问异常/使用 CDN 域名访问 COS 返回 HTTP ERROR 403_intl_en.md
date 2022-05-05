## Symptom

When I use a Content Delivery Network (CDN) domain to access Cloud Object Storage (COS), the error code “HTTP ERROR 403” is returned.


## Possible Causes

The CDN acceleration domain is disabled.

## Troubleshooting Procedure

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** in the left sidebar.
3. Click the name of the desired bucket to go to the configuration page.
4. Select **Domains and Transfer** > **Default CDN Acceleration Domain**.
5. In the **Default CDN Acceleration Domain** area, check whether the **Status** is **Enabled**.
 - If not, [enable default acceleration domain](https://intl.cloud.tencent.com/document/product/436/31505).
 - If yes, proceed with the next step.
6. In the **Custom CDN Acceleration Domain** area, check whether the **Status** is **Online**.
 - If yes, [contact us](https://intl.cloud.tencent.com/support).
 - If not, [enable custom acceleration domain](https://intl.cloud.tencent.com/document/product/436/31506).

