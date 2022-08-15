You can use the `CREATE TABLE AS` statement to save the result of the `SELECT` query statement as a new table. Data Lake Compute stores data files created with `CREATE TABLE AS` in the COS bucket path you specified. The following describes how to save a query result as a new data table in the console.
1. Run a `SELECT` task to get the returned result of a task in the console.
2. Click ![](https://main.qcloudimg.com/raw/45d1b6b6da60cc0284353b63e5da2f2f.png) in the top-right corner of the **Running result** section and select **Save result as new table**.
![]()
3. In the pop-up window, configure the information of the new data table and click **Confirm**. Then, the system will automatically generate the `CREATE TABLE AS` statement.
 - Select the database of the new data table. By default, the system selects the database of the original table.
 - Enter the name of the new data table.
 - Select the bucket path for data files in the new data table.
 - Select the new data table format, which can be Parquet, ORC, Avro, CSV, or JSON.
![]()
4. Select the `CREATE TABLE AS` statement and click **Run**.

**System restraints**
- The rules for creating a target table are the same as the restraints on manipulating a data table.
- Saving the query result as a new table will generate new data files in the specified COS bucket path, which must exist and has no other data files.
