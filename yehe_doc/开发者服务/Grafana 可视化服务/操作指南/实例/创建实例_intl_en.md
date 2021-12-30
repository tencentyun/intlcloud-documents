This document describes how to create a Grafana instance.

>?Currently, Grafana is in beta test, and each root account can apply for one instance.

## Directions

1. Log in to the [TCMG console](https://console.cloud.tencent.com/monitor/grafana).
2. Click **Create** and configure the following information as prompted:
<table>
    <tr>
        <th style = "width:10%">
            Item
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
            Currently, only Trial Edition is supported.
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
            You can customize the name of a Grafana instance.
        </td>
    </tr>
    <tr>
        <td>
            Available Region
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
            It indicates a logically isolated network space in Tencent Cloud. A VPC consists of at least one subnet. The system will provide a default VPC and subnet for you in each region. If the existing VPCs/subnets don't meet your requirements, you can create new ones as instructed in 
            <a href="https://intl.cloud.tencent.com/zh/document/product/215/31805">
                Creating VPCs
            </a>
            and
            <a href="https://intl.cloud.tencent.com/zh/document/product/215/31806">
                Creating Subnets
            </a>
            .
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
            It is `admin` by default and cannot be changed.
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
            Defines the Grafana login password, which must contain 8–16 characters in at least three of the following four character types: uppercase letters, lowercase letters, digits, and special symbols (-!@#$%^&amp;*+=_;:.?).
        </td>
    </tr>
    <tr>
        <td>
            Public Network Access
        </td>
        <td>
            Yes
        </td>
        <td>
            Specify whether to allow access to Grafana over public network.
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
            <a href="https://intl.cloud.tencent.com/zh/document/product/213/19548">
                Managing Instances via Tags</a>.
        </td>
    </tr>
</table>


3. After completing the configuration, click **Buy Now**.
