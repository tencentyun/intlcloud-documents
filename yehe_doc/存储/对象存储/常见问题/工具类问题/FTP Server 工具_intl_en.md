### How do I enable the FTP feature?

COS is a persistent storage that supports web-based requests but does not provide native FTP access. Intermediate transfer is required to use the FTP protocol. **It is recommended that you set up your service by using the [FTP Server Tool](https://www.qcloud.com/document/product/436/7214) provided by Tencent Cloud.**
As an outdated protocol, FTP protocol is unable to verify data integrity, ensure transfer security, or be integrated with the CAM system. Therefore, it is not recommended to use the FTP protocol for access, and Tencent Cloud will provide support for the FTP protocol and intermediate transfer software. 
For data synchronization, it is recommended to use the [COS Migration tool](https://intl.cloud.tencent.com/document/product/436/15392) or the [COSCMD tool](https://www.qcloud.com/document/product/436/10976).

### What does the masquerade_address option in the configuration file do and when does it need to be configured?

The `masquerade_address` is a server address configured for the client. When the FTP server runs on a host that is mapped to an external IP through NAT, you need to configure the masquerade_address option as an FTP server external IP that the client can access in order to notify the client to use the IP for data communication with the server.

For example, assume that you execute `ifconfig` on the host where the FTP server is running, and get a private ENI IP `10.xxx.xxx.xxx`, which is mapped to the public IP `119.xxx.xxx.xxx`. At this time, if the FTP Server does not explicitly set `masquerade_address` to the public IP (119.xxx.xxx.xxx) that the client uses to access the server, the FTP Server in Passive mode may use the private IP (10.xxx.xxx.xxx) to return packets to the client. As a result, the client is able to connect to the FTP Server, but cannot return data packets to the client properly.




### After the masquerade_address option is correctly configured, I can log in to the FTP server normally, but when I run the FTP command for fetching data such as "list" or "get", the error "The server returns a non-routable address" or "ftp: connect: No route to host" occurs. How do I deal with it?

The most possible reason for this is that the FTP server's `iptables` or firewall policy is configured to reject or drop all ICMP protocol packets. After receiving the data connection IP returned by the FTP server in the PASSIVE mode, the FTP client will send an ICMP packet first to verify the connectivity of the IP. In this case, errors such as "The server returns a non-routable address" may occur.

Solution: Configure the iptables policy to only reject or drop the ICMP packet types you want to block. For example, if you only want to block the external ICMP packets of Ping type, you can change the policy to: `iptables -A INPUT -p icmp --icmp-type 8 -s 0/0 -j [REJECT/DROP]`.
Alternatively, you can allow the IP of the client that will access the FTP server.

### Why is the uploaded part retained in COS when the upload of a large file is canceled halfway?

The FTP server for the latest version of COS provides a complete streaming upload feature. When you upload a large file, the cancellation or disconnection of the upload will trigger the completion of upload. In this case, COS considers that your data stream has been uploaded and combines the uploaded data into a complete file. If you want to resume the upload, you can upload the file with the same name to overwrite the original one, or delete the incomplete file manually and upload the file again.



### What will happen if the size of an uploaded file exceeds the limit?

If the size of the uploaded file exceeds the limit set in the configuration file, the system returns an IOError exception and marks the error message in the log.

If you have any other questions, please [contact use](https://intl.cloud.tencent.com/contact-sales) and provide the complete `cos_v5.log` log to facilitate troubleshooting.

### Why does a limit on the size of file to be uploaded need to be set in the COS FTP server configuration?

For a multipart upload in COS, the maximum number of file parts to be uploaded is 10,000, and the size of each file part is limited to 1 MB to 5 GB. The purpose of imposing the limits is to reasonably calculate the size of a file part.

The FTP server supports uploading a single file less than 200 GB by default. But it is not recommended to set the limit to a too large value, because a larger file size limit will cause a larger buffer for file parts during upload, thus increasing the consumption of your memory. Therefore, you are advised to set a reasonable file size limit as needed.



