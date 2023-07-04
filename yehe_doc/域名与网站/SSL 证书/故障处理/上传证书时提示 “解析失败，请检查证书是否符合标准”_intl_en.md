## Symptom

"DNS query failed. Check whether the certificate conforms to the standard" is prompted when a third-party SSL certificate is uploaded in the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl).

## Possible Causes
- Cause 1: The format of the uploaded certificate is incorrect.

- Cause 2: The uploaded certificate chain is incomplete.

- Cause 3: Extra spaces are not deleted before certificate format verification.


## Solutions

#### The format of the uploaded certificate is incorrect

Check whether the uploaded certificate is in the correct format.
- The certificate file starts with "-----BEGIN CERTIFICATE-----" and ends with "-----END CERTIFICATE-----".

- The private key starts with "-----BEGIN (RSA) PRIVATE KEY-----" and ends with "-----END (RSA) PRIVATE KEY-----".


#### The uploaded certificate chain is incomplete

Check whether the uploaded certificate chain is complete. For more information, see [How Can I Combine an SSL Certificate Chain?](https://intl.cloud.tencent.com/document/product/1007/39701).

#### Extra spaces are not deleted before certificate format verification

Check whether the uploaded certificate contains extra spaces.