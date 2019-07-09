After a service is published, you must create a usage plan and a key and bind them to the service before you can call it successfully.
1. Create a pair of secret_id + secret_key.
	(1) Go to the Key tab, and click **New**.
	![Key List](https://main.qcloudimg.com/raw/b276d29ab28f009de133e3a0c3e3c25b.png)
	(2) Enter the key name, and click **Submit**.
	![Create a Key](https://main.qcloudimg.com/raw/baa5c6e8619a5ab31606c8171de8b518.png)

2. Create a usage plan.
	(1) Go to the Usage Plan tab, and click **New**.
	![Usage plan list](https://main.qcloudimg.com/raw/df54039d0f5219b7c88e5f8addde3185.png)
	(2) Edit the usage plan, and click **Finish**.
![Create a usage plan](https://main.qcloudimg.com/raw/7e8d556a48d08541f43e5620ba69cd7e.png)

3. Bind the created secret_id + secret_key in the Usage Plan tab.
	(1) Go to the Usage Plan tab, and select the created service.
	(2) Click **Bind Key**.
	![Bind a key](https://main.qcloudimg.com/raw/9e3fe4beff8bfa64fb942ba5471a2afe.png)
	(3) Bind the created secret_id + secret_key in the Usage Plan tab, and click **Submit**.
	![Bind a key](https://main.qcloudimg.com/raw/9dee728d2241e95a028ab7f5d0dff736.png)
	
4. Bind the usage plan to a service environment.
	(1) Go to the Usage Plan tab, and select the created service.
	(2) Go to the **Bound Environment** page, and click **Bind Service Environment**.
	(3) Enter the service and the environment to be bound, and click **Submit**.
	![Enter the environment to be bound to](https://main.qcloudimg.com/raw/dd917c8709d5e9097b6614711c3050b8.png)
> Note: If two usage plans are to be bound to the same environment, the two usage plans cannot be bound to the same key.

5. After the steps above are completed, you can provide the secret_id + secret_key created in Step 1 to end users. End users can obtain the verification using the secret_id + secret_key, and then access the API published in the service via the secondary domain name of the service or by binding a private domain name.
