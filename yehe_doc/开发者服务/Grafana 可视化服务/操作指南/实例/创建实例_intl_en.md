This document describes how to create a TencentCloud Managed Service for Grafana (TCMG) instance.



## Directions

1. Enter the [TCMG purchase page](https://buy.tencentcloud.com/grafana) and configure the following items as needed:
<table>
    <tr>
        <th style = "width:10%">
            Configuration Item
        </th>
        <th style = "width:10%">
            Required
        </th>
        <th>
            Configuration Description
        </th>
    </tr>
    <tr>
        <td>
            Billing Mode
        </td>
        <td>
            Yes
        </td>
        <td>
            Currently, only monthly subscription billing is supported.
        </td>
    </tr>
        <td>
            Region and AZ
        </td>
        <td>
            Yes
        </td>
        <td>
            Select a region based on the region of your Tencent Cloud service. Tencent Cloud services in different regions cannot interconnect with each other over private network. Selecting the region closet to your end users can minimize access latency. Once the instance is created, you cannot switch the region.
        </td>
    </tr>
    <tr>
        <td>
            Network
        </td>
        <td>
            Yes
        </td>
        <td>
            Currently, only subnets in certain AZs are supported. For more information, see the <a href="https://buy.tencentcloud.com/grafana">TCMG purchase page</a>. 
						“Network” refers to a logically isolated network space in Tencent Cloud. A VPC consists of at least one subnet. The system will provide a default VPC and subnet for you in each region. If the existing VPCs/subnets don't meet your requirements, you can create new ones as instructed in 
            <a href="https://intl.cloud.tencent.com/document/product/215/31805">
                Creating VPC
            </a> 
            and 
            <a href="https://intl.cloud.tencent.com/document/product/215/31806">
                Creating Subnets
            </a>
            .
        </td>
    </tr>
		<tr>
        <td>
           Instance Edition
        </td>
        <td>
            Yes
        </td>
        <td>
         Three instance editions are supported: Basic, Advanced, and Pro. They only differ in the number of accounts they support. For more information, see <a href="https://intl.cloud.tencent.com/document/product/1124/49506" >Monthly Subscription</a>.
        </td>
    </tr>
		 <tr>
        <td>
          Instance Name
        </td>
        <td>
Yes
        </td>
        <td>
          You can customize the name of a TCMG instance.
        </td>
    </tr>
    <tr>
        <td>
            Username
        </td>
        <td>
            Yes
        </td>
        <td>
            The default username is “admin” and cannot be changed.
        </td>
    </tr>
    <tr>
        <td>
            Password
        </td>
        <td>
            Yes
        </td>
        <td>
            A custom Grafana login password, which must contain 8–16 characters in at least three of the following four character types: uppercase letters, lowercase letters, digits, and symbols (-!@#$%^&amp;*+=_;:.?).
        </td>
    </tr>
    <tr>
        <td>
            Tag
        </td>
        <td>
            No
        </td>
        <td>
            Tags can be configured to manage resources by category in different dimensions. For more information, see 
            <a href="https://intl.cloud.tencent.com/document/product/213/19548">
                Managing Instances via Tags</a>.
        </td>
    </tr>
		    <tr>
        <td>
          Auto-Renewal
        </td>
        <td>
            No
        </td>
        <td>
         Your instance will be automatically renewed monthly upon expiration if your account has a sufficient balance.
    </tr>
</table>

 ![](https://qcloudimg.tencent-cloud.cn/raw/106d44c3450d78e4d216bd3d67ebd9eb.png)
2. Confirm the information you enter, click **Buy Now**, and make payments.

