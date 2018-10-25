After writing the code, you can debug the instance before launching it.
Analytical Development provides an independent simulation environment, which allows you to upload data, make simulation runs and check output results.
![](https://main.qcloudimg.com/raw/8997c110d99ad2daf25e6b4980d3ab15.png)
The data source is identified automatically depending on the SQL code and displayed as a list item. Before debugging, click the **Upload** button at the end of the data source to upload the data to be debugged.
Only txt file is supported with the size limited to 1 MB. Each line in the file represents a data record where fields are separated by commas.
```
2018-05-23 18:01:28,0,0
2018-05-23 18:01:18,2,8
2018-05-23 18:01:08,9,5
2018-05-23 18:00:58,9,4
2018-05-23 18:00:48,5,9
2018-05-23 18:00:38,4,2
2018-05-23 18:00:28,6,2
2018-05-23 18:00:18,1,0
2018-05-23 18:00:08,4,2
```
The file will go through a validity verification once uploaded. If the verification is passed, the file name is displayed normally; otherwise an error will be returned.
![](https://main.qcloudimg.com/raw/32b5114e254e240f29a1d8d762fdedda.png)
Now, preparations have been made for debugging. Click the **Debug** button. A prompt indicating the operations at the backend will appear.
![](https://main.qcloudimg.com/raw/c5c22cd844d0df7373c86544eb0c0a33.png)
After a moment, the results will be displayed on the interface, which can be downloaded by clicking the **Download Results** button.
![](https://main.qcloudimg.com/raw/87eb7de3ed55849c14d48c156ddd8eb4.png)
After you finish debugging, check the results to confirm that the SQL statements meet your needs before launching the instance.


