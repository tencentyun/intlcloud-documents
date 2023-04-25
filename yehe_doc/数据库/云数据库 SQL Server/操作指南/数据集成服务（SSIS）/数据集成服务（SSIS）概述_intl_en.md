
## Overview
SSIS, SSAS, and SSRS are three key components for SQL Server to implement business intelligence (BI).
- SQL Server Integration Services (SSIS) provides enterprise-grade data integration and conversion solutions to extract, transform, and load (ETL) data from various sources.
- SQL Server Analysis Services (SSAS) is a data analysis engine used to create cubes (multidimensional data models).
- SQL Server Reporting Services (SSRS) is a report tool used to create, deploy, and manage mobile and paginated reports.

TencentDB for SQL Server has released the business intelligence server feature, which provides a complete set of BI solutions integrating data storage, ETL, and visual analysis and supports SSIS. SSIS can be used to sustain complex business scenarios, such as merging data from heterogeneous data stores, cleansing and standardizing data, populating data warehouses and datasets, transforming data for complex business logic, supporting management features, and automating data loading. It helps meet your diversified needs in various use cases, including BI analysis, high-value data mining, and primary data management system setup.

SSIS can extract and transform data from various data sources and load the data into one or multiple targets. SSIS capabilities in Tencent Cloud currently can be used for TencentDB for SQL Server and flat files (with .txt, .csv, .xlsx, and .xls extensions).

To use the SSIS capabilities in TencentDB for SQL Server, you need to use the SSIS engine in a business intelligence server to deploy a project first.

## Use Cases
### Merging data from heterogeneous data stores
Data is usually stored in many different data storage systems, and you often need to extract data from these sources and merge it into a single consistent dataset. This process faces various problems, including complex and different traditional systems, data formats, and preprocessing flows.

SSIS can use .NET and OLE DB access APIs to connect to TencentDB and use an ODBC driver to connect to multiple legacy databases. It can also connect to flat files and Excel files. In addition, it has some source components to extract data from different data sources and provides the data transformation feature. After transforming data into compatible formats, it can further merge data physically into one target database. Then, it can load the data into flat files and SQL Server databases.

### Cleansing and standardizing data
Various data sources use different conventions and standards, and different business processing jobs need to be executed during data loading. Therefore, whether data is loaded into an online transaction processing (OLTP) or online analytic processing (OLAP) database, an Excel spreadsheet, or a file, it needs to be cleaned and standardized before it is loaded.

SSIS includes built-in transformations that you can add to packages to clean and standardize data, change the case of data, convert data to a different type or format, or create new column values based on expressions. For example, a package can concatenate first and last name columns into a single full name column, and then change the characters to uppercase. A package can also clean data by replacing the values in columns with values from a reference table, using either an exact lookup or fuzzy lookup to locate values in the reference table.

### Processing complex business logic during data transformation
A data transformation process requires built-in logic to respond dynamically to the data it accesses and processes. The data may need to be summarized, converted, and distributed based on data values. The process may even need to reject data based on an assessment of column values. SSIS offers many types of relevant jobs:
- Merging data from multiple data sources.
- Evaluating data and applying data conversions.
- Splitting a dataset into multiple datasets based on data values.
- Applying different aggregations to different subsets of a dataset.
- Loading subsets of the data into different or multiple destinations.

### Automating administrative features and data loading
SSIS provides components to automate management, such as copying TencentDB for SQL Server databases and their contained objects, copying TencentDB for SQL Server objects, loading data, and setting the scheduling cycle and frequency of SSIS tasks.

## Benefits
### High-value data mining
SSIS aggregates discrete and partially structured data in an enterprise at different standards by cleansing and processing the data. This helps tap into the value of data and form an enterprise-level unified database, which serves as a high-quality data source for enterprise decision making.

### Primary data management system setup
Legacy business systems may have various problems such as complex and different data sources, formats, and preprocessing flows required for merging. SSIS can extract, transform, load, and merge data from multiple storage systems into one target database for unified primary business database setup. This not only facilitates internal data maintenance and management but also reduces the storage and maintenance costs otherwise incurred by many different databases.

### BI analysis
SSIS provides a complete set of BI analysis solutions ranging from data storage and ETL to visual analysis. With SSIS, you can perform such operations on different data sources at one stop and then easily implement real-time self-service visual data analysis throughout the entire linkage. SSIS also helps you set up an enterprise data middleend to guide refined data-driven business operations.

### Data integration for internal business systems
SSIS greatly improves your efficiency, accuracy and system performance of data collection and cleansing while simplifying the entire data aggregation and analysis process. You can configure SSIS to automatically schedule data ETL jobs, which facilitates data integration with your internal business systems.

## Use Limits
- Currently, the business intelligence server feature is in beta test and can be used free of charge. During the beta test, you can purchase only one business intelligence server with the 2-core 4 GB MEM specification in each region and up to three under each root account. Billing will start in pay-as-you-go mode after the beta test ends.
- Currently, three SSIS versions are supported: SQL Server 2016 Integration Services, SQL Server 2017 Integration Services, and SQL Server 2019 Integration Services.
- TencentDB for SQL Server single-node (formerly Basic Edition) and two-node (formerly High Availability/Cluster Edition) instances can use SSIS capabilities through the business intelligence server, while read-only instances cannot.
- Currently, the business intelligence server feature is available only in four regions: Guangzhou, Shanghai, Beijing, and Hong Kong (China).

## Notes
- SSIS capabilities in Tencent Cloud currently can be used for TencentDB for SQL Server and flat files (with .txt, .csv, .xlsx, and .xls extensions).
- The business intelligence server and source/target SQL Server instances must be in the same region. SQL Server database instances can communicate with business intelligence servers in different AZs in the same region.
- One business intelligence server can be connected to an unlimited number of database instances. In other words, you can connect one business intelligence server to multiple source and target instances to run multiple SSIS project tasks.
- The CPU and memory specifications of a business intelligence server are subject to the complexity of SSIS project tasks. The disk space is subject to the size of added flat files.
- You can get the **COS File URL** for file upload and deploy the flat file to the business intelligence server only after uploading the flat file to COS. Note that the access permission of the COS object must be set to public read/private write. Only flat files in .txt, .csv, .xlsx, or .xls format are supported. The filename must start with a letter and can contain only digits, letters, underscores, and hyphens.
- A domain prefix will be automatically added to Windows authentication accounts of the business intelligence server created in the console, and you don't need to care about the prefix. For example, if you create an account `act1` in the console, the account name displayed in the list will be `xx_x_xx_xxxx/act1`.
- Source and target database instances and the business intelligence server involved in an SSIS project need to be interconnected before the project can be deployed. Therefore, all of them need to be added to the same interworking group, and the interworking IP for business intelligence services needs to be enabled for each of them.
- After the database instances and business intelligence server are added to an interworking group, each of them has two IPs: private IP and interworking IP for business intelligence services, with different purposes. Therefore, carefully distinguish between them in operation steps.
- SSIS projects only support the project deployment mode.
- You can use SQL Server Agent to run SSIS program packages.
- Do not manually create or restore the `SSISDB` database; otherwise, SSIS may not run properly.

## Flowchart
**Prerequisites**
Prepare a built SSIS project file with the `.ispac` extension.
**1. [Purchase a business intelligence server.](https://intl.cloud.tencent.com/document/product/238/48059)**
TencentDB for SQL Server uses SSIS capabilities, which require project deployment through the SSIS engine in a business intelligence server. If you are using SSIS for the first time, you need to purchase a business intelligence server. If the source and target TencentDB for SQL Server instances in your SSIS project already have a business intelligence server in the same region, skip this step and proceed to **step 2**.

**2. [Create a Windows authentication account.](https://intl.cloud.tencent.com/document/product/238/48058)**
You need to create a Windows authentication account for the business intelligence server for login and SSIS project deployment.
>?Accounts created on the business intelligence server all have Windows authentication permissions. Business intelligence servers can use only this type of accounts, and account permissions cannot be modified.

**3. [Add a flat file.](https://intl.cloud.tencent.com/document/product/238/48057)**
Before deploying an SSIS project, you need to check whether the project involves flat files, and if so, you need to add the flat files to the business intelligence server first. If the source and target instances in the project don't involve flat files, skip this step and proceed to **step 4**.

**4. [Interconnect the source and target instances and business intelligence server.](https://intl.cloud.tencent.com/document/product/238/48056)**
Before deploying an SSIS project, you need to interconnect the source and target database instances and business intelligence server involved in the project. The interworking group management feature is used to sustain interconnection between instances. Therefore, in the same account and region, all database instances and the business intelligence server in the SSIS project need to be added to the same interworking group, and the interworking IP for business intelligence services needs to be enabled for each of them before they can access each other.

**5. [Deploy an SSIS project.](https://www.tencentcloud.com/document/product/238/47721)**
Before deploying an SSIS project, you need to connect to the business intelligence server as follows:
5.1 Create a Windows authentication account with the same account name and password as that on the business intelligence server in a Windows CVM instance.
5.2 Use the Windows authentication account created in step 5.1 to log in to the Windows CVM instance.
5.3 Use the Windows authentication account to log in to the business intelligence server.
5.4 Deploy an SSIS project.
5.5 Configure the SSIS service, including connection configurations for flat files and the source and target TencentDB for SQL Server instances.
5.6 Run the SSIS service and execute the package.
5.7 Configure an agent job by creating job steps and schedule.

## SSIS Operations
<table>
<thead><tr><th>Feature Page</th><th>Feature</th><th>Operation Guide and Directions</th></tr></thead>
<tbody>
<tr>
<td rowspan="6">Instance List</td>
<td>Purchasing business intelligence server</td><td>For detailed directions on how to create/purchase a business intelligence server, see <a href="https://www.tencentcloud.com/document/product/238/48059" target="_blank">Purchasing Business Intelligence Server</a>.</td></tr>
<td>Renaming instance</td><td>The operation steps are the same as those for a TencentDB for SQL Server instance. For detailed directions, see <a href="https://www.tencentcloud.com/document/product/238/46508" target="_blank">Renaming Instance</a>.</td></tr>
<td>Restarting instance</td><td>The operation steps are the same as those for a TencentDB for SQL Server instance. For detailed directions, see <a href="https://www.tencentcloud.com/document/product/238/46505" target="_blank">Restarting Instance</a>.</td></tr>
<td>Terminating instance</td><td>The operation steps are the same as those for a TencentDB for SQL Server instance. For detailed directions, see <a href="https://www.tencentcloud.com/document/product/238/35787" target="_blank">Terminating Instance</a>.</td></tr>
<td>Recycle bin</td><td>After a business intelligence server is terminated or deleted by mistake, the operations that can be performed in the recycle bin are the same as those for a TencentDB for SQL Server instance. For detailed directions, see <a href="https://www.tencentcloud.com/document/product/238/46504" target="_blank">Recycle Bin</a>.</td></tr>
<td>Editing tag</td><td>The operation steps are the same as those for a TencentDB for SQL Server instance. For detailed directions, see <a href="https://www.tencentcloud.com/document/product/238/46506" target="_blank">Setting Instance Tag</a>.</td></tr>
<tr>
<td rowspan="8">Instance management</td>
<td>Setting instance remarks</td><td>The operation steps are the same as those for a TencentDB for SQL Server instance. For detailed directions, see <a href="https://www.tencentcloud.com/document/product/238/46507" target="_blank">Setting Instance Remarks</a>.</td></tr>
<td>Changing network</td><td>The operation steps are the same as those for a TencentDB for SQL Server instance. For detailed directions, see <a href="https://www.tencentcloud.com/document/product/238/46497" target="_blank">Changing Network (from VPC to VPC)</a>.</td></tr>
<td>Modifying project</td><td>The operation steps are the same as those for a TencentDB for SQL Server instance. For detailed directions, see <a href="https://www.tencentcloud.com/document/product/238/35786" target="_blank">Setting Instance Project</a>.</td></tr>
<td>Setting instance maintenance information</td><td>The operation steps are the same as those for a TencentDB for SQL Server instance. For detailed directions, see <a href="https://www.tencentcloud.com/document/product/238/35785" target="_blank">Setting Instance Maintenance Information</a>.</td></tr>
<td>View monitoring chart</td><td>The monitoring metrics of a business intelligence server and a TencentDB for SQL Server instance are not completely the same. Specific monitoring metrics are as displayed on the actual monitoring page. For detailed directions, see <a href="https://www.tencentcloud.com/document/product/238/46503" target="_blank">Viewing Monitoring Charts</a>.</td></tr>
<td>Configuring security group</td><td>A business intelligence server also needs to be configured with a security group. For detailed directions, see <a href="https://www.tencentcloud.com/document/product/238/35789" target="_blank">Configuring Security Group</a>.</td></tr>
<td>Managing account</td><td>For detailed directions on how to create and delete accounts, see <a href="https://intl.cloud.tencent.com/document/product/238/48058" target="_blank">Creating Windows Authentication Account</a>.</td></tr>
<td>Managing SSIS</td><td>For detailed directions on how to manage SSIS and add flat files, see <a href="https://www.tencentcloud.com/document/product/238/48057" target="_blank">Adding Flat File</a>.</td></tr>
<tr>
<td rowspan="1">Interworking Group Management</td>
<td>Interconnecting source/target instances and business intelligence server</td><td>For detailed directions on how to enable the interworking IP for business intelligence services and add instances to an interworking group, see <a href="https://www.tencentcloud.com/document/product/238/48056" target="_blank">Interconnecting Source/Target Instances and Business Intelligence Server</a>.</td></tr>
</tbody></table>
