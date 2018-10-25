Click the instance name on the instance list page. Select **OPS** to go to the OPS page. You can view the code, start/stop the running instance, modify parameters and view real time data on this page, as shown below:
![](https://main.qcloudimg.com/raw/2cabbf664908c101d51d240e9579aa3f.png)
### View the code
You can find the SQL code of the instance that is currently running in the text box on the page. Modifying code is not allowed on the page.

### Start/Stop the launched instance
You can start and stop the instance by clicking the button on the upper left corner of the page.
- When the instance is "Running", the "Stop" button displays, and you can click it to stop the instance.
- When the instance is "Stopped", the "Start" button displays, and you can click it to start the instance.
- When the instance is "In operation", the button is grayed out and no operation is allowed.

### Modify the parameters of the running instance
The button on the upper right corner of the page is used to modify parameters of the running instance. Click the button to set the instance CU and CheckPoint (enable/disable, and time interval).
![](https://main.qcloudimg.com/raw/f7b3a27e4155bbf914e2d03856add8ad.png)
- When the instance is "Running", after the configuration is modified, the instance will restart according to the new configuration.
- When the instance is "Stopped", the configuration you modified will be saved.
- When the instance is "In operation", you cannot make any modifications.

### View data in real time
The run results of the running instance and data sample in the sources are displayed at the bottom of the page. No data is displayed when the instance is not "Running".
![](https://main.qcloudimg.com/raw/356749a8f8b91313db6375eaf187be53.png)
You can view the latest run results in real time and source data by switching between tabs.
On the **Real-time Run Results** page, click the **Refresh** button to get the latest run results in real time (which is not applicable to the source data page).
You can get more results or source data (not the latest data) by scrolling down the progress bar.
You can also get the latest run results or source data by clicking the table name on the page.
