# Adding a Website
Website is the smallest unit of vulnerability scanning, which can be scanned individually or added to a detection task for scheduled scan. You can add websites on the website management page. Currently, CWS support adding websites accessed through domain names and IPs, including HTTP and HTTPS, multi-level sub-domain name, ported and multi-level sub-directory websites.

## Steps
1.Go to the website management console and click **Add a website**.

2.Complete the fields and click **OK** to go to the next step to verify the website.

- Choose the type of website to be added based on how your website is accessed.
- Enter the website URL in the website input box, one per line.
- Select your website type. CWS will set User-Agent access according to the type you choose:

    a. PC website: A website accessible through a PC browser.

    b. Mobile website: A website accessible through a mobile browser.

    c. WeChat website: A website accessible through WeChat.

3.Select DNS verification or file verification in the website verification pop-up.

i. If you choose DNS verification, please copy the host records and record values.

Enter the domain name resolution service console of your website (all domain name resolution service providers are supported, including Tencent Cloud DNS, DNSPod, Alibaba Cloud DNS, Net.cn DNS) and add TXT resolution.

Go back to the Tencent Cloud Console and click **Verify now** to complete the verification.

ii. If you choose file verification, please download the verification file (in HTML format).   
　　Upload it to the corresponding directory on your website.    
　　Confirm that the file is successfully uploaded.  
　　Click **Verify now** to complete the verification.

4.The website is added and verified now.