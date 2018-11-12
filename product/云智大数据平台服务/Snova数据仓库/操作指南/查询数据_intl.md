### Querying Data Using Command Line

After data warehouse is accessed as per the instructions in [Accessing Data Warehouse](/document/product/878/20075), the data can be queried. Below is an example:

1.First, enter the specified DB named test using the command below.

   ```
   \c test;
   ```

2.Create a table named test. Enter the following command:

   ```
   create table test(a1 int);
   ```

3.Insert the data. Enter the following command: 

   ```
   insert into test values(3),(4);
   ```

4.Query the data. Enter the following command: 

   ```
   select * from test;
   ```

   

