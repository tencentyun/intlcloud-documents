
### What are authorization ID, key, and token?
- **Authorization ID**: The unique ID assigned to you by HTTPDNS, which allows you to connect to HTTPDNS over HTTP DES/AES.
- **Key**: The unique encryption key assigned to you by HTTPDNS, which corresponds to the authorization ID. Depending on the encryption method, it can be either a DES or AES key used to encrypt the request parameters and decrypt the DNS query result.
- **Token**: The unique token assigned to you by HTTPDNS, which allows you to connect to HTTPDNS over HTTPS.

### How do I connect to `119.29.29.98` over HTTP DES/AES?
1. Switch the accessed IP to `119.29.29.98` in the business code (for AES/DES encryption). 
2. Encrypt the domain and IP parameters with the DES/AES key provided in the console, such as: 
```
 http://119.29.29.98/d?dn=cloud.tencent.com&id=xxx&ip=1.2.3.4 
```                
`cloud.tencent.com` and `1.2.3.4` are the domain and IP and need to be encrypted, while the authorization ID `xxx` doesn't. 
3. Decrypt the DNS query result with the DES/AES key provided in the console.

### How do I connect to `119.29.29.99` over HTTPS?

1. Switch the accessed IP to `119.29.29.99` in the business code (for HTTPS encryption).
2. Add the token parameter provided in the console, such as:
```
https://119.29.29.99/d?dn=cloud.tencent.com&token=xxxxx&ip=1.2.3.4
```

### Will fees change after I switch from the original HTTPDNS Enterprise Edition IP `119.29.29.99` to the Enterprise Edition IP `119.29.29.98/99`?
After you switch the IP, you can continue to use the monthly free tier and the purchased DNS plan, and the specification of and discount on the original plan will remain unchanged.
