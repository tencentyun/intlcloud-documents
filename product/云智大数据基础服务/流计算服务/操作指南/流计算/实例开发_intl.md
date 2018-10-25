Click the instance name on the instance list page. Select **Analytical Development** to go to the instance development page.
You can develop SQL for an instance, debug and launch an instance on this page, as shown below:
![](https://main.qcloudimg.com/raw/b9b94602f77f48b2d749e818e420a95b.png)
### 1. Develop SQL
In the text box, enter the instance's SQL to be developed to define the DDL for the instance's source and sink tables and the SQL operations required to execute the instance. The text box provides features such as automatic keyword prompt and highlighting. Besides, you can choose a data stream to automatically generate DDL code for an appropriate table, as shown below:
![](https://main.qcloudimg.com/raw/82a19b1c292c546d1e336925ec00caba.png)

In addition, you can also check the instance's SQL syntax by clicking the **Syntax Check** button to see if there is any SQL syntax error in current instance or whether the topic of the defined source or sink table exists.
![](https://main.qcloudimg.com/raw/307cd0e74998af074d3cc1cb116fa7bb.png)

### 2. Debug
Analytical Development provides an independent simulation environment, which allows you to upload data, make simulation runs and check output results.
![](https://main.qcloudimg.com/raw/d393d7dda80341f7e609403fa2e93d53.png)
Only txt file is supported with the size limited to 1 MB.
![](https://main.qcloudimg.com/raw/e5a075359ae76471d789d458ccf10d0f.png)

### 3. Launch
When you have finished developing the SQL and debugging your instance, you can launch the instance after it is configured. When configuring the instance, you need to set the number of resources to be used (1CU indicates 1-core CPU and 4 GB memory), whether to enable CheckPoint, and the time interval between CheckPoints. The **Save** button is only used to save the current configurations and SQL for further modification. The **Save and Launch** button is used to launch an instance. The overall process is as follows:
![](https://main.qcloudimg.com/raw/ef769dd2e6a7a8f9b72a1b8eb39782b4.png)
- If the current instance is "Not launched", clicking the **Save and Launch** button will save the instance configuration and start the instance.
- If the current instance is "Running", launching the instance will update the instance configuration and restart the instance.
- If the current instance is "Stopped", launching the instance will save the instance configuration and start the instance.
- If the current instance is "In operation", you cannot launch any instance.
