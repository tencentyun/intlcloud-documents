The following describes how to configure and provide a usage plan for a specific user:
1. Create a service. Create and configure an API to make it effective and responsive.
2. Publish the service to an environment, such as "release".
3. Create a pair of secret_id + secret_key.
	(1) Go to the Key tab, and click **New**.
	![New key](https://main.qcloudimg.com/raw/2c3cca73058efbd7b9dc9629e29445d7.png)
	(2) Enter the key name, and click **Submit**.
	![Key information](https://main.qcloudimg.com/raw/0b6423bb78d5bd4e47da58f9a7aaf102.png)
4. Create a usage plan.
	(1) Go to the Usage Plan tab, and click **New**.
![Plan](https://main.qcloudimg.com/raw/49896155d25c105600452a143536357f.png)
	(2) Edit the usage plan, and click **Finish**.
	![Plan information](https://main.qcloudimg.com/raw/347292ce30227ebd896b3de9666996ae.png)

5. Bind the usage plan to a service environment.
	(1) Select the service just created on the Service page, and then go to the Usage Plan tab and click **Bind**.
	![Binding plan](https://main.qcloudimg.com/raw/aec853e5f51cce4b9385d3be92fef72d.png)
	(2) Enter the release environment to be bound to, select the usage plan to be bound, and click **Submit**.
	![Binding information](https://main.qcloudimg.com/raw/2b833603229d4be3a8d02202b13d6430.png)

6. After the steps above are completed, you can provide the secret_id + secret_key created in Step 3 to end users. End users can obtain the verification using the secret_id + secret_key, and then access the API published in the service via the secondary domain name of the service or by binding a private domain name.

