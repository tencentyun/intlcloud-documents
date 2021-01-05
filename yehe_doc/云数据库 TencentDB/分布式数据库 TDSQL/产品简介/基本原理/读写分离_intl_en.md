## Overview
When read requests lead to high pressure and demand on the processing of high volume of data, read/write separation can be used to distribute the read requests to secondary nodes.
TDSQL for MySQL supports read/write separation by default. Each secondary in the primary-secondary architecture has the read-only permission. If multiple secondaries are configured, TProxy automatically assigns read requests to secondaries with lower loads to sustain the read traffic of large applications.

## How It Works
Read/write separation is to separate read and write capabilities by letting the primary node handle transactional operations (`INSERT`, `UPDATE`, and `DELETE`) and the secondary nodes perform query operations (`SELECT`).

## Read-only Account
A read-only account is a type of account only with read permission to read data from a secondary (or read-only replica) in a database cluster by default.
A read-only account can be used to implement automatic distribution of read requests to secondaries and return results.
![](https://main.qcloudimg.com/raw/ae753538608bfd9139cfc875ef2e2a4f.png)
