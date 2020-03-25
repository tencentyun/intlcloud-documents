The Phoenix supports SQL queries. The following are some common operations:

- Create a table

    ``` sql
    0: jdbc:phoenix:> CREATE TABLE IF NOT EXISTS TEST (
                        host char(50) not null,
                        txn_count bigint
                        CONSTRAINT pk PRIMARY KEY (host) );
    ```

- Insert data

    ``` sql
    0: jdbc:phoenix:>UPSERT INTO TEST(host,txn_count) VALUES('192.168.1.1',1);
    0: jdbc:phoenix:>UPSERT INTO TEST(host,txn_count) VALUES('192.168.1.2',2);
    ```

- Query data

    ``` sql
    0: jdbc:phoenix:>SELECT * FROM TEST;
    ```

- Delete a data table

    ``` sql
    0: jdbc:phoenix:>DROP TABLE IF EXISTS TEST;
    ```

For more operations and instructions, please see the [community documentation](http://phoenix.apache.org/language/index.html).
