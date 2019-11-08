Tencent Cloud Elasticsearch Service (ES) supports SQL instead of DSL as the query language. For those engaged in product operations and data analysis and new ES users, using SQL for queries can reduce their learning costs for getting started with ES.

ES provides two SQL parsers. All open-source versions of ES come pre-installed with the SQL parsing plugin provided by the open-source community. ES 6.4.3 and above (on both Basic Edition and Platinum Edition) supports the native SQL parser of Elasticsearch.

### Native SQL parser

You can use the SQL API for simple queries.

```
POST /_xpack/sql?format=txt
{
    "query": "SELECT * FROM my_index"
}
```

For more information on the API of the native SQL parser and how to use it, see the [official documentation](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/sql-rest.html).

### Open-source SQL parsing plugin
```
POST /_sql
"select * from my_index"
```
For more information on the API of the SQL plugin and how to use it, see [here](https://github.com/NLPchina/elasticsearch-sql/blob/master/README.md).

### SQL JDBC access
Access to ES clusters via JDBC is supported in the Platinum edition of ES 6.4.3 and above. You need to download the JDBC driver first which is available [here](https://www.elastic.co/downloads/jdbc-client) or by adding the following dependencies in Maven:

```
<dependency>
  <groupId>org.elasticsearch.plugin</groupId>
  <artifactId>x-pack-sql-jdbc</artifactId>
  <version>6.4.3</version>
</dependency>
```

Sample code for SQL JDBC access:

```
import java.sql.*;
import java.util.Properties;

public class Main {

    public static void main(String[] args) {
        try {
            Class.forName("org.elasticsearch.xpack.sql.jdbc.jdbc.JdbcDriver");
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
            return;
        }
        String address = "jdbc:es://http://YOUR_ES_VIP:9200";
        Properties properties = new Properties();
        properties.put("user", "elastic");
        properties.put("password", "YOUR_PASS");

        Connection connection = null;
        try {
            connection = DriverManager.getConnection(address, properties);
            Statement statement = connection.createStatement();
            ResultSet results = statement.executeQuery("select FlightNum from kibana_sample_data_flights limit 10");
            while (results.next()) {
                System.out.println(results.getString(1));
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            try {
                if (connection != null && !connection.isClosed()) {
                    connection.close();
                }
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
}
```
