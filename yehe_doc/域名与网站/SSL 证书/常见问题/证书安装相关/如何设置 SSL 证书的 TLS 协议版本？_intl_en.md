Versions of the TLS protocol include TLSv1.0, TLSv1.1, TLSv1.2, TLSv1.3, and more. You can set the TLS version for your SSL certificates in the Tencent Cloud service console or web service on the server as needed.

### Tencent Cloud services
If your SSL certificates are deployed to the following Tencent Cloud services, you can configure by referring to the following documentations:
- CLB: [HTTPS Forwarding Configurations](https://intl.cloud.tencent.com/document/product/214/6534)
- CDN: [TLS Version Configuration](https://intl.cloud.tencent.com/document/product/228/38934)

### Server web services
If your SSL certificates are installed in the web service on the server, find `ssl_protocols TLSv1 TLSv1.1 TLSv1.2` in the certificate configuration file of your web service and modify it as needed.
For example, if your certificate needs to support the TLSv1.1 and TLSv1.2 versions, remove `TLSv1` from `ssl_protocols TLSv1 TLSv1.1 TLSv1.2`.
