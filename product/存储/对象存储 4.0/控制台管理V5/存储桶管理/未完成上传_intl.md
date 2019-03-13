## Product Introduction
If prompted "**Deletion failed. Delete the valid data in the bucket first.**" when deleting a bucket, you can go to the **Partially Uploaded** tab to view the files that are partially uploaded and delete them. Only after you have deleted all partially uploaded and completely uploaded files in a bucket can you delete the bucket.

## Procedure

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) with a Tencent Cloud account, click **Bucket List** on the left navigation pane, and click the bucket you want to delete to enter the bucket details page.
![](https://main.qcloudimg.com/raw/b425fa4e3aeb5bbc6bc14cba7a7327b9.png)

2. In the bucket details page, click the **Partially Uploaded** tab to view the files that are partially uploaded. You can click **Delete** on the right to delete a partially uploaded file, or click **Clear All Fragments** to quickly delete all partially uploaded files.
![](https://main.qcloudimg.com/raw/f8d75cda49e20d02e52a57120b79657e.png)
>**Note:**
>Files that are suspended or canceled during upload are displayed in **Partially Uploaded**. Only completely uploaded files are displayed in **File List**.

3. After "Clear All Fragments" or "Delete" operation is executed, the list will be empty under **Partially Uploaded** as shown in the following figure.
![](https://main.qcloudimg.com/raw/12e74ae0bead00b4522f504146eae338.png)

