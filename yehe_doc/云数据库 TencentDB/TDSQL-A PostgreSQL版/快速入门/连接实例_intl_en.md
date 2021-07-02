
This document describes how to connect a TDSQL-A for PostgreSQL instance through a CVM instance. The instances must be under the same account and in the same VPC in the same region.
>?TDSQL-A for PostgreSQL is currently in beta test. If you want to try it out, please [submit an application for beta test eligibility](https://cloud.tencent.com/apply/p/vbtsrbx5vd).

## Directions
This document uses a CVM instance on CentOS 7.2 64-bit as an example. For more information on CVM instance purchase, please see [Purchasing Channels](https://cloud.tencent.com/document/product/213/506).

1. [Log in to the Linux CVM instance](https://cloud.tencent.com/document/product/213/5436) and run the following command to download PostgreSQL:
```
rpm -Uvh https://download.postgresql.org/pub/repos/yum/10/redhat/rhel-7-x86_64/pgdg-redhat-repo-42.0-11.noarch.rpm
```
>?Replace the PostgreSQL download address in the example with the one corresponding to the actual OS.
2. Run the following command to install PostgreSQL:
```
yum install -y postgresql10-server postgresql10
```
3. Run the following command to connect to TDSQL-A for PostgreSQL:
```
psql -h instance address -p port -U dbadmin -d postgres
```
>?You can view the instance address and port on the instance details page in the [TDSQL-A console](https://console.cloud.tencent.com/tdsqla/tdapg).

