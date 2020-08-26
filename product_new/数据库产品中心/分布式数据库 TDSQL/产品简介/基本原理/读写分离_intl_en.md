## Feature overview
When the read requests lead to high pressure and demand during processing of high volume of data, read-write separation can be used to distribute the read requests to slave nodes.
TDSQL supports read-write separation by default. Each slave in the master-slave architecture can be read-only. If multiple slaves are configured, read requests will be automatically allocated to low-load slaves by the gateway cluster (TProxy) to support the read traffic of large applications.

## How it works
Read-write separation is to separate read and write capabilities by letting the master node handle transactional operations (INSERT, UPDATE, and DELETE) and the slave nodes perform query operations (SELECT).

## Read-only account
A read-only account is a type of account only with read permission to read data from a slave (or read-only instance) in a database cluster by default.
A read-only account can be used to implement automatic distribution of read requests to slaves and return results.
![](https://main.qcloudimg.com/raw/ae753538608bfd9139cfc875ef2e2a4f.png)
