## Configuration Process of Nginx HTTPS Two-Way Authentication

Here, we use the third-party developer domain name `http://www.example.com` as an example and two cases may arise:

- **The third-party developer already has a certificate issued by a third-party authority.**
 - The developer prepares the certificate `www.example.com.crt` issued by and the key `www.example.com.key` assigned by the third-party authority for `www.example.com`. Note that the certificate must be issued by a third-party authority, such as Topway or GlobalSign.
 - IM provides the developer backend with a CA certificate [TencentQQAuthCA.crt](http://share.weiyun.com/7d86303625fda66998bcc46f79320503), which is used to authenticate the certificate of the requesting party (that is, IM).
 - Configure by referring to the "Reference for Nginx HTTPS Two-Way Authentication Configuration" below.

- **The third-party developer sends an application to IM, requesting IM to issue a certificate for its domain name.**
 - The developer provides IM with the domain name of the developer backend, for example, `www.example.com`.
 - IM issues a certificate `www.example.com.crt` and assigns a key `www.example.com.key` for the developer backend with the domain name `www.example.com`.
 - IM provides the developer backend with a CA certificate [TencentQQAuthCA.crt](http://share.weiyun.com/7d86303625fda66998bcc46f79320503), which is used to authenticate the certificate of the requesting party (that is, IM).
 - Configure by referring to the "Reference for Nginx HTTPS Two-Way Authentication Configuration" below.

## Reference for Nginx HTTPS Two-Way Authentication Configuration

1. Copy `www.example.com.crt`, `www.example.com.key`, and `TencentQQAuthCA.crt` to the conf folder under the Nginx installation directory.
2. Modify the **nginx.conf** file based on the following reference configuration:
```
server { 
    listen 443 ssl;
    ssl_protocols TLSv1 TLSv1.1;
    server_name            www.example.com; # Domain name
    ssl_certificate        www.example.com.crt; # Certificate issued by Tencent to the third party
    ssl_certificate_key    www.example.com.key; # Private key paired with the certificate
    ssl_verify_client on; # Verify the request source
    ssl_client_certificate TencentQQAuthCA.crt; # CA certificate authenticated by Tencent
    location / {
        root   html;
        index  index.html index.htm;
    }
}
```
