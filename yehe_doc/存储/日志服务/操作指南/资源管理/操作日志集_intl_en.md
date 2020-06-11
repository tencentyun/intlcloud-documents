This topic focuses on how to work with logsets in the CLS console.

## Adding a Logset

1. Log in to the [CLS Console](https://console.cloud.tencent.com/cls), and click **Logset** in the left sidebar.
2. In the Logset Management page, select a CLS region for your logset.
>
> - It is recommended that you select the same region as the CVM or any other Tencent Cloud service from which you collect logs.
> - Once a logset is created, its Region attribute cannot be modified.
3. Click **Create Logset**, and in the pop-up window, configure the following:
	- Logset Name: project_test, for example.
	- Retention: supports 3-90 days. For more days, please contact us by [submitting a ticket](https://console.cloud.tencent.com/workorder/category).
    ![](https://main.qcloudimg.com/raw/4e5da331257c6df2f7a981bcd31b4229.png)
4. Click **OK**, and the logset will be created successfully.



Delete a Logset

1. Go to the [Logset Management](https://console.cloud.tencent.com/cls/logset) page.
2. Locate the logset you want to delete, and click **Delete** under Operation on the right.
>Before deleting a logset, you need to empty all the logs topics it contains.
>![](https://main.qcloudimg.com/raw/8fe145e4a6ad7ec126352e50f7c1619d.png)
3. In the pop-up window, click **OK** to delete the logset.
   ![](https://main.qcloudimg.com/raw/09032e04fe4e6fdb2432306ce140f937.png)





## Updating a Logset Name

1. Go to the [Logset Management](https://console.cloud.tencent.com/cls/logset) page.
2. Locate the logset whose name you want to update, and click **View** under Operation on the right to enter the logset details page.
3. Then click **Edit** in the Basic Info section to edit the logset information.
   ![](https://main.qcloudimg.com/raw/e8c49e75c44c8a9dbd83323d05fecde6.png)
4. Modify the logset information in Edit mode, click **Save**, and the logset information will be updated.
   ![](https://main.qcloudimg.com/raw/41fd0e8a08ba9cdbe37751e835b1a4ef.png)

