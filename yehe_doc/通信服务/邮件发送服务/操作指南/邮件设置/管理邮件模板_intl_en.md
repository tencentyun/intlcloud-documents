## Managing Email Template
Before sending a template email, you need to create an email template. This document describes how to create and edit an email template in the console.

**Create an email template**
1.  Log in to the [DMS Console](https://console.cloud.tencent.com/dms).
2.  On the left sidebar in the console, click **Email Settings** > **Email Template** > **Create Email Template** to enter the template editing page.
![Image from Gyazo](https://main.qcloudimg.com/raw/138a946b91f19c0506ea4401d02ebaa8.png)
3.  You need to enter a unique **template name** for the email template and can customize any number of variables for the **email subject** and **email body**. You should define a variable in the format of `**{{ variable }}**`.
The following are common variables:
    - {{EAddr}}: recipient email address.  
	- {{Name}}: recipient name.  
	- {{NickName}}: recipient nickname.  
	- {{Gender}}: recipient title (Mr./Ms.).
	
	Click **OK** to save the email template.
	
	The template feature of DMS is based on the Handlebars template system. You can use Handlebars to create templates containing advanced features (such as nested attributes, array iteration, basic conditional statements, and inline elements). For samples of such features, please see [How do I send highly customized template emails?](https://intl.cloud.tencent.com/document/product/1070/38234).

**Edit and delete an email template**

1.  Log in to the [DMS Console](https://console.cloud.tencent.com/dms).
2. On the left sidebar in the console, click **Email Settings** > **Email Template** > **Delete** to delete the email template.
3.  Click **Edit** to enter the email template editing page. You can edit the **template name**, **email subject**, and **email body**. Click **OK** to save the email template.
> After an email template is **deleted** or **renamed**, it will become unavailable when you send a template email; therefore, you need to select a new template in such case.

