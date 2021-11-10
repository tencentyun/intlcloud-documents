TDSQL for MySQL instances support read-write separation in the following modes:
- A comment flag such as `/*slave*/` can be added to send specified SQL statements to the secondary server.
>?Comment flags including `/*slave:slaveonly*/`, `/*slave:20*/`, and `/*slave:slaveonly,20*/` are also supported, where the value indicates the delay requirement that the secondary server should satisfy, and `slaveonly` indicates that the query will not be sent to the primary server if there is no eligible secondary server.

- Requests sent by read-only accounts are sent to the secondary server according to the configured attributes.
