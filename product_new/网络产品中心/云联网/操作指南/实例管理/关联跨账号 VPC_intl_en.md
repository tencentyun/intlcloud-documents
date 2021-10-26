To associate VPC and CCN under different accounts, the VPC account should initiate an association request. The association is established when the CCN account accepts the request.  
The following figure illustrates the detailed steps:
![](https://main.qcloudimg.com/raw/c351b9e558517ee4d432f16ef4bd5448.png)
## Submitting Association Request via a VPC Account
1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc/vpc?rid=1) . 
2. Click the ID of the VPC to be added to a CCN to open the details page. Then,  click **Associate Now**.
![](https://main.qcloudimg.com/raw/a17881a5c0441e3f1e834d8e7e0a0f98.png)
3. In the window that appears, enter the peer account ID and the peer CCN ID, and then click **OK** to submit the application.
 ![](https://main.qcloudimg.com/raw/2a9c18546c2a1c0442564ff8445c438c.png)

## Accepting the Application via the CCN Account
1. Log in to [CCN Console](https://console.cloud.tencent.com/vpc/ccn) and  click the ID of the CCN instance with a pending association request. 
2. On the **Bind with Instance** tab page, find the information about the VPC to be approved, and click **Accept** to add the VPC to the CCN. 
![](https://main.qcloudimg.com/raw/00e77fe68fb24e1de8f3ead93fcbea46.png)

## (Optional) Checking the Route Table
After the association request is accepted and the association succeeds, you need to view the route table to check whether the IP range of this instance conflicts with that of an existing CCN instance, to prevent a routing failure. 
For more information about related operations, see [Checking Route Table](https://intl.cloud.tencent.com/document/product/1003/30066).

## (Optional) Setting a Bandwidth for Cross-Region Interconnection
For more information about related operations, see [Setting a Bandwidth for Cross-Region Interconnection](https://intl.cloud.tencent.com/document/product/1003/30073).
