Click the instance name on the instance list page. Select **Analytical Development** to go to the instance development page.
You can develop SQL for an instance, debug and launch an instance on this page, as shown below:
![](https://main.qcloudimg.com/raw/cc08b42a15efcb09119d08cdb3037941.png)


#### DDL statements are generated automatically through operations on the page
1. Click **Select data stream** on the top of the editor, and a pop-up window appears as below.
![](https://main.qcloudimg.com/raw/9ba3cdcd375634313654eaf4e97ad57f.png)
2. Choose the name of the Stream Connector project you created previously in the drop-down box of Project Name.
3. Choose the topic used as the source in the drop-down box of Topic.
4. Click the **Add** button, and you can find the DDL statements generated automatically in the IDE. The code is as follows:
![](https://main.qcloudimg.com/raw/f73b40bfedaa84cbf023e8cf17ed6e34.png)

#### Continue adding output topics and write computing logic statements in the IDE
The entire SQL code is as follows:
```
CREATE TABLE `demoSource` (
  `record_time` VARCHAR,
  `user_id` VARCHAR,
  `page_id` VARCHAR
) WITH (
  `type` = 'cdp',
  `project` = 'demo',
  `topic` = 'demoSource'
);
CREATE TABLE `demoSink` (
  `record_time` VARCHAR,
  `pv` BIGINT,
  `uv` BIGINT,
  PRIMARY KEY ( `record_time` )
) WITH (
  `type` = 'cdp',
  `project` = 'demo',
  `topic` = 'demoSink'
);
INSERT INTO demoSink
SELECT
  SUBSTRING(record_time, 1, 16) as record_time,
  count(user_id) as pv,
  count(DISTINCT user_id) as uv
FROM demoSource
GROUP BY SUBSTRING(record_time, 1, 16);
```
>**Note:** The SQL for SCS supports the standard SQL 2003 specification.






