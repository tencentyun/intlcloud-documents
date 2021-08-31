In most cases, browsers for PCs can obtain the intermediate certificate from the URL of Authority Information Access (AIA). However, on browsers of some Android systems, the certificate may appear to be untrusted or cannot be accessed.
This main reason is that browsers for those Android systems do not support obtaining the intermediate certificate from the URL of AIA. In this case, you need to combine the certificate chain files into one according to the SSL certificate chain structure and deploy it on the server again. When the browser connects with the server, it downloads the user certificate as well as the intermediate certificate so that the certificate will appear to be trusted for your browser’s access. The SSL certificate chain structure is as follows:

```
-----BEGIN CERTIFICATE-----
Domain certificate
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----

Root CA certificate
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----

Intermediate CA certificate

-----END CERTIFICATE-----
```

>?
>- Normally, an SSL certificate chain is made up of the root CA certificate > intermediate CA certificate(s) > domain certificate. There may be multiple intermediate certificates.
>- International standard SSL certificates provided by Tencent Cloud are complete certificate chains, which are available without needing to be combined.



### How can I view the SSL certificate chain?
1. Open a browser to access the website that has successfully installed and deployed the SSL certificate. Chrome is used as an example herein.
2. Click ![](https://main.qcloudimg.com/raw/f338bd1d67db54ba1928bc4fd37e3e13.png) in the browser address box, and click **Certificate** on the page that is displayed, as shown in the following figure:
![](https://main.qcloudimg.com/raw/d45d35cd0d9ae5744e97fc4ca613d85e.png)
3. On the **Certificate** page, click **Certificate Path** to view the SSL certificate chain, as shown in the following figure:
![](https://main.qcloudimg.com/raw/540ba2322d8520db61f5128fb08a92ad.png)




