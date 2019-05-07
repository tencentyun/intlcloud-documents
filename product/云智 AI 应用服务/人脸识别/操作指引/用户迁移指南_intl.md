>!
- Face Recognition v1.0 (API request domain name: `recognition.image.myqcloud.com` or `service.image.myqcloud.com`) will be discontinued after June 20, 2019. Please upgrade the 1.0 version of APIs under your account to [the 2.0 version](https://cloud.tencent.com/document/product/867/32770) by this date.
- If you encounter any problems during migration, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=581&level2_id=600&source=0&data_title=%E6%99%BA%E8%83%BD%E9%89%B4%E9%BB%84&step=1) to report problems.
 
Face Recognition v2.0 offers facial detection, analysis, recognition, and million-scale search services with improved accuracy and real-timeness, meeting your massive search and precise recognition demands.

## Update Log
- [Face Search](https://cloud.tencent.com/document/product/867/32798) (formerly known as Face Retrieval) supports million-scale face searches. The maximum number of groups for one single Tencent Cloud account is increased from 5,000 to 20,000, and the maximum number of faces in one single group is increased from 20,000 to one million. Search results for millions of faces can be returned in just a few seconds.
- The following Android offline SDKs are added to the service: face detection, structured-light 3D/infrared light liveness detection, and face comparison and search. You can apply the SDK license for your devices (specify the number of devices allowed to use the SDK) or platform on the Tencent Cloud Console.
- [Face Detection and Analysis](https://cloud.tencent.com/document/product/867/32800) has the following added features: face attributes such as hairstyle and mask, face quality assessment (to determine whether the quality of the face image is good enough for face recognition).
- The [console](https://console.cloud.tencent.com/aiface/face-lib/manage) is optimized and now supports visual operations on groups and querying face search transactions. The real-time granularity of data reports is improved to 5 minutes.
- [APIs](https://cloud.tencent.com/document/product/867/32770) are optimized to support the TencentCloud API 3.0 format.

## Release Notes
The API request domain name of Face Recognition v2.0 is `iai.tencentcloudapi.com`, and the corresponding console address is https://console.cloud.tencent.com/aiface.
- If you are already using the `iai.tencentcloudapi.com` domain name, no changes are required. 
- If the API request domain name you are using is `recognition.image.myqcloud.com` or `service.image.myqcloud.com`, please migrate to v2.0 as soon as possible.

## API User Guide
Face Recognition v2.0 supports TencentCloud API 3.0 format and provides SDKs in Python, Java, PHP, Go, NodeJS, and .NET formats. You can download SDKs in different languages in the corresponding API documentation for quick access to the Face Recognition service.
In addition, you can use [API Explore](https://console.cloud.tencent.com/api/explorer?Product=iai&Version=2018-03-01&Action=DetectFace) and [TCCLI](https://cloud.tencent.com/document/product/440/6176) to quickly and easily debug APIs.

## Purchase Guide for Offline SDKs
See [Purchase Guide](https://cloud.tencent.com/document/product/867/30585).

## Console User Guide
Face Recognition v2.0 supports visual operations on groups, and you can add, delete, query, and modify groups in the console.
#### Group Management
- Create a group
On the **[People management](https://console.cloud.tencent.com/aiface/face-lib/manage)** page, click **Create a group** in the upper left corner, enter the group name and ID as prompted, and click **OK** to create a group.
![](https://main.qcloudimg.com/raw/e09c81ae50f86203bee8bc0fb0717303.png)
- Edit a group
In the group list, click **Edit** in the "Action" column for the group you want to edit to edit its name.
- Delete a group
In the group list, click **Delete** in the "Action" column for the group you want to delete to delete it.
>!If a person exists in multiple groups at the same time, deleting a group will not deleted the person, but the custom description field information in the group will be deleted.

#### Personnel Management
- Create a member
On the **[Personnel management](https://console.cloud.tencent.com/aiface/face-lib/manage)** page, select the target group name, click **Create a member** in the upper left corner, and upload their photo and enter their information as prompted.
![](https://main.qcloudimg.com/raw/1548e1cf7259fa9df4ab9b9fdb5dac94.png)
- Edit a member
In the member list, click **Edit** in the "Action" column for the member you want to edit to edit their photo, name, and gender.
- Delete a member
In the member list, click **Delete** in the "Action" column for the member you want to delete to delete them.
>!If a member exists in multiple groups at the same time, deleting this member from one group will cause them to be deleted from all groups.

## FAQs
For more information about how to migrate to v2.0, see the FAQs for [Face Recognition v2.0](https://cloud.tencent.com/document/product/867/30246).



