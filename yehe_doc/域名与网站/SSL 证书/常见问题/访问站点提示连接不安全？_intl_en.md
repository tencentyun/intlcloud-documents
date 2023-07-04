### The accessed site prompts "connection is not secure" after SSL certificate deployment. Has the certificate deployment failed?
The certificate has been successfully deployed. This problem occurs because the browser considers the access to sites using HTTPS protocol unsafe when the pages contain unencrypted HTTP contents. In this case, code needs to be modified.

**For frontend modification, here are some guidelines:**
- Use the relative path to reference resources.
- When referencing the absolute path, use `//` to reference resources. For example, `//img.qcloud.com/example.png` indicates compliance with the protocol of the current page, and the browser will automatically complete it.

