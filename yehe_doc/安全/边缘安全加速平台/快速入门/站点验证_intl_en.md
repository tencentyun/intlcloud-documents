## Overview
EdgeOne will ask you to pass site verification to prove your ownership of a site in the following cases:
- You discover that a site has already been added by another account when adding it.<br><img src="https://staticintl.cloudcachetci.com/yehe/backend-news/jXa5485_1.png" width=700px>

- You select CNAME access when adding a site, which leads to site verification in step 4.<br><img src="https://staticintl.cloudcachetci.com/yehe/backend-news/ENsI447_2.png" width=700px>

## Directions
EdgeOne provides DNS verification and file verification to check the site ownership. The steps are as follows:

### DNS verification
<dx-steps>
- Log in at your DNS service provider, add a TXT record, and add the specified host record and record value as required.
- Wait for the system to automatically complete the verification. If the record does not take effect after a long time, you can click **Refresh** to trigger system verification.
- After the record takes effect, click **Verify**.
</dx-steps>
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/Ah4y369_3.png" style="zoom:150%;" />


### File verification
#### Directions for Windows
<dx-steps>
- Go to the root directory of the server and create the verification directory `.well-known/teo-verification`.
- Click the file URL in step 2 to get the verification file and upload it to the verification directory.
- Copy the URL in step 3 to your browser and make sure that the resource is accessible.
- Click **Verify**.
</dx-steps>

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/GzPY329_6.png" width=700px>


#### Directions for Linux
<dx-steps>
- Run the command to enter the root directory of the web server.
- Copy the code in step 2 to the command and run it.
- Copy the URL in step 3 to your browser and make sure that the resource is accessible.
- Click **Verify**.
</dx-steps>

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/6nrc408_7.png" width=700px>
