## UDF description
You can write a user-defined function (UDF), package it into a JAR file, and define it as a function in Data Lake Compute for use in query analysis. Currently, UDFs in Data Lake Compute are in the Hive format and inherit `org.apache.hadoop.hive.ql.exec.UDF` to implement the `evaluate` method.
Example: A simple array UDF
```
public class MyDiff extends UDF {   
    public ArrayList<Integer> evaluate(ArrayList<Integer> input) {
        ArrayList<Integer> result = new ArrayList<Integer>();     
        result.add(0, 0);        
        for (int i = 1; i < input.size(); i++) {              
        result.add(i, input.get(i) - input.get(i - 1));        
        }      
        return result;    
    }
}
```
Sample POM file
```
<dependencies>          
    <dependency>        
        <groupId>org.slf4j</groupId>        
			<artifactId>slf4j-log4j12</artifactId>       
			<version>1.7.16</version>        
			<scope>test</scope>    
        </dependency>    
        <dependency>        
            <groupId>org.apache.hive</groupId>        
            <artifactId>hive-exec</artifactId>        
            <version>1.2.1</version>    
        </dependency>
</dependencies>
```
## Creating a function
If you are familiar with the SQL syntax, you can create a function by running the `CREATE FUNCTION` statement on the **Data Explore** page. You can also create a function visually in the following steps:
>? The data management page of Data Lake Compute is currently in beta test. To try it out, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.

1. Log in to the [Data Lake Compute console](https://console.cloud.tencent.com/dlc) and select the service region.
2. Select **Data management** on the left sidebar and select the target database.
3. Click **Function** to enter the function management page.
4. Click **Create function**.
![]()
You can also upload a local UDF program package or select a COS path (which requires COS permissions). The following example shows how to create a function by selecting a COS path.
The function class name includes the package information and the function execution class name.

## Using a function
1. Log in to the [Data Lake Compute console](https://console.cloud.tencent.com/dlc) and select the service region.
2. Select **Data Explore** on the left sidebar and select a compute engine to use a SQL function.
![]()









