### Create an Integrator
Configurations can be made to allow Stream Connector to communicate with existing products on Tencent Cloud. To output data to CDB automatically, configure an Integrator of a topic which is used to output stream computing results.
1. Click **New Integrator** in the topic list.
![](https://main.qcloudimg.com/raw/b534bff3b0539e031bb08d23c9b29d99.png)
2. Enter the Integrator information on the pop-up page. 
The **Type** is always "CDB For MySQL". Enter the username and password of the target CDB database, and click the **Verify** button to connect to the CDB database using the username and password. There will be a message after the verification is passed.
![](https://main.qcloudimg.com/raw/b6fe5b6ca6eea6ca593361b693e21bdf.png)
Then, select a database and a table of the CDB database under the **Verify** button.
![](https://main.qcloudimg.com/raw/f0bf19a4e2a6a20d1df0664af4002c8f.png)	
3. After selection, click the **Create** button to create an Integrator.	

### Start and stop an Integrator
Stream Connector will not export the data to CDB at the backend until the Integrator is started. So, be sure to start the Integrator after it is created.
![](https://main.qcloudimg.com/raw/5e6f9ba80017bdeb6ae1192fa59fe8fb.png)
### Delete an Integrator
An Integrator cannot be deleted until it is stopped.
![](https://main.qcloudimg.com/raw/72a25c390d613f1577f9de85c5204145.png)
