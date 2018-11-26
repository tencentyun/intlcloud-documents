## 1. Log in to the console
Log in to the **Stream Compute Service** console. Click **Stream Connector** in the left navigation bar to enter the Stream Connector system.


## 2. Create a Project
Click the **New Project** button. Enter the required information in the window that appears, and then click **Create**.

> Note: Stream Connector must be in the same region as SCS. Stream Connector can only work with products such as Ckafka and CDB within the same region. Attempts to access data across regions will fail.


## 3. Create a Topic
**Create a topic for the SCS data source**
Click on the project name you just created to enter the project. Click the **New Topic** button and enter the topic information on the page that appears.
![image](https://main.qcloudimg.com/raw/1885e35ba189a46e0cd7d14176a16ccd.png)
There are three input options available, and tuple is used in this example.

**Tuple**: The most frequently used option, indicating that the data is in text format.
**Blob**: Used for binary data, which cannot be used with SCS.
**Upsert**: Selected when you export data from Stream Connector to CDB and want to update records against the result of aggregating primary keys.
**Partitions**: Select the default value 1.

**Create a Stream Connector topic for outputting stream computing results**
![image](https://main.qcloudimg.com/raw/bc9513af3090213149715ee662c8729f.png)
This topic is highly similar to the topic serving as data source, only with slight variations in the table structure. To perform aggregate calculations that require updating the results, select the upsert type and specify a primary key.


##4. Create an Integrator
Configurations can be made to allow Stream Connector to communicate with existing products on Tencent Cloud. To output data to CDB automatically, configure an integrator of a topic which is used to output stream computing results.

###4.1 Apply for a CDB instance and create a database and table, using the same schema for the table as you used for the topic.

    CREATE TABLE `demo_sink` (
      `record_time` varchar(32) NOT NULL,
      `pv` bigint(20) NOT NULL,
      `uv` bigint(20) NOT NULL,
      PRIMARY KEY (`record_time`)
    ) ENGINE=InnoDB DEFAULT CHARSET=utf8

###4.2 Click **New Integrator** in the topic list.
![image](https://main.qcloudimg.com/raw/d698554a92e8c48acdcd20e8490dab30.png)
The **Type** is always "CDB For MySQL". Enter the instance ID, username, and password of the target CDB database.

###4.3 Click the **Verify** button to connect to the CDB database using the username and password. There will be a message after the verification is passed.
![image](https://main.qcloudimg.com/raw/355b7a4e535f3f25e6ab02f9762c79fd.png)
3. Select the database and table you just applied for and created, and click the **Create** button to create an integrator.


##5. Start an Integrator
Click the **Start** button in the operation column to start the integrator you just created.
![image](https://main.qcloudimg.com/raw/b02e3579600bc1f674d285674c162edf.png)

Your Stream Connector is now ready for use. You have created a Stream Connector topic for inputting data and a Stream Connector topic for outputting data compute results and with the ability to automatically transfer data to a specified CDB database.

