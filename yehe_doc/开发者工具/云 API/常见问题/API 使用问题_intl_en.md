### What should I do if an error occurs when I try to run a single signature file in C++?
If the following error occurs when the `g++ -o main sign.cpp` command is executed on the command line:
![](https://main.qcloudimg.com/raw/47b54bd02a875e4e8ce44805ff89b887.png) 
Run the following command to solve the problem.
```bash
g++ -o main sign.cpp -lssl -lcrypto
```


### What should I do if error 10060 occurs?
When the error message `Socket error 10060 - Connection timed out` is prompted, it is actually an error thrown by the socket programming interface, indicating that the network connection has timed out. Your machine will not be able to communicate with the TencentCloud API server. Please check the following:
- Whether a proxy needs to be set up for local access to the public network.
- Whether the local firewall has rules that restrict public network access.
- Whether the router has rules that restrict public network access.

### What are the error codes of TencentCloud API?

TencentCloud API error codes divide into common ones and API-specific ones:
- Common error codes: you can go to **API documentation** > **Call Method** >**Returned Result** in the documentation of specific services to view them in the returned result document.
- API-specific error codes: you can view them in the specific API document, such as [RunInstances](https://intl.cloud.tencent.com/document/product/213/33237#6.-.E9.94.99.E8.AF.AF.E7.A0.81).

